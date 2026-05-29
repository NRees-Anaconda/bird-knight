---
description: Generate documentation (docstrings, JSDoc, comments) for a code file
argument-hint: <file-path>
allowed-tools: [Read, Edit, Write]
---

# Documentation Generator

Read the file at the path provided: $ARGUMENTS

Analyze the code and generate appropriate documentation based on the file type.

## For Python files

Generate Google-style docstrings for:
- **Module level** — brief description of the file's purpose at the top
- **Classes** — purpose, attributes, and usage example
- **Functions/methods** — following this format:

```python
def function_name(param1: str, param2: int = 0) -> bool:
    """Brief one-line description.

    Longer explanation if the function is non-trivial.

    Args:
        param1: Description of param1.
        param2: Description of param2. Defaults to 0.

    Returns:
        Description of return value.

    Raises:
        ValueError: When param1 is empty.
    """
```

## For JavaScript/TypeScript files

Generate JSDoc comments:

```javascript
/**
 * Brief description.
 *
 * @param {string} param1 - Description
 * @param {number} [param2=0] - Description (optional)
 * @returns {boolean} Description
 * @throws {Error} When something fails
 * @example
 * const result = functionName("test");
 */
```

## For other languages

Generate idiomatic doc comments for the language (Rustdoc for Rust, GoDoc for Go, XML docs for C#, etc.).

## Rules

- Infer parameter descriptions from the code logic, variable names, and usage context
- Include a usage example for any public function that isn't self-explanatory
- Preserve existing documentation that is correct and complete
- Flag existing docs that contradict the actual code behavior
- Do NOT document obvious getters/setters or trivial one-liners unless their behavior is surprising
- Keep docstrings concise — one line if the function is simple

## Output

Present the generated documentation showing what would be added/changed. Then ask:

"Would you like me to apply these docstrings to the file, or output them separately?"

If the user wants them applied, use Edit to insert them into the file.
