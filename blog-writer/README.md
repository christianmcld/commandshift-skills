# Blog Writer

A Claude Code skill that writes SEO-optimized blog posts backed by real research, specific data, and human-quality writing. Built to combat "AI slop" with strict quality rules.

## What It Does

- Researches the topic: keyword analysis, competitor content gaps, real statistics
- Generates a detailed outline with SEO targets before writing
- Writes 1500-3000 word posts with proper H1/H2/H3 hierarchy
- Includes real data points, named sources, and specific examples
- Enforces anti-AI-slop rules (banned phrases, mandatory specificity)
- Adds a meta description, FAQ schema, internal linking suggestions
- Provides social media distribution copy (Twitter, LinkedIn, email)
- Runs 5 quality checks before delivery

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/blog-writer.md
```

## Example Usage

```
/blog-writer

Write a blog post about "how to use AI for small business marketing" — target keyword is "AI marketing for small business"
```

```
/blog-writer

I need a 2000-word post comparing the top 5 project management tools for remote teams. Include real pricing and features.
```

```
/blog-writer

Write a thought leadership piece about why most AI implementations fail. Target audience: CTOs and VP Engineering.
```

## Requirements

- **Web Search** (important) — For finding real statistics, competitor analysis, and current data
- **Firecrawl MCP Server** (optional) — For scraping top-ranking competitor articles

## Output

A complete blog post package:
- Full article in Markdown with proper heading hierarchy
- Meta title and description
- SEO checklist (verified)
- Internal and external linking suggestions
- Social media distribution copy
- FAQ schema markup (JSON-LD)
