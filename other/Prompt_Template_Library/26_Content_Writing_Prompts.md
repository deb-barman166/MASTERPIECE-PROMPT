# Content Writing Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-26

---

## 01. Overview

Content Writing prompting is a domain-specific technique for producing long-form written content — articles, blog posts, guides, and web copy — intended for publication. Effective prompts in this domain need to specify audience, voice/tone, structural conventions (headings, length), SEO considerations if relevant, and the content's purpose (inform, persuade, entertain) — dimensions that shape not just what's said but how it needs to be organized and paced for a reader who may skim before committing to read fully.

## 02. Purpose

- Produce publication-ready content matching a specific voice, audience, and purpose.
- Ensure appropriate structure for how the content will actually be read (skimmed vs. read linearly).
- Balance information density with readability for the target audience's expertise level.
- Support the specific goal of the content (education, conversion, brand awareness) rather than generic "good writing."

## 03. Use Cases

- Blog posts and articles
- Website landing page or About page copy
- How-to guides and tutorials
- Thought leadership / opinion pieces
- Newsletter content
- Long-form educational content

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models — strong long-form writing performance)
- Gemini
- Grok
- Perplexity (useful for research-backed content specifically)

## 05. Prompt Category

`Domain-Specific` · `Content Creation` · `Long-Form Writing`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Topic**: What the content is about
- **Purpose**: Inform, persuade, entertain, educate, convert
- **Target audience**: Who will read this and their existing knowledge level

## 08. Optional Inputs

- Voice/tone (formal, conversational, authoritative, playful)
- Target length
- Structural requirements (headings, intro/conclusion style)
- Key points that must be included
- Call to action (if persuasive/conversion-focused)
- SEO keywords to naturally incorporate

## 09. Variables

| Variable | Required? |
|---|---|
| `{{topic}}` | Yes |
| `{{purpose}}` | Yes |
| `{{target_audience}}` | Yes |
| `{{voice_tone}}` | No |
| `{{target_length}}` | No |
| `{{structural_requirements}}` | No |
| `{{key_points}}` | No |
| `{{call_to_action}}` | No |
| `{{seo_keywords}}` | No |

## 10. Prompt Template

```text
Write content on the following topic.

TOPIC:
{{topic}}

PURPOSE:
{{purpose}}

TARGET AUDIENCE:
{{target_audience}}

VOICE / TONE:
{{voice_tone}}

TARGET LENGTH:
{{target_length}}

STRUCTURAL REQUIREMENTS:
{{structural_requirements}}

KEY POINTS THAT MUST BE INCLUDED:
{{key_points}}

CALL TO ACTION (if applicable):
{{call_to_action}}

SEO KEYWORDS TO NATURALLY INCORPORATE (if applicable):
{{seo_keywords}}

INSTRUCTIONS:
- Write for the specified audience's actual knowledge level — don't
  over-explain basics to an expert audience, or assume unstated context
  with a beginner audience.
- Structure the content for skimmability where appropriate: clear headings,
  short paragraphs, and a strong opening that states what the reader will
  gain.
- Match the specified voice/tone consistently throughout.
- Incorporate SEO keywords naturally; do not force awkward keyword
  repetition that harms readability.
- End with the specified call to action, if one was provided.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{topic}}` | The subject of the content | "How to negotiate a salary raise" |
| `{{purpose}}` | The content's goal | "Educate and build confidence to take action" |
| `{{target_audience}}` | Who is reading and their expertise | "Early-career professionals with little negotiation experience" |
| `{{voice_tone}}` | The writing style/personality | "Encouraging, practical, no corporate jargon" |
| `{{target_length}}` | Approximate word count | "800-1000 words" |
| `{{structural_requirements}}` | Formatting expectations | "H2 subheadings, a numbered action-step list near the end" |
| `{{key_points}}` | Must-include content | "Must mention researching market rate and practicing the conversation aloud" |
| `{{call_to_action}}` | What the reader should do next | "Encourage the reader to schedule the conversation within 2 weeks" |
| `{{seo_keywords}}` | Terms to naturally include | "salary negotiation tips, how to ask for a raise" |

## 12. Example Input

