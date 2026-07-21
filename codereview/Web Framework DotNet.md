# Web Frameworks: .NET

This note is written as a practical code-review guide for .NET applications, with a focus on reviewing both ASP.NET Framework (legacy Web Forms) and ASP.NET Core (modern MVC / Razor / API) in a white-box way.

The goal is not to memorise a single lab walkthrough. The goal is to learn a repeatable review loop:

1. Read the source.
2. Map the request path.
3. Trace the input into framework sinks.
4. Triage the impact.
5. Verify the bug on the running app.

That workflow is what turns a vague reading of a framework into a real security review.

## Why .NET is worth reviewing differently

The .NET ecosystem has two major generations, and they fail in different ways:

- ASP.NET Framework is the older Windows-centric platform. It is commonly found behind classic Web Forms pages with hidden `__VIEWSTATE` fields and old serializer patterns.
- ASP.NET Core is the modern cross-platform stack. It uses controllers, Razor views, model binding, and EF Core for data access.

The important takeaway is that the same application may look similar from the outside while exposing different sink classes on the inside. A reviewer should therefore treat the framework version as part of the bug-hunting strategy.

## The review methodology

For a real source review, the sequence matters.

### 1. Read the source before you test

A security reviewer should start from the application source, not from guesses. This means locating:

- request entry points
- controller actions or handlers
- data access methods
- model binding targets
- serializers and deserializers
- authentication and authorization checks

The point is to identify the sink first, then confirm the exploit path second.

### 2. Trace the data flow

Once you find a likely sink, ask:

- Where does the request value come from?
- Does it remain a typed object, or does it get interpolated into a string?
- Is the framework accepting a rich entity type directly from the caller?
- Does the app use reflection or type-name metadata for deserialization?

This is the core of code review: not just spotting a risky API, but understanding whether attacker-controlled data can reach it.

### 3. Rank the impact before writing the report

When you find multiple bugs, do not list them as equal findings. Rank them by impact:

- Code execution on the host is the highest priority.
- Data exposure or privilege escalation is next.
- Low-signal informational issues come last.

A strong report leads with the impact that matters most.

### 4. Prove every finding on the live system

A code review is not complete until the sink is demonstrated. In the lab, this means showing the request, the payload, and the resulting effect on the running application.

## Review patterns in .NET

### 1. ASP.NET Framework ViewState and machine key leakage

ASP.NET Web Forms uses hidden `__VIEWSTATE` fields. These are not just harmless state blobs. They are serialized object graphs that the server later deserializes.

If the `machineKey` used to sign and validate `__VIEWSTATE` is leaked, a Web Forms page can become a deserialization sink that leads to code execution.

#### What to look for in source

Look for:

- Web Forms pages with `runat="server"`
- `<machineKey ... />` in `web.config`
- any backup copy such as `web.config.bak`
- classic handler or page code that accepts postbacks with signed state

Example configuration:

```xml
<machineKey
  validationKey="<REDACTED>"
  decryptionKey="<REDACTED>"
  validation="SHA1"
  decryption="AES"
  compatibilityMode="Framework20SP1" />
```

#### Why this matters

The key is the critical secret. The page itself is not the security boundary; the application is trusting a signed, server-generated state blob. If that signing material can be recovered, the server will accept attacker-crafted serialized state.

#### Typical exploitation flow

1. Recover the leaked `machineKey` from a backup file or other exposed artifact.
2. Read the page's `__VIEWSTATEGENERATOR` value from the live form.
3. Use a tool such as `ysoserial.net` to generate a gadget chain.
4. Submit the signed payload in the POST body.
5. Confirm the effect by reading the output on disk or via a writable export directory.

Example command pattern:

```powershell
ysoserial.exe -p ViewState -g TypeConfuseDelegate ^
  --validationalg="SHA1" ^
  --validationkey="VALIDATIONKEY_FROM_BACKUP" ^
  --generator="CA0B0334" ^
  -c "cmd /c copy C:\flags\viewstate.txt C:\sites\LegacyPortal\loot\out.txt"
```

