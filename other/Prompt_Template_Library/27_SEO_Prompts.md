# SEO Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-27

---

## 01. Overview

SEO prompting is a domain-specific technique for optimizing content and site elements for search engine visibility — keyword strategy, on-page optimization, meta content, and content structure aligned with search intent. Effective SEO prompts require specifying the target keyword(s) and their search intent (informational, navigational, transactional, commercial), the competitive landscape, and the specific on-page element being optimized (title tag, meta description, headings, body content) — since each element has different length constraints and optimization goals.

## 02. Purpose

- Align content with actual search intent, not just keyword presence.
- Optimize specific on-page elements within their real technical constraints (character limits, etc.).
- Balance keyword optimization with genuine readability and user value.
- Support both new content creation and optimization of existing underperforming content.

## 03. Use Cases

- Writing SEO-optimized title tags and meta descriptions
- Keyword research and search intent classification
- Structuring content around a target keyword's likely search intent
- Auditing/improving existing content for better search performance
- Generating header (H1-H3) structures aligned with keyword clusters

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (useful for current SERP/competitive research)

## 05. Prompt Category

`Domain-Specific` · `Marketing` · `Search Optimization`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Target keyword(s)**: The primary term(s) to optimize for
- **Content element**: What's being optimized (title tag, meta description, full article, headers)

## 08. Optional Inputs

- Search intent classification (informational, navigational, transactional, commercial)
- Competitor content/SERP context
- Character/length limits for the specific element
- Secondary/related keywords
- Brand voice constraints

## 09. Variables

| Variable | Required? |
|---|---|
| `{{target_keywords}}` | Yes |
| `{{content_element}}` | Yes |
| `{{search_intent}}` | No |
| `{{competitor_context}}` | No |
| `{{length_limit}}` | No |
| `{{secondary_keywords}}` | No |
| `{{brand_voice}}` | No |

## 10. Prompt Template

```text
Optimize the following content element for search engines.

TARGET KEYWORD(S):
{{target_keywords}}

CONTENT ELEMENT BEING OPTIMIZED:
{{content_element}}

SEARCH INTENT:
{{search_intent}}

SECONDARY/RELATED KEYWORDS:
{{secondary_keywords}}

COMPETITOR/SERP CONTEXT (if available):
{{competitor_context}}

LENGTH LIMIT:
{{length_limit}}

BRAND VOICE:
{{brand_voice}}

INSTRUCTIONS:
- Prioritize matching the actual search intent over keyword density —
  informational queries need different content than transactional ones.
- Stay within the specified length limit precisely; note the exact
  character count if the element has a strict limit (e.g., title tags,
  meta descriptions).
- Include the primary keyword naturally and prominently (e.g., near the
  start of a title tag) without keyword stuffing.
- If competitor context is provided, identify a differentiation angle
  rather than simply mimicking what's already ranking.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{target_keywords}}` | The primary term(s) to rank for | "best running shoes for flat feet" |
| `{{content_element}}` | The specific element being written | "Title tag and meta description" |
| `{{search_intent}}` | The likely reason someone searches this | "Commercial investigation — comparing options before buying" |
| `{{secondary_keywords}}` | Related terms to weave in | "flat feet running shoe support, overpronation shoes" |
| `{{competitor_context}}` | What's currently ranking | "Top results are mostly 'best of' listicles from shoe review sites" |
| `{{length_limit}}` | Character constraints | "Title tag: 50-60 characters; Meta description: 150-160 characters" |
| `{{brand_voice}}` | Tone constraints from brand guidelines | "Friendly expert, not overly salesy" |

## 12. Example Input

```text
TARGET KEYWORD: best running shoes for flat feet
CONTENT ELEMENT: Title tag and meta description
SEARCH INTENT: Commercial investigation (comparing before buying)
SECONDARY KEYWORDS: flat feet running support, overpronation shoes
COMPETITOR CONTEXT: Top results are listicle-style "best of" articles
LENGTH LIMIT: Title tag 50-60 chars; meta description 150-160 chars
BRAND VOICE: Friendly expert, not salesy
```

## 13. Example Output

