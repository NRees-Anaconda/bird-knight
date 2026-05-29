---
description: Scan code for security vulnerabilities and hardcoded secrets
argument-hint: <file-or-directory>
allowed-tools: [Read, Bash]
---

# Security Scanner

Scan the file or directory provided for security vulnerabilities: $ARGUMENTS

If a directory is given, find source files (`.py`, `.js`, `.ts`, `.go`, `.rb`, `.java`, `.php`, `.rs`) and scan each one.

## Check for these vulnerability classes

### Injection
- **SQL Injection** — string concatenation or f-strings in SQL queries instead of parameterized queries
- **Command Injection** — user input passed to `os.system()`, `subprocess.shell=True`, `eval()`, `exec()`
- **XSS** — unescaped user input rendered in HTML/templates
- **Path Traversal** — user input in file paths without sanitization (`../` attacks)
- **SSRF** — user-controlled URLs passed to HTTP clients without allowlist validation

### Secrets & Credentials
- **Hardcoded API keys** — patterns like `api_key = "sk-..."`, `token = "ghp_..."`
- **Hardcoded passwords** — `password = "..."`, `passwd`, `secret`
- **Private keys** — `BEGIN RSA PRIVATE KEY` or similar PEM blocks
- **Connection strings** — database URLs with embedded credentials

### Crypto & Auth
- **Weak hashing** — MD5 or SHA1 used for passwords or security-sensitive data
- **Insecure randomness** — `random.random()` used for tokens/secrets instead of `secrets` module
- **Missing auth checks** — route handlers without authentication decorators/middleware

### Data Exposure
- **Verbose error messages** — stack traces or internal paths leaked to users
- **Debug mode in production** — `DEBUG = True`, `app.debug = True`
- **Sensitive data in logs** — logging passwords, tokens, PII

### Deserialization
- **Unsafe pickle/yaml** — `pickle.loads()` on untrusted data, `yaml.load()` without SafeLoader

## Severity ratings

- **Critical** — directly exploitable, immediate risk (RCE, SQLi, hardcoded prod secrets)
- **High** — exploitable with some conditions (XSS, path traversal, weak crypto for auth)
- **Medium** — defense-in-depth issues (verbose errors, missing headers, debug mode)
- **Low** — informational, best-practice suggestions

## Output format

For each finding:

| Severity | File | Line | Issue |
|----------|------|------|-------|
| CRITICAL | path/to/file.py | 42 | SQL injection via string formatting |

**Code:**
```
vulnerable code snippet
```

**Risk:** Explanation of what an attacker could do.

**Fix:** Specific remediation with code example.

---

End with a summary table:

| Severity | Count |
|----------|-------|
| Critical | N |
| High | N |
| Medium | N |
| Low | N |

"Scanned N file(s). Found N total issue(s)."
