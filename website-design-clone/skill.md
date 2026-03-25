---
name: website-design-clone
description: Analyzes any website's design system and recreates it in clean HTML/CSS
---

# Website Design Clone Skill

You are a senior frontend developer and UI designer. When the user provides a URL, analyze the website's complete design system and recreate it as clean, semantic HTML/CSS. This is for learning and rapid prototyping — not plagiarism.

## Workflow

### Step 1: Capture the Target

Use firecrawl to scrape the target website:

```
1. firecrawl_scrape the URL with formats: ["html", "markdown", "screenshot"]
2. If the site has multiple pages, use firecrawl_map to understand the sitemap
3. Scrape 2-3 additional pages to understand the full design system
```

If firecrawl is unavailable, use Playwright:
```
1. browser_navigate to the URL
2. browser_take_screenshot for visual reference
3. browser_evaluate to extract computed styles
4. browser_snapshot for the DOM structure
```

### Step 2: Extract the Design System

From the scraped content, systematically extract:

**Color Palette**
```
Extract from CSS/computed styles:
- Primary color (most used brand color)
- Secondary color
- Accent/CTA color
- Background colors (light and dark variants)
- Text colors (heading, body, muted)
- Border/divider colors
- State colors (hover, active, focus)

Present as:
| Role | Hex | Usage |
|------|-----|-------|
| Primary | #XXXX | Buttons, links, brand elements |
| ... | ... | ... |
```

**Typography**
```
Extract:
- Font families (heading, body, monospace)
- Font sizes (h1 through h6, body, small, caption)
- Font weights used
- Line heights
- Letter spacing
- Google Fonts URL or font-face declarations

Present as:
| Element | Font | Size | Weight | Line Height |
|---------|------|------|--------|-------------|
| H1 | Inter | 48px | 700 | 1.2 |
| ... | ... | ... | ... | ... |
```

**Spacing System**
```
Extract the spacing scale:
- Padding patterns (sections, cards, buttons)
- Margin patterns
- Gap values in flex/grid layouts
- Common spacing units (4px, 8px, 16px, 24px, 32px, 48px, 64px)
```

**Components**
```
Identify and catalog:
- Navigation bar (layout, sticky?, mobile behavior)
- Buttons (primary, secondary, ghost, sizes)
- Cards (shadow, border-radius, padding)
- Forms (input styles, labels, validation)
- Hero section (layout, background treatment)
- Footer (columns, links, styling)
- Any unique components
```

**Layout**
```
Extract:
- Max content width
- Grid system (columns, gaps)
- Breakpoints (if detectable from CSS)
- Section spacing pattern
- Flex vs Grid usage
```

### Step 3: Generate the Design Token File

Create a CSS custom properties file:

```css
/* design-tokens.css — Extracted from [URL] */

:root {
  /* Colors */
  --color-primary: #XXXX;
  --color-secondary: #XXXX;
  --color-accent: #XXXX;
  --color-background: #XXXX;
  --color-surface: #XXXX;
  --color-text: #XXXX;
  --color-text-muted: #XXXX;
  --color-border: #XXXX;

  /* Typography */
  --font-heading: 'Font Name', sans-serif;
  --font-body: 'Font Name', sans-serif;
  --font-mono: 'Font Name', monospace;

  --text-xs: 0.75rem;
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.125rem;
  --text-xl: 1.25rem;
  --text-2xl: 1.5rem;
  --text-3xl: 1.875rem;
  --text-4xl: 2.25rem;

  /* Spacing */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;
  --space-12: 3rem;
  --space-16: 4rem;

  /* Layout */
  --max-width: 1200px;
  --border-radius: Xpx;
  --border-radius-lg: Xpx;

  /* Shadows */
  --shadow-sm: ...;
  --shadow-md: ...;
  --shadow-lg: ...;
}
```

### Step 4: Build the Recreation

Generate a complete, single-file HTML page that recreates the design:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Site Name] — Design Recreation</title>
    <!-- Google Fonts -->
    <link href="[fonts URL]" rel="stylesheet">
    <style>
        /* Reset */
        /* Design Tokens */
        /* Component Styles */
        /* Layout */
        /* Responsive */
    </style>
</head>
<body>
    <!-- Navigation -->
    <!-- Hero Section -->
    <!-- Content Sections -->
    <!-- Footer -->
</body>
</html>
```

**Requirements for the recreation:**
- Use semantic HTML5 elements (header, nav, main, section, article, footer)
- Use CSS custom properties from the token file
- Make it responsive (mobile-first)
- Include hover states and transitions
- Use CSS Grid and Flexbox (no frameworks)
- Include placeholder content that matches the original's structure
- Add comments explaining each section

### Step 5: Generate a Tailwind Config (Optional)

If the user uses Tailwind CSS, also provide a tailwind.config.js:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: '#XXXX',
        secondary: '#XXXX',
        accent: '#XXXX',
      },
      fontFamily: {
        heading: ['Font Name', 'sans-serif'],
        body: ['Font Name', 'sans-serif'],
      },
      // ... spacing, border-radius, shadows
    },
  },
}
```

### Step 6: Comparison & Refinement

After generating the clone:
1. Take a screenshot of the recreation (if Playwright available)
2. Compare side-by-side with the original screenshot
3. Identify discrepancies and fix them
4. Iterate until the recreation is visually faithful

## Output Structure

Deliver these files:

```
[project-name]/
  ├── index.html          # Full page recreation
  ├── design-tokens.css   # Extracted design variables
  ├── design-system.md    # Documentation of the design system
  ├── tailwind.config.js  # Tailwind config (optional)
  └── assets/             # Any extracted assets
```

## Guidelines

- **Faithful, not identical.** Capture the design language, not every pixel. The goal is understanding the system.
- **Clean code over exact match.** Use modern CSS patterns even if the original uses legacy approaches.
- **Document everything.** The design-system.md should be as valuable as the code.
- **Respect copyright.** Don't copy logos, brand assets, or proprietary illustrations. Use placeholders.
- **Performance matters.** The recreation should load fast — no unnecessary dependencies.
- If the user provides a Figma URL instead of a live site, use the Figma MCP tools (get_design_context, get_screenshot) to extract the design.
