# Perplexity Prompting Guide

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-49 · Platform Guide

---

## Overview

This document covers platform-specific considerations for using this library's templates with Perplexity. It's a companion to the general templates, not a replacement — apply the relevant template first, then adjust using the notes here for Perplexity-specific conventions.

Perplexity differs from the other platforms covered in this library in a fundamental way: it's natively built as a search-and-answer engine rather than a general-purpose conversational assistant, which shapes which templates fit well and which don't.

---

## 1. Platform-Specific Strengths

- Natively search-first design with real-time web retrieval by default, making it an excellent fit for Template 33 (Research Prompts) and Template 20 (RAG Prompting) without needing to manually configure search tooling.
- Strong, consistent citation habits by default, since sourcing is central to its core product design rather than an optional add-on.
- Well-suited to fact-finding, current-events, and comparative research tasks where grounding in real, current sources matters more than open-ended generation.

## 2. Where Perplexity Is a Weaker Fit

Many templates in this library assume general-purpose conversational or generative capability that isn't Perplexity's core design focus:

- **Long-form creative writing (Template 39):** Perplexity's search-and-answer design isn't optimized for open-ended fiction/poetry generation.
- **Complex code generation (Templates 21-24):** Less specialized for this than dedicated coding-capable assistants.
- **Image/video generation (Templates 31-32):** Not a native capability.
- **Function calling / structured tool use (Template 19):** Less common use case for this platform's typical usage pattern.
- **Multi-agent or complex agentic workflows (Templates 16-17):** Outside its core product focus.

For these categories, consider the model compatibility notes in each template (Section 22) and lean toward other platforms unless you have a specific reason tied to Perplexity's search integration.

## 3. Structuring Research Prompts for Perplexity

Because search and citation are native to how Perplexity operates, Template 33 (Research Prompts) can often be used with a lighter structure than on other platforms — the `{{source_quality_requirements}}` and citation expectations that need to be explicitly requested elsewhere are often closer to Perplexity's default behavior. That said, explicitly stating scope boundaries and time-frame relevance (per Template 33's structure) remains valuable, since these shape what Perplexity searches for, not just how it presents results.

## 4. Recommended Templates for This Platform

| Template | Fit Notes |
|---|---|
| `33_Research_Prompts.md` | Excellent native fit — core product strength |
| `20_RAG_Prompting.md` | Strong fit given native search/citation habits |
| `27_SEO_Prompts.md` | Useful for current SERP/competitive research specifically |
| `28_Marketing_Prompts.md` | Useful for the competitive research component specifically |

## 5. Platform-Specific Caveats

- Response style tends toward concise, citation-backed answers rather than long-form generative content — adjust length expectations for templates requesting extensive output.
- Real-time search means results can genuinely change between requests for the same query as underlying sources update — this is a feature for currency but means output isn't fully reproducible run-to-run in the way some other platforms' generation might be.
- Less suited to tasks requiring sustained multi-turn creative or technical collaboration compared to general-purpose assistants.

## 6. Quick Adaptation Checklist

When adapting any template for Perplexity specifically:

- [ ] Favor Research (33) and RAG (20) style templates where this platform's strengths are most relevant
- [ ] For other template categories, check Section 22 (Model Compatibility) in that specific template first
- [ ] Expect and design for citation-backed, relatively concise output by default
- [ ] Account for potential result variability between runs given real-time search grounding

## Related Documents

- `44_AI_Model_Compatibility.md` — cross-model comparison
- `33_Research_Prompts.md` — the strongest-fit template for this platform
- `20_RAG_Prompting.md` — closely aligned with Perplexity's native design

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
