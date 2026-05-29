---
name: check-spelling
description: Check any text file for spelling errors, grammar mistakes, and punctuation issues. Use when reviewing documentation, README files, comments, or any prose content for correctness.
---

# Spelling and Grammar Check

Read the file at the path provided by the user.

Review the file contents for:

1. **Spelling errors** — misspelled words, typos, repeated words ("the the")
2. **Grammar errors** — subject-verb agreement, incorrect tense, sentence fragments, run-on sentences, misused words (e.g., "it's" vs "its", "affect" vs "effect")
3. **Punctuation errors** — missing or misplaced commas, periods, apostrophes, quotation marks

## Rules

- Ignore code blocks, file paths, URLs, CLI commands, and technical identifiers (variable names, function names, etc.)
- Ignore frontmatter (YAML between `---` fences)
- Ignore brand names and product names that may not appear in a standard dictionary
- Do NOT suggest stylistic rewrites or tone changes — only flag clear errors
- Do NOT flag correctly-used technical jargon

## Output Format

If errors are found, list them as:

- **Line X**: `original text` → `suggested fix` (reason)

If no errors are found, say "No spelling or grammar errors found."

At the end, provide a summary count: "Found N error(s) in [filename]."
