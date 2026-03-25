# Skill Builder

A meta-skill that generates complete Claude Code skills from plain-language descriptions. Describe what you want to automate, and it produces a production-ready skill.md and README.md with proper structure, error handling, and documentation.

## Install

```bash
cp -r ~/content-engine/skills/skill-builder ~/.claude/skills/skill-builder
```

Or ensure your Claude Code config includes `~/content-engine/skills/` as a skills directory.

## Usage

```
/skill skill-builder
```

Then describe what you want:

- "Create a skill that audits npm packages for outdated dependencies and generates an upgrade plan"
- "Build a skill that takes a meeting transcript and produces action items in Notion"
- "I need a skill that monitors a list of URLs for uptime and writes a daily report"

### Specifying Output Location

```
/skill skill-builder — save to ~/my-project/skills/url-monitor/
```

### Enhancing Existing Skills

If a similar skill already exists in `~/content-engine/skills/`, the builder will detect it and offer to enhance rather than duplicate.

## Example Output

For the prompt "skill that turns GitHub issues into a prioritized sprint backlog":

```
Created:
  ~/content-engine/skills/sprint-planner/skill.md (145 lines)
  ~/content-engine/skills/sprint-planner/README.md (42 lines)

Skill: sprint-planner
Pattern: Research-then-Synthesize
Tools: [Bash (gh CLI), Read, Write, Grep]
```

The generated skill.md includes frontmatter, role assignment, multi-step workflow, output format spec, error handling, and constraints — ready to invoke immediately.

## Requirements

- Claude Code CLI
- No external dependencies for the builder itself
- Generated skills may require additional tools (MCP servers, API keys) depending on what they automate
