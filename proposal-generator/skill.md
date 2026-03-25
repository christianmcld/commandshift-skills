---
name: proposal-generator
description: Generate professional agency proposals as HTML — executive summary, scope, timeline, pricing, and terms from client info and project details.
---

# Proposal Generator Skill

You generate polished, professional agency proposals as self-contained HTML documents. The user provides client information and project scope, and you produce a complete proposal ready to send.

## Activation

This skill activates when the user:
- Asks to create a proposal, quote, or SOW
- Mentions writing a proposal for a client
- Provides client/project details and wants a formatted deliverable

## Input

### Required
1. **Client info** — Company name, contact person, industry
2. **Project scope** — What the client needs (described in any level of detail)

### Optional
- **Your company name** — Default: CommandShift
- **Your name/title** — For the proposal signoff
- **Budget range** — If known or discussed
- **Timeline** — Desired start date or deadline
- **Pricing model** — Fixed, hourly, retainer, or value-based
- **Special terms** — Payment schedule, IP ownership, etc.
- **Branding** — Accent color, logo URL, company tagline

## Processing Steps

1. **Analyze the project scope**: Break vague descriptions into concrete deliverables and phases.
2. **Estimate effort**: Based on scope, assign realistic time estimates per deliverable.
3. **Structure pricing**: Calculate pricing based on the chosen model. If no budget is given, provide tiered options.
4. **Build timeline**: Create a phased delivery schedule with milestones.
5. **Generate HTML**: Produce the complete proposal document.

## Proposal Structure

### 1. Cover Page

```
[Your Company Logo/Name]
[Tagline]

PROPOSAL

[Project Name]
Prepared for [Client Company]
[Date]

Confidential
```

### 2. Executive Summary

3-4 paragraphs covering:
- Understanding of the client's situation and needs (show you listened)
- High-level proposed solution
- Expected outcomes and business impact
- Why your team is the right fit

This section sells. It should connect the client's pain to your solution to measurable results.

### 3. Scope of Work

For each deliverable/phase:

```markdown
### Phase [N]: [Name]

**Objective:** [What this phase achieves]

**Deliverables:**
- [Deliverable 1] — [brief description]
- [Deliverable 2] — [brief description]

**Duration:** [X weeks]

**Your responsibilities:**
- [What your team does]

**Client responsibilities:**
- [What the client needs to provide — access, feedback, assets, etc.]
```

Rules for scope:
- Be specific enough that the client knows exactly what they're getting
- Include client responsibilities to set expectations
- Define what is NOT included (scope boundaries) in a separate section
- Each deliverable should be measurable/verifiable

### 4. Out of Scope

Explicitly list what is not included. This protects both parties:
```markdown
The following are not included in this proposal and can be addressed in a separate engagement:
- [Item 1]
- [Item 2]
```

### 5. Timeline

Visual timeline using HTML/CSS:

```html
<div class="timeline">
  <div class="timeline-phase">
    <div class="phase-marker">Phase 1</div>
    <div class="phase-content">
      <h4>Discovery & Planning</h4>
      <p>Weeks 1-2</p>
      <ul>
        <li>Milestone: Requirements document approved</li>
      </ul>
    </div>
  </div>
  <!-- more phases -->
</div>
```

Include:
- Phase names and durations
- Key milestones
- Client review/approval points
- Dependencies between phases

### 6. Pricing

Present pricing clearly. Offer tiered options when no budget is specified:

```markdown
### Option A: Essential
[Core deliverables only]
**Investment:** $X,XXX

### Option B: Professional (Recommended)
[Core + enhanced deliverables]
**Investment:** $XX,XXX

### Option C: Premium
[Everything + ongoing support]
**Investment:** $XX,XXX
```

For each tier, list exactly what's included so the difference is clear.

Use the word "Investment" not "Cost" or "Price."

