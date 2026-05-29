# Skills

A collection of reusable skills for AI coding assistants. Skills are folders of instructions and resources that AI models load dynamically to perform specialized tasks in a repeatable way.

This repository follows the [Agent Skills](https://agentskills.io) standard. Each skill is self-contained in its own folder with a `SKILL.md` file containing instructions and metadata.

## About This Repository

These skills cover common developer workflows — code quality checks, security scanning, documentation generation, web scraping, API testing, and more. They're designed to be generic and portable across projects.

Each skill is self-contained in its own folder with a `SKILL.md` file containing the instructions and metadata that Claude uses. Browse through these skills to get inspiration for your own, or copy them directly into your projects.

## Skills

### Code Quality

| Skill | Description |
|-------|-------------|
| [check-python](skills/check-python) | Check Python code for errors, anti-patterns, and PEP 8 issues |
| [check-spelling](skills/check-spelling) | Check any file for spelling and grammar errors |
| [check-complexity](skills/check-complexity) | Analyze code complexity metrics and suggest refactorings |
| [security-scan](skills/security-scan) | Scan code for OWASP Top 10 vulnerabilities and hardcoded secrets |

### Documentation & Analysis

| Skill | Description |
|-------|-------------|
| [generate-docs](skills/generate-docs) | Generate docstrings, JSDoc, and doc comments for code files |
| [analyze-data](skills/analyze-data) | Profile CSV/JSON data with summary statistics and quality checks |
| [git-summary](skills/git-summary) | Summarize recent git activity, contributors, and hot files |

### Web & APIs

| Skill | Description |
|-------|-------------|
| [scrape-web](skills/scrape-web) | Extract structured data from web pages |
| [test-api](skills/test-api) | Test API endpoints and produce structured reports |

### Utilities

| Skill | Description |
|-------|-------------|
| [build-regex](skills/build-regex) | Build and test regex patterns from natural language |
| [audit-deps](skills/audit-deps) | Audit project dependencies for vulnerabilities and issues |

## Usage

### Claude Code

Copy a skill folder into your project's `.claude/skills/` directory, or install from this repository:

```bash
# Copy a skill into your project
cp -r skills/check-python /path/to/your/project/.claude/skills/
```

After installing, Claude will use the skill automatically when relevant, or you can reference it directly.

### Creating Your Own Skills

Use the [template](template/SKILL.md) as a starting point:

```yaml
---
name: my-skill-name
description: A clear description of what this skill does and when to use it
---

# My Skill Name

[Instructions that Claude will follow]

## Examples
- Example usage 1
- Example usage 2

## Guidelines
- Guideline 1
- Guideline 2
```

The frontmatter requires only two fields:
- `name` — A unique identifier (lowercase, hyphens for spaces)
- `description` — A complete description of what the skill does and when to use it

The markdown body contains the instructions, examples, and guidelines that Claude will follow.

## Repository Structure

```
bird-knight/
├── skills/           # All skills, one folder each
│   ├── check-python/
│   │   └── SKILL.md
│   ├── check-spelling/
│   │   └── SKILL.md
│   └── ...
├── template/         # Skill template for creating new skills
│   └── SKILL.md
├── spec/             # Agent Skills specification reference
│   └── agent-skills-spec.md
└── README.md
```

## Contributing

To add a new skill:

1. Create a folder under `skills/` with a descriptive name
2. Add a `SKILL.md` with proper frontmatter (`name` and `description`)
3. Write clear instructions in the markdown body
4. Optionally add `scripts/`, `examples/`, or other supporting files

## License

Apache 2.0
