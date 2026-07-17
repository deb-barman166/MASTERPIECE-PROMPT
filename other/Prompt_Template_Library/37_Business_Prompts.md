# Business Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-37

---

## 01. Overview

Business prompting is a domain-specific technique for strategic and operational business tasks — analysis, planning documents, decision frameworks, and internal communications. Effective business prompts require specifying the business context (industry, company stage, scale), the decision or deliverable's actual stakes, relevant constraints (budget, timeline, resources), and the audience (board, team, external partner) — since business communication and analysis need to be calibrated to organizational reality, not generic best practices divorced from actual constraints.

## 02. Purpose

- Ground business analysis and recommendations in actual company context and constraints.
- Produce deliverables appropriately calibrated to their real audience and stakes.
- Support structured business frameworks (SWOT, competitive analysis, business case) applied to real situations.
- Balance strategic thinking with practical, resource-aware recommendations.

## 03. Use Cases

- Business case development and decision memos
- SWOT and competitive analysis
- Strategic planning documents
- Performance review and feedback drafting
- Negotiation preparation
- Internal policy or process documentation
- Pitch deck content and investor communications

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (useful for market/competitive research)

## 05. Prompt Category

`Domain-Specific` · `Business` · `Strategic`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Business context**: Industry, company stage/size, relevant background
- **Task/deliverable**: What specifically needs to be produced

## 08. Optional Inputs

- Constraints (budget, timeline, resources, headcount)
- Audience for the deliverable
- Decision framework to apply (SWOT, cost-benefit, etc.)
- Risk tolerance/company culture notes
- Competitive context

## 09. Variables

| Variable | Required? |
|---|---|
| `{{business_context}}` | Yes |
| `{{task_deliverable}}` | Yes |
| `{{constraints}}` | No |
| `{{audience}}` | No |
| `{{decision_framework}}` | No |
| `{{competitive_context}}` | No |

## 10. Prompt Template

```text
Help with the following business task.

BUSINESS CONTEXT:
{{business_context}}

TASK/DELIVERABLE:
{{task_deliverable}}

CONSTRAINTS:
{{constraints}}

AUDIENCE:
{{audience}}

DECISION FRAMEWORK TO APPLY (if applicable):
{{decision_framework}}

COMPETITIVE CONTEXT:
{{competitive_context}}

INSTRUCTIONS:
- Ground recommendations in the actual stated context and constraints, not
  generic best practices that ignore real limitations.
- Match tone and depth to the stated audience — a board memo, a team
  update, and an external pitch all require different framing even for the
  same underlying content.
- Where trade-offs exist, state them explicitly rather than presenting a
  single recommendation as risk-free.
- If a decision framework is specified, apply it explicitly and show the
  structured reasoning, not just a conclusion.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{business_context}}` | Company/industry background | "10-person SaaS startup, B2B project management tool, pre-Series A" |
| `{{task_deliverable}}` | What needs to be produced | "A business case for hiring a dedicated customer success role" |
| `{{constraints}}` | Real limitations | "Budget allows for one new hire this quarter, not two" |
| `{{audience}}` | Who will read/use this | "Co-founder who controls budget approval, data-driven and skeptical of new headcount" |
| `{{decision_framework}}` | Structured approach to apply | "Cost-benefit analysis with a 12-month payback consideration" |
| `{{competitive_context}}` | Relevant market factors | "Competitors in this space typically have dedicated CS by this stage" |

## 12. Example Input

```text
BUSINESS CONTEXT: 10-person B2B SaaS startup, pre-Series A, currently no
dedicated customer success role
TASK: Business case for hiring a customer success manager
CONSTRAINTS: Budget for exactly one hire this quarter
AUDIENCE: Co-founder, data-driven, skeptical of new headcount without clear ROI
DECISION FRAMEWORK: Cost-benefit with 12-month payback view
```

## 13. Example Output

