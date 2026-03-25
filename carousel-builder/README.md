# Carousel Builder Skill

Generate high-performing Instagram carousel slides as individual HTML files (1080x1350px) with a modern dark/purple design system.

## Design System

- **Theme:** Dark backgrounds (#0A0A0F) with purple accents (#8B5CF6)
- **Font:** Inter (loaded from Google Fonts)
- **Size:** 1080x1350px per slide (standard Instagram carousel)
- **Style:** Minimal, bold typography, high contrast, hiviz.co-inspired

## Setup

No dependencies required. Slides are self-contained HTML files that load Inter from Google Fonts CDN.

### Converting to PNG

**Option 1: Playwright (recommended)**

```bash
npx playwright install chromium
```

Then use the Playwright MCP or script:

```javascript
const { chromium } = require('playwright');

async function slidesToPNG(folder) {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  await page.setViewportSize({ width: 1080, height: 1350 });

  const fs = require('fs');
  const files = fs.readdirSync(folder).filter(f => f.endsWith('.html')).sort();

  for (const file of files) {
    await page.goto(`file://${folder}/${file}`);
    await page.waitForTimeout(1000); // wait for font load
    const pngName = file.replace('.html', '.png');
    await page.screenshot({ path: `${folder}/${pngName}` });
    console.log(`Saved ${pngName}`);
  }

  await browser.close();
}

slidesToPNG(process.argv[2]);
```

Run: `node convert.js ~/content-engine/carousels/01-claude-code-skills`

**Option 2: Manual Screenshot**

Open each `.html` file in a browser window sized to 1080x1350 and take a screenshot.

## Usage

### With Claude Code

```
/carousel-builder

Topic: 5 AI tools that replace expensive SaaS
Type: listicle
Audience: founders and solopreneurs
```

### Carousel Types

| Type | Best For | Slides | Save Rate |
|------|----------|--------|-----------|
| Educational | Step-by-step tutorials | 8-10 | 8-12% |
| Listicle | Top X lists | 7-8 | 7-11% |
| Comparison | X vs Y, contrarian takes | 7-8 | 5-8% |
| Framework | Mental models, systems | 8-10 | 10-15% |
| Before/After | Transformation stories | 6-8 | 6-9% |

### Output Structure

```
~/content-engine/carousels/
  01-topic-name/
    slide-01.html  (cover)
    slide-02.html  (content)
    ...
    slide-08.html  (CTA)
```

## Design Tokens

```css
/* Colors */
--purple-primary: #8B5CF6;
--purple-light: #A78BFA;
--purple-dark: #7C3AED;
--bg-primary: #0A0A0F;
--bg-card: #12121A;
--bg-surface: #1A1A2E;
--text-primary: #F8FAFC;
--text-secondary: #CBD5E1;
--text-muted: #64748B;

/* Typography */
--font: 'Inter', sans-serif;
--h1: 72px / weight 800;
--h2: 48px / weight 700;
--body: 32px / weight 400;
--small: 24px / weight 400;

/* Spacing */
--slide-padding: 80px;
--slide-width: 1080px;
--slide-height: 1350px;
```

## Engagement Benchmarks

Target metrics for AI/tech niche:
- Swipe-through rate: 50%+
- Save rate: 5-10%
- Engagement rate: 8-12%
- Optimal slide count: 8-10
