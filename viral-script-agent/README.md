# Viral Script Agent

A Claude Code skill that researches top creators in any niche, reverse-engineers their viral content patterns, and generates 10 original scripts optimized for engagement.

## What It Does

- Researches the top 5-10 creators in your niche using web search
- Identifies 8+ hook patterns that drive engagement (cost replacement, capability reveal, contrarian, etc.)
- Catalogs 5 proven script structures with examples from the niche
- Extracts current trends (topics, formats, audio, visual styles)
- Generates 10 fully-scripted, ready-to-film pieces with:
  - Beat-by-beat script with timing
  - Visual/screen direction
  - Caption with hashtags
  - Posting notes and thumbnail suggestions
- Builds a 2-week content calendar with content mix ratios

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/viral-script-agent.md
```

## Example Usage

```
/viral-script-agent

My niche is AI tools for business. I post Instagram Reels. I have 5K followers. Generate scripts.
```

```
/viral-script-agent

Analyze what @levelsio and @marc_louvion are doing on Twitter for indie hacker content. Generate scripts for my YouTube Shorts.
```

```
/viral-script-agent

I run a fitness coaching business. Research what's going viral in fitness TikTok and write me 10 scripts.
```

## Requirements

- **Web Search** (primary) — For researching creators and trends
- **Firecrawl MCP Server** (optional) — For deeper analysis of specific creator pages
- **Apify MCP** (optional) — For scraping social media profiles if needed

## Output

A complete content package in Markdown:
1. Competitor analysis with engagement patterns
2. Pattern library (hooks, structures, CTAs)
3. 10 original scripts with full production direction
4. 2-week content calendar
5. Current trend report for the niche
