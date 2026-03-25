# SEO Audit Skill

A Claude Code skill that performs comprehensive SEO audits on any website, analyzing on-page SEO, meta tags, headings, keyword density, content quality, technical SEO, and competitor positioning.

## What It Does

- Crawls any URL and extracts all SEO-relevant data
- Scores 10 SEO categories on a 100-point scale
- Analyzes title tags, meta descriptions, heading hierarchy, keyword density
- Checks technical SEO (schema markup, canonical tags, Open Graph)
- Compares against competitors ranking for the same keywords
- Generates prioritized action items with specific fix recommendations
- Identifies quick wins you can implement immediately

## Installation

Copy the skill file to your Claude Code commands directory:

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/seo-audit.md
```

Or use it as a project-level skill:

```bash
mkdir -p .claude/commands
cp skill.md .claude/commands/seo-audit.md
```

## Example Usage

```
/seo-audit

Audit https://example.com/blog/my-post for SEO issues
```

```
/seo-audit

Run a full SEO audit on https://mysite.com and compare against https://competitor.com
```

```
/seo-audit

Audit my homepage at https://mysite.com — I'm targeting the keyword "AI consulting services"
```

## Requirements

- **Firecrawl MCP Server** (primary) — Used for scraping pages, mapping site structure, and searching for competitors
- **WebFetch** (fallback) — Can be used if firecrawl is unavailable
- **Web Search** (optional) — For finding competitor pages and checking SERP positioning

## Output

Generates a structured Markdown report with:
- Overall score out of 100
- Category-by-category breakdown with pass/warning/fail status
- Specific, actionable recommendations (not generic advice)
- Priority-ordered action items
- Competitor comparison table (when applicable)
- Quick wins section for immediate improvements
