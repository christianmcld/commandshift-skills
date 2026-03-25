# Website Design Clone

A Claude Code skill that takes any website URL, analyzes its complete design system, and generates a clean HTML/CSS recreation with extracted design tokens.

## What It Does

- Scrapes and screenshots the target website
- Extracts the full design system: colors, typography, spacing, shadows, border-radius
- Catalogs all UI components (nav, buttons, cards, forms, hero, footer)
- Generates a CSS custom properties file with all design tokens
- Builds a semantic HTML/CSS recreation of the page
- Optionally generates a Tailwind CSS config
- Creates design system documentation

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/website-design-clone.md
```

## Example Usage

```
/website-design-clone

Clone the design of https://linear.app — I want to build something with the same look and feel
```

```
/website-design-clone

Extract the design system from https://stripe.com/payments and give me the tokens + Tailwind config
```

```
/website-design-clone

Analyze https://example.com and recreate just the hero section and navigation in HTML/CSS
```

## Requirements

- **Firecrawl MCP Server** (primary) — For scraping HTML and taking screenshots
- **Playwright MCP** (alternative) — For interactive sites or extracting computed styles
- **Figma MCP** (optional) — If analyzing a Figma file instead of a live site

## Output

A project folder containing:
- `index.html` — Full page recreation with semantic HTML and modern CSS
- `design-tokens.css` — Extracted CSS custom properties
- `design-system.md` — Human-readable documentation of the design system
- `tailwind.config.js` — Tailwind config (optional)
