# ChatGPT Migration Skill

Parses your ChatGPT data export and converts it into Claude-native formats: memory files, CLAUDE.md instructions, conversation summaries, and usage pattern analysis.

## What It Does

When you export your data from ChatGPT (Settings > Data Controls > Export Data), you get a zip file containing JSON files with your conversations, custom instructions, and memories. This skill reads those files and produces organized, useful output that helps you onboard to Claude without losing context.

### It extracts:
- **Custom instructions** into a CLAUDE.md file
- **Memory items** into categorized memory files
- **Conversation highlights** with summaries of your most important chats
- **Usage patterns** showing your common topics, tools, and workflows
- **Migration report** with statistics and recommended next steps

## Install

Place `skill.md` in your Claude Code skills directory:

```
~/content-engine/skills/chatgpt-migration/skill.md
```

## How to Export from ChatGPT

1. Go to [chat.openai.com](https://chat.openai.com)
2. Settings > Data Controls > Export Data
3. Click "Export" and wait for the email
4. Download and unzip the file

You'll get a folder with:
- `conversations.json` (main file)
- `user.json` (custom instructions)
- `model_comparisons.json` (optional)
- `message_feedback.json` (optional)

## Example Usage

### Full migration
```
/chatgpt-migration

My export is at ~/Downloads/chatgpt-export/
Migrate everything to Claude format.
```

### Selective migration
```
/chatgpt-migration

Only migrate conversations from the last 60 days.
Export path: ~/Downloads/chatgpt-2026-03-25/
```

### Just extract instructions
```
/chatgpt-migration

I only want my custom instructions converted to CLAUDE.md.
File: ~/Downloads/chatgpt-export/user.json
```

## Output

All files are created in `~/claude-migration/`:

```
~/claude-migration/
  CLAUDE.md                 # Custom instructions in Claude format
  memories.md               # Extracted and categorized memory items
  conversation-index.md     # Full index of all conversations
  highlights.md             # Summaries of important conversations
  patterns.md               # Usage analysis and workflow insights
  migration-report.md       # Stats and next steps
```

## After Migration

1. Review `CLAUDE.md` and copy relevant parts into your project's CLAUDE.md or `~/.claude/CLAUDE.md`
2. Review `memories.md` and add items to your Claude memory system
3. Skim `highlights.md` for any conversations you want to reference
4. Read `patterns.md` for suggestions on optimizing your Claude setup

## Requirements

- Claude Code with skills support
- A ChatGPT data export (the zip file or extracted folder)
- No API keys or external services needed

## Privacy

Your ChatGPT export may contain sensitive information (personal details, API keys, business data). All processing happens locally. Review the output files before syncing or sharing them.
