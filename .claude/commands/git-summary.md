---
description: Summarize recent git activity in the repository
argument-hint: <days-or-commits> (optional, defaults to 7 days)
allowed-tools: [Bash]
---

# Git Activity Summary

Generate a structured summary of recent git activity in this repository.

## Interpret the argument

The user may provide an argument via $ARGUMENTS:
- Number followed by "d" or "days" (e.g., "14d", "30 days") — look back that many days
- Plain number (e.g., "20") — show that many recent commits
- Empty or not provided — default to 7 days

## Gather data using git commands

1. **Recent commits**: `git log --since="<N> days ago" --pretty=format:"%h %ad %an: %s" --date=short`
2. **Hot files** (most frequently changed): `git log --since="<N> days ago" --name-only --pretty=format:""` then sort by frequency
3. **Top contributors**: `git shortlog -sn --since="<N> days ago"`
4. **Active branches**: `git branch -a --sort=-committerdate | head -10`
5. **Working tree status**: `git status --short`

## Output format

### Activity Overview
Total commits in the period, date range covered.

### Top Contributors
Authors ranked by commit count (with counts).

### Hot Files
Top 10 most-changed files — these deserve review attention.

### Branch Status
Recently active branches (up to 10), with last commit date.

### Uncommitted Work
Staged, unstaged, or untracked changes. Flag any merge conflicts.

Keep it concise. If a section has no data, say "None" rather than omitting it.
