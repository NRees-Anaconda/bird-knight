---
description: Analyze code complexity and suggest simplifications
argument-hint: <file-path>
allowed-tools: [Read]
---

# Code Complexity Analyzer

Read the file at the path provided: $ARGUMENTS

Analyze the code's complexity using these metrics:

## Metrics per function/method

### Cyclomatic Complexity
Count decision points: `if`, `elif`, `else`, `for`, `while`, `and`, `or`, `except`, ternary expressions, `case`/`match` arms. Base complexity is 1; add 1 for each decision point.

Rating scale:
- **Simple** (1-5): Easy to understand and test
- **Moderate** (6-10): Requires some thought, consider simplifying
- **Complex** (11-20): Hard to test thoroughly, should be refactored
- **Very Complex** (20+): Extremely difficult to maintain, must be refactored

### Nesting Depth
Maximum level of nested control structures. Flag anything > 3 levels.

### Function Length
Count non-blank, non-comment lines. Flag functions > 30 lines.

### Parameter Count
Flag functions with > 5 parameters.

### Cognitive Complexity
How hard it is for a human to understand the control flow. Factors:
- Nesting increases cognitive load more than flat branching
- `break`, `continue`, `goto` add mental overhead
- Recursion adds complexity
- Boolean logic chains (`a and b or c and not d`)

## Output format

### Summary Table

| Function | Cyclomatic | Nesting | Length | Params | Rating |
|----------|-----------|---------|--------|--------|--------|
| func_a   | 3         | 2       | 15     | 2      | Simple |
| func_b   | 14        | 5       | 68     | 7      | Complex |

### File Score
Overall complexity rating based on the worst-scoring functions.

### Detailed Findings

For each function rated Moderate or above, provide:

**`function_name`** — Complexity: N (Rating)
- What makes it complex (specific constructs contributing)
- Suggested refactoring:
  - **Extract method** — pull out nested logic into named helper functions
  - **Replace conditional with polymorphism** — when switching on type
  - **Introduce parameter object** — when too many params
  - **Guard clauses** — replace nested if/else with early returns
  - **Table-driven logic** — replace long if/elif chains with a dict/map
  - **Decompose boolean expressions** — name complex conditions

Only suggest refactorings that genuinely apply to the specific code.

### Functions that are fine
List Simple-rated functions briefly (just name and score) to confirm they were analyzed.
