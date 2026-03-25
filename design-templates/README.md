# Design Templates

A Claude Code skill that creates professional design assets — social media graphics, thumbnails, banners, and marketing materials — from text descriptions.

## What It Does

- Creates designs for Instagram, Facebook, Twitter/X, LinkedIn, YouTube, and more
- Supports multiple generation methods: Canva MCP, image generation, or HTML/CSS
- Defines design systems (colors, fonts, layout) for brand consistency
- Generates reusable templates with swappable variables
- Produces batch content packs (same design adapted for multiple platforms)
- Follows professional design principles (hierarchy, contrast, whitespace)

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/design-templates.md
```

## Example Usage

```
/design-templates

Create an Instagram post (1080x1080) announcing our new AI product. Dark theme, modern style. Headline: "The Future of Work" in white. Accent color: electric blue.
```

```
/design-templates

I need a YouTube thumbnail for a video titled "I Replaced My $5K Agency With AI". Make it bold, high-contrast, attention-grabbing.
```

```
/design-templates

Generate a content pack for my brand launch — Instagram post, story, Twitter header, and LinkedIn banner. Brand colors are #1A1A2E and #00D4FF. Minimal style.
```

## Requirements

- **Canva MCP** (recommended) — For template-based design generation
- **Image generation tool** (alternative) — For AI-generated graphics
- No strict dependencies — Can also output HTML/CSS designs for maximum control

## Output

- Generated design assets (via Canva or image generation)
- HTML/CSS template files for pixel-perfect control
- Design system documentation
- Reusable template with variables for quick iterations
- Platform-specific adaptations of the same design
