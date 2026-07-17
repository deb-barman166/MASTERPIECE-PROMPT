# Marketing Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-28

---

## 01. Overview

Marketing prompting is a domain-specific technique for producing strategic and creative marketing assets — campaign concepts, positioning statements, ad copy, and messaging frameworks. Effective marketing prompts require specifying the product/offer, the target customer segment (including their pain points and motivations), the competitive positioning, the channel the content will run on (each with different conventions and constraints), and the specific marketing objective (awareness, consideration, conversion, retention).

## 02. Purpose

- Produce marketing content grounded in actual customer pain points and positioning, not generic sales language.
- Match content to the specific channel's format conventions and constraints.
- Align messaging with a clear marketing funnel stage and objective.
- Differentiate from competitors based on genuine positioning, not superlatives alone.

## 03. Use Cases

- Ad copy (search, social, display)
- Campaign concept development
- Product positioning and messaging frameworks
- Value proposition and elevator pitch development
- Customer persona-driven messaging variations
- Competitive differentiation messaging

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (useful for competitive/market research)

## 05. Prompt Category

`Domain-Specific` · `Marketing` · `Strategic Messaging`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Product/offer description**: What's being marketed
- **Target customer segment**: Who this is for, including pain points/motivations
- **Marketing objective**: Awareness, consideration, conversion, or retention

## 08. Optional Inputs

- Channel/format (search ad, social post, email, landing page)
- Competitive positioning/differentiation
- Brand voice guidelines
- Length/character constraints per channel
- Call to action

## 09. Variables

| Variable | Required? |
|---|---|
| `{{product_offer}}` | Yes |
| `{{target_segment}}` | Yes |
| `{{marketing_objective}}` | Yes |
| `{{channel_format}}` | No |
| `{{competitive_positioning}}` | No |
| `{{brand_voice}}` | No |
| `{{length_constraints}}` | No |
| `{{call_to_action}}` | No |

## 10. Prompt Template

```text
Create marketing content for the following.

PRODUCT/OFFER:
{{product_offer}}

TARGET CUSTOMER SEGMENT:
{{target_segment}}

MARKETING OBJECTIVE:
{{marketing_objective}}

CHANNEL/FORMAT:
{{channel_format}}

COMPETITIVE POSITIONING:
{{competitive_positioning}}

BRAND VOICE:
{{brand_voice}}

LENGTH/CHARACTER CONSTRAINTS:
{{length_constraints}}

CALL TO ACTION:
{{call_to_action}}

INSTRUCTIONS:
- Lead with the customer's actual pain point or motivation, not a generic
  product feature list.
- Match the format conventions of the specified channel (e.g., search ads
  need concise, keyword-relevant copy; social posts can be more
  conversational).
- If competitive positioning is provided, differentiate based on genuine
  distinguishing factors rather than unsupported superlatives ("the best,"
  "#1").
- Stay within any specified length/character constraints exactly.
- Close with the specified call to action, matched naturally to the
  objective (e.g., "Learn More" for awareness vs. "Buy Now" for conversion).
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{product_offer}}` | What's being marketed | "A meal-kit subscription service with 20-minute recipes" |
| `{{target_segment}}` | Who this targets and their motivations | "Busy working parents who want home-cooked meals but lack time to plan/shop" |
| `{{marketing_objective}}` | The funnel stage goal | "Conversion — get them to sign up for a trial" |
| `{{channel_format}}` | Where this will run | "Facebook/Instagram feed ad" |
| `{{competitive_positioning}}` | How this differs from alternatives | "Faster prep time than competitors (20 min vs. their 45 min average)" |
| `{{brand_voice}}` | Tone guidelines | "Warm, relatable, not preachy about health" |
| `{{length_constraints}}` | Format-specific limits | "Primary text under 125 characters, headline under 40 characters" |
| `{{call_to_action}}` | Desired next action | "Start Your Free Trial" |

## 12. Example Input

```text
PRODUCT/OFFER: Meal-kit subscription with 20-minute recipes
TARGET SEGMENT: Busy working parents, limited time to plan/shop/cook
MARKETING OBJECTIVE: Conversion (free trial signup)
CHANNEL/FORMAT: Instagram feed ad
COMPETITIVE POSITIONING: 20 min prep vs. competitors' ~45 min average
BRAND VOICE: Warm, relatable, not preachy
LENGTH CONSTRAINTS: Headline under 40 chars, primary text under 125 chars
CALL TO ACTION: Start Your Free Trial
```

