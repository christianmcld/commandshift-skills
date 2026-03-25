# AI Automation Audit Skill

Conducts a structured business automation audit. Describe your workflows, get back a prioritized list of the top 10 automation opportunities ranked by ROI, time saved, and implementation complexity.

## What It Does

You describe how your business operates — what tasks eat up time, what tools you use, where bottlenecks are. The skill analyzes everything and produces a detailed audit report with:

- **Top 10 opportunities** ranked by a priority score (ROI x time saved / complexity)
- **Implementation plans** for each opportunity with specific tools and steps
- **A phased roadmap** from quick wins (this week) to strategic projects (months out)
- **Tool stack recommendations** with costs
- **Total impact estimate** in hours saved and dollar value per year

## Install

Place `skill.md` in your Claude Code skills directory:

```
~/content-engine/skills/ai-audit/skill.md
```

## Example Usage

### Full audit from description
```
/ai-audit

I run a 10-person e-commerce company. We spend time on:
- Customer support (email + chat, ~30 hrs/week across team)
- Product descriptions and photography editing
- Inventory management and reordering
- Social media content (3 platforms, daily posts)
- Monthly reporting for stakeholders
- Vendor communication and purchase orders

Tools: Shopify, Zendesk, Slack, Google Sheets, Canva
```

### Quick audit
```
/ai-audit

Solo consultant. I spend 15 hours/week on proposals, 10 on email, 5 on invoicing.
What should I automate first?
```

### Focused audit
```
/ai-audit

We're a SaaS company. Only audit our customer onboarding and support workflows.
Currently: manual email sequences, Intercom for chat, Notion for docs, custom Rails app.
```

## Output

Reports are saved to `~/content-engine/output/audits/` as markdown files.

Each report includes:
1. Executive summary with total savings estimate
2. Top 10 ranked opportunities with full implementation details
3. Phased roadmap (week 1 quick wins through month 3+ strategic projects)
4. Recommended tool stack with costs

## Scoring System

Each opportunity gets three scores:

| Metric | Scale | Meaning |
|--------|-------|---------|
| ROI | 1-10 | Business value (revenue, cost savings, error reduction) |
| Time Saved | hrs/week | Realistic estimate of weekly hours recovered |
| Complexity | 1-10 | Implementation difficulty (1 = quick win, 10 = major project) |

**Priority Score** = (ROI x Time Saved) / Complexity

Higher priority score = do it first.

## Requirements

- Claude Code with skills support
- No API keys or external tools needed
- The more detail you provide about your workflows, the better the audit
