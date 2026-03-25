# Image Enhancer

A Claude Code skill that takes AI-generated images from generic "AI slop" to professional quality through systematic prompt engineering, style direction, and iterative refinement.

## What It Does

- Analyzes existing AI images for common quality issues (plastic skin, flat lighting, generic composition)
- Applies a 7-layer prompt engineering framework: subject, composition, lighting, color, texture, style, negatives
- Generates 3-5 enhanced variations with different artistic approaches
- Provides quick-start templates for common use cases (product shots, headshots, social graphics, cinematic)
- Includes a diagnostic table mapping common AI image problems to their fixes
- Iterates through multiple rounds of refinement

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/image-enhancer.md
```

## Example Usage

```
/image-enhancer

I generated this image of a workspace for my website hero but it looks too "AI." Make it look like real product photography. [attach image or describe it]
```

```
/image-enhancer

I need a professional headshot for LinkedIn. I tried generating one but it looks plastic. Here's what I have — enhance it.
```

```
/image-enhancer

Turn this generic AI illustration of a city into something that looks like it belongs in an editorial magazine.
```

## Requirements

- **Image generation tool** (any available) — For generating enhanced versions
- **Canva MCP** (optional) — For additional design refinement
- No strict dependencies — Can also output enhanced prompts for use in external tools (Midjourney, DALL-E, Stable Diffusion)

## Output

- Analysis of current image quality issues
- Enhanced prompts with all 7 layers applied
- 3-5 generated variations with different approaches
- Recommendation for best variation based on use case
- Reusable prompt templates for future generations

## Prompt Engineering Framework

The skill applies 7 systematic layers to transform generic prompts into professional-quality directions:

1. **Subject Clarity** — Replace generic descriptions with specific details
2. **Composition & Framing** — Camera angle, lens, rule of thirds
3. **Lighting** — Direction, type, quality, mood
4. **Color & Mood** — Palette, grading, temperature
5. **Texture & Detail** — Material rendering, grain, resolution
6. **Style Anchoring** — Reference photographers, publications, or art styles
7. **Negative Prompting** — Explicitly exclude AI artifacts and unwanted elements
