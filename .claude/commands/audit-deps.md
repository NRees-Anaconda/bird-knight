---
description: Audit project dependencies for issues and vulnerabilities
argument-hint: <dependency-file> (optional, auto-detects)
allowed-tools: [Read, Bash]
---

# Dependency Auditor

Audit dependencies for the project. If a file is specified, use it: $ARGUMENTS

If no argument is provided, auto-detect dependency files by looking for:
- `requirements.txt`, `requirements/*.txt`
- `pyproject.toml`, `setup.py`, `setup.cfg`
- `package.json`, `package-lock.json`
- `Cargo.toml`
- `go.mod`, `go.sum`
- `Gemfile`, `Gemfile.lock`
- `pom.xml`, `build.gradle`

## For each dependency file found, analyze:

### Overview
- Total dependency count (direct vs transitive if lockfile available)
- Language/ecosystem

### Version Pinning
- Fully pinned (e.g., `==1.2.3`, exact version)
- Loosely pinned (e.g., `>=1.2`, `^1.2.3`, `~1.2`)
- Unpinned (no version constraint at all)
- Flag unpinned dependencies as risks for reproducibility

### Known Issues
- Run native audit tools if available:
  - Python: `pip-audit` or `safety check`
  - Node.js: `npm audit` or `yarn audit`
  - Rust: `cargo audit`
  - Go: `govulncheck`
- If tools aren't installed, note this and suggest installing them

### Dependency Health
- Flag any deprecated packages (if detectable)
- Flag duplicate dependencies across multiple files
- Note overly broad version ranges that could introduce breaking changes
- Flag dev dependencies that appear in production dependency lists

## Output format

Group findings by severity:

### Critical
Known vulnerabilities from audit tools.

### Warning
Unpinned versions, deprecated packages, overly broad ranges.

### Info
Suggestions for cleanup, consolidation, or best practices.

---

End with:
- Total dependencies scanned
- Summary count by severity
- Top 3 actionable recommendations
