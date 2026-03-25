# AI News Briefing

A Claude Code skill that searches for the latest AI developments from the last 30 days, filters by your interests, and generates a personalized briefing with action items.

## What It Does

- Searches 7+ categories: models, products, industry, open source, research, regulation, tools
- Scores every story on impact, relevance, recency, and credibility
- Highlights the top 3 stories that matter most
- Organizes findings into scannable tables and summaries
- Provides "What to Watch" predictions for the next month
- Generates personalized action items based on your role and interests
- Links every claim to its source

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/ai-news-briefing.md
```

## Example Usage

```
/ai-news-briefing

Give me the AI news briefing for the last 30 days. I'm a founder building SaaS products.
```

```
/ai-news-briefing

AI briefing focused on open source models and developer tools. Deep dive format.
```

```
/ai-news-briefing

What happened in AI this month? Executive summary, skip regulation news.
```

## Requirements

- **Web Search** (required) — For finding current AI news and developments
- **Firecrawl MCP Server** (optional) — For scraping full articles for deeper analysis
- **Hugging Face MCP** (optional) — For checking trending models and papers

## Output

A structured Markdown briefing:
- Top 3 most important developments
- Category-by-category tables (models, industry, open source, research, regulation)
- Expanded analysis on key stories
- Predictions for next month
- Personalized action items
- Full source list
