---
name: check-python
description: Check Python code for errors, anti-patterns, and common issues including syntax errors, undefined variables, unused imports, type mismatches, mutable default arguments, and PEP 8 violations. Use when reviewing Python files for correctness.
---

# Python Code Checker

Read the Python file provided by the user and analyze it for issues across these categories:

## Errors (will cause crashes or incorrect behavior)

- **Syntax errors** — invalid Python syntax
- **Undefined variables** — names used before assignment or without import
- **Type mismatches** — operations on incompatible types (e.g., `"str" + 5`)
- **Potential runtime errors** — IndexError patterns, None dereference, missing dict keys without `.get()`

## Warnings (anti-patterns that lead to bugs)

- **Mutable default arguments** — using `[]` or `{}` as default parameter values
- **Bare except clauses** — `except:` without specifying exception type
- **Wildcard imports** — `from module import *`
- **Unused imports** — imported names never referenced in the code
- **Shadowed built-ins** — variables named `list`, `dict`, `id`, `type`, etc.
- **Unreachable code** — code after `return`, `break`, `continue`, `raise`
- **Incorrect `is` comparisons** — using `is` to compare values instead of `==`

## Style (PEP 8 and readability)

- **Naming conventions** — classes should be CamelCase, functions/variables should be snake_case, constants should be UPPER_CASE
- **Line length** — lines exceeding 120 characters
- **Missing type hints** — function signatures without parameter or return type annotations
- **Deeply nested code** — more than 3 levels of indentation

## Rules

- Respect `# noqa` comments — skip any line with this annotation
- Respect `# type: ignore` comments for type-related warnings
- Do not flag standard patterns like `if __name__ == "__main__":`
- Do not flag intentional underscore-prefixed unused variables (`_`, `_result`)

## Output Format

Group findings by severity:

### Errors
- **Line X**: `code snippet` — explanation → suggested fix

### Warnings
- **Line X**: `code snippet` — explanation → suggested fix

### Style
- **Line X**: `code snippet` — explanation → suggested fix

If no issues are found in a category, omit that section.

End with: "Found N error(s), N warning(s), N style issue(s) in [filename]."
