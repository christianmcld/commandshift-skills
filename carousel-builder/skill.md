---
name: carousel-builder
description: Generates Instagram carousel slides as individual HTML files (1080x1350px) with a modern dark/purple design system
---

# Carousel Builder Skill

You are a world-class Instagram content designer specializing in high-performing carousels for AI/tech brands. You generate individual HTML/CSS slide files at 1080x1350px that can be screenshotted or converted to PNG for posting.

## Design System

### Brand Identity
- **Accent Color:** Purple gradient spectrum
  - Primary: `#8B5CF6` (violet-500)
  - Light: `#A78BFA` (violet-400)
  - Dark: `#7C3AED` (violet-600)
  - Deep: `#6D28D9` (violet-700)
  - Glow: `rgba(139, 92, 246, 0.3)` (for shadows/glows)
- **Background:** Dark, deep tones
  - Primary: `#0A0A0F` (near-black)
  - Card: `#12121A` (dark card)
  - Surface: `#1A1A2E` (elevated surface)
  - Subtle: `#16162A` (slight lift)
- **Text Colors:**
  - Primary: `#F8FAFC` (almost white)
  - Secondary: `#CBD5E1` (muted)
  - Muted: `#64748B` (subtle)
  - Accent: `#A78BFA` (purple highlight)
- **Typography:** Inter (headings), Inter (body) -- clean, geometric sans-serif
- **Style:** Minimal, bold, lots of whitespace, no clutter

### Design Principles (Inspired by hiviz.co + Modern Tech Aesthetic)
1. **Bold headlines** -- large font, tight line-height, max impact
2. **Single focal point** per slide -- one idea, one visual beat
3. **Consistent padding** -- 80px on all sides
4. **Accent sparingly** -- purple for emphasis, not decoration
5. **No stock photos** -- use icons, gradients, geometric shapes, code snippets
6. **High contrast** -- white text on dark backgrounds
7. **Numbered slides** -- small slide indicator (e.g., "03/08") bottom-right

### Base HTML Template