```text
TITLE TAG (58 characters):
Best Running Shoes for Flat Feet (2026 Expert Picks)

META DESCRIPTION (156 characters):
Flat feet need the right support to avoid pain. We tested top running
shoes for overpronation and arch support — see our expert picks and why
they work.

RATIONALE:
- Title tag leads with the exact target keyword, includes a freshness
  signal ("2026") and a differentiator ("Expert Picks") to stand out
  against generic "best of" competitors.
- Meta description opens by naming the underlying problem (flat feet
  needing support) before the solution, matching commercial-investigation
  intent — the reader is still evaluating, not ready to buy a specific
  product yet.
- "Overpronation" and "arch support" (secondary keywords) are worked in
  naturally rather than appended as a keyword list.
- Voice stays expert/informative rather than pushing a direct sales angle,
  matching the specified brand voice.
```

## 14. Customization Guide

- **Always specify search intent, not just the keyword**: The same keyword can serve very different intents (e.g., "best running shoes" could be informational research or ready-to-buy commercial intent) — this materially changes what content should say.
- **Provide exact length limits for technical elements**: Title tags and meta descriptions have real display truncation limits; vague guidance ("keep it short") risks output that gets cut off in actual search results.
- **Include competitor/SERP context when optimizing for a competitive keyword**: This helps the model suggest genuine differentiation rather than generic best-practice content that blends in with what's already ranking.
- **State brand voice constraints even briefly**: SEO optimization without voice guardrails can drift into generic, keyword-stuffed phrasing that doesn't match how the brand actually communicates.

## 15. Output Format Options

- Plain text (with character counts noted)
- Table (for multiple keyword/element combinations)
- Markdown
- CSV (for bulk title tag/meta description generation)

## 16. Best Practices

- Specify search intent explicitly — it should drive content structure more than raw keyword matching.
- Always request exact character counts for length-constrained elements like title tags and meta descriptions.
- Ask for a rationale alongside the optimized copy, so keyword placement and intent-matching decisions are visible and can be evaluated, not just trusted blindly.
- Provide competitor context when available to push toward differentiation rather than a generic best-practices response.

## 17. Common Mistakes

- Treating all searches for a keyword as having the same intent, producing content mismatched to what searchers actually want.
- Not specifying length limits, resulting in title tags or meta descriptions that would be truncated in actual search results.
- Over-indexing on keyword density at the expense of natural readability, which can also work against modern search algorithms that weigh genuine relevance and quality.
- Requesting content optimization without any competitor/SERP context, missing the chance to differentiate from what's already ranking.

## 18. Prompt Variations

- **Basic Version**: Keyword + element only, no intent or length specification.
- **Advanced Version**: Full structure with intent, length limits, and competitor context (Section 10).
- **Expert Version**: Adds a request for 3 variations of the title tag/meta description (e.g., benefit-led, curiosity-led, and authority-led angles) for A/B testing, plus a brief prediction of which angle likely performs best given the stated search intent.

## 19. Related Prompts

- `26_Content_Writing_Prompts.md` — SEO keyword strategy often informs the structure of the full content piece
- `28_Marketing_Prompts.md` — SEO is one channel within a broader marketing strategy
- `08_Meta_Prompting.md` — useful for refining an underperforming SEO prompt template based on actual ranking results over time

## 20. Tips

- For genuinely current SERP research (what's actually ranking right now), pairing this template with a web-search-enabled model workflow produces far more grounded competitor context than relying on the model's training knowledge alone, since search rankings change frequently.
- When optimizing existing underperforming content, providing the current title tag/meta description alongside the target keyword lets the model diagnose specifically what might be causing low click-through, not just generate new copy from scratch.

## 21. Limitations

- Model knowledge of current search algorithm behavior and ranking factors may not reflect the most recent updates; SEO best practices should be cross-checked against current guidance from search engines themselves for anything algorithm-specific.
- Without real-time SERP access, competitor context must be manually provided — the model cannot independently verify what's currently ranking unless connected to a search tool.
- SEO success depends on many factors beyond on-page optimization (backlinks, site authority, technical SEO) that this template doesn't address.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (useful for current SERP research) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#seo` `#search-optimization` `#marketing` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
