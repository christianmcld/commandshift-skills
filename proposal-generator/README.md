# Proposal Generator Skill

Generates professional agency proposals as self-contained HTML documents. Provide client info and project scope, get back a complete proposal with executive summary, detailed scope of work, timeline visualization, tiered pricing, terms, and signature blocks.

## What It Does

You give it the basics — who the client is, what they need — and it produces a ready-to-send proposal document. The output is a single HTML file with clean, professional styling that converts to PDF.

### Proposal sections included:
1. Cover page
2. Executive summary
3. Detailed scope of work (phased)
4. Out of scope (scope protection)
5. Visual timeline with milestones
6. Tiered pricing options (Essential / Professional / Premium)
7. About us / team
8. Terms and conditions
9. Next steps with CTA
10. Signature block

## Install

Place `skill.md` in your Claude Code skills directory:

```
~/content-engine/skills/proposal-generator/skill.md
```

## Example Usage

### Full proposal
```
/proposal-generator

Client: Acme Corp, Jane Smith (VP Operations)
Industry: B2B SaaS

Project: Automate their customer onboarding workflow. Currently takes 4 hours
per customer, they onboard 20/month. They use HubSpot and Slack.

Budget: $15-25K
Timeline: Want to start in 2 weeks
```

### Quick proposal
```
/proposal-generator

Client: Local Realty Group
Project: AI chatbot for their website to handle property inquiries and schedule viewings
Budget: ~$5K
```

### Retainer proposal
```
/proposal-generator

Client: GrowthStack Marketing (Sarah Lee, CEO)
Project: Ongoing AI automation retainer — monthly optimization of their
marketing workflows, content pipeline, and reporting automation.
Pricing model: Monthly retainer
```

## Output

Files are saved to `~/content-engine/output/proposals/` as self-contained HTML.

### Converting to PDF

```bash
# Option 1: Browser
open ~/content-engine/output/proposals/acme-corp-proposal-2026-03-25.html
# Cmd+P > Save as PDF

# Option 2: Command line
wkhtmltopdf proposal.html proposal.pdf

# Option 3: Puppeteer
npx puppeteer-pdf proposal.html -o proposal.pdf
```

## Customization

Override defaults by specifying:

```
Company name: YourAgency
Your name: John Doe, Founder
Accent color: #FF6B35
Pricing model: hourly (or fixed, retainer, value-based)
Payment terms: Net 30, 50/50 split
```

## Pricing Defaults

When you don't specify pricing, the skill estimates based on industry benchmarks:

| Service | Project Range |
|---------|--------------|
| Strategy/Consulting | $3K-15K |
| AI/Automation | $5K-25K |
| Web Development | $5K-50K |
| Content/Marketing | $2K-10K |
| Monthly Retainer | $2K-10K/mo |

Always review and adjust the generated pricing to match your actual rates.

## Requirements

- Claude Code with skills support
- A browser or PDF tool for final output
- No API keys or external services needed
