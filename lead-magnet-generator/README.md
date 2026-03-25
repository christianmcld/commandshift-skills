# Lead Magnet Generator Skill

Generates professional lead magnets as self-contained HTML files, styled with CommandShift's dark branding, ready for PDF conversion.

## What It Does

Give it a topic and a format, and it produces a complete, designed HTML document you can convert to PDF and use as a downloadable lead magnet. Content is specific and actionable, not generic filler. Every output includes branding, a call-to-action, and print-friendly styling.

## Supported Formats

| Format | Best For | Typical Length |
|--------|----------|----------------|
| `checklist` | Step-by-step validation lists | 3-4 pages |
| `framework` | Strategic models and methodologies | 4-6 pages |
| `guide` | In-depth educational content | 5-8 pages |
| `template` | Fill-in-the-blank tools | 3-5 pages |
| `cheatsheet` | Quick reference / dense info | 2-3 pages |

## Install

Place `skill.md` in your Claude Code skills directory:

```
~/content-engine/skills/lead-magnet-generator/skill.md
```

No external dependencies. Output is pure HTML with inline CSS.

## Example Usage

### Basic checklist
```
/lead-magnet-generator

Topic: AI automation for e-commerce businesses
Format: checklist
```

### Framework with custom audience
```
/lead-magnet-generator

Topic: Building an AI-first agency
Format: framework
Audience: Marketing agency owners doing $500K-$2M revenue
CTA: Schedule a strategy call at commandshift.ai/call
```

### Comprehensive guide
```
/lead-magnet-generator

Topic: Replacing your VA with AI agents
Format: guide
Page count: 8 pages
```

## Output

Files are saved to `~/content-engine/output/lead-magnets/` as self-contained HTML.

### Converting to PDF

**Option 1 — Browser print:**
```bash
open ~/content-engine/output/lead-magnets/your-file.html
# Cmd+P > Save as PDF
```

**Option 2 — Command line:**
```bash
wkhtmltopdf ~/content-engine/output/lead-magnets/your-file.html output.pdf
```

**Option 3 — Puppeteer (best quality):**
```bash
npx puppeteer-pdf ~/content-engine/output/lead-magnets/your-file.html -o output.pdf
```

## Brand Customization

Default branding is CommandShift (dark theme, cyan accent). Override with:

```
Brand name: YourBrand
Accent color: #FF6B35
CTA: Visit yourbrand.com/free-audit
```

## Requirements

- Claude Code with skills support
- A browser or PDF conversion tool for final output
- No API keys needed
