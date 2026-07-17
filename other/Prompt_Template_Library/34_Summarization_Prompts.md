# Summarization Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-34

---

## 01. Overview

Summarization prompting is a domain-specific technique for condensing longer content into a shorter form while preserving what actually matters. The key variable that's easy to overlook is that "summarize this" is underspecified — a summary for a busy executive, a summary for someone deciding whether to read the full piece, and a summary that preserves technical precision for a domain expert are all legitimately different outputs from the same source text. Effective summarization prompts specify the summary's purpose/audience, the target length, and what should be prioritized (key facts, action items, arguments, emotional tone) versus what can be safely dropped.

## 02. Purpose

- Produce summaries genuinely calibrated to who will read them and why.
- Preserve the specific information type that matters most for the use case (decisions, facts, arguments, sentiment).
- Avoid both over-compression (losing critical nuance) and under-compression (a "summary" nearly as long as the original).
- Handle different source formats (articles, meeting transcripts, research papers, long documents) appropriately.

## 03. Use Cases

- Condensing long articles or reports into executive summaries
- Meeting transcript summarization with action items
- Research paper abstracts/key-findings extraction
- Long document TL;DR generation
- Multi-document synthesis into a single summary
- Email thread or conversation summarization

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models — strong long-context summarization)
- Gemini
- Grok
- Perplexity (useful for summarizing search-retrieved content)

## 05. Prompt Category

`Domain-Specific` · `Information Processing` · `Condensation`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Source content**: The text/document to summarize
- **Target length**: How short the summary should be

## 08. Optional Inputs

- Audience/purpose
- Priority information type (facts, decisions, arguments, sentiment)
- Format (narrative paragraph, bullet points, structured sections)
- What to explicitly exclude
- Whether direct quotes are needed for key points

## 09. Variables

| Variable | Required? |
|---|---|
| `{{source_content}}` | Yes |
| `{{target_length}}` | Yes |
| `{{audience_purpose}}` | No |
| `{{priority_information}}` | No |
| `{{summary_format}}` | No |
| `{{explicit_exclusions}}` | No |

## 10. Prompt Template

```text
Summarize the following content.

SOURCE CONTENT:
{{source_content}}

TARGET LENGTH:
{{target_length}}

AUDIENCE/PURPOSE:
{{audience_purpose}}

PRIORITY INFORMATION TO PRESERVE:
{{priority_information}}

FORMAT:
{{summary_format}}

EXPLICITLY EXCLUDE:
{{explicit_exclusions}}

INSTRUCTIONS:
- Prioritize the information type specified above; it's acceptable to omit
  other details even if interesting, to stay within the target length.
- Preserve factual accuracy — do not add interpretation or conclusions not
  present in the source content.
- Match the summary's structure to its stated purpose (e.g., a
  decision-focused summary should lead with decisions, not background).
- Stay within the target length precisely; note the actual word/sentence
  count if it's a hard constraint.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{source_content}}` | The text to be summarized | A 3,000-word quarterly business report |
| `{{target_length}}` | Desired summary length | "3-4 sentences" or "under 150 words" |
| `{{audience_purpose}}` | Who reads this and why | "Executive who needs to decide whether to greenlight budget increase" |
| `{{priority_information}}` | What matters most to preserve | "Financial figures and the specific recommendation, not background context" |
| `{{summary_format}}` | Structural presentation | "3 bullet points: what happened, why it matters, what's being asked" |
| `{{explicit_exclusions}}` | What to leave out | "Skip methodology details, focus only on findings" |

## 12. Example Input

```text
SOURCE CONTENT: [A 2,000-word meeting transcript covering a product
roadmap discussion, including some tangents about unrelated team logistics]

TARGET LENGTH: Under 100 words
AUDIENCE/PURPOSE: Team members who missed the meeting, need to know what
was decided and what they're responsible for
PRIORITY INFORMATION: Decisions made and action items with owners
FORMAT: Bullet points
EXPLICIT EXCLUSIONS: Skip the tangential logistics discussion entirely
```

## 13. Example Output

