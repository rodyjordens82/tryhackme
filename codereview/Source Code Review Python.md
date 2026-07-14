# Python Code Review Cheat Sheet

A practical guide for reviewing Python web applications for security issues. This version is written for white-box review: read the source, trace untrusted input, identify dangerous sinks, and verify the impact.

## Why this matters

Most Python web vulnerabilities are caused by a small set of recurring patterns:

- Untrusted input reaches a dangerous sink
- Framework defaults expose debugging or internal behavior
- Session data is trusted without enough integrity checks
- Raw SQL is built from user input
- Templates are built from user-controlled strings
- One leaked secret is reused across services

A strong review does not stop at finding a bug; it explains how the data flows, why the issue is exploitable, and how serious the impact is.

---

## 1. Review workflow

Use the same loop for every application:

1. Identify the framework and version
2. Read configuration files and dependency manifests
3. Map routes to views, handlers, or controllers
4. Trace user-controlled values from entry points to sinks
5. Rank findings by impact
6. Verify the issue with a proof-of-concept or code-level reasoning

### A reliable mental model

Untrusted input -> request parsing -> business logic -> dangerous sink

Examples:

- Request parameter -> ORM/database query
- Request body -> session handling
- User string -> template rendering

---

## 2. Files to inspect first

### Core files to review

- settings.py or config files
- requirements.txt, Pipfile, or pyproject.toml
- views/controllers/handlers
- models or database access code
- templates and rendering code
- authentication and session handling

### What to look for

- Debug mode enabled in production
- Secrets exposed via error output
- Raw SQL using `.extra()`, `.raw()`, or `cursor.execute()`
- Flask session handling that trusts client-side values
- Template rendering from user-controlled strings
- Reused secrets across services

---

## 3. Django review checklist

### 3.1 Debug mode leakage

Django debug pages can expose sensitive information when `DEBUG=True` and an exception is triggered.

#### Red flags

- `DEBUG = True`
- Exception messages that include secrets or configuration values
- Settings or environment variables echoed into error output

#### Why it matters

A technical 500 page can leak:

- `SECRET_KEY`
- environment values
- stack traces and local variables
- request data

#### Review guidance

If a handler raises an exception that includes a secret, and debug mode is enabled, treat that as a high-risk information disclosure issue.

---

### 3.2 Raw SQL injection through ORM escape hatches

Django’s ORM is usually parameterized, but developers can bypass that protection.

#### Red flags

- `.extra(where=[...])`
- `.raw("...")`
- `cursor.execute("...")`

#### Unsafe pattern

```python
Article.objects.extra(where=[f"title = '{q}'"])
```

#### Safer pattern

```python
Article.objects.extra(where=["title = %s"], params=[q])
```

#### Review guidance

If a value is interpolated into SQL text, the query is potentially injectable. Treat the endpoint as vulnerable until proven otherwise.

---

## 4. Flask review checklist

### 4.1 Signed cookies are not encrypted

Flask sessions are often stored client-side and signed with a secret key.

#### Red flags

- `app.secret_key = ...`
- Session values set directly from request data or app logic
- Role or privilege checks based on session contents

#### Why it matters

If the signing secret is known, an attacker can forge a session and change values such as `role` or `admin` flags.

#### Review guidance

Review whether session contents are integrity-protected and whether the signing secret is strong and not reused across services.

---

### 4.2 Server-side template injection (SSTI)

SSTI happens when user input is included in a template string that is later rendered by the template engine.

#### Red flags

- `render_template_string(...)` fed with a string built from request data
- Template strings assembled with concatenation
- User-controlled values inserted into template source

#### Unsafe pattern

```python
template = PAGE_HEAD + q + PAGE_TAIL
return render_template_string(template)
```

#### Safer pattern

```python
return render_template("results.html", q=q)
```

#### Review guidance

If a request parameter influences the template source itself, treat it as SSTI. Jinja2 can evaluate expressions and reach Python objects and system commands.

---

## 5. Review patterns to grep for

Useful search terms for a Python codebase:

```bash
rg -n "DEBUG\s*=\s*True|render_template_string|secret_key|extra\(|raw\(|execute\(|os\.environ|get\(" .
```

### High-value targets

- Settings and configuration modules
- Views and route handlers
- Authentication and session code
- Database access layers
- Template rendering utilities
- Dependency manifests and environment handling

---

## 6. Review questions to ask

When reading a Python application, ask:

- Where does untrusted input enter the application?
- Does it flow into SQL, templates, sessions, or file operations?
- Is debug mode enabled or exposed?
- Is a secret used for signing or sessions stored in a way that can be leaked?
- Does the app trust client-side data without server-side validation?
- Is the same secret reused across services?

---

## 7. Impact ranking

When reporting findings, rank them by impact:

- Information disclosure: secrets, config values, stack traces
- Privilege escalation: forged sessions or role changes
- Data exposure: SQL injection or unauthorized access to records
- Remote code execution: SSTI leading to command execution

A templated command-execution issue is usually higher severity than a simple data leak.

---

## 8. Suggested remediation patterns

### Good defaults

- Disable debug mode in production
- Never echo secrets into error messages
- Keep secrets out of source and logs
- Parameterize SQL queries
- Avoid client-side trust for auth decisions
- Keep templates static and pass user data as variables
- Avoid reusing the same secret across services

---

## 9. Reporting template

Use a structure like this in your notes or reports:

- Finding title
- Location: file and relevant function
- Root cause
- Attack path
- Impact
- Recommended fix
- Proof or validation notes

Example:

- Title: Debug mode leaks Django secret key
- Location: settings.py and a failing view
- Root cause: exception message includes `SECRET_KEY` while `DEBUG=True`
- Impact: full session/signing compromise
- Fix: disable debug mode and stop echoing secrets

---

## 10. Bottom line

A strong Python review focuses on the same idea everywhere:

- Find the entry point
- Trace the data flow
- Identify the dangerous sink
- Judge whether the sink is reachable and exploitable
- Report the issue clearly, with a fix that addresses the root cause