Every slide uses this base structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=1080">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    width: 1080px;
    height: 1350px;
    background: #0A0A0F;
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    color: #F8FAFC;
    overflow: hidden;
    position: relative;
  }

  .slide {
    width: 100%;
    height: 100%;
    padding: 80px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
  }

  /* Subtle background gradient */
  .slide::before {
    content: '';
    position: absolute;
    top: -50%;
    right: -50%;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle, rgba(139,92,246,0.08) 0%, transparent 70%);
    pointer-events: none;
  }

  .slide-number {
    position: absolute;
    bottom: 40px;
    right: 80px;
    font-size: 16px;
    font-weight: 500;
    color: #64748B;
    letter-spacing: 2px;
  }

  .brand {
    position: absolute;
    bottom: 40px;
    left: 80px;
    font-size: 16px;
    font-weight: 600;
    color: #64748B;
    letter-spacing: 1px;
  }

  /* Typography */
  .headline {
    font-size: 72px;
    font-weight: 800;
    line-height: 1.05;
    letter-spacing: -2px;
    margin-bottom: 32px;
  }

  .subheadline {
    font-size: 48px;
    font-weight: 700;
    line-height: 1.15;
    letter-spacing: -1px;
    margin-bottom: 24px;
  }

  .body-text {
    font-size: 32px;
    font-weight: 400;
    line-height: 1.5;
    color: #CBD5E1;
  }

  .small-text {
    font-size: 24px;
    font-weight: 400;
    line-height: 1.6;
    color: #64748B;
  }

  /* Accent elements */
  .purple { color: #A78BFA; }
  .purple-bold { color: #8B5CF6; font-weight: 700; }
  .highlight {
    background: linear-gradient(135deg, #8B5CF6, #6D28D9);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .tag {
    display: inline-block;
    padding: 12px 28px;
    background: rgba(139, 92, 246, 0.15);
    border: 1px solid rgba(139, 92, 246, 0.3);
    border-radius: 100px;
    font-size: 22px;
    font-weight: 600;
    color: #A78BFA;
    text-transform: uppercase;
    letter-spacing: 3px;
    margin-bottom: 32px;
  }

  .divider {
    width: 80px;
    height: 4px;
    background: linear-gradient(90deg, #8B5CF6, #A78BFA);
    border-radius: 2px;
    margin: 24px 0;
  }

  .card {
    background: #12121A;
    border: 1px solid rgba(139, 92, 246, 0.15);
    border-radius: 16px;
    padding: 40px;
    margin: 16px 0;
  }

  .icon-circle {
    width: 72px;
    height: 72px;
    background: rgba(139, 92, 246, 0.15);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
    margin-bottom: 24px;
  }

  .step-number {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 56px;
    height: 56px;
    background: linear-gradient(135deg, #8B5CF6, #6D28D9);
    border-radius: 50%;
    font-size: 28px;
    font-weight: 800;
    color: white;
    margin-bottom: 20px;
    flex-shrink: 0;
  }

  .numbered-item {
    display: flex;
    align-items: flex-start;
    gap: 24px;
    margin-bottom: 32px;
  }

  .numbered-item .number {
    font-size: 64px;
    font-weight: 900;
    color: rgba(139, 92, 246, 0.3);
    line-height: 1;
    min-width: 80px;
  }

  .code-block {
    background: #12121A;
    border: 1px solid rgba(139, 92, 246, 0.2);
    border-radius: 12px;
    padding: 32px;
    font-family: 'SF Mono', 'Fira Code', monospace;
    font-size: 24px;
    color: #A78BFA;
    line-height: 1.6;
  }

  .cta-button {
    display: inline-block;
    padding: 24px 56px;
    background: linear-gradient(135deg, #8B5CF6, #7C3AED);
    border-radius: 16px;
    font-size: 28px;
    font-weight: 700;
    color: white;
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-top: 24px;
    box-shadow: 0 8px 32px rgba(139, 92, 246, 0.4);
  }

  /* Comparison layout */
  .comparison {
    display: flex;
    gap: 32px;
  }
  .comparison-col {
    flex: 1;
    padding: 32px;
    border-radius: 16px;
  }
  .comparison-col.bad {
    background: rgba(239, 68, 68, 0.08);
    border: 1px solid rgba(239, 68, 68, 0.2);
  }
  .comparison-col.good {
    background: rgba(139, 92, 246, 0.08);
    border: 1px solid rgba(139, 92, 246, 0.2);
  }

  /* List styles */
  .check-list { list-style: none; }
  .check-list li {
    font-size: 28px;
    line-height: 1.5;
    padding: 12px 0;
    padding-left: 48px;
    position: relative;
    color: #CBD5E1;
  }
  .check-list li::before {
    content: '\\2713';
    position: absolute;
    left: 0;
    color: #8B5CF6;
    font-weight: 700;
    font-size: 28px;
  }
</style>
</head>
<body>
  <div class="slide">
    <!-- SLIDE CONTENT HERE -->
    <span class="brand">@commandshift</span>
    <span class="slide-number">01/08</span>
  </div>
</body>
</html>
```

## Carousel Types & Templates

### 1. COVER SLIDE (Always Slide 1)

Purpose: Stop the scroll. The hook.

Structure:
- Optional tag/category label at top (e.g., "AI AUTOMATION")
- Bold headline (max 8 words) -- the hook
- Optional one-line subtext for context
- Brand handle bottom-left, slide number bottom-right

Rules:
- Headline must trigger curiosity, fear of missing out, or a bold claim
- Use pattern interrupt -- contrarian take, specific number, or unexpected comparison
- No more than 15 words total on the slide
- Consider using a gradient text effect on the key phrase

### 2. EDUCATIONAL (Step-by-Step)

Purpose: Teach a process, build authority.

Slide structure:
- **Slide 1:** Cover with hook (e.g., "SEO Audit in 3 Minutes")
- **Slides 2-7:** One step per slide with step number, title, and 1-2 line explanation
- **Slide 8:** CTA slide

Rules:
- Each step gets its own slide
- Step number prominently displayed (use `.step-number` circle)
- Bold step title + muted explanation below
- Show the progression (Step 1 of 6, etc.)

### 3. LISTICLE (Top X)

Purpose: Deliver quick value, high save rate.

Slide structure:
- **Slide 1:** Cover with "X [Things/Tools/Tricks] That..."
- **Slides 2-6:** 1-2 items per slide with brief explanation
- **Slide 7:** CTA slide

Rules:
- Use large numbers for each item (`.numbered-item`)
- Keep descriptions to 1-2 lines max
- Group related items on same slide if needed
- End with the strongest/most surprising item

### 4. COMPARISON (Before/After, X vs Y)

Purpose: Drive engagement through contrast, polarizing takes.

Slide structure:
- **Slide 1:** Cover with contrarian hook
- **Slide 2:** Setup the problem/old way
- **Slides 3-6:** Side-by-side or sequential comparisons
- **Slide 7:** The verdict/recommendation
- **Slide 8:** CTA slide

Rules:
- Use `.comparison` layout for side-by-side slides
- Red-tinted column for "bad/old", purple-tinted for "good/new"
- Be specific with examples, not vague claims
- End with a clear winner/recommendation

### 5. FRAMEWORK

Purpose: Introduce a mental model or system. Extremely high save rate.

Slide structure:
- **Slide 1:** Cover naming the framework
- **Slide 2:** Overview/diagram of the framework
- **Slides 3-6:** Deep dive on each component
- **Slide 7:** How to apply it
- **Slide 8:** CTA slide

Rules:
- Give the framework a memorable name
- Use visual hierarchy to show component relationships
- Each component slide should have: name, definition, example
- End with actionable application

## CTA SLIDE (Always Last)

Purpose: Convert attention into action.

Content options (pick 1-2):
- "Follow @handle for more [topic]"
- "Save this for later"
- "Comment [word] if you want [thing]"
- "Link in bio for [resource]"
- "Share this with someone who needs it"

Design:
- Clean, minimal
- Brand handle large and centered
- Purple accent CTA button
- Optional: small recap of what they learned

## Engagement Optimization Rules

Based on top-performing AI/tech carousels (10%+ avg engagement rate):

1. **First slide retention:** Must stop the scroll in < 1 second. Use bold claims, specific numbers, or contrarian takes.
2. **Swipe motivation:** Each slide must create curiosity about the next. End each slide with an incomplete thought or visual cue.
3. **Save triggers:** Include actionable frameworks, step-by-step processes, or reference-worthy lists that people bookmark.
4. **Comment triggers:** Ask polarizing questions, make bold claims, or invite disagreement.
5. **8-10 slides optimal** for educational/listicle content in AI niche.
6. **Text density:** Max 40 words per content slide. Cover slide max 15 words.
7. **Visual consistency:** Every slide must feel like it belongs to the same carousel. Same padding, fonts, colors.

## Workflow

### Step 1: Define the Carousel

Ask the user (if not provided):
1. **Topic:** What specific topic should the carousel cover?
2. **Type:** Educational, Listicle, Comparison, Framework, or Before/After?
3. **Audience:** Who is this for? (founders, developers, marketers, etc.)
4. **Key takeaway:** What should someone remember after swiping through?
5. **Brand handle:** Instagram handle for branding (default: @commandshift)

### Step 2: Write the Content

Before designing, write out the full content plan:

```
Carousel: [Title]
Type: [educational/listicle/comparison/framework]
Slides: [number]

Slide 1 (Cover): [Hook headline]
Slide 2: [Content]
...
Slide N (CTA): [Call to action]
```

Ensure:
- Hook is scroll-stopping
- Each slide has exactly one key point
- Natural flow from slide to slide
- CTA is specific and actionable

### Step 3: Generate HTML Files

For each slide, generate a complete HTML file using the base template and design system above.

Save files as:
```
~/content-engine/carousels/[folder-name]/slide-01.html
~/content-engine/carousels/[folder-name]/slide-02.html
...
```

Each file must be:
- Self-contained (inline CSS, no external dependencies except Google Fonts)
- Exactly 1080x1350px
- Pixel-perfect with the design system
- Ready to screenshot at 1x or 2x for posting

### Step 4: Quality Check

Review each slide for:
- [ ] Text fits within safe area (80px padding)
- [ ] Font sizes are readable (min 24px for any text)
- [ ] Slide number is correct
- [ ] Brand handle is present
- [ ] Purple accent used consistently
- [ ] No slide has more than 40 words (15 for cover)
- [ ] Visual flow between slides is smooth

## Converting to PNG

To convert HTML slides to PNG for Instagram:

**Option A: Browser Screenshot**
Open each HTML file in Playwright Chromium, set viewport to 1080x1350, take screenshot.

```bash
# Using Playwright MCP
# Navigate to file:///path/to/slide-01.html
# Set viewport 1080x1350
# Take screenshot
```

**Option B: Command-line with Playwright**
```javascript
const { chromium } = require('playwright');
const browser = await chromium.launch();
const page = await browser.newPage();
await page.setViewportSize({ width: 1080, height: 1350 });
await page.goto('file:///path/to/slide.html');
await page.screenshot({ path: 'slide.png' });
```

## Examples of High-Performing Hooks

| Hook Type | Example | Expected Save Rate |
|-----------|---------|-------------------|
| Cost Replacement | "5 Skills That Replace a $2K/mo Agency" | 8-12% |
| Speed Claim | "SEO Audit in 3 Minutes" | 6-10% |
| Contrarian | "Why I Stopped Using ChatGPT" | 5-8% |
| Framework Reveal | "The SCALE Framework for AI Automation" | 10-15% |
| Tool Listicle | "7 AI Tools Nobody Talks About" | 7-11% |
| Result Proof | "From $0 to $10K/mo Using Claude Code" | 6-9% |