The important review lesson is simple:

> A Web Forms page plus a recoverable `machineKey` is often a direct path to remote code execution.

#### Fixes

- Rotate the leaked `machineKey`.
- Remove backup configuration files from the web root.
- Avoid trusted deserialization on server-generated state where it is not absolutely required.
- Prefer modern frameworks or isolated serialization strategies where possible.

### 2. Entity Framework Core raw SQL injection

EF Core is often described as safe because LINQ queries are parameterized. That is true only for the normal LINQ path.

The escape hatch is the raw SQL API:

- `FromSqlRaw`
- `FromSqlInterpolated`
- `ExecuteSqlRaw`

These methods are safe only if the user input remains bound as a parameter. They become injectable when the input is concatenated into the SQL string before the call.

#### Unsafe pattern

```csharp
var sql = $"SELECT Id, Title, Body FROM Articles WHERE Title = '{q}'";
var results = _db.Articles.FromSqlRaw(sql).ToList();
```

This is classic SQL injection because the request value is embedded directly into the SQL text.

#### Safe pattern

```csharp
var results = _db.Articles
    .FromSqlRaw("SELECT Id, Title, Body FROM Articles WHERE Title = {0}", q)
    .ToList();
```

This version keeps the value bound as a parameter.

#### A reviewer’s checklist

Search for:

- `FromSqlRaw(`
- `FromSqlInterpolated(`
- `ExecuteSqlRaw(`
- string interpolation (`$"..."`)
- string concatenation with request values (`+` or `string.Concat`)

If a request value is part of the SQL text, treat the endpoint as injectable until proven otherwise.

#### Demonstration

If the application has a `Flags` table and the query returns three columns, the review can often build a UNION-based payload from the source model inspection alone.

Example request:

```bash
curl -s --get http://10.113.140.14:5000/Articles/Search \
  --data-urlencode "q=' UNION SELECT 999, Value, Value FROM Flags -- "
```

A successful response will return the flag in the returned JSON document.

#### Why this works

The injection works because the query text is hand-built. The ORM does not save the code from itself. Parameterization is only guaranteed when the framework binds the value at the API boundary.

#### Fixes

- Prefer LINQ over raw SQL whenever possible.
- Use parameterized raw SQL templates.
- Avoid interpolated strings that contain user-controlled content.
- Use a separate safe read path for sensitive tables such as flags or admin metadata.

### 3. ASP.NET Core model binding overposting

Model binding makes request handling convenient. A controller action can bind directly to a rich model type, and the framework will map incoming form fields and query parameters onto that class by property name.

That convenience turns into a security problem when the model contains sensitive fields that the UI never intended the client to set.

#### Unsafe model and action

```csharp
public class User
{
    public int Id { get; set; }
    public string Email { get; set; }
    public string DisplayName { get; set; }
    public string PasswordHash { get; set; }
    public bool IsAdmin { get; set; }
}

public async Task<IActionResult> Update(User model)
{
    user.Email = model.Email;
    user.DisplayName = model.DisplayName;
    user.IsAdmin = model.IsAdmin;
    await _db.SaveChangesAsync();
    return Ok();
}
```

The form might only render `Email` and `DisplayName`, but the binder will happily accept any property name present in the request, including `IsAdmin`.

#### Exploit style

```text
Email=you%40test.com&DisplayName=You&IsAdmin=true
```

A successful POST means the model binder accepted the extra property, and the database record has now been updated.

#### Important nuance

The authentication cookie may still contain old claims. In practice, the user may need to sign out and sign back in to refresh the claims after the database row changes.

#### Fixes

Use one of these approaches:

- Allow-list binding with `[Bind("Email,DisplayName")]`
- A dedicated DTO that contains only safe fields

Example:

```csharp
public class UpdateUserDto
{
    public string Email { get; set; }
    public string DisplayName { get; set; }
}
```

Then bind to the DTO, never directly to the entity.

> In review terms, binding a full entity type from the request is a mass-assignment risk.

### 4. Newtonsoft.Json type-name handling and unsafe deserialization

The classic .NET deserialization sinks are not limited to `ViewState`. Any serializer that can instantiate an attacker-selected type from input is a risk.

Common sink patterns include:

- `BinaryFormatter.Deserialize(...)`
- `LosFormatter.Deserialize(...)`
- `ObjectStateFormatter.Deserialize(...)`
- `JavaScriptSerializer` with a `SimpleTypeResolver`
- `JsonConvert.DeserializeObject(...)` with `TypeNameHandling` enabled

#### Dangerous source shape

```csharp
var settings = new JsonSerializerSettings
{
    TypeNameHandling = TypeNameHandling.All
};

var obj = JsonConvert.DeserializeObject<object>(body, settings);
```

This allows the request body to control the type name used during deserialization.

#### Why `TypeNameHandling.Auto` is still dangerous

`TypeNameHandling.Auto` is not safe merely because the default is less aggressive than `All`. If the target type is `object`, an interface, or an abstract class, Json.NET may still resolve the `$type` metadata and instantiate the attacker-chosen type.

#### Safe alternative

Prefer `System.Text.Json` with a fixed target model type:

```csharp
var model = JsonSerializer.Deserialize<MyModel>(body);
```

The critical condition is that the code chooses the model type, not the attacker.

#### Exploit flow

A common `Json.NET` gadget chain is `ObjectDataProvider`, which allows method invocation during deserialization. The payload is supplied in JSON, the serializer resolves the type from the `$type` field, and the gadget fires.

#### Fixes

- Remove `TypeNameHandling` entirely.
- Bind to a concrete DTO or model type.
- Avoid generic `object` deserialization from user input.
- Prefer `System.Text.Json` with a strict model.

## Practical red-team review checklist for .NET

When you are handed a .NET application, these are the high-value review questions:

- Is the app ASP.NET Framework or ASP.NET Core?
- Does it use Web Forms, MVC, Razor, or API controllers?
- Are there raw SQL entry points such as `FromSqlRaw` or `ExecuteSqlRaw`?
- Does the app bind a full entity or DTO directly from the request?
- Does the app use insecure deserialization or type-name metadata?
- Are there any backups or exposed config files such as `web.config.bak`?
- Does the app use authentication claims or roles that are refreshed only after re-login?

## Recommended spotting pattern

A reviewer should be able to quickly grep for the following patterns:

```text
machineKey
ViewState
FromSqlRaw
FromSqlInterpolated
ExecuteSqlRaw
TypeNameHandling
JsonConvert.DeserializeObject
BinaryFormatter.Deserialize
JavaScriptSerializer
SimpleTypeResolver
Bind("...")
IActionResult Update(User model)
```

These search terms map directly to the most common sink-rich code paths in .NET.

## Reporting advice

A good code-review write-up should do three things:

1. Lead with the highest-impact issue.
2. Show the sink and the vulnerable code path.
3. Give a one-line remediation.

Example report ordering:

1. ViewState / machineKey recovery → remote code execution.
2. Raw SQL injection in EF Core → data disclosure.
3. Overposting on the user update action → privilege escalation.
4. `TypeNameHandling` deserialization → gadget execution path.

## Final takeaway

The main lesson from reviewing .NET applications is that the framework itself often points to the sink:

- Web Forms signs and deserializes `__VIEWSTATE`
- EF Core parameterizes LINQ but not hand-built raw SQL
- model binding trusts the client by property name
- JSON type-name metadata can create a direct gadget path

The review skill is not magical. It is a sequence of small, repeatable steps: read the source, find the sink, verify the exploit, and report the impact clearly.

That is the pattern that makes .NET code review useful in any real-world codebase.

