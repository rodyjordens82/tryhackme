# Java Code Review Cheat Sheet

A practical checklist for reviewing Java web applications, especially Spring Boot services, for security issues. This guide is written for white-box review: read the source, trace untrusted input, identify dangerous sinks, and verify the impact.

## Why this matters

Most Java web vulnerabilities come from a small set of recurring patterns:

- Untrusted input reaches a dangerous sink
- Framework defaults expose internal functionality
- Request models are bound too broadly
- SQL is assembled by string concatenation instead of parameter binding
- User-controlled bytes are deserialised into live Java objects

A good review does not just find bugs; it also explains how the code reaches them and how serious the impact is.

---

## 1. Review workflow

Use the same loop for every application:

1. Identify the framework and version
2. Read configuration files and dependency manifests
3. Map routes to controllers and services
4. Trace user-controlled values from entry points to sinks
5. Rank findings by impact
6. Verify the issue with a proof-of-concept or a code-level explanation

### A reliable mental model

Untrusted input -> request parsing -> business logic -> dangerous sink

Examples:

- Request parameter -> SQL query -> database
- Request body -> object binding -> persistence layer
- Base64 body -> object deserialisation -> code execution

---

## 2. Files to inspect first

### Configuration and build files

Check these early:

- pom.xml or build.gradle
- application.properties or application.yml
- security configuration classes
- controller and service classes
- entity/model classes
- repository interfaces

### What to look for

- Exposed management endpoints
- Insecure default settings
- Old or vulnerable libraries
- Raw SQL construction
- Broad object binding
- Deserialisation of untrusted input

---

## 3. Spring Boot-specific review checklist

### 3.1 Actuator exposure

Spring Boot Actuator often exposes management endpoints that should not be reachable by normal users.

#### Red flags

- `management.endpoints.web.exposure.include=*`
- Actuator enabled without authentication
- Management port exposed beyond internal use

#### Why it matters

Actuator can leak:

- Environment values
- Heap dumps
- Mappings
- Config properties

#### What to verify

- Check whether `/actuator` and `/actuator/env` are reachable
- Look for values that should be secret but are exposed in cleartext
- Review whether heap dumps are available

#### Example

```properties
management.endpoints.web.exposure.include=*
```

#### Review guidance

Treat exposed Actuator endpoints as a secret disclosure risk. The fix is usually to limit exposure and protect the endpoint with authentication and network restrictions.

---

### 3.2 SQL injection via string-built queries

Spring does not make SQL safe by itself. If the app builds SQL text with user input and passes it to JDBC or JPA, the query can become injectable.

#### Red flags

- String concatenation with request parameters
- `String.format(...)` used for SQL text
- Raw SQL passed to `JdbcTemplate`
- `EntityManager.createQuery(...)` with concatenated strings

#### Unsafe pattern

```java
String sql = "SELECT id, title, body FROM articles WHERE title = '" + q + "'";
List<Map<String, Object>> rows = jdbc.queryForList(sql);
```

#### Safer pattern

```java
jdbc.queryForList("SELECT id, title, body FROM articles WHERE title = ?", q);
```

#### Review guidance

Ask this question for every data access path:

- Does user input reach the database as a bound parameter, or as part of the SQL text?

If it is part of the SQL text, it is potentially injectable.

---

### 3.3 Mass assignment / over-posting

Spring can bind request parameters directly into Java objects. If the object is a persistence entity, an attacker may be able to modify fields the UI never intended to expose.

#### Red flags

- `@ModelAttribute SomeEntity`
- Request data bound directly to an entity class
- Controllers saving the bound object without field restrictions

#### Unsafe pattern

```java
@PostMapping("/account/update")
public String update(@ModelAttribute User user, HttpSession session) {
    users.save(user);
    return "redirect:/account/profile";
}
```

#### Safer pattern

```java
public class ProfileUpdateDto {
    private String email;
}
```

Or constrain the binder explicitly:

```java
@InitBinder
public void initBinder(WebDataBinder binder) {
    binder.setAllowedFields("email");
}
```

#### Review guidance

Do not bind persistence entities directly from untrusted input. Use a dedicated DTO or restrict the allowed fields.

---

### 3.4 Deserialisation of untrusted data

Java deserialisation is a classic source of remote code execution when attacker-controlled bytes are read into Java objects.

#### Red flags

- `ObjectInputStream.readObject()`
- `XStream.fromXML()`
- `XMLDecoder.readObject()`
- `SnakeYAML` load methods
- Jackson with `enableDefaultTyping()` or open type info

#### Unsafe pattern

```java
byte[] data = Base64.getDecoder().decode(body);
try (ObjectInputStream ois = new ObjectInputStream(new ByteArrayInputStream(data))) {
    Object obj = ois.readObject();
}
```

#### Review guidance

If attacker-controlled data reaches a deserialisation sink, review the classpath for gadget libraries such as Commons Collections. If that library is present, the issue can be exploitable.

---

## 4. Review patterns to grep for

Useful search terms for a Java codebase:

```bash
rg -n "ObjectInputStream|readObject\(|@ModelAttribute|createQuery\(|queryForList\(|execute\(|String\.format\(|management\.endpoints|@Value\(|enableDefaultTyping|fromXML\(|yaml\.load\(" .
```

### High-value targets

- Controllers with request mappings
- Services that call repositories or JDBC
- Models/entities that expose sensitive fields
- Security configuration classes
- `pom.xml` and `build.gradle` dependency lists
- Any endpoint that accepts raw bytes or serialized payloads

---

## 5. Review questions to ask

When reading a Java application, ask:

- What is the attack surface?
- Where does untrusted input enter the application?
- Does it flow into SQL, file operations, command execution, or deserialisation?
- Is the framework or library exposing internal functionality by default?
- Are persistence entities bound directly from request data?
- Are secrets or configuration values exposed through management endpoints?
- Are dependencies known to be vulnerable or useful for gadget chains?

---

## 6. Impact ranking

When reporting findings, rank them by impact:

- Information disclosure: credentials, secrets, config values
- Data tampering: privilege escalation, unauthorised updates
- Access control bypass: admin access, role changes
- Remote code execution: full host compromise

A deserialisation issue that reaches code execution is usually higher severity than a simple data exposure issue.

---

## 7. Suggested remediation patterns

### Good defaults

- Limit Actuator exposure to only what is needed
- Put management endpoints behind authentication
- Parameterise SQL queries
- Bind DTOs instead of entity objects
- Avoid deserialising untrusted data
- Keep sensitive fields out of request-bound models

---

## 8. Reporting template

Use a structure like this in your notes or reports:

- Finding title
- Location: file and relevant method
- Root cause
- Attack path
- Impact
- Recommended fix
- Proof or validation notes

Example:

- Title: Actuator endpoints exposed to unauthenticated users
- Location: `application.properties`
- Root cause: wildcard exposure of management endpoints
- Impact: disclosure of environment values and heap dumps
- Fix: restrict exposure and require authentication

---

## 9. Bottom line

A strong Java review focuses on the same idea everywhere:

- Find the entry point
- Trace the data flow
- Identify the dangerous sink
- Judge whether the sink is reachable and exploitable
- Report the issue clearly, with a fix that addresses the root cause