```text
BUSINESS CASE: Customer Success Manager Hire

CONTEXT:
At 10 people with no dedicated CS function, customer onboarding and
retention currently fall to the founding team and engineering, pulling
focus from core product development.

COST:
Estimated fully-loaded cost for a CSM hire at this stage: [salary range +
benefits estimate based on stated context].

EXPECTED BENEFIT (12-MONTH VIEW):
- Reduced founder/engineering time on support (estimate: X hours/week
  reclaimed, redirected to product development)
- Improved retention: even a modest reduction in monthly churn compounds
  significantly on annual recurring revenue at this stage
- Faster expansion revenue: dedicated CS typically identifies upsell
  opportunities that a stretched founding team misses

PAYBACK ANALYSIS:
If the hire reduces churn by even [X]% and reclaims [Y] hours/week of
founder time redirected toward revenue-generating work, the estimated
payback period falls within approximately [Z] months — under the 12-month
threshold requested.

TRADE-OFF TO ACKNOWLEDGE:
This is the one hire budget allows this quarter, which means another role
(e.g., an additional engineer) is deprioritized. The recommendation assumes
retention/expansion revenue impact outweighs the opportunity cost of
delayed feature velocity — this is a real trade-off, not a risk-free choice.

RECOMMENDATION:
Proceed with the CS hire, given the current stage's heavier reliance on
retention over pure feature velocity, while flagging the deprioritized
engineering hire as the explicit cost of this choice.
```

*(Note: Specific dollar figures and percentages would be filled in based on
actual company data in real use; placeholders are used here for illustration.)*

## 14. Customization Guide

- **Provide real business context, not generic descriptions**: "A startup" gives the model nothing to calibrate against; "10-person, pre-Series A, B2B SaaS" allows genuinely stage-appropriate reasoning.
- **State constraints as hard limits, not aspirations**: A business case built without acknowledging the real budget/headcount ceiling produces recommendations that look good on paper but aren't actually actionable.
- **Match output to the actual audience's decision-making style**: A data-skeptical audience needs quantified reasoning; a vision-driven audience may respond better to strategic narrative — state this so the output is persuasive to the actual reader, not a generic reader.
- **Name the decision framework explicitly when structure matters**: Without this, the model may default to a generic pros/cons list rather than the more rigorous framework (SWOT, cost-benefit, Porter's Five Forces) actually useful for the decision at hand.

## 15. Output Format Options

- Markdown (memo/document format)
- Table (for structured comparisons, SWOT grids)
- Bullet List (for quick executive summaries)
- Slide-outline format (for pitch deck content)

## 16. Best Practices

- Provide specific, real business context rather than generic descriptions — stage, size, and industry materially change what's actually appropriate advice.
- State constraints as genuine hard limits so recommendations are actually actionable, not just theoretically sound.
- Match tone, depth, and framing to the real audience and their decision-making style.
- Request explicit trade-off acknowledgment rather than a single recommendation presented as costless.

## 17. Common Mistakes

- Vague business context that produces generic, textbook-style advice disconnected from actual company reality.
- Ignoring stated constraints, resulting in a technically sound but practically unusable recommendation.
- Not specifying the audience, leading to a mismatch between the content's tone/depth and what will actually land with the real reader.
- Presenting a recommendation without acknowledging genuine trade-offs, which undermines credibility with a sophisticated audience.

## 18. Prompt Variations

- **Basic Version**: Business context + task only, no constraints/framework specification.
- **Advanced Version**: Full structure with constraints, audience, and decision framework (Section 10).
- **Expert Version**: Adds a request for a pre-emptive "strongest counter-argument" section, where the model argues against its own recommendation before concluding — useful for stress-testing a business case before it's presented to a genuinely skeptical audience.

## 19. Related Prompts

- `28_Marketing_Prompts.md` — go-to-market and positioning strategy overlaps significantly with broader business strategy work
- `29_Email_Prompts.md` — many business communications (negotiation, difficult conversations) are delivered via email
- `05_Tree_of_Thought.md` — useful for exploring multiple strategic options before committing to a single business recommendation

## 20. Tips

- For genuinely high-stakes business decisions, explicitly requesting the strongest case against the recommendation (not just supporting reasoning) before finalizing produces a more defensible, battle-tested deliverable than a purely one-sided business case.
- When real financial figures are available, providing them directly (rather than asking the model to estimate) dramatically improves the credibility and usefulness of any cost-benefit or ROI analysis.

## 21. Limitations

- Financial estimates, market sizing, and competitive claims generated without real data should be treated as illustrative placeholders, not verified figures — real business decisions should be grounded in actual company data.
- Business and market conditions change quickly; general strategic frameworks remain useful, but specific competitive or market claims should be verified against current information for anything time-sensitive.
- This template supports business reasoning and communication; it is not a substitute for professional legal, financial, or accounting advice for decisions with material regulatory or financial consequences.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (useful for market/competitive research) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#business` `#strategy` `#business-case` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
