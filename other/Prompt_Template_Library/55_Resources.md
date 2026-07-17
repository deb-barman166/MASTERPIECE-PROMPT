# Resources

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-55 · External References

---

## Overview

This document lists the categories of external resources worth consulting alongside this library, organized by type. Because prompt engineering guidance, model capabilities, and platform documentation change frequently, this document intentionally points to resource *categories* and *how to find current versions* rather than hardcoding specific URLs likely to become outdated. Always verify you're looking at current documentation, particularly for anything platform- or model-specific.

---

## 1. Official Model Provider Documentation

The single most reliable source for current capability details, API syntax, and best practices is each provider's own official documentation. For anything in this library's platform guides (Templates 45-49) that may have changed, check:

- **OpenAI:** Official API documentation and prompting guides, typically covering function calling schemas, model comparison, and usage policies.
- **Anthropic (Claude):** Official documentation covering tool use, prompting guides, and model comparison — particularly useful for verifying current context window sizes and tool use schema conventions referenced in Template 46.
- **Google (Gemini):** Official AI/Cloud documentation covering function calling, multimodal capabilities, and search grounding configuration referenced in Template 47.
- **xAI (Grok):** Official API documentation, particularly for verifying current function calling compatibility and real-time data access scope referenced in Template 48.
- **Perplexity:** Official API and product documentation for citation behavior and search configuration referenced in Template 49.

**Why this matters:** Templates 45-49 in this library describe general conventions as of compilation, but exact schemas, parameter names, and capabilities are updated by providers regularly. Treat this library's platform guides as orientation, and official docs as the source of truth for exact syntax.

## 2. Image and Video Generation Tool Documentation

For Templates 31 and 32, the specific parameter syntax (aspect ratio flags, negative prompts, style parameters) is tool-specific and updates frequently:

- Midjourney's official prompt guide and parameter list
- DALL-E's documentation (via OpenAI)
- Stable Diffusion's documentation (varies by specific implementation/fork)
- Adobe Firefly's documentation
- Runway, Pika, Sora, Veo, and Luma's respective documentation for video generation parameters

## 3. Foundational Prompt Engineering Concepts

For deeper theoretical background behind the techniques in Templates 01-20, useful categories of resource include:

- Academic papers introducing specific techniques (e.g., the original Chain-of-Thought, Tree-of-Thought, ReAct, and Self-Consistency papers, typically findable by searching the technique name plus "paper" on academic search engines)
- Provider-published prompt engineering guides (most major model providers publish their own guidance, which sometimes reflects model-specific nuances not covered in general-purpose libraries like this one)

## 4. Domain-Specific Reference Material

For the domain templates (21-40), general prompting principles from this library should be paired with genuine domain expertise resources:

- **SQL (23):** Official documentation for your specific database system (PostgreSQL, MySQL, SQL Server, etc.)
- **Web Development (24):** Framework-specific official documentation (React, Vue, etc.) and accessibility guidelines (WCAG)
- **SEO (27):** Search engine's own webmaster/creator guidelines, updated as ranking factors evolve
- **Security (40):** OWASP resources for current secure coding practices and vulnerability classes
- **Translation (35):** Native speaker review remains valuable even with strong prompting

## 5. Communities and Ongoing Learning

Prompt engineering is a fast-evolving field. Beyond static documentation, consider:

- Provider-run developer communities/forums for real-world troubleshooting
- Changelogs and release notes from model providers (often where genuinely new capabilities are first announced)
- Practitioner-shared prompt examples and case studies (evaluate critically — quality varies significantly)

---

## How to Verify This Library Is Current

Given how quickly this field changes, a periodic sanity-check practice:

1. Check `56_Changelog.md` for this library's own last update date.
2. Cross-check `44_AI_Model_Compatibility.md` against current provider documentation, especially for newer or recently updated models.
3. For any template you rely on heavily and repeatedly, spot-check its Section 22 (Model Compatibility) and Section 21 (Limitations) against current reality — these are the sections most likely to go stale first.

## Related Documents

- `44_AI_Model_Compatibility.md` — the library's own cross-model comparison, to be checked against current provider docs
- `45`-`49` — platform-specific guides referencing provider documentation directly
- `56_Changelog.md` — tracks when this library itself was last meaningfully updated

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