Include:
- What's included at each tier
- Payment schedule (e.g., 50% upfront, 25% at midpoint, 25% on completion)
- Additional/optional line items
- Revision limits if applicable

### 7. About Us

Brief company overview:
- Who you are (2-3 sentences)
- Relevant experience (specific to this client's industry/needs)
- Key team members who'll work on this project (name, role, one-line bio)
- Social proof: relevant results, client names (if allowed), or metrics

### 8. Terms & Conditions

Standard terms (customize based on user input):

```markdown
**Payment Terms:** [Net 15/30, payment schedule]
**Project Start:** Upon signed agreement and initial payment
**Revisions:** [X] rounds of revisions included per deliverable
**IP Ownership:** All deliverables become client property upon final payment
**Confidentiality:** Both parties agree to keep project details confidential
**Cancellation:** Either party may cancel with [X] days written notice;
  client pays for work completed to date
**Validity:** This proposal is valid for [30] days from the date above
```

### 9. Next Steps

Clear call to action:
```markdown
## Next Steps

1. Review this proposal and share any questions
2. Select your preferred option (A, B, or C)
3. Sign the agreement below
4. We'll schedule a kickoff call within [X] business days

Ready to get started? Reply to this email or book a call: [link]
```

### 10. Signature Block

```markdown
________________________________          ________________________________
[Your Name]                               [Client Contact Name]
[Your Title]                              [Client Title]
[Your Company]                            [Client Company]
Date: _______________                     Date: _______________
```

## HTML Styling

Use professional, clean styling:

```css
:root {
  --bg: #FFFFFF;
  --text: #1A1A2E;
  --text-light: #6B7280;
  --accent: #2563EB;
  --accent-light: #EFF6FF;
  --border: #E5E7EB;
  --section-bg: #F9FAFB;
}

body {
  font-family: 'Inter', -apple-system, sans-serif;
  color: var(--text);
  line-height: 1.7;
  max-width: 800px;
  margin: 0 auto;
  padding: 40px;
}
```

Requirements:
- Self-contained HTML with inline CSS
- Google Fonts link for Inter
- Print-friendly with `@media print` styles
- Page break hints for PDF conversion
- Clean, professional look (not flashy — proposals need to feel trustworthy)
- Tables for pricing must be well-formatted
- Timeline visualization using CSS (not images)

## File Output

Save to: `~/content-engine/output/proposals/[client-name]-proposal-[date].html`

Create the directory if it doesn't exist. Use kebab-case for the filename.

After generating, tell the user:
1. File location
2. How to convert to PDF
3. Suggest they review pricing and customize the About Us section
4. Remind them to update the signature block

## Pricing Estimation Guidelines

When the user doesn't specify pricing, estimate based on these benchmarks (adjust for their context):

| Service Type | Hourly Range | Project Range |
|-------------|-------------|---------------|
| Strategy/Consulting | $150-300/hr | $3,000-15,000 |
| AI/Automation Setup | $150-250/hr | $5,000-25,000 |
| Web Development | $100-200/hr | $5,000-50,000 |
| Content/Marketing | $100-175/hr | $2,000-10,000 |
| Design | $100-200/hr | $3,000-15,000 |
| Ongoing Retainer | - | $2,000-10,000/mo |

Always present as estimates that the user should adjust. Add a comment in the HTML: `<!-- REVIEW: Adjust pricing to match your rates -->`

## Example Interaction

**User:** "Write a proposal for Acme Corp. Contact is Jane Smith, VP of Operations. They want us to automate their customer onboarding process. Currently it takes their team 4 hours per new customer and they onboard 20/month. They use HubSpot and Slack. Budget is probably $15-25K."

**Action:** Generate a complete proposal with:
- Executive summary connecting onboarding pain to automation solution
- 3-phase scope (Discovery, Build, Launch + Optimize)
- 6-week timeline
- Three pricing tiers around the $15-25K range
- ROI calculation showing time savings
- Standard terms
- Save as HTML
