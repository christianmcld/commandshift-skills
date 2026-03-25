# Ad Campaign Generator

A Claude Code skill that generates complete multi-platform advertising campaigns from a product description. Outputs ready-to-use ad copy for Facebook, Instagram, and Google Ads with targeting, budget allocation, and creative direction.

## What It Does

- Defines 3 distinct audience segments with demographics, psychographics, and pain points
- Generates 5 Facebook/Instagram ad variations per segment (15+ total ads)
- Creates 3 Google Search Responsive Ad groups with keywords, headlines, and extensions
- Recommends budget allocation across platforms with timeline
- Provides KPI targets and industry benchmarks
- Suggests landing page optimizations if a URL is provided
- Uses proven copywriting frameworks (PAS, AIDA, Before-After-Bridge, Social Proof, Direct Offer)

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/ad-campaign-generator.md
```

## Example Usage

```
/ad-campaign-generator

Generate a full ad campaign for my SaaS product — it's a project management tool for freelancers called TaskFlow, priced at $19/mo. Budget is $3K/month. Goal is signups.
```

```
/ad-campaign-generator

Create ads for my e-commerce store https://example.com — we sell premium leather bags. Target audience is professional women 28-45. Budget $5K/month.
```

## Requirements

- **Firecrawl MCP Server** (optional) — For scraping product pages and landing pages to extract messaging
- **Web Search** (optional) — For competitor research and industry benchmarks

## Output

A single Markdown document containing:
- Audience segment profiles
- 15+ Facebook/Instagram ad variations with copy, creative direction, and targeting
- 3 Google Search ad groups with keywords and extensions
- Budget allocation table
- Campaign timeline and KPI targets
- Landing page recommendations
