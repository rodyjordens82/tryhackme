# Secure Code Review Methodology

A comprehensive guide for conducting white-box security assessments of web applications. Covers PHP and Python frameworks with universal taint analysis principles.

---

## Table of Contents

- [Executive Summary](#executive-summary)
- [Testing Approaches](#testing-approaches)
- [Initial Reconnaissance & Orientation](#initial-reconnaissance--orientation)
- [Taint Analysis Framework](#taint-analysis-framework)
- [Vulnerability Classes & Patterns](#vulnerability-classes--patterns)
- [Tooling & Automation](#tooling--automation)
- [Framework-Specific Guides](#framework-specific-guides)
- [Verification & Exploitation](#verification--exploitation)
- [Reporting Standards](#reporting-standards)
- [Quick Reference Cards](#quick-reference-cards)
- [Conclusion](#conclusion)

---

## 1. Executive Summary

### What is Secure Code Review?

Secure code review is the practice of reading an application's source code to:

- ✅ Find security flaws before deployment
- ✅ Understand why vulnerabilities exist
- ✅ Judge how they can be reached and abused

Unlike black-box testing, where we infer behavior from external responses, code review provides full visibility of internal logic.

### Why White-Box Testing?

| Aspect | Black-Box | Grey-Box | White-Box |
|--------|-----------|----------|-----------|
| Visibility | No source code | Partial source/credentials | Full source + config |
| Inference | Guess server behavior | Some internal knowledge | See exact logic |
| Depth | Surface-level issues | Targeted findings | Deeper, certain discoveries |
| Efficiency | Hours of fuzzing needed | Moderate time investment | Bugs visible in minutes |
| Best For | Production testing | Time-limited engagements | Code drops, internal audits |

> Core insight: When source code is available, we stop guessing where bugs might be and start reading where they are.

### Universal Vulnerability Pattern

Almost every web vulnerability follows this shape:

`User-Controlled Input → Entry Point (Source) → [Sanitization?] → Dangerous Operation (Sink)`

When we follow data from arrival to danger, we perform taint analysis—the foundation of secure code review.

## 2. Testing Approaches

### Box Types by Access Level

| Approach | Access Level | Typical Use Cases |
|----------|--------------|-------------------|
| White-Box | Full source and configuration | Deepest assurance, code drops, internal review, secure SDLC |
| Grey-Box | Partial information (some source, some credentials) | Time-limited engagements, focused review, most penetration tests |
| Black-Box | External behaviour only | Production testing with no source, bug bounty programs |

### Review Strategy Selection

| Strategy | Description | When to Use |
|----------|-------------|-------------|
| Coverage-Driven | Read everything systematically | Small or critical codebases where completeness matters most |
| Threat-Driven | Start from assets and entry points that matter most | Large codebases where reading every line is impossible |
| Time-Boxed | Prioritize highest-value paths within fixed timeframe | Industry standard when codebase is larger than available time |

> Industry reality: The codebase is almost always larger than the time we have. Time-box the work and prioritize the highest-value paths.

## 3. Initial Reconnaissance & Orientation

### The First Ten Minutes Matter Most

Do NOT start reading files at random. Use a proven reading order to orient yourself before hunting for bugs.

### Step-by-Step Reading Order

| Step | What to Read | What It Tells Us | Estimated Time |
|------|--------------|------------------|----------------|
| 1 | README and docs | What the app does, how it is run, which framework | 2 min |
| 2 | Dependency manifest | Libraries, versions, third-party attack surface | 3 min |
| 3 | Configuration files | Debug flags, secrets, database strings | 3 min |
| 4 | Routing / entry points | Full list of ways in (attack surface map) | 2 min |
| 5 | Auth middleware/decorators | Which routes are protected, which are not | 5 min |
| 6 | Database/models layer | Where data is stored, how queries are built | 5 min |
| 7 | Individual route handlers | Logic behind each entry point | Ongoing |

> Critical principle: Only read handlers in detail once you know which ones are worth the time.

### 3.1 Dependency Analysis

Python:

```bash
cat requirements.txt       # Direct dependencies
cat pyproject.toml         # Modern Python packaging
pip-audit                  # Scan against CVE database
```

PHP:

```bash
cat composer.json          # Direct dependencies
cat composer.lock          # Exact installed versions (direct + transitive)
```

Java:

```bash
cat pom.xml                # Maven dependencies
gradle dependencies       # Gradle dependencies
```

What to look for:

- Framework identification and version
- Pinned vulnerable library versions
- Dev dependencies that might expose debug information
- Known CVE versions searchable before reading application code

Example finding:

```json
{
  "require": {
    "laravel/framework": "^8.XX",
    "facade/ignition": "2.5.1"  // ← Debug handler - check if exposed!
  }
}
```

### 3.2 Configuration Review

Configuration files are where developers make mistakes before a single request is handled.

| Language | Config Files | Key Dangers |
|----------|--------------|-------------|
| Python/Flask | `config.py`, `.env` | `DEBUG = True`, `SECRET_KEY` literals |
| PHP/Laravel | `.env`, `config/` | `APP_DEBUG=true`, committed `APP_KEY` |
| Java/Spring | `application.properties`, `application.yml` | Exposed credentials, debug flags |
| .NET | `appsettings.json`, `web.config` | Connection strings, debug modes |

Red flags in configuration:

```python
# Python/Flask
DEBUG = True              # ← Exposes detailed error pages
SECRET_KEY = "hardcoded"  # ← Should never be in source
DATABASE_URL = "postgres://user:pass@host/db"  # ← Embedded credentials
```

```bash
# PHP/Laravel
APP_DEBUG=true            # ← Exposes stack traces
APP_KEY=base64:xxx        # ← Secret underpinning framework's trust model
DB_PASSWORD=plaintext     # ← Committed credentials
```

Immediate action items:

- Note any `DEBUG = True` flags
- Capture database connection strings
- Document all hardcoded secrets

### 3.3 Attack Surface Mapping

Every route is an entry point. Enumerating them is the most useful activity before reading logic.

| Framework | Route Syntax | Location |
|-----------|--------------|----------|
| Flask/Python | `@app.route("/path")` | Route decorators on functions |
| Django | `urlpatterns = [...]` | `urls.py` |
| Laravel/PHP | `Route::get('/path', ...)` | `routes/web.php`, `routes/api.php` |
| Express/Node | `app.get('/path', ...)` | Router definitions |
| Spring Boot | `@GetMapping("/path")` | Controller annotations |

Create an attack surface map:

```bash
# Python - enumerate Flask routes
grep -rn "@app.route" --include="*.py" .

# PHP - inspect routes directory manually
ls -la routes/
cat routes/web.php
```

Route documentation template:

```markdown
## Route: GET /search
- **Handler:** SearchController.search()
- **Authentication:** Required (`login_required`)
- **Parameters:** `q` (query string)
- **Data Flow:** `q` → template string → HTML output
- **Risk Factors:** Template rendering, search functionality
```

### 3.4 Authentication Boundary Analysis

With routes listed, mark which ones require authentication.
The most interesting routes are:

- Sensitive routes missing authentication
- Routes that check roles using client-supplied values

Python/Flask authentication patterns:

```python
# Protected - good
@app.route("/vault/<int:item_id>")
@login_required
def vault(item_id):
    ...

# Unprotected - BAD
@app.route("/admin/users")  # ← Missing @login_required!
def admin_users():
    ...

# Role bypass - BAD
@app.route("/dashboard")
@login_required
def dashboard():
    role = request.args.get('role')  # ← Client controls role
    if role == 'admin': ...
```

Checklist:

- Document all routes without authentication
- Verify role checks don't trust client-supplied values
- Test for IDOR by accessing resources with different IDs
- Confirm session-based authentication is implemented correctly

## 4. Taint Analysis Framework

### The Source-to-Sink Model

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────┐
│   SOURCE    │ ──→ │   SANITISER?     │ ──→ │    SINK     │
│(User Input) │     │(Is it adequate   │     │ (Dangerous  │
│             │     │  for context?)   │     │  Function)  │
└─────────────┘     └──────────────────┘     └─────────────┘
      ↓                      ↓                       ↓
  Entry Point           Neutralization?         Harm Potential
```

Key definition: A sanitiser is only effective if it is:

- Correct for the context the value reaches
- Complete for all attack vectors
- Enforced before the sink

### 4.1 Identifying Sources

Sources are any place user-controlled data enters the application.

#### Python (Flask/Django)

| Source | Purpose | Risk Level |
|--------|---------|------------|
| `request.args` | Query string parameters | High |
| `request.form` | POST form fields | High |
| `request.json` | JSON request body | High |
| `request.cookies` | Cookie values | High |
| `request.headers` | Request headers | Often overlooked |
| `request.files` | Uploaded files | High |

Example sources:

```python
name = request.args.get("name")      # GET parameter
email = request.form["email"]        # POST field
data = request.json                 # JSON body
session_id = request.cookies.get("session")
host = request.headers["Host"]       # HEADER VALUE!
uploaded = request.files["file"]
```

#### PHP (Laravel / Standard)

| Source | Purpose | Risk Level |
|--------|---------|------------|
| `$_GET` | Query string parameters | High |
| `$_POST` | Form body data | High |
| `$_REQUEST` | Merged GET/POST/COOKIE | Critical |
| `$_COOKIE` | Cookie values | High |
| `$_FILES` | Uploaded files | High |
| `$_SERVER` | Headers, environment | Often missed |
| `$request->input()` | Laravel wrapper | High |

Less obvious sources:

```php
$data = file_get_contents('php://input');
$data = $_SERVER['HTTP_USER_AGENT'];    // User-Agent header
$data = $_SERVER['HTTP_X_FORWARDED_FOR'];  // Proxy header
$data = $_SERVER['HTTP_HOST'];          // Host header
```

Framework sources:

```php
$term = $request->query('q');           // Laravel
$value = $request->input('field');      // Laravel
$value = $request->get('param');        // Symfony
```

### 4.2 Cataloguing Sinks

A sink is any operation that becomes dangerous when fed attacker input.
A sink on its own is not a bug. A sink reached by a source, with no safe step between them, is a bug.

| Vulnerability Class | Python Sinks | PHP Sinks |
|---------------------|--------------|-----------|
| SQL Injection | `cursor.execute()`, `connection.query()`, ORM `.raw()`, `.extra()`, `text()` | `mysqli_query()`, `PDO::query()`, `DB::select()` raw strings |
| Command Injection | `os.system()`, `subprocess.run(shell=True)`, `os.popen()` | `system()`, `exec()`, `shell_exec()`, `passthru()`, backticks |
| Template Injection | `render_template_string()`, Jinja2 dynamic templates | N/A |
| Deserialisation | `pickle.loads()`, `yaml.load()` (unsafe), `json.loads()` with hooks | `unserialize()`, `phar://` streams |
| Path Traversal | `open()`, `send_file()`, `os.path.join(user_input)` | `fopen()`, `readfile()`, `include()`, `file_get_contents()` |
| Code Execution | `eval()`, `exec()`, `compile()`, `__import__()` | `eval()`, `assert()`, `create_function()`, `preg_replace(/e)` |
| SSRF | `requests.get()`, `urllib.urlopen()`, `http.client` | `file_get_contents(URL)`, `curl_exec()` |
| XXE | `xml.etree.ElementTree.fromstring()` | `simplexml_load_string()`, `DOMDocument::loadXML()` |
| XSS | Jinja2 `{!! !!}`, direct echo, response without escaping | `echo`, `print`, template output without `htmlspecialchars()` |

Framework-specific safe counterparts:

| Dangerous Pattern | Safe Counterpart |
|------------------|------------------|
| `render_template_string(f"...")` | `render_template("template.html", data=value)` |
| `send_file(os.path.join(...))` | `send_from_directory(dir, filename)` |
| `cursor.execute(f"...")` | `cursor.execute("...", (params,))` |
| `subprocess.run(cmd, shell=True)` | `subprocess.run([cmd, args])` |
| `eval(user_input)` | Never — use safer alternatives |

### 4.3 Tracing Values: Two-Directional Analysis

We can trace either way depending on codebase structure.

#### Backward Tracing (Sink-First)
1. Find suspicious sink with grep
2. Trace backwards through assignments
3. Check if value is user-controlled
4. Verify any sanitization between source and sink

Use when sinks are rare or you need a targeted review.

#### Forward Tracing (Source-First)
1. Identify user input in handler
2. Follow variable through transformations
3. Track until it reaches dangerous function
4. Judge each transformation's effectiveness

Both approaches answer the same question: does input reach a dangerous sink safely?

### 4.4 Second-Order Vulnerabilities

Sanitizing at the source is not enough. Data can be cleaned on input, stored, and later dropped into a sink in a different handler.

Classic examples:

- Username validated at registration → stored → used in raw query by admin report later
- Comment sanitized at posting → stored → rendered unsafely in profile page
- File path validated on upload → stored → opened in download endpoint without re-validation

Detection checklist:

- Mark all data going into databases
- Mark all data coming out of databases
- Trace whether stored data reaches unsafe sinks later
- Watch for ORM queries that build raw queries from stored values

## 5. Vulnerability Classes & Patterns

### 5.1 SQL Injection

The bug: building a query by pasting user input into a string instead of using placeholders.

#### Vulnerable pattern

```python
q = request.args.get("q")
cursor.execute(f"SELECT * FROM items WHERE name = '{q}'")
```

```php
$term = $request->query('q');
DB::select("SELECT id, name FROM products WHERE name LIKE '%$term%'");
```

#### Safe pattern

```python
cursor.execute("SELECT * FROM items WHERE name = ?", (q,))
```

```php
DB::select("SELECT id, name FROM products WHERE name LIKE ?", ['%' . $term . '%']);
```

Watch for:

- Second-order cases where stored input is later interpolated
- ORM escape hatches like `text()`, `.raw()`, `.extra()`
- Raw query helpers like `DB::select()` or `cursor.execute()` with string interpolation

Impact: data exfiltration, auth bypass, DB modification, file read.

### 5.2 Command Injection

The bug: putting user input into a shell command string.

#### Vulnerable pattern

```python
host = request.args.get("host")
subprocess.run(f"ping -c 1 {host}", shell=True)
```

```python
os.system(f"ping {host}")
os.popen(f"whoami {host}")
```

#### Safe pattern

```python
subprocess.run(["ping", "-c", "1", host])
```

Why it matters:

- `shell=True` hands the whole string to `/bin/sh`
- `;`, `|`, `&&`, backticks become shell syntax
- without shell, each item is a literal argument

Example exploit:

- Input: `127.0.0.1; cat /etc/passwd`
- Result: `ping -c 1 127.0.0.1; cat /etc/passwd`

### 5.3 Server-Side Template Injection (SSTI)

The bug: rendering user-controlled content as a template.

#### Vulnerable pattern

```python
name = request.args.get("name")
return render_template_string(f"Hello {name}")
```

#### Safe pattern

```python
return render_template("hello.html", name=name)
```

Smoke test: send `{{7*7}}` and check for `49`.

Gadget chain example:

```jinja
{{ cycler.__init__.__globals__.os.popen('id').read() }}
```

Key steps:

- Access attributes via `__class__`, `__mro__`
- Use `__globals__` to reach module objects
- Reference `os` through helpers such as `cycler`
- Execute commands with `popen()` or subprocess functions

### 5.4 Insecure Deserialisation

The bug: deserialising attacker-controlled data with a loader that can instantiate arbitrary objects.

#### Vulnerable patterns

```python
# Python pickle - WORST OFFENDER
data = request.cookies.get("prefs")
prefs = pickle.loads(base64.b64decode(data))
```

```python
import yaml
data = yaml.load(request.args.get('config'))
```

#### Safe patterns

```python
import json
data = json.loads(cookie_value)
```

```python
import yaml
data = yaml.load(config, Loader=yaml.SafeLoader)
```

```python
# Or avoid deserialisation entirely
```

Mechanism: `pickle` can be instructed to call arbitrary objects through `__reduce__`.

PHP equivalent:

```php
$data = $_COOKIE['session'];
$user = unserialize($data);
```

### 5.5 Path Traversal

The bug: building a file path using attacker input without ensuring it stays inside the intended directory.

#### Vulnerable pattern

```python
filename = request.args.get("file")
return send_file(os.path.join(UPLOAD_DIR, filename))
```

Why `os.path.join()` does not protect:

- It only joins strings
- Absolute paths discard the base directory
- Example: `os.path.join('/uploads', '/etc/passwd')` → `/etc/passwd`

#### Safe pattern

```python
from flask import send_from_directory
return send_from_directory(UPLOAD_DIR, filename)
```

Impact: read access to source files, config, `/etc/passwd`, SSH keys, uploads.

Advanced bypass:

- Input: `/etc/passwd`
- Result: `/etc/passwd`

### 5.6 Broken Access Control & IDOR

The bug: acting on a client-supplied resource identifier without checking ownership.

#### Vulnerable pattern

```python
@app.route("/vault/<int:item_id>")
@login_required
def vault(item_id):
    record = Vault.query.get(item_id)
    return jsonify(record.data)
```

#### Safe pattern

```python
@app.route("/vault/<int:item_id>")
@login_required
def vault(item_id):
    record = Vault.query.filter_by(id=item_id, owner_id=current_user.id).first()
    if not record:
        abort(404)
    return jsonify(record.data)
```

Related issues:

- Missing `@login_required`
- Role checks using client-supplied values
- Sequential IDs making enumeration trivial

Discovery method:

- Find the database lookup
- Check the filter/WHERE clause
- If it only uses the supplied ID, ownership is missing

### 5.7 Hardcoded Secrets

The bug: embedding secrets in source code under version control.

#### Vulnerable pattern

```python
SECRET_KEY = "fl4sk_s3cr3t_d0_n0t_sh1p_2026"
API_KEY = "AKIAIOSFODNN7EXAMPLE"
DATABASE_URL = "postgres://user:password@localhost/db"
```

Why it matters:

- Secrets are compromised when the repo is read
- Git history preserves them
- Automated scanners search history too

Safe pattern:

```python
import os
SECRET_KEY = os.environ.get("SECRET_KEY")
API_KEY = os.environ["API_KEY"]
```

Grep detection:

```bash
grep -rnE "(SECRET|KEY|TOKEN|PASSWORD|API_KEY)\s*=\s*['"]" --include="*.py" .
grep -rE "AKIA[0-9A-Z]{16}" .
```

### 5.8 Loose Comparison & Type Juggling (PHP)

The bug: using loose equality in security-sensitive logic.

| Operator | Behavior | Security Implication |
|----------|----------|----------------------|
| `==` | Loose comparison | Dangerous for security checks |
| `===` | Strict comparison | Use for security-critical comparisons |

#### Magic hash attack

```php
$hash1 = "0e462097431906509019562988736854";  // MD5 of "240610708"
$hash2 = "0e830400451993494058024219903391";  // MD5 of "QNKCDZO"

if ($hash1 == $hash2) {
    echo "Authentic!";
}
```

Fix:

```php
return hash_equals($provided, $expected);
// OR
return $provided === $expected;
```

Related issues:

- `in_array($needle, $haystack)` without strict mode
- `switch ($value)` uses `==`
- `strcmp($a, $b) == 0` in PHP < 8 with arrays

### 5.9 Variable Overwrite (PHP)

The bug: using `extract()` or `parse_str()` on untrusted data.

#### Vulnerable pattern

```php
$isAdmin = false;
extract($_REQUEST);
if ($isAdmin) {
    // admin functionality
}
```

Exploit: `?isAdmin=1` overwrites the variable.

Safe alternatives:

```php
extract($_REQUEST, EXTR_SKIP);
```

Or better:

```php
$allowed = ['name', 'email', 'message'];
foreach ($allowed as $key) {
    $$key = $_REQUEST[$key] ?? null;
}
```

### 5.10 Weak Randomness

The bug: using non-cryptographic RNG for security tokens.

| Function | Algorithm | Issue |
|----------|-----------|-------|
| `rand()`, `mt_rand()` | Mersenne Twister | Predictable |
| `uniqid()` | Timestamp-based | Low entropy |
| `md5(uniqid(mt_rand()))` | Combined | Still predictable |

#### Vulnerable patterns

```python
token = hashlib.md5(str(time.time()) + str(random.randint(0, 9999))).hexdigest()
```

```php
$token = md5(uniqid(mt_rand(), true));
```

#### Safe patterns

```python
import secrets
token = secrets.token_hex(32)
```

```php
$token = bin2hex(random_bytes(32));
```

## 6. Tooling & Automation

### Reading every file does not scale

The fix: triage first, then manually review confirmed candidates.

### 6.1 Grep-Based Triage

#### Basic sink hunting

```bash
# Python
grep -rn --include="*.py" -E "os\.system|subprocess|eval\(|exec\(|pickle\.loads|render_template_string|cursor\.execute|send_file|open\(" .

# PHP
grep -rn --include="*.php" -E "system\(|exec\(|shell_exec\(|unserialize\(|eval\(|include\(|require\(" .
```

#### Secret hunting

```bash
grep -rnE "(SECRET|KEY|TOKEN|PASSWORD|API_KEY)\s*=\s*['"]" --include="*.py" .
grep -rE "AKIA[0-9A-Z]{16}" .
grep -rnE "DEBUG\s*=\s*True|TESTING\s*=\s*True|verify\s*=\s*False" .
```

Performance tip: use `rg` for large codebases.

```bash
rg -n "render_template_string" --type py .
```

### 6.2 Semgrep for Structural Analysis

`grep` matches text. `semgrep` matches code structure.

```bash
pip install semgrep
```

```bash
semgrep --config p/owasp-top-ten .
semgrep --config p/python .
semgrep --config /opt/review/semgrep-rules .
```

Sample output:

```
app.py
❯❱ python.flask.security.injection.tainted-sql-string
       94┆ f"SELECT title, secret FROM vault WHERE owner_id = {uid} AND title LIKE '%{q}%'

❯❱ python.flask.security.audit.avoid_app_run_with_bad_host
      128┆ app.run(host="0.0.0.0", port=5000)

┌─────────────────┐
│ 2 Code Findings │
└─────────────────┘
```

Minimal custom rule:

```yaml
rules:
  - id: render-template-string-usage
    pattern: render_template_string(...)
    message: render_template_string on possible user input, check for SSTI
    severity: WARNING
    languages: [python]
```

### 6.3 Triage Workflow

Remember: grep and Semgrep produce candidates, never confirmed findings.

- Instrument found
  - Can source reach?
    - No → reject
    - Yes → is sanitiser adequate?
      - Yes → reject
      - No → confirm vulnerability
        - document exploit path

Triage priority order:

- `render_template_string()` → High
- `cursor.execute()` with f-string → High
- `subprocess()` with `shell=True` → High
- `pickle.loads()` → High
- `send_file()` with user input → Medium
- `open()` → Low

## 7. Framework-Specific Guides

### 7.1 Python/Flask Architecture

Directory structure:

- `/app.py` — Main application file
- `/config.py` — Configuration
- `/requirements.txt` — Dependencies
- `/templates/` — Jinja2 templates
- `/uploads/` — User file uploads
- `/init_db.py` — Database initialization

Flask-specific patterns:

| Area | Safe | Dangerous |
|------|------|-----------|
| Templates | `render_template("fixed.html", var=value)` | `render_template_string(f"...{input}...")` |
| File serving | `send_from_directory(dir, filename)` | `send_file(os.path.join(dir, filename))` |
| Database | `db.session.query(Model).filter_by(id=id)` | `db.execute(f"SELECT * WHERE id={id}")` |
| Subprocess | `subprocess.run([cmd, arg])` | `subprocess.run(f"{cmd} {arg}", shell=True)` |

Authentication:

```python
@app.route("/secret")
@login_required
def secret():
    ...
```

- Sessions are signed cookies
- `SECRET_KEY` leakage allows session forgery

ORM escape hatches:

```python
Model.query.from_statement(text(f"SELECT * FROM users WHERE id={id}"))
db.session.execute(f"UPDATE users SET role='{role}' WHERE id={id}")
```

### 7.2 PHP/Laravel Architecture

Directory structure:

- `/public/index.php` — Front controller
- `/routes/web.php` — Route definitions
- `/routes/api.php` — API routes
- `/app/Http/Controllers/` — Controller logic
- `/app/Models/` — Eloquent models
- `/config/*.php` — Configuration
- `/.env` — Environment variables
- `/composer.json` — Dependencies

Laravel-specific patterns:

| Area | Safe | Dangerous |
|------|------|-----------|
| Database | `DB::table('users')->where('id', $id)->get()` | `DB::select("SELECT * WHERE id=$id")` |
| Mass assignment | `$fillable = ['name', 'email']` | `$guarded = []` |
| Blade | `{{ $variable }}` | `{!! $variable !!}` |
| Eloquent | PDO binding by default | Raw `DB::select()` |

Middleware protection:

```php
Route::middleware(['auth'])->group(function () {
    Route::get('/admin', [AdminController::class, 'index']);
});

if (Gate::allows('admin')) { ... }
```

Common Laravel vulnerabilities:

- Missing auth on admin routes
- `$guarded = []` mass assignment
- Raw `DB::select()` interpolation
- Blade `{!! !!}` with user input
- `APP_DEBUG=true` exposing stack traces

## 8. Verification & Exploitation

### 8.1 Confirmation Process

- Run the application locally
- Test specific payloads
- Verify actual impact
- Capture proof of concept
- Retest with a clean setup

### 8.2 Proof-of-Concept Template

## Vulnerability: [Name]

### Severity: CRITICAL/HIGH/MEDIUM/LOW

**Location:** `file.py:line_number`

**Source:** `request.args.get('param')`

**Sink:** `cursor.execute()` - SQL Injection

**Path:** User input → f-string interpolation → Database execution

**Proof of Concept:**

```bash
curl "http://target/search?q=' UNION SELECT flag, flag FROM system_flags-- -"
```

**Evidence:**

Response: flag

**Impact:**

Full database read access to sensitive tables

**Remediation:**

```python
cursor.execute("SELECT title FROM vault WHERE owner_id = ? AND title LIKE ?", (uid, '%'.concat(q).concat('%')))
```

### 8.3 Exploitation Patterns by Vulnerability

#### SQL Injection via UNION

**Prerequisites:** Know column count and matching data types.

**Technique:**

```sql
-- Original query has 2 columns
SELECT title, secret FROM vault WHERE owner_id = ? AND title LIKE '%{q}%'

-- UNION must match column count
q=' UNION SELECT flag, flag FROM system_flags-- -
```

#### SSTI to Remote Code Execution

Jinja2 gadget chain:

```jinja
{{ cycler.__init__.__globals__.os.popen('printenv FLAG').read() }}
```

#### Path Traversal

Basic:

```http
GET /files/download?file=../../../etc/passwd
```

Absolute path injection:

```http
GET /files/download?file=/etc/passwd
```

Double encoding:

```http
GET /files/download?file=..%252F..%252Fetc%252Fpasswd
```

## 9. Reporting Standards

### Finding Template Structure

# [Vulnerability Title]

## Severity

[CRITICAL | HIGH | MEDIUM | LOW]

## Summary

[One sentence describing the issue and business impact]

## Affected Component

- **File:** `path/to/file.ext`
- **Line(s):** `42-45`
- **Endpoint:** `GET /api/users/{id}`

## Technical Details

### Root Cause

[Explain why the code is vulnerable]

### Vulnerable Code

```python
@app.route("/vault/<int:item_id>")
def vault(item_id):
    record = Vault.query.get(item_id)
    return jsonify(record.data)
```

### Attack Vector

[Describe how attacker exploits this]

### Remediation

```python
@app.route("/vault/<int:item_id>")
def vault(item_id):
    record = Vault.query.filter_by(id=item_id, owner_id=current_user.id).first()
    if not record:
        abort(404)
    return jsonify(record.data)
```

### Evidence

[Include screenshots, curl commands, or other proof]

### References

- `CWE-XXX`: [Vulnerability Type]
- `OWASP Top 10`: [Category]
- [Relevant documentation links]

### Prioritization Matrix

| Criteria | Weight | Rationale |
|----------|--------|-----------|
| **Exploitability** | High | How easy to exploit in practice? |
| **Asset Sensitivity** | High | What data/system is exposed? |
| **Authentication Required** | Medium | Does exploit require credentials? |
| **User Interaction** | Medium | Does attacker need to trick a user? |
| **Network Boundary** | Low | Internal vs external exposure |

**Scoring Guide:**

- **Critical:** Remote code execution, full database compromise, auth bypass
- **High:** SQL injection, SSTI, path traversal to sensitive files
- **Medium:** IDOR affecting non-critical data, reflected XSS
- **Low:** Debug mode enabled, informational disclosure, missing security headers

---

## 10. Quick Reference Cards

### Red Flags to Catch on Sight

- Loose comparison (`==`) in auth/authorization logic
- `extract()` on untrusted data
- `eval()`, `assert()`, `create_function()`
- `unserialize()` on any input
- `system()` / `exec()` with variable arguments
- `file_get_contents()` with user-controlled paths
- `md5()` / `sha1()` for security tokens
- `rand()` / `mt_rand()` / `uniqid()` for crypto
- `@error` suppression on sensitive calls
- Missing `===` in PHP security checks
- `send_file(os.path.join(user_input))`
- `render_template_string(f"...{input}...")`

### Taint Analysis Questionnaire

- Where does this value enter the application? (SOURCE)
- What dangerous function could receive it? (SINK)
- Is there sanitisation between them?
- If yes, is it correct for THIS sink's context?
- Is the sanitisation enforced?
- Can I prove exploitation in practice?

### Command Cheatsheet

```bash
# Find command injection
rg -n "system\(|exec\(|shell_exec\(" .

# Find deserialization
rg -n "unserialize\s*\(|pickle\.loads" .

# Find file inclusions
rg -n "include|require" --type php .

# Find SQL patterns
rg -n "cursor\.execute|DB::select|\.execute\(" .

# Find templates
rg -n "render_template_string" .

# Find secrets
grep -rnE "(SECRET|KEY|PASSWORD|TOKEN)\s*=\s*" .

# Navigate structure
tree -L 2 .

# Count lines
wc -l **/*.{py,php}
```

### Framework Cheat Sheet

| Framework | Routes | Config | Safe SQL | Safe Templates | Safe Files |
|-----------|--------|--------|----------|----------------|------------|
| Flask | `@app.route()` | `config.py` | `cursor.execute("?", ...)` | `render_template()` | `send_from_directory()` |
| Laravel | `routes/web.php` | `.env` | `DB::table()->where()` | `{{ $var }}` | `Storage::disk()` |
| Django | `urlpatterns` | `settings.py` | `Model.objects.filter()` | `{{ var }}` | `FileResponse()` |

### Testing Checklist

#### Pre-Engagement

- Confirm scope and authorization
- Obtain test credentials
- Set up reporting template
- Prepare tooling

#### During Review

- Complete reading order
- Map attack surface
- Triage with grep/Semgrep
- Manually verify candidates
- Exploit and capture PoCs
- Document second-order paths

#### Post-Analysis

- Write executive summary
- Detail each finding with remediation
- Include severity justification
- Provide reproducible PoCs

## Conclusion

White-box code review is fundamentally a reading problem before it is an exploitation problem. The exploits are often short — the work was in the reading that came first.

### The Five-Step Method

- ✅ Orient in the codebase (reading order)
- ✅ Map the attack surface from routing and configuration
- ✅ Trace user input from source to sink
- ✅ Triage with grep and Semgrep
- ✅ Verify each candidate by hand

Universal truth: The language and framework only change the names. The sink is a raw query whether it is built with an f-string in Python, Spring's `JdbcTemplate` in Java, or string concatenation in C#.

Starting every review: read the config, list the routes, and follow the input.

---

Version: 2.0

Last Updated: July 2026
'''