## 13. Example Output

```text
HEADLINE (38 characters):
Dinner in 20 Minutes. Every Night.

PRIMARY TEXT (122 characters):
Between work and pickup lines, who has an hour to cook? Real meals, real
fast — half the time of typical meal kits.

CTA BUTTON: Start Your Free Trial

RATIONALE:
- Headline leads with the core benefit (time) rather than the product
  category, since "meal kit" itself isn't the motivating factor for a
  time-strapped parent — the outcome is.
- Primary text opens with a relatable pain point ("who has an hour to
  cook?") before introducing the differentiator (half the time of typical
  competitors), matching the warm, non-preachy brand voice by focusing on
  practical relief rather than guilt about not cooking from scratch.
- Competitive differentiation ("half the time") is stated as a comparative
  fact rather than an unsupported superlative like "the fastest," keeping
  the claim defensible.
```

## 14. Customization Guide

- **Describe the target segment by motivation, not just demographics**: "Working parents" is a start, but "working parents who feel guilty about not cooking but genuinely lack time" gives the model an actual emotional hook to write toward.
- **Match format constraints to the real channel specs**: Character limits, tone conventions, and typical content structure vary significantly between search ads, social posts, email subject lines, and landing pages — specify the actual channel, not just "an ad."
- **State competitive positioning as verifiable facts, not aspirational claims**: "20 min vs. their 45 min average" is defensible; "the best meal kit" is not — precise positioning produces more credible, differentiated copy.
- **Match call-to-action language to the funnel stage**: Awareness content shouldn't push a hard "Buy Now" CTA; conversion content shouldn't stay vague with "Learn More" if a direct action is the actual goal.

## 15. Output Format Options

- Plain text (with character counts noted)
- Table (for multiple ad variations)
- Markdown
- JSON (for ad platform bulk upload formatting)

## 16. Best Practices

- Ground messaging in the target segment's actual pain point or motivation, not a generic feature list.
- Specify the real channel/format so conventions (length, tone, structure) are matched accurately.
- Provide competitive positioning as concrete, defensible facts rather than vague superlatives.
- Match the call-to-action intensity to the actual marketing objective/funnel stage.

## 17. Common Mistakes

- Describing the target segment only by demographics, missing the psychological motivation that actually drives message resonance.
- Not specifying the channel, resulting in copy that doesn't fit the format conventions or length constraints of where it will actually run.
- Using unsupported superlative claims ("the best," "#1") instead of specific, defensible differentiators.
- Mismatching CTA intensity to funnel stage (e.g., a hard sell in a pure-awareness placement).

## 18. Prompt Variations

- **Basic Version**: Product + segment + objective only, no channel/positioning detail.
- **Advanced Version**: Full structure with channel, positioning, voice, and constraints (Section 10).
- **Expert Version**: Adds a request for 3 distinct angle variations (e.g., pain-point-led, aspiration-led, and social-proof-led) for the same offer and segment, useful for creative testing across ad sets.

## 19. Related Prompts

- `26_Content_Writing_Prompts.md` — longer-form marketing content (blog posts, landing pages) shares many of the same audience/voice principles
- `29_Email_Prompts.md` — email marketing specifically has its own format conventions worth a dedicated template
- `30_Social_Media_Prompts.md` — social-specific format and engagement conventions

## 20. Tips

- For any claim involving a comparison to competitors, keeping the comparison factual and specific (not just superlative) both produces better copy and avoids potential regulatory/legal issues with unsubstantiated marketing claims.
- Testing multiple angle variations (pain-point vs. aspiration vs. social proof) for the same audience often reveals which emotional lever actually resonates — a single "best guess" version limits this discovery.

## 21. Limitations

- Marketing copy performance ultimately needs to be validated with real audience testing (A/B tests, engagement metrics) — a well-constructed prompt produces plausible, on-brand copy, not guaranteed performance.
- Claims about competitors or market positioning should be verified for accuracy before publishing, since the model cannot independently confirm competitive facts unless provided or retrieved via search.
- Format/character limits for specific ad platforms change over time; always verify current specs for the actual platform being used rather than relying solely on the model's training knowledge.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (useful for competitive research) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#marketing` `#advertising` `#copywriting` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
