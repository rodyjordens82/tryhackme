# 🔍 Secure Code Review Methodology
A practical guide for conducting white-box security assessments of web applications. Focus on PHP applications, with concepts applicable across languages.

## 📋 Table of Contents
- [Introduction](#introduction)
- [Testing Approaches](#testing-approaches)
- [Initial Reconnaissance](#initial-reconnaissance)
  - [Identify Framework & Dependencies](#identify-framework--dependencies)
  - [Read Configuration Files](#read-configuration-files)
  - [Locate Entry Points](#locate-entry-points)
  - [Set Up Your Environment](#set-up-your-environment)
- [Taint Analysis Framework](#taint-analysis-framework)
  - [Identifying Sources](#identifying-sources)
  - [Cataloguing Sinks](#cataloguing-sinks)
  - [Tracing Values: Practical Example](#tracing-values-practical-example)
  - [False Positive: Inadequate Sanitisation](#false-positive-inadequate-sanitisation)
- [Common Vulnerability Patterns](#common-vulnerability-patterns)
  - [Loose Comparison & Type Juggling](#loose-comparison--type-juggling)
  - [Variable-Handling Functions](#variable-handling-functions)
  - [Weak Randomness](#weak-randomness)
  - [Magic Methods & Deserialisation](#magic-methods--deserialisation)
  - [Stream Wrappers](#stream-wrappers)
  - [Error Suppression & Insecure Defaults](#error-suppression--insecure-defaults)
- [Tooling & Automation](#tooling--automation)
  - [Finding Sinks with ripgrep](#finding-sinks-with-ripgrep)
  - [Triage Process](#triage-process)
  - [Manual Verification](#manual-verification)
- [Reporting Findings](#reporting-findings)
- [Appendix A: Laravel-Specific Review Checklist](#appendix-a-laravel-specific-review-checklist)
- [Appendix B: PHP Version Awareness](#appendix-b-php-version-awareness)

---

## 1. Introduction

### What is Secure Code Review?

Secure code review is the practice of reading an application's source code to:

- Find security flaws
- Understand why they exist
- Judge how they can be reached and abused

Unlike black-box testing where we infer behavior from external responses, code review provides full visibility of the code, making it a white-box activity.

### Why White-Box Testing?

| Aspect | Black-Box | White-Box |
|--------|-----------|-----------|
| Visibility | No source code | Full source access |
| Inference | Guess server behavior | See exact logic |
| Depth | Surface-level issues | Deeper, more certain findings |
| Time Investment | Less efficient for deep bugs | Flaw and root cause visible together |

Almost every web vulnerability follows the same pattern:

**Untrusted Input → Entry Point → (Sanitization?) → Dangerous Sink**

When we follow data from where it arrives to where it is dangerously used, we perform taint analysis.

## 2. Testing Approaches

### Box Types by Access Level

| Approach | Access | Typical Use Case |
|----------|--------|------------------|
| White-Box | Full source and configuration | Deepest assurance, code drops, internal review |
| Grey-Box | Partial information (source without credentials, or docs without code) | Time-limited engagements, focused review |
| Black-Box | External behaviour only | Production testing with no source, bug bounty |

### Review Strategy Selection

| Strategy | Description | When to Use |
|----------|-------------|-------------|
| Coverage-Driven | Read everything | Small or critical codebases where completeness matters most |
| Threat-Driven | Start from assets and entry points | Large codebases where reading every line is impossible |
| Time-Boxed | Prioritize highest-value paths | Standard practice when codebase is larger than available time |

## 3. Initial Reconnaissance

### First Hour Routine

#### 3.1 Identify Framework & Dependencies

For PHP applications:

```bash
# Examine dependency files
cat composer.json
cat composer.lock
```

What to look for:

- Framework identification (Laravel, Symfony, etc.)
- Version pinning
- Known vulnerable libraries
- Development dependencies that might expose debug information

Example `composer.json` analysis:

```json
{
  "require": {
    "php": "^7.3|^8.0",
    "laravel/framework": "^8.XX",
    "guzzlehttp/guzzle": "^7.0.1"
  },
  "require-dev": {
    "facade/ignition": "2.5.1",  # ← Debug handler - check if exposed!
    "phpunit/phpunit": "^9.X"
  }
}
```

#### Framework-Specific Knowledge

| Framework | Routes Location | Config Location | Security Controls |
|-----------|-----------------|-----------------|-------------------|
| Laravel | `routes/web.php`, `routes/api.php` | `.env`, `config/` | Middleware, Policies |
| Symfony | `routes/`, `config/packages/` | `config/` | Security Bundle |

#### 3.2 Read Configuration Files

Critical files to examine:

- `.env` — Environment variables, debug flags, secrets
- `config/database.php` — Database credentials
- `config/app.php` — App settings
- `config/auth.php` — Authentication configuration

Danger signs in configuration:

- `APP_DEBUG=true` — Exposes detailed error pages
- `APP_KEY=<exposed key>` — Should never be committed
- `DB_PASSWORD=plain text` — Credentials in repo

#### 3.3 Locate Entry Points

**Front Controller Pattern:**

- Every request routes through a single entry script
- Laravel: `public/index.php`
- Routes serve as natural index of attack surface

Attack surface map structure:

```
HTTP Route → Controller Action → Model/Helper Classes
      ↓              ↓                    ↓
   [Entry]       [Processing]         [Data Layer]
```

Action item: create a route-to-controller mapping document:

- `GET /` → `HomeController@index` → Model: `Product`
- `POST /login` → `AuthController@login` → Model: `User`
- `GET /admin/users` → `AdminController@index` → ⚠️ No authentication!

#### 3.4 Set Up Your Environment

```bash
# Recommended tooling setup
cd /var/www/app
code .                          # VS Code for navigation
rg --version                    # ripgrep for searching
```

## 4. Taint Analysis Framework

### The Source-to-Sink Model

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────┐
│   SOURCE    │ ──→ │   SANITISER?     │ ──→ │    SINK     │
│(Untrusted   │     │(Is it adequate   │     │ (Dangerous  │
│  Input)     │     │  for context?)   │     │  Function)  │
└─────────────┘     └──────────────────┘     └─────────────┘
```

Key definition: a sanitiser is only effective if it's:

- Correct for the context the value reaches
- Complete (handles all attack vectors)
- Enforced (actually applied before the sink)

### 4.1 Identifying Sources

#### PHP Superglobals (Most Common)

| Source | Purpose | Risk Level |
|--------|---------|------------|
| `$_GET` | Query string parameters | High |
| `$_POST` | Form body data | High |
| `$_REQUEST` | Merged GET/POST/COOKIE | Critical (often overlooked) |
| `$_COOKIE` | Cookie values | High |
| `$_FILES` | Uploaded files | High |
| `$_SERVER` | Headers, environment | Often missed! |

#### Less Obvious Sources

```php
// Raw request body
$data = file_get_contents('php://input');
$data = fread(fopen('php://input', 'r'), filesize('php://input'));

// Header values through $_SERVER
$user_agent = $_SERVER['HTTP_USER_AGENT'];
$x_forwarded_for = $_SERVER['HTTP_X_FORWARDED_FOR'];
$host = $_SERVER['HTTP_HOST'];

// Framework-wrapped sources
$term = $request->query('q');       // Laravel
$value = $request->input('field');  // Laravel
$value = $request->get('param');    // Symfony
```

### 4.2 Cataloguing Sinks

| Vulnerability Class | Common PHP Sinks |
|---------------------|------------------|
| SQL Injection | `mysqli_query`, `PDO::query()`, raw query strings, framework raw-query helpers |
| Command Injection | `system()`, `exec()`, `shell_exec()`, `passthru()`, `popen()`, `proc_open()`, backtick operator |
| Code Injection | `eval()`, `assert()` with string, `create_function()`, `preg_replace()` with `/e` modifier |
| File Inclusion | `include`, `require`, `include_once`, `require_once` |
| Path Traversal | `fopen()`, `readfile()`, `file_get_contents()`, `file_put_contents()`, `unlink()`, `move_uploaded_file()` |
| Object Injection | `unserialize()`, `phar://` through file operations |
| SSRF | `file_get_contents()` on URL, `curl_exec()`, HTTP clients (Guzzle, cURL) |
| XXE | `simplexml_load_string()`, `DOMDocument::loadXML()`, `simplexml_load_file()` |
| XSS | `echo`, `print`, `printf`, template output without escaping |

> Important: A sink is only a problem when a source reaches it without adequate sanitisation. The table is a search checklist, not a bug list.

### 4.3 Tracing Values: Practical Example

```php
// app/Http/Controllers/ReportController.php
public function search(Request $request)
{
    $term = $request->query('q');                              // ← SOURCE
    $rows = DB::select("SELECT id, name, sku FROM products \
                        WHERE name LIKE '%$term%'");            // ← SINK (SQL)
    return view('reports.search', ['rows' => $rows]);
}
```

Trace steps:

- Source identified: `$request->query('q')` - attacker controls via query string
- Assigned to: `$term` - no transformation
- Passed to: `DB::select()` with direct interpolation
- Result: **VULNERABLE** - no sanitisation between source and sink

Exploit demonstration:

- Input: `q=%' UNION SELECT username, password, NULL FROM users -- -`
- Query becomes: `SELECT ... WHERE name LIKE '%' UNION SELECT ... -- -%'`

### 4.4 False Positive: Inadequate Sanitisation

```php
$id   = $request->query('id');
$safe = htmlspecialchars($id);                                // ← Looks safe
$row  = DB::select("SELECT * FROM users WHERE id = $safe");   // ← Still vulnerable!
```

Why this fails:

- `htmlspecialchars()` encodes for HTML context (`<` → `&lt;`)
- SQL injection requires escaping SQL context (`'` → `\'`)
- Context mismatch = still injectable

False confidence indicators:

- Variables named `$safe`, `$clean`, `$validated`
- Any sanitising function appears on the path
- But context doesn't match the sink!

Validation that isn't enforced:

```php
$result = validate_input($data);
if ($result !== true) { /* log warning */ }
// Code continues anyway - validation not enforced!
```

## 5. Common Vulnerability Patterns

### 5.1 Loose Comparison & Type Juggling

| Operator | Behavior | Security Implication |
|----------|----------|----------------------|
| `==` | Loose comparison (type conversion) | Dangerous for security checks |
| `===` | Strict comparison (value AND type) | Always use for security-critical comparisons |

#### Magic Hash Attack

```php
$hash1 = "0e462097431906509019562988736854"; // MD5 of "240610708"
$hash2 = "0e830400451993494058024219903391"; // MD5 of "QNKCDZO"

if ($hash1 == $hash2) {  // TRUE! Both treated as 0
    echo "Authentic!";
}
```

#### Practical Example - License Bypass

```php
// app/Support/License.php
public function verify(string $provided): bool
{
    $expected = $this->storedHash();   // e.g. "0e462097431906509019562988736854"
    return $provided == $expected;     // ← VULNERABLE to magic hash
}
```

Fix: always use strict comparison in security contexts.

```php
return hash_equals($provided, $expected);  // Timing-safe comparison
// OR
return $provided === $expected;
```

Additional type-juggling pitfalls:

- `in_array($needle, $haystack)` - uses `==` unless strict flag set
- `switch ($value)` - compares cases with `==`
- `strcmp($a, $b) == 0` - returns `NULL` (equals `0`) when given array input (PHP < 8)

### 5.2 Variable-Handling Functions

#### `extract()` — Variable Overwrite

```php
// app/Http/Controllers/AccountController.php
$isAdmin = false;
extract($_REQUEST);                              // ← CRITICAL RISK
if ($isAdmin) {                                  // ← Privileged branch
    // admin functionality
}
```

- Exploit: Add `?isAdmin=1` to request
- Mechanism: `extract()` overwrites existing variables with array keys

Safe alternative:

```php
extract($_REQUEST, EXTR_SKIP);  // Skip existing variables
```

Or better — explicitly whitelist input:

```php
$allowed = ['name', 'email', 'message'];
foreach ($allowed as $key) {
    $$key = $_REQUEST[$key] ?? null;
}
```

#### `parse_str()` Without Output Argument

```php
// Single argument form - populates scope directly
parse_str($query_string);  // ← Creates variables in current scope

// PHP 8+ requires second argument:
parse_str($query_string, $output);  // ✓ Safer - contained in $output
```

#### Variable Variables

```php
$$name = "malicious_value";  // Input chooses variable name to write
```

### 5.3 Weak Randomness

| Function | Algorithm | Issue |
|----------|-----------|-------|
| `rand()` | Mersenne Twister | Predictable |
| `mt_rand()` | Mersenne Twister | Predictable |
| `uniqid()` | Timestamp-based | Very low entropy |

Vulnerable token generation:

```php
// app/Http/Controllers/AccountController.php
$token = md5(uniqid(mt_rand(), true));  // ← PREDICTABLE TOKEN
```

Exploitation: attacker estimates server time/state to reproduce tokens.

Cryptographically secure alternative:

```php
$token = bin2hex(random_bytes(32));      // ✓ CSPRNG
$int = random_int($min, $max);           // ✓ Integer range
```

### 5.4 Magic Methods & Deserialisation

| Method | Trigger | Security Risk |
|--------|---------|---------------|
| `__wakeup()` | Object restored from serialization | Execute on unserialization |
| `__destruct()` | Object destroyed | Resource manipulation on cleanup |
| `__toString()` | Used as string | Can trigger during output/interpolation |
| `__call()` | Undefined method invoked | Method injection vector |

#### Deserialization Chain Example

```php
class TempFile {
    public $path;
    public function __destruct() {
        unlink($this->path);  // Deletes file when object destroyed
    }
}
```

- If `unserialize()` exists elsewhere:
  - Attacker crafts serialized `TempFile` with malicious path
  - On unserialization → `__wakeup()` → eventual destruction → `__destruct()`

Detection strategy: when you find `unserialize($input)`, immediately search for:

- Magic methods in application classes
- Properties that could be controlled by attacker
- Gadget chains connecting input to dangerous operations

### 5.5 Stream Wrappers

| Wrapper | Function | Attack Vector |
|---------|----------|---------------|
| `php://filter` | Stream transformation | Read source code via file inclusion |
| `data://` | Inline content encoding | Smuggle executable code into inclusion |
| `phar://` | PHP Archive access | Trigger deserialisation through file ops |
| `expect://` | Command execution | Execute commands (extension dependent) |

Practical impact: any file-related sink becomes multi-exploit capable.

```php
// Normal inclusion
include($page);

// Becomes:
include("php://filter/read=convert.base64-encode/resource=config.php");
include("data://text/plain;base64,".base64_encode($payload));
include("phar:///upload/malicious.phar/file.txt");
```

### 5.6 Error Suppression & Insecure Defaults

```php
@$unserialize($data);  // ← Hides failures during testing
@file_get_contents($url);  // ← May fail silently
```

Review flag: treat `@` on security-relevant calls as “read this line closely.”

Insecure framework defaults to check:

- `APP_DEBUG=true` — Detailed stack traces in production
- `APP_KEY` not rotated — Default signing key known

## 6. Tooling & Automation

### 6.1 Finding Sinks with ripgrep

Efficient codebase-wide searching:

```bash
# Command injection sinks
rg -n "system\(|exec\(|shell_exec\(|passthru\(|popen\(|proc_open\(" .

# Deserialization sinks
rg -n "\bunserialize\s*\(" .

# SQL-related functions
rg -n "mysqli_\|PDO::" .

# Eval and code execution
rg -n "eval\(|assert\(|create_function\(" .

# Unencrypted cryptography
rg -n "md5\(|sha1\(" .
```

Flag reference:

- `-n` = Print line numbers
- `-i` = Case insensitive
- `--type php` = Search only PHP files

### 6.2 Triage Process

Every grep hit is a starting point, NOT a confirmed bug:

```
Finding → Trace → Evaluate → Confirm or Reject
   ↓        ↓         ↓          ↓
Search   Follow   Check      Document
from     value    sanitiser  result
```

Decision tree:

```text
graph TD
    A[Sink Found] --> B{Can Source Reach?}
    B -->|No| C[Reject - No Path]
    B -->|Yes| D{Is Sanitiser Adequate?}
    C --> E[Next Finding]
    D -->|Yes, Correct Context| F[Reject - Safe Path]
    D -->|No/Incomplete/Wrong Context| G[Confirm Vulnerability]
    G --> H[Document Exploit Path]
```

### 6.3 Manual Verification

Once code review identifies a potential issue:

- Run the application locally
- Test the specific payload
- Verify impact (not just theoretical)
- Capture proof-of-concept requests/responses

### Tool Comparison

| Tool | Best For | Limitation |
|------|----------|------------|
| `ripgrep` | Finding sinks quickly | Reports paths, not exploits |
| Static Analyzers | Automated pattern detection | High false positive rate |
| Manual Review | Context awareness | Slow, doesn't scale alone |
| Dynamic Scanners | Runtime verification | Blind to logic errors |

Recommended stack: `ripgrep` → Manual Triage → Static Analyzer → Dynamic Verification

## 7. Reporting Findings

### Finding Template

```markdown
## [Vulnerability Name]

### Severity: CRITICAL/HIGH/MEDIUM/LOW

**Location:** `app/Http/Controllers/ReportController.php:15`

**Source:** `$request->query('q')`

**Sink:** `DB::select()` - SQL Injection

**Vulnerability Path:**
query parameter → term variable → DB::select() with direct interpolation

**Root Cause:** Input is interpolated directly into SQL string without parameterization

**Proof of Concept:**

GET /reports/search?q=' UNION SELECT username, password, NULL FROM users -- -

**Impact:** Full database read access to sensitive tables

**Remediation:** Use parameterized queries
```

```php
$rows = DB::select("SELECT id, name, sku FROM products \
                    WHERE name LIKE ?", ['%' . $term . '%']);
```

References:

- CWE-89: SQL Injection
- OWASP Top 10: Injection
```

### Prioritization Matrix

| Criteria | Weight | Notes |
|----------|--------|-------|
| Exploitability | High | How easy to exploit in practice? |
| Asset Sensitivity | High | What data/system is exposed? |
| Authentication Requirement | Medium | Does exploit require auth? |
| User Interaction | Medium | Does attacker need to trick a user? |
| Network Boundary | Low | Internal vs external exposure |

---

## Appendix A: Laravel-Specific Review Checklist

### Framework Architecture Locations

- `/routes/web.php` — Route definitions
- `/routes/api.php` — API routes
- `/app/Http/Controllers/` — Controller logic
- `/app/Models/` — Eloquent models
- `/app/Providers/` — Service providers
- `/config/*.php` — Configuration
- `.env` — Environment variables (CHECK THIS!)

### Laravel-Specific Patterns to Watch

**Authentication:**

```php
// Middleware-based protection
Route::middleware(['auth'])->group(function () {
    // Protected routes
});

// GATE policy
if (Gate::allows('admin')) { ... }
```

**Mass Assignment Protection:**

```php
protected $fillable = ['name', 'email'];  // Whitelist
protected $guarded = [];                  // Empty means ALL assignable (RISK!)
```

**Framework Escaping:**

- Blade templates: `{{ $variable }}` auto-escapes HTML (SAFE)
- Blade directives: `{!! $variable !!}` does NOT escape (DANGEROUS)
- Eloquent: Uses PDO parameter binding by default (SAFE)
- Raw queries: `DB::select()` - manual handling required

## Appendix B: PHP Version Awareness

### Critical Changes Across Versions

**PHP 7 vs PHP 8:**

- Number/string comparison: Changed behavior (closed some bypasses)
- Magic hashes: Still work in PHP 8 if both strings are numeric-form
- `strcmp()` with array: Throws `TypeError` in PHP 8, returned `NULL` in PHP 7
- `parse_str()` single argument: Removed in PHP 8

Always check: `php --version` on target and adjust techniques accordingly.

### Quick Reference Card

**Red Flags to Catch on Sight**

- Loose comparison (`==`) in authentication/authorization
- `extract()` on untrusted data
- `eval()`, `assert()`, `create_function()`
- `unserialize()` on any input
- `system()`/`exec()` with variable arguments
- `file_get_contents()` with user-controlled path
- `md5()`/`sha1()` for security tokens
- `rand()`/`mt_rand()`/`uniqid()` for crypto
- `@` error suppression on sensitive calls
- Missing `===` everywhere — `===` should be used

### Taint Analysis Questionnaire

1. Where does this value enter the application? (SOURCE)
2. What dangerous function could receive it? (SINK)
3. Is there sanitisation between them?
4. If yes, is it correct for THIS sink's context?
5. Is the sanitisation enforced (not computed but ignored)?
6. Can I prove exploitation in practice?

### Command Cheatsheet

```bash
# Find command injection
rg -n "system\(|exec\(|shell_exec\(" .

# Find deserialization
rg -n "unserialize\s*\(" .

# Find file inclusions
rg -n "include|require" --type php .

# Find SQL patterns
rg -n "mysqli_query|PDO::query" .

# Navigate structure
tree -L 2 .

# Count lines
wc -l **/*.php
```

Last Updated: July 2026
Methodology Version: 1.0
