# Inbox Manager

A Claude Code skill that connects to your Gmail, categorizes every email, drafts responses, and manages your inbox toward zero. Handles bulk cleanup of thousands of emails.

## What It Does

- Audits your inbox: unread counts, top senders, category breakdown
- Categorizes emails into 4 priority levels (Urgent, Action, FYI, Archive)
- Drafts responses for emails requiring replies (you review before sending)
- Bulk cleans newsletters, notifications, and old emails
- Suggests Gmail filters for ongoing automation
- Generates a daily email digest with action items
- Never sends or deletes anything without your explicit approval

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/inbox-manager.md
```

## Example Usage

```
/inbox-manager

Audit my inbox and tell me how bad it is
```

```
/inbox-manager

Process my unread emails from the last 7 days — categorize them and draft responses for anything urgent
```

```
/inbox-manager

I have 3000 unread emails. Help me get to inbox zero — start by cleaning up newsletters and notifications
```

```
/inbox-manager

Set up Gmail filters so newsletters and notifications skip my inbox automatically
```

## Requirements

- **Gmail MCP** (required) — For reading emails, creating drafts, and managing labels
  - `gmail_get_profile` — Verify connection
  - `gmail_search_messages` — Search and filter emails
  - `gmail_read_message` — Read individual emails
  - `gmail_read_thread` — Read email threads
  - `gmail_create_draft` — Draft responses
  - `gmail_list_labels` — Manage labels

## Privacy

- Only creates drafts — never sends emails without your approval
- Never deletes emails — only archives
- Email content stays within your Claude Code session
- Always asks before applying labels or filters
