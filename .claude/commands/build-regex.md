---
description: Build and test regular expressions from natural language descriptions
argument-hint: <what-to-match>
allowed-tools: [Bash]
---

# Regex Builder

Build a regular expression based on this description: $ARGUMENTS

## Process

### 1. Generate the pattern

Create a regex that matches the described pattern. Provide:

- **The regex pattern** itself
- **Plain-English breakdown** — explain each part of the pattern
- **Flags needed** — case-insensitive, multiline, dotall, etc.

### 2. Provide in multiple flavors

Present the regex in these formats:

**Python:**
```python
import re
pattern = re.compile(r"<pattern>", re.FLAGS)
```

**JavaScript:**
```javascript
const pattern = /<pattern>/flags;
```

**grep (POSIX/ERE):**
```bash
grep -E '<pattern>' file.txt
```

**sed:**
```bash
sed -n '/<pattern>/p' file.txt
```

### 3. Test cases

Provide at least 5 strings that SHOULD match and 5 that should NOT:

**Should match:**
- example1
- example2
- ...

**Should NOT match:**
- example1
- example2
- ...

### 4. Verify with code

Run the regex against all test cases to confirm it works:

```bash
python3 -c "
import re
pattern = re.compile(r'<pattern>')
should_match = [...]
should_not_match = [...]
for s in should_match:
    result = 'PASS' if pattern.search(s) else 'FAIL'
    print(f'  {result}: {repr(s)} (expected match)')
for s in should_not_match:
    result = 'PASS' if not pattern.search(s) else 'FAIL'
    print(f'  {result}: {repr(s)} (expected no match)')
"
```

### 5. Warnings

Note any potential issues:
- Catastrophic backtracking risks (nested quantifiers)
- Greedy vs lazy considerations
- Unicode/encoding edge cases
- Differences between regex flavors that might cause portability issues
