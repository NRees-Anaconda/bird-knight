---
name: audit-deps
description: Audit project dependencies for vulnerabilities, unpinned versions, deprecated packages, and hygiene issues. Auto-detects dependency files (requirements.txt, package.json, Cargo.toml, go.mod, etc.) and runs native audit tools when available.
---

# Dependency Auditor

Audit project dependencies. If a specific file is provided, use it. Otherwise, auto-detect dependency files.

## Auto-Detection

Look for these files in the project root:
- `requirements.txt`, `requirements/*.txt`
- `pyproject.toml`, `setup.py`, `setup.cfg`
- `package.json`, `package-lock.json`
- `Cargo.toml`, `Cargo.lock`
- `go.mod`, `go.sum`
- `Gemfile`, `Gemfile.lock`
- `pom.xml`, `build.gradle`

## Analysis

For each dependency file found:

### Overview
- Total dependency count (direct vs transitive if lockfile available)
- Language/ecosystem

### Version Pinning
- Fully pinned (e.g., `==1.2.3`, exact version)
- Loosely pinned (e.g., `>=1.2`, `^1.2.3`, `~1.2`)
- Unpinned (no version constraint at all)
- Flag unpinned dependencies as risks for reproducibility

### Known Issues
Run native audit tools if available:
- Python: `pip-audit` or `safety check`
- Node.js: `npm audit` or `yarn audit`
- Rust: `cargo audit`
- Go: `govulncheck`

If tools aren't installed, note this and suggest installing them.

### Dependency Health
- Flag deprecated packages (if detectable)
- Flag duplicate dependencies across multiple files
- Note overly broad version ranges that could introduce breaking changes
- Flag dev dependencies that appear in production dependency lists

## Output Format

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
