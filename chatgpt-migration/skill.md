---
name: chatgpt-migration
description: Import ChatGPT conversation exports into Claude memory format — extract memories, custom instructions, and key conversations.
---

# ChatGPT Migration Skill

You help users migrate from ChatGPT to Claude by parsing their ChatGPT data export, extracting useful information, and converting it into Claude-native formats (memory files, CLAUDE.md, and organized conversation summaries).

## Activation

This skill activates when the user:
- Mentions migrating from ChatGPT
- Provides a ChatGPT data export (conversations.json or the full zip)
- Asks to import ChatGPT history, memories, or custom instructions

## Input

The user should provide one or more of:
1. **conversations.json** — The main conversation export file from ChatGPT (Settings > Data Controls > Export Data)
2. **model_comparisons.json** — Optional, contains preference data
3. **message_feedback.json** — Optional, contains thumbs up/down data
4. **user.json** — Contains custom instructions and user profile

The user may provide:
- The file path to the extracted export directory
- Or paste specific content directly

## Processing Pipeline

### Step 1: Parse the Export

Read and parse the ChatGPT export files. The primary file is `conversations.json`, which has this structure:

```json
[
  {
    "title": "Conversation Title",
    "create_time": 1700000000.0,
    "update_time": 1700001000.0,
    "mapping": {
      "node-id": {
        "id": "node-id",
        "message": {
          "author": { "role": "user" | "assistant" | "system" },
          "content": { "parts": ["message text"] },
          "create_time": 1700000000.0
        },
        "parent": "parent-node-id",
        "children": ["child-node-id"]
      }
    }
  }
]
```

To extract messages in order:
1. Find the root node (the one with no parent or parent is null).
2. Walk the tree following `children` arrays.
3. Collect messages in traversal order, filtering for user and assistant roles.

### Step 2: Extract Custom Instructions

From `user.json`, extract:
- `custom_instructions.about_user_message` — User's self-description
- `custom_instructions.about_model_message` — How the user wants the AI to respond

Convert these into CLAUDE.md format:

```markdown
# User Context (migrated from ChatGPT custom instructions)

## About the User
[content from about_user_message]

## Response Preferences
[content from about_model_message]
```

### Step 3: Extract Memory Items

ChatGPT memories are stored as short factual statements. If the export contains a memories section, extract each one. Convert to Claude memory format:

```markdown
# Migrated Memories (from ChatGPT, [date])

## User Profile
- [memory items about the user]

## Preferences
- [memory items about preferences]

## Projects
- [memory items about ongoing work]

## Technical
- [memory items about tech stack, tools, etc.]
```

Categorize each memory item by analyzing its content:
- Names, roles, location, personal info -> User Profile
- Style preferences, communication preferences -> Preferences
- Project names, goals, deadlines -> Projects
- Languages, frameworks, tools, APIs -> Technical

### Step 4: Analyze Conversations

Process all conversations and generate:

**A. Conversation Index** — A summary table:
```markdown
| # | Title | Date | Messages | Category | Key Topics |
|---|-------|------|----------|----------|------------|
| 1 | ... | ... | ... | ... | ... |
```

**B. High-Value Conversations** — Identify conversations worth preserving:
- Conversations with 20+ messages (deep discussions)
- Conversations with code blocks (technical work)
- Conversations referenced or returned to multiple times
- Recent conversations (last 30 days)

For each high-value conversation, create a summary:
```markdown
### [Title]
**Date:** [date] | **Messages:** [count]
**Summary:** [2-3 sentence summary]
**Key Outputs:** [any code, decisions, or artifacts produced]
**Relevant To:** [which current projects or workflows this relates to]
```

**C. Pattern Analysis** — Identify recurring themes:
- Most discussed topics
- Common request types (coding, writing, research, brainstorming)
- Tools and technologies mentioned frequently
- Projects that span multiple conversations

### Step 5: Generate Output Files

Create these files:

**1. `~/claude-migration/CLAUDE.md`**
Combined custom instructions converted to Claude format. Include user context, response preferences, and key project context extracted from conversations.

**2. `~/claude-migration/memories.md`**
All extracted memory items, categorized and deduplicated.

**3. `~/claude-migration/conversation-index.md`**
Full index of all conversations with metadata.

**4. `~/claude-migration/highlights.md`**
Summaries of high-value conversations.

**5. `~/claude-migration/patterns.md`**
Analysis of usage patterns, common topics, and recommendations for setting up Claude workflows.

**6. `~/claude-migration/migration-report.md`**
Summary of what was migrated:
```markdown
# ChatGPT to Claude Migration Report

**Date:** [today]
**Export Date Range:** [first conversation] to [last conversation]

## Statistics
- Total conversations: [n]
- Total messages: [n]
- High-value conversations preserved: [n]
- Memory items extracted: [n]
- Custom instructions: [migrated/not found]

## What Was Migrated
- [x] Custom instructions -> CLAUDE.md
- [x] Memory items -> memories.md
- [x] Conversation summaries -> highlights.md
- [x] Usage patterns -> patterns.md

## Recommended Next Steps
1. Review CLAUDE.md and adjust for Claude's capabilities
2. Move memories.md content into your Claude memory system
3. Review highlights.md for any conversations to reference in future work
4. [Specific recommendations based on their usage patterns]
```

## Handling Large Exports

ChatGPT exports can be very large (100MB+ for heavy users). Strategy:

1. **Don't try to process everything at once.** Read the file in chunks or parse conversation-by-conversation.
2. **Prioritize recent conversations.** Start with the last 90 days, then offer to process older ones.
3. **Skip system messages and tool outputs** that don't contain useful content.
4. **Deduplicate.** ChatGPT users often ask the same thing in different conversations.

If the file is too large to process in one pass, tell the user:
> "Your export contains [N] conversations. I'll start with the most recent 100 and the highest-value older ones. Want me to process more after?"

## Edge Cases

- **No custom instructions**: Skip that section, note it in the report.
- **Non-English conversations**: Preserve in original language, note the language.
- **Conversations with images/files**: Note that these assets aren't in the text export. List what was referenced.
- **Very old exports** (pre-GPT-4): Flag that conversation quality may vary.
- **Shared conversations**: These may appear in the export — include them but flag as shared.

## Privacy Note

Remind the user: "Your ChatGPT export may contain sensitive information. The migration files I create will be stored locally. Review them before sharing or syncing anywhere."

## Example Interaction

**User:** "I just exported my ChatGPT data. The files are at ~/Downloads/chatgpt-export/. Can you migrate everything to Claude format?"

**Action:**
1. Read `~/Downloads/chatgpt-export/conversations.json` and `user.json`
2. Parse and process per the pipeline above
3. Create all output files in `~/claude-migration/`
4. Present the migration report to the user
5. Suggest next steps for getting Claude set up with their context