```text
TOPIC: How to start a small vegetable garden with limited space
PURPOSE: Educate and encourage beginners to start
TARGET AUDIENCE: Complete beginners, likely apartment dwellers or small-yard owners
VOICE/TONE: Warm, encouraging, not overly technical
TARGET LENGTH: 600-700 words
STRUCTURAL REQUIREMENTS: H2 subheadings, end with a simple first-step suggestion
KEY POINTS: Must mention container gardening and starting with easy
vegetables (herbs, lettuce)
```

## 13. Example Output

```text
[Content would be generated here as a full article, following the specified
structure: an inviting opening acknowledging the reader may feel space-
limited, H2 sections such as "You Don't Need a Yard: Container Gardening
Basics" and "Start Easy: Herbs and Lettuce First," maintaining a warm,
non-technical tone throughout, at approximately 600-700 words, concluding
with a simple actionable first step like "This weekend, pick up one pot,
one bag of potting soil, and a basil plant — that's all you need to begin."]
```

*(Note: Full article output omitted here for brevity in this template
reference; in actual use, the complete generated article would appear.)*

## 14. Customization Guide

- **Match structural requirements to the reading context**: Content meant for a blog will typically want more headings and skimmable structure than content meant to be read start-to-finish, like a narrative essay.
- **Specify audience expertise precisely**: "General audience" is vague; "complete beginners with no prior experience" or "practitioners familiar with the basics" changes what needs explaining.
- **Set key points explicitly when accuracy/completeness matters**: Without this, the model may organize the content well but omit a detail you consider essential.
- **Use SEO keywords sparingly and naturally**: Over-specifying keyword density instructions tends to produce awkward, forced-sounding copy; a short list of terms to weave in naturally works better than rigid frequency targets.

## 15. Output Format Options

- Markdown (with headings)
- HTML (for direct web publishing)
- Plain text
- Bullet List (for outline-stage content)

## 16. Best Practices

- Always specify audience expertise level — this single detail shapes vocabulary, explanation depth, and assumed context more than any other variable.
- State the content's purpose explicitly (inform vs. persuade vs. entertain) since this changes structure and tone even for the same topic.
- Provide key points that must be included rather than assuming the model will guess your priorities.
- For long content, consider using Skeleton-of-Thought (Template 06) first to approve structure before full expansion.

## 17. Common Mistakes

- Not specifying audience expertise, resulting in content pitched at the wrong level (too basic or too advanced).
- Omitting the content's purpose, leading to a well-written but strategically misaligned piece (e.g., informative when persuasive was needed).
- Over-specifying SEO keyword requirements, producing unnatural, keyword-stuffed prose.
- Requesting long-form content without any structural guidance, resulting in a wall of text that's hard to skim.

## 18. Prompt Variations

- **Basic Version**: Topic + audience only, no tone/structure/SEO specification.
- **Advanced Version**: Full structure with tone, length, structural requirements, and key points (Section 10).
- **Expert Version**: Adds a request for 2-3 alternative headline/opening options, plus a brief note on what makes each option's angle different, useful for A/B testing content hooks.

## 19. Related Prompts

- `06_Skeleton_of_Thought.md` — recommended for planning structure before expanding long-form content
- `27_SEO_Prompts.md` — for deeper keyword research and optimization beyond natural incorporation
- `34_Summarization_Prompts.md` — useful for condensing long content into excerpts or social snippets afterward

## 20. Tips

- For content meant to build trust or authority, explicitly asking for specific, concrete examples rather than generic statements noticeably improves perceived credibility.
- When voice/tone matters a lot, providing a short example of writing in the desired voice (even from a different topic) is often more effective than describing the tone in adjectives alone — this is essentially one-shot prompting (Template 02) applied to style matching.

## 21. Limitations

- Generated content should be fact-checked, especially for specific claims, statistics, or how-to instructions where errors could mislead readers.
- Voice/tone matching from description alone has natural variance; for brand-critical content, providing a style example produces more consistent results than adjectives alone.
- Very long content (multi-thousand word guides) often benefits from being planned and generated in sections (see Skeleton-of-Thought and Prompt Chaining) rather than in a single pass.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (useful for research-backed content) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#content-writing` `#blogging` `#copywriting` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
