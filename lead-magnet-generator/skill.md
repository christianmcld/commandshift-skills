---
name: lead-magnet-generator
description: Generate lead magnets as HTML — checklists, frameworks, guides, and templates — styled in dark CommandShift branding.
---

# Lead Magnet Generator Skill

You generate professional lead magnets as self-contained HTML files ready for PDF conversion. Every output uses CommandShift's dark theme branding and is designed to capture leads for AI service businesses.

## Activation

This skill activates when the user asks to create a lead magnet, downloadable resource, checklist, framework, guide, or template for marketing purposes.

## Input

Required:
1. **Topic** — The subject of the lead magnet (e.g., "AI automation for agencies", "ChatGPT prompt engineering")
2. **Format** — One of: `checklist`, `framework`, `guide`, `template`, `cheatsheet`

Optional:
- **Target audience** — Who is this for? Default: business owners and operators.
- **Page count target** — How substantial? Default: 3-5 pages equivalent.
- **CTA** — Call to action at the end. Default: "Book a free automation audit at commandshift.ai"
- **Brand name** — Default: CommandShift
- **Accent color** — Default: #00D4FF (CommandShift cyan)

## Brand Styling

All output uses this base design system:

```css
:root {
  --bg-primary: #0A0A0F;
  --bg-secondary: #12121A;
  --bg-card: #1A1A25;
  --text-primary: #FFFFFF;
  --text-secondary: #A0A0B0;
  --accent: #00D4FF;
  --accent-hover: #00B8E0;
  --border: #2A2A3A;
  --success: #00FF88;
  --warning: #FFB800;
  --gradient: linear-gradient(135deg, #00D4FF, #7B61FF);
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  background: var(--bg-primary);
  color: var(--text-primary);
  line-height: 1.7;
  margin: 0;
  padding: 0;
}
```

## Processing Steps

1. **Analyze the topic**: Identify the core value proposition and what the reader will gain.
2. **Research depth**: Use your knowledge to include specific, actionable content — not generic filler.
3. **Structure the content**: Apply the appropriate format template below.
4. **Write compelling copy**: Every section must deliver tangible value. No fluff.
5. **Generate complete HTML**: Single self-contained file with inline CSS, no external dependencies.
6. **Include conversion elements**: Header, footer CTA, and subtle branding throughout.

## Format Templates

### Checklist Format

Structure:
- Title page with hook headline
- Brief intro (why this checklist matters — 2-3 sentences)
- Checklist sections (3-5 sections, 4-8 items each)
- Each item: checkbox + actionable task + one-line explanation
- Summary/next steps section
- CTA footer

HTML pattern for checklist items:
```html
<div class="checklist-item">
  <div class="checkbox"></div>
  <div class="item-content">
    <h4>Action item title</h4>
    <p>Brief explanation of why this matters and how to do it.</p>
  </div>
</div>
```

### Framework Format

Structure:
- Title page with framework name and one-line description
- Framework overview diagram (use CSS grid/flexbox for visual layout)
- Step-by-step breakdown (3-7 steps)
- Each step: number + name + description + example + common mistakes
- Implementation timeline
- CTA footer

The framework should have a memorable name (acronym or metaphor). Examples: "The SCALE Framework", "The 5-Layer Automation Stack", "The Revenue Engine Model".

### Guide Format

Structure:
- Title page with benefit-driven headline
- Table of contents (linked anchors)
- Introduction (the problem + what they'll learn)
- Chapters (3-6 chapters, each with subsections)
- Key takeaways per chapter (boxed callout)
- Resource list / tool recommendations
- CTA footer

Guides should be the most substantial format — aim for depth equivalent to 5-8 printed pages.

### Template Format

Structure:
- Title page explaining what the template is for
- Instructions section (how to use this template)
- The template itself (tables, forms, or structured layouts the reader fills in)
- Filled example (showing a completed version)
- Tips for customization
- CTA footer

Use table layouts and form-like styling to make templates look professional and fillable.

### Cheatsheet Format

Structure:
- Title with "Cheatsheet" or "Quick Reference" in the name
- Dense, scannable layout (2-column where appropriate)
- Categorized sections with short, punchy entries
- Color-coded categories or difficulty levels
- Pro tips in highlighted callout boxes
- CTA footer

Cheatsheets prioritize information density. Use smaller text, tighter spacing, and visual grouping.

## HTML Output Requirements

Every generated HTML file must:

1. **Be fully self-contained** — all CSS inline in a `<style>` tag, no external resources.
2. **Include Google Fonts link** for Inter (the only external dependency allowed).
3. **Be print-friendly** — include `@media print` styles that handle page breaks cleanly.
4. **Use semantic HTML** — proper heading hierarchy, lists, tables.
5. **Include these meta tags**:
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
6. **Include a header** with brand logo text and lead magnet title.
7. **Include a footer** with CTA, brand name, and current year.
8. **Use CSS page-break hints** for PDF conversion:
```css
.page-break { page-break-before: always; }
.no-break { page-break-inside: avoid; }
```

## Content Quality Standards

- **Specificity over generality**: "Use Claude to summarize customer support tickets, reducing response time by 40%" beats "Use AI to improve customer service".
- **Numbers and data**: Include statistics, benchmarks, timeframes, and dollar amounts where reasonable.
- **Actionable**: Every item should tell the reader exactly what to do, not just what to think about.
- **Credibility signals**: Reference real tools, real platforms, real methodologies.
- **No filler paragraphs**: If a sentence doesn't teach, persuade, or instruct, cut it.

## File Output

Write the HTML to: `~/content-engine/output/lead-magnets/[slug]-[format].html`

Create the directory if it doesn't exist. Use kebab-case for the filename derived from the topic.

Example: Topic "AI Automation for Agencies", Format "checklist" writes to:
`~/content-engine/output/lead-magnets/ai-automation-for-agencies-checklist.html`

After generating, tell the user:
1. Where the file was saved
2. How to convert to PDF: `open [file] && print to PDF` or `wkhtmltopdf [file] output.pdf`
3. Estimated page count

## Example Interaction

**User:** Generate a lead magnet. Topic: "AI tools every small business should use in 2026". Format: checklist.

**Action:** Generate a complete HTML checklist with 5 sections (Operations, Marketing, Sales, Finance, Customer Service), each with 5-6 specific tool recommendations with use cases, styled in CommandShift dark theme, saved to the output directory.
