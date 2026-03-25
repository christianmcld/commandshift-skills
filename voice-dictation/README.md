# Voice Dictation Skill

Transforms raw voice transcripts into polished, ready-to-send content. Supports email, Slack messages, code documentation, structured notes, and meeting notes.

## What It Does

You speak (or paste a messy transcript), specify the output format, and Claude cleans it up into properly formatted, professional content. It removes filler words, fixes grammar, organizes ideas, extracts action items, and applies the right tone for your audience.

## Supported Output Types

| Type | Use Case |
|------|----------|
| `email` | Professional emails with subject line, proper structure, clear CTA |
| `slack` | Concise, thread-friendly Slack messages |
| `code` | JSDoc/docstring comments, bug reports, feature specs |
| `notes` | Structured notes with key points, details, action items |
| `meeting-notes` | Full meeting format with attendees, decisions, action table |

## Install

Place `skill.md` in your Claude Code skills directory:

```
~/content-engine/skills/voice-dictation/skill.md
```

No additional dependencies for the formatting skill itself.

For voice capture, use one of:
- **macOS Dictation**: System Settings > Keyboard > Dictation (built-in, free)
- **Whisper**: `brew install openai-whisper` or use the API
- **Any speech-to-text tool** that outputs a text transcript

## Example Usage

### Basic email formatting
```
/voice-dictation

Raw transcript: "hey so I wanted to follow up with the client about the proposal we sent last week I think we should offer them the premium tier because they mentioned wanting analytics and um also see if they can do a quarterly commitment instead of monthly"

Format: email
Recipient: Client (formal)
```

### Slack message
```
/voice-dictation

"the deploy went through all tests passing but we need to update the env vars on staging before QA can start testing probably takes 30 minutes"

Format: slack
```

### Meeting notes
```
/voice-dictation

"ok so in the standup today we had me sarah and jake and we talked about the migration timeline sarah said the database migration scripts are ready jake is still working on the frontend components he needs two more days and we decided to push the staging deploy to friday instead of wednesday action items are jake finishes components by thursday sarah runs migration dry run tomorrow and I update the client on the new timeline"

Format: meeting-notes
```

## Requirements

- Claude Code with skills support
- A way to capture voice as text (macOS Dictation, Whisper, or manual paste)
- No API keys or external services needed for the formatting step

## Tips

- You can pipe Whisper output directly: `whisper audio.mp3 --output_format txt && cat audio.txt | claude "format as email"`
- If you don't specify a format, the skill will ask you to choose one
- Works with any language — it will translate to English by default unless told otherwise
- The skill preserves technical jargon and proper nouns exactly as spoken
