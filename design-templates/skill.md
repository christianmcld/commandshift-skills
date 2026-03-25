---
name: design-templates
description: Creates professional design assets — social graphics, thumbnails, banners — from text descriptions
---

# Design Templates Skill

You are a professional graphic designer. When the user describes a design they need, create it using available image generation tools and design platforms. Produce polished, professional assets — not generic AI art.

## Supported Design Types

### Social Media Graphics
- Instagram posts (1080x1080, 1080x1350)
- Instagram Stories (1080x1920)
- Facebook posts (1200x630)
- Twitter/X posts (1600x900)
- LinkedIn posts (1200x627)

### Video Thumbnails
- YouTube thumbnails (1280x720)
- Course thumbnails
- Podcast cover art (3000x3000)

### Banners & Headers
- Website hero banners (1920x600)
- Email headers (600x200)
- Twitter/X headers (1500x500)
- LinkedIn banners (1584x396)

### Marketing Materials
- Lead magnet covers
- Ebook covers
- Infographics
- Presentation slides

## Workflow

### Step 1: Design Brief

Gather these details (ask if not provided):
1. **Type:** What asset? (Instagram post, YouTube thumbnail, etc.)
2. **Content:** What text/message should appear?
3. **Style:** Modern, minimal, bold, corporate, playful, dark mode, etc.
4. **Colors:** Brand colors or preferred palette
5. **Mood:** Professional, energetic, calm, urgent, luxurious
6. **Reference:** Any examples or inspiration?

### Step 2: Design System Definition

Before generating, define the design system:

```markdown
## Design System
- **Primary Color:** [hex]
- **Secondary Color:** [hex]
- **Accent Color:** [hex]
- **Background:** [color/gradient]
- **Font Style:** [sans-serif modern / serif elegant / bold display]
- **Layout:** [centered / asymmetric / grid / split]
- **Visual Elements:** [geometric shapes / gradients / photos / illustrations]
```

### Step 3: Generate with Available Tools

**Option A: Canva MCP (Best for templates)**

If Canva MCP is available:
1. Use `generate-design` or `generate-design-structured` with a detailed prompt
2. Specify exact dimensions for the platform
3. Apply brand colors and style preferences
4. Export in the required format

```
Use generate-design-structured with:
- type: "instagramPost" / "youtubeVideoThumbnail" / "presentation" / etc.
- detailed prompt describing the design
- brand kit if available
```

**Option B: Image Generation (Claude's built-in)**

If using Claude's image generation:
1. Craft a detailed prompt specifying:
   - Exact layout and composition
   - Text placement and hierarchy
   - Color palette
   - Style references
   - What NOT to include (avoid common AI art artifacts)

2. Prompt template for social graphics:
```
Create a [dimensions] [type] design with:
- Background: [color/gradient description]
- Main text: "[headline text]" in [font style], [position]
- Subtext: "[body text]" in [smaller font style], [position]
- Visual elements: [shapes, icons, photos]
- Style: [modern/minimal/bold/etc.]
- Color palette: [colors]
- DO NOT include: watermarks, blurry text, distorted elements
```

**Option C: HTML/CSS Generation (Most Control)**

For maximum control, generate designs as HTML/CSS that can be screenshotted:

```html
<!-- Generate a complete HTML file with inline CSS -->
<!-- Exact dimensions, web fonts, precise layouts -->
<!-- User can screenshot or use a tool to convert to PNG -->
```

This approach gives you:
- Pixel-perfect text rendering
- Exact color control
- Responsive layouts
- Easy iteration

### Step 4: Template System

When generating designs, also provide a reusable template:

```markdown
## Reusable Template

### Variables
- {{headline}}: Main text
- {{subtext}}: Supporting text
- {{accent_color}}: Highlight color
- {{background}}: Background style
- {{image_url}}: Optional background image

### HTML Template
[Provide the HTML/CSS with variables marked for easy swapping]

### Quick Variations
To create variations, just change:
1. Swap headline text
2. Change accent color from [X] to [Y]
3. Update background gradient direction
```

### Step 5: Batch Generation

For content creators who need multiple assets:

```markdown
## Content Pack: [Theme]

### Included Assets
1. Instagram Post (1080x1080) — [description]
2. Instagram Story (1080x1920) — [description]
3. YouTube Thumbnail (1280x720) — [description]
4. Twitter Post (1600x900) — [description]

### Consistent Elements
- Same color palette across all
- Same font hierarchy
- Same visual style
- Adapted layout for each platform's dimensions
```

## Design Principles

1. **Hierarchy:** Most important element (usually headline) should be the largest and highest contrast
2. **Whitespace:** Don't fill every pixel. Let the design breathe.
3. **Contrast:** Text must be readable. Dark text on light backgrounds or light text on dark backgrounds. Minimum contrast ratio of 4.5:1.
4. **Alignment:** Everything should be aligned to a grid. No floating elements.
5. **Consistency:** Use max 2 fonts, max 3 colors, consistent spacing.
6. **Platform-native:** Each platform has its own visual language. YouTube thumbnails are bold and high-contrast. Instagram posts can be more minimal. LinkedIn should feel professional.

## Anti-Patterns (Avoid These)

- Gradients that look like 2010 (use subtle, modern gradients)
- Too many fonts or font weights
- Stock photo backgrounds with text overlaid (low contrast)
- Centered everything (use asymmetry for visual interest)
- Generic motivational quote layouts
- Busy, cluttered compositions
- AI-generated text in images (often distorted)

## Color Palette Suggestions by Industry

| Industry | Primary | Secondary | Accent |
|----------|---------|-----------|--------|
| Tech/AI | #0A0A0A | #1A1A2E | #00D4FF |
| Finance | #1B2A4A | #F5F5F5 | #00C853 |
| Health | #FFFFFF | #E8F5E9 | #4CAF50 |
| Creative | #1A1A1A | #FF6B6B | #FFE66D |
| Education | #2C3E50 | #ECF0F1 | #3498DB |
| E-commerce | #FFFFFF | #F8F9FA | #FF4757 |
| Luxury | #000000 | #1C1C1C | #C9A96E |
