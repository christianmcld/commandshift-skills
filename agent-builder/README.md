# Agent Builder

A Claude Code skill for designing and building new Claude Code agents from scratch.

## What It Does

Provides a structured, repeatable framework for creating Claude Code agents. Instead of writing ad-hoc prompts, this skill walks you through:

1. Defining the agent's mission, inputs, and outputs
2. Selecting the right tool set
3. Building the system prompt with proper structure
4. Adding error handling for all common failure modes
5. Testing with happy path, edge case, and failure scenarios
6. Writing documentation

Includes three ready-to-use templates: **Research Agent**, **Content Agent**, and **Data Processing Agent**.

## Install

Copy or symlink to your skills directory:

```bash
cp -r ~/content-engine/skills/agent-builder ~/.claude/skills/agent-builder
```

Or reference it directly if your Claude Code config points to `~/content-engine/skills/`.

## Usage

Invoke from Claude Code:

```
/skill agent-builder
```

Then describe what you want to build:

- "Build me an agent that audits a codebase for security vulnerabilities"
- "Create a research agent that tracks competitor pricing"
- "I need a data processing agent that normalizes CSV address fields"

### Quick Start with Templates

If your agent fits a common pattern, ask for a template directly:

```
/skill agent-builder — use the research agent template for tracking AI funding rounds
```

```
/skill agent-builder — use the content template for LinkedIn carousel posts
```

```
/skill agent-builder — use the data processing template for deduplicating contact lists
```

## Example Output

Running the skill produces two files in your target directory:

```
my-agent/
  skill.md      # The agent's complete instructions
  README.md     # Documentation for users
```

The skill.md will contain valid frontmatter, a multi-step workflow, output format spec, error handling, and constraints — ready to use as a Claude Code skill immediately.

## Requirements

- Claude Code CLI
- No external dependencies — this skill only generates markdown files
- For agents that use web search: WebSearch/WebFetch tools must be available
- For agents that use MCP integrations: relevant MCP servers must be configured
