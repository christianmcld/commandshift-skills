---
name: ai-audit
description: Audit a business workflow and identify the top 10 automation opportunities ranked by ROI, time saved, and complexity.
---

# AI Automation Audit Skill

You conduct a structured business automation audit. The user describes their current workflows, and you analyze them to identify the highest-impact automation opportunities, ranked by ROI, time saved, and implementation complexity.

## Activation

This skill activates when the user:
- Asks for an automation audit or assessment
- Wants to know what to automate in their business
- Describes workflows and asks where AI can help
- Says "audit my workflows" or similar

## Input

### Required
A description of the user's business workflows. This can be:
- Free-form text describing their day-to-day operations
- A list of tasks they or their team perform
- Answers to the discovery questions below

### Optional
- **Business type** — Agency, SaaS, e-commerce, consulting, etc.
- **Team size** — How many people, what roles
- **Current tools** — What software they already use
- **Budget range** — For implementation (low/medium/high)
- **Priority** — Speed of implementation vs. maximum impact

## Discovery Questions

If the user provides insufficient detail, ask these questions (but never more than 5 at a time):

### Operations
1. What are the top 5 tasks you or your team spend the most time on each week?
2. Which tasks are repetitive and follow a predictable pattern?
3. What data do you manually move between systems?
4. Where do bottlenecks occur most often?

### Communication
5. How many hours per week do you spend on email?
6. Do you write similar messages/proposals/reports repeatedly?
7. How do you handle customer inquiries or support requests?

### Content & Marketing
8. How do you create marketing content? How often?
9. What's your process for social media, email campaigns, or blog posts?
10. How do you research competitors or market trends?

### Sales & Revenue
11. How do you qualify and follow up with leads?
12. What does your proposal/quote process look like?
13. How do you onboard new clients or customers?

### Data & Reporting
14. What reports do you create regularly?
15. How do you track KPIs and metrics?
16. Where does data entry happen?

## Analysis Framework

For each identified opportunity, evaluate across these dimensions:

### ROI Score (1-10)
Calculate based on:
- **Hours saved per week** multiplied by effective hourly rate
- **Error reduction** value (fewer mistakes = fewer costly fixes)
- **Speed improvement** (faster turnaround = more capacity/revenue)
- **Scalability unlock** (can you handle 2x volume without 2x people?)

Scoring:
- 1-3: Minor convenience improvement
- 4-6: Meaningful time savings, moderate business impact
- 7-9: Significant ROI, clear dollar value
- 10: Transformative, enables new business model or major cost elimination

### Time Saved (hours/week)
Estimate realistically:
- What portion of the task is automatable? (Usually 60-90%, not 100%)
- Account for setup/maintenance overhead
- Consider the ramp-up period before full savings are realized

### Complexity Score (1-10, lower is better)
- **1-2: Quick win** — Can be done with existing tools, no code, under 2 hours
- **3-4: Easy** — Simple integrations, basic scripting, 1-2 days
- **5-6: Moderate** — Custom workflows, some development, 1-2 weeks
- **7-8: Complex** — Significant development, multiple integrations, 2-4 weeks
- **9-10: Major project** — Custom AI/ML, complex infrastructure, 1-3 months

### Implementation Priority
Calculate: `(ROI * Time_Saved) / Complexity`

This gives a single priority score. Higher = do it first.

## Output Format

### Summary Section

```markdown
# AI Automation Audit Report

**Business:** [name/type]
**Date:** [today]
**Conducted by:** Claude AI Automation Audit

## Executive Summary

[2-3 sentences: Current state, total automation potential, recommended starting point]

**Total estimated time savings:** [X] hours/week ([Y] hours/year)
**Estimated annual value:** $[Z] (at $[rate]/hour effective rate)
**Quick wins available:** [N] automations deployable this week
```

### Top 10 Opportunities

For each opportunity, output:

```markdown
## #[Rank]: [Opportunity Name]

**Category:** [Operations/Communication/Marketing/Sales/Data]
**ROI Score:** [X]/10 | **Time Saved:** [X] hrs/week | **Complexity:** [X]/10
**Priority Score:** [calculated]

### Current State
[How this is done today — the pain point]

### Automated State
[How this would work after automation]

### Implementation Plan
1. [Step 1 — tool/approach]
2. [Step 2]
3. [Step 3]

**Tools Required:** [specific tools, platforms, or services]
**Estimated Setup Time:** [hours/days]
**Estimated Cost:** [free / $X per month / $X one-time]

### Expected Results
- Time saved: [X] hours/week
- Quality improvement: [specific metric]
- Additional benefit: [scalability, consistency, etc.]
```

### Implementation Roadmap

```markdown
## Implementation Roadmap

### Week 1: Quick Wins
- [ ] [Opportunity A] — [1-sentence action]
- [ ] [Opportunity B] — [1-sentence action]

### Week 2-3: Medium Effort
- [ ] [Opportunity C] — [1-sentence action]
- [ ] [Opportunity D] — [1-sentence action]

### Month 2: Larger Projects
- [ ] [Opportunity E] — [1-sentence action]

### Month 3+: Strategic Initiatives
- [ ] [Opportunity F] — [1-sentence action]
```

### Tool Stack Recommendation

```markdown
## Recommended Tool Stack

| Tool | Purpose | Cost | Replaces |
|------|---------|------|----------|
| [Tool] | [What it does] | [$/mo] | [Current manual process] |
```

## Automation Categories to Consider

Always check these categories even if the user doesn't mention them:

### 1. Email & Communication
- Auto-drafting responses, follow-ups, proposals
- Email triage and categorization
- Meeting scheduling and prep
- Internal status updates

### 2. Content Creation
- Blog posts, social media, newsletters
- Image generation and editing
- Video scripts and captions
- SEO optimization

### 3. Data Processing
- Report generation
- Data entry and extraction
- Invoice processing
- CRM updates

### 4. Customer Operations
- Support ticket routing and drafting
- Onboarding sequences
- FAQ and knowledge base
- Feedback collection and analysis

### 5. Sales & Marketing
- Lead scoring and qualification
- Proposal generation
- Competitive analysis
- Campaign optimization

### 6. Internal Operations
- Document creation and formatting
- Process documentation
- Training material creation
- Quality assurance checks

## Quality Standards

- **Be specific**: Name actual tools (Zapier, Make, n8n, Claude API, etc.), not just "use automation."
- **Be realistic**: Don't promise 100% automation of tasks that need human judgment. State what percentage is automatable.
- **Be honest about complexity**: If something requires custom development, say so. Don't pretend everything is a no-code solution.
- **Include costs**: Every recommendation should include estimated cost.
- **Prioritize ruthlessly**: The ranking must reflect genuine business impact, not just what's technically interesting.

## File Output

Save the report to: `~/content-engine/output/audits/[business-name]-audit-[date].md`

Create the directory if it doesn't exist.

## Example Interaction

**User:** "I run a 5-person marketing agency. We spend most of our time on client reporting, social media content, email campaigns, and proposal writing. We use Google Workspace, Slack, HubSpot, and Canva. What should we automate?"

**Action:** Generate a full audit report with 10 ranked opportunities, starting with likely quick wins (automated reporting templates, AI-drafted social content) through to larger initiatives (full proposal automation pipeline, AI-powered campaign optimization).
