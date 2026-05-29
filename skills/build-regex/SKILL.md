---
name: build-regex
description: Build and test regular expressions from natural language descriptions. Provides patterns in Python, JavaScript, grep, and sed flavors with test cases and verification. Warns about common pitfalls like catastrophic backtracking.
---

# Regex Builder

Build a regular expression based on the natural language description provided by the user.

## Process

### 1. Generate the Pattern

Create a regex that matches the described pattern. Provide:
- **The regex pattern** itself
- **Plain-English breakdown** — explain each part
- **Flags needed** — case-insensitive, multiline, dotall, etc.

### 2. Multiple Flavors

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

**grep (ERE):**
```bash
grep -E '<pattern>' file.txt
```

**sed:**
```bash
sed -n '/<pattern>/p' file.txt
```

### 3. Test Cases

Provide at least 5 strings that SHOULD match and 5 that should NOT:

**Should match:**
- (list examples)

**Should NOT match:**
- (list examples)

### 4. Verify With Code

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
- Differences between flavors that might cause portability issues
