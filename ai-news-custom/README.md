# AI News Custom Briefing

A comprehensive, personalized AI industry briefing that searches 7+ news categories, scores stories by impact and relevance, and generates an actionable report with predictions and recommendations. Learns your preferences over time.

## What It Does

- Searches 8 AI news categories: Foundation Models, Agents, Dev Tools, Business/Funding, Regulation, Research, Applications, Open Source
- Scores every story on impact (1-10) and personal relevance (1-10)
- Generates a structured briefing with executive summary, top stories, category deep dives, trend analysis, predictions, and action items
- Saves preferences to `~/.ai-news-prefs.json` and refines future briefings based on your interests
- Supports full, brief, and action-items-only output formats

## Install

```bash
cp -r ~/content-engine/skills/ai-news-custom ~/.claude/skills/ai-news-custom
```

## Usage

### Default 30-Day Briefing

```
/skill ai-news-custom
```

### Personalized Briefing

```
/skill ai-news-custom

I'm an AI service business founder focused on Claude Code, AI agents,
and automation tools. Give me the last 30 days.
```

### Focused Briefing

```
/skill ai-news-custom — last 7 days, focus on AI agents and developer tools only
```

### Quick Executive Summary

```
/skill ai-news-custom — brief format, last 2 weeks
```

### Action Items Only

```
/skill ai-news-custom — actionable format, I'm deciding which AI tools to integrate this quarter
```

## Example Output

The full briefing includes:

- **Executive Summary**: 5-7 bullet points of the biggest stories
- **Top 10 Stories**: Scored and ranked with source links
- **8 Category Sections**: 3-5 stories each with concise summaries
- **Trends & Patterns**: Cross-category themes identified
- **3 Predictions**: With confidence levels and reasoning
- **5-7 Action Items**: Specific, time-bound recommendations for your context
- **Sources**: Full list with URLs

Output saved to `~/content-engine/output/ai-briefing-YYYY-MM-DD.md`.

## Preference Learning

After the first run with context about your role/interests, the skill creates `~/.ai-news-prefs.json`. On subsequent runs, it:

- Weights categories you care about more heavily
- Tracks companies and topics you follow
- Avoids re-covering stories from previous briefings
- Adjusts scoring relevance to your role

You can edit the prefs file directly to fine-tune.

## Requirements

- Claude Code CLI
- WebSearch and WebFetch tools (for gathering news)
- Write access to `~/content-engine/output/` for saving briefings
- Optional: `~/.ai-news-prefs.json` for preference persistence (auto-created on first personalized run)
