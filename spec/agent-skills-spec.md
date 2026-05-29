# Agent Skills Spec

The official Agent Skills specification is located at [https://agentskills.io/specification](https://agentskills.io/specification).

## Quick Reference

A skill is a folder containing at minimum a `SKILL.md` file with:

1. **YAML frontmatter** (between `---` fences):
   - `name` (required) — unique identifier, lowercase with hyphens
   - `description` (required) — what the skill does and when to use it

2. **Markdown body** — instructions, examples, and guidelines that the AI model follows

Skills may also include supporting files:
- `scripts/` — helper scripts the skill can invoke
- `examples/` — example usage patterns
- `LICENSE.txt` — license terms