```text
Meeting Summary:

Decisions made:
- Q3 roadmap prioritizes the mobile redesign over the API v2 migration
- Launch target moved from August to September to allow for additional
  user testing

Action items:
- [Name] to finalize mobile redesign specs by end of next week
- [Name] to communicate the revised timeline to stakeholders
- API v2 migration re-planned for Q4, no immediate action needed
```

*(Word count: 62 — under the 100-word target; logistics tangent excluded as instructed)*

## 14. Customization Guide

- **Always specify audience/purpose, even briefly**: The same source content genuinely needs a different summary for "someone deciding whether to read the full thing" vs. "someone who will never read the full thing and needs everything actionable now."
- **Set target length as a real constraint, not a vague suggestion**: "Short" is interpreted inconsistently; "under 100 words" or "3 sentences" is unambiguous and verifiable.
- **State priority information explicitly for mixed-content sources**: A meeting transcript, for example, might contain decisions, debate, and small talk — specifying what to prioritize prevents an even-handed summary that dilutes the actually important parts.
- **Use explicit exclusions for known-irrelevant sections**: If part of the source is reliably not useful (e.g., a recurring administrative preamble in meeting transcripts), naming it for exclusion saves the summary from wasting space on it.

## 15. Output Format Options

- Narrative paragraph
- Bullet List
- Structured sections (e.g., Decisions / Action Items / Open Questions)
- Table (for comparative multi-document summaries)
- TL;DR + expandable detail format

## 16. Best Practices

- Specify target length as a concrete, checkable constraint rather than a vague relative term.
- State audience/purpose explicitly, since it should genuinely change what's prioritized in the summary.
- Request factual preservation without added interpretation — a summary should compress, not editorialize.
- For mixed-content sources (meetings, long threads), explicitly name what to prioritize and what to exclude.

## 17. Common Mistakes

- Vague length targets ("keep it short") that produce inconsistent summary lengths across different runs.
- Not specifying audience/purpose, resulting in a generic summary that doesn't serve the actual reader's needs.
- Allowing interpretation or conclusions to creep into what should be a factual condensation of the source.
- Summarizing mixed-content sources evenly rather than prioritizing the genuinely important parts.

## 18. Prompt Variations

- **Basic Version**: Source + target length only, no audience/priority specification.
- **Advanced Version**: Full structure with audience, priority information, and format (Section 10).
- **Expert Version**: Adds a request for the summary to include a very brief note on what was excluded and why, useful for high-stakes summarization where the reader needs to know if something significant was left out (e.g., "excluded: a dissenting opinion raised but not resolved in the discussion").

## 19. Related Prompts

- `26_Content_Writing_Prompts.md` — summaries sometimes need to be rewritten in a more polished, publication-ready voice after initial condensation
- `33_Research_Prompts.md` — research findings frequently need to be summarized into a digestible form after gathering
- `20_RAG_Prompting.md` — summarization is a specific, target-length-constrained case of grounded generation from provided context

## 20. Tips

- For summaries that will inform a decision, explicitly requesting that the summary lead with the decision-relevant information (not background/context first) makes the summary far more immediately useful for a busy reader.
- When summarizing something with a clear narrative arc or chronological structure (a meeting, a story, a process), asking the model to preserve that structure at a condensed scale, rather than reorganizing by importance, sometimes produces a more natural and easier-to-follow summary — the right choice depends on whether the reader needs the story or just the takeaways.

## 21. Limitations

- Very long source content may exceed context window limits for some models, particularly if minimal information loss is required — extremely long documents may need to be summarized in sections first, then synthesized (see Prompt Chaining, Template 14).
- Summarization inherently involves judgment calls about what's important; even a well-specified prompt reflects the model's interpretation of the stated priorities, which is worth a quick human sanity-check for high-stakes summaries.
- Highly technical or domain-specific source content may need domain expertise to verify that a compressed summary hasn't lost technically important nuance, even if it reads as complete to a non-expert.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ (strong long-context performance) |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (useful for search-retrieved content) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#summarization` `#condensation` `#tldr` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
