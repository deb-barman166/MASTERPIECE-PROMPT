# AI Model Compatibility Overview

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-44 · Reference Document

---

## Overview

Every template in this library includes a per-template Model Compatibility table (Section 22). This document aggregates that information into a single cross-library view, organized by model, so you can quickly see which techniques a given model handles well and where its practical limits tend to be. It also links to the platform-specific prompting guides (Templates 45-49) for deeper, model-native guidance.

**A note on currency:** Model capabilities change frequently as providers release updates. Treat the specifics here as directional guidance current as of this library's compilation, and verify against the model provider's current documentation for anything decision-critical.

---

## 1. General Compatibility Matrix

| Template Category | ChatGPT | Claude | Gemini | Grok | Perplexity |
|---|---|---|---|---|---|
| Foundational (01-03) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Reasoning (04-07, 09-10, 12) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Meta-level (08, 13) | ✅ | ✅ | ✅ | ✅ | ⚠️ Partial |
| Agentic (11, 16-19) | ✅ (with tools) | ✅ (with tool use) | ✅ (with function calling) | ✅ (with tool access) | ✅ (search-native) |
| RAG (20) | ✅ | ✅ | ✅ | ✅ | ✅ (natively RAG-oriented) |
| Code/Technical (21-24) | ✅ | ✅ (strong) | ✅ | ✅ | ⚠️ Limited |
| Data/Research (25, 33) | ✅ (best with code execution) | ✅ (best with code execution) | ✅ | ✅ | ✅ (research-native) |
| Content/Marketing (26-30) | ✅ | ✅ | ✅ | ✅ | ✅ (search-assisted) |
| Media Generation (31-32) | ⚠️ Via DALL-E integration | ❌ Not applicable | ✅ Via Imagen | ❌ Not applicable | ❌ Not applicable |
| Language/Education (35-36) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Business/Productivity (37-38) | ✅ | ✅ | ✅ | ✅ | ⚠️ Limited |
| Creative Writing (39) | ✅ | ✅ (noted strength) | ✅ | ✅ | ⚠️ Limited |
| Security (40) | ✅ | ✅ | ✅ | ✅ | ✅ |

*Legend: ✅ Fully supported · ⚠️ Partial/conditional support · ❌ Not applicable to this model type*

---

## 2. Model-by-Model Summary

### ChatGPT (OpenAI)
**Strengths:** Broad general-purpose capability, mature function calling/plugin ecosystem, strong code generation, DALL-E integration for image generation within the same interface.
**Best suited for:** Function Calling (19), Tool Use (18), Code Generation (21), general-purpose tasks across nearly all templates.
**See:** `45_OpenAI_Prompting.md` for platform-specific guidance.

### Claude (Anthropic)
**Strengths:** Strong long-context handling (beneficial for RAG and Summarization), noted creative writing quality, careful reasoning performance, native tool use and computer use capabilities.
**Best suited for:** Chain-of-Thought (04), Self-Reflection (10), RAG (20), Creative Writing (39), Data Analysis (25) with code execution enabled, long-document Summarization (34).
**See:** `46_Claude_Prompting.md` for platform-specific guidance.

### Gemini (Google)
**Strengths:** Strong multimodal capability, native integration with Google Workspace/Search context, Imagen integration for image generation.
**Best suited for:** Multimodal tasks, RAG with search grounding, Image Generation (31) via Imagen.
**See:** `47_Gemini_Prompting.md` for platform-specific guidance.

### Grok (xAI)
**Strengths:** Real-time X/Twitter data access, particularly attuned to X/Twitter platform conventions for social content.
**Best suited for:** Social Media Prompts (30) specifically for X/Twitter, current-events research when paired with search access.
**See:** `48_Grok_Prompting.md` for platform-specific guidance.

### Perplexity
**Strengths:** Natively search/research-oriented, strong citation habits, real-time information retrieval by default.
**Best suited for:** Research Prompts (33), RAG-style grounded answers (20), current-events and fact-finding tasks.
**Less suited for:** Long-form creative writing, code generation, and other tasks outside its research-first design.
**See:** `49_Perplexity_Prompting.md` for platform-specific guidance.

---

## 3. Choosing the Right Model for a Task

| If your task is primarily... | Consider prioritizing... |
|---|---|
| Current-events research or fact-finding | Perplexity, or any model with search enabled |
| Long-document analysis or summarization | Claude (long-context strength) |
| Code generation and debugging | Claude or ChatGPT |
| Image generation | ChatGPT (DALL-E) or Gemini (Imagen) |
| Creative writing | Claude or ChatGPT |
| Real-time social/current data | Grok |
| Multimodal (text + image + more) | Gemini |
| Agentic/tool-use workflows | Claude or ChatGPT (most mature tool ecosystems) |

This table reflects general tendencies, not fixed rules — model capabilities are updated frequently, and the best choice for any specific task should be validated empirically rather than assumed from this table alone.

---

## 4. Cross-Model Prompting Considerations

- **Function/tool calling syntax differs by provider.** Templates 18 and 19 use generic pseudocode; always adapt to the specific provider's actual API schema conventions.
- **Context window sizes vary significantly** and change with model updates — this affects how much source content can be included for RAG (20), Summarization (34), and Data Analysis (25) tasks.
- **Not all models support the same tool ecosystem.** Agentic (16), ReAct (11), and Tool Use (18) templates assume tool/function-calling infrastructure that must be separately configured per platform.
- **Media generation is provider-specific**, not a general LLM capability — Templates 31 and 32 apply to dedicated image/video generation tools, some of which are integrated into a chat interface (like DALL-E within ChatGPT) and some of which are standalone (Midjourney, Runway).

## Related Documents

- `45_OpenAI_Prompting.md` through `49_Perplexity_Prompting.md` — detailed platform-specific guides
- `52_Prompt_Library_Index.md` — full template index

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
