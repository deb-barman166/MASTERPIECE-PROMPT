# Gemini (Google) Prompting Guide

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-47 · Platform Guide

---

## Overview

This document covers platform-specific considerations for using this library's templates with Google's Gemini models. It's a companion to the general templates, not a replacement — apply the relevant template first, then adjust using the notes here for Gemini-specific conventions.

**Note:** Google updates model capabilities frequently. Verify specifics against Google's current documentation for anything decision-critical, particularly around function calling schemas and multimodal input limits.

---

## 1. Platform-Specific Strengths

- Strong native multimodal capability (text, image, audio, video understanding in a single model), relevant to any template involving mixed media input.
- Google Search grounding integration, benefiting RAG (Template 20) and Research Prompts (33) with more current, verifiable information.
- Native Imagen integration for image generation (Template 31) within the Gemini ecosystem.
- Deep integration with Google Workspace (Docs, Sheets, Gmail), relevant to Business (37) and Productivity (38) workflows conducted within that ecosystem.
- Large context window support in certain model tiers, benefiting long-document tasks (20, 25, 34).

## 2. Function Calling Syntax Notes (relevant to Template 19)

Gemini's function calling uses a `functionDeclarations` structure within the `tools` parameter:

```json
{
  "functionDeclarations": [
    {
      "name": "create_event",
      "description": "Creates a calendar event",
      "parameters": {
        "type": "OBJECT",
        "properties": {
          "title": { "type": "STRING" },
          "start_time": { "type": "STRING" },
          "duration_minutes": { "type": "INTEGER" }
        },
        "required": ["title", "start_time", "duration_minutes"]
      }
    }
  ]
}
```

Note the uppercase type conventions (`OBJECT`, `STRING`, `INTEGER`), which differ from the lowercase JSON Schema convention used by some other providers. This maps onto Template 19's `{{function_schemas}}` variable for Gemini-specific implementations.

## 3. Search Grounding for RAG and Research

Gemini's search grounding feature can be enabled to ground responses in real-time Google Search results, which is directly relevant to Template 20 (RAG) and Template 33 (Research Prompts). When this feature is enabled, the `{{retrieved_context}}` variable in Template 20 may be populated automatically by the grounding feature rather than manually supplied — check whether you're using manual context injection or automatic grounding, since the prompt structure differs slightly between the two approaches.

## 4. Recommended Templates for This Platform

| Template | Fit Notes |
|---|---|
| `20_RAG_Prompting.md` | Strong fit with native search grounding |
| `33_Research_Prompts.md` | Benefits from search grounding for current information |
| `31_Image_Generation_Prompts.md` | Native Imagen integration |
| `37_Business_Prompts.md` / `38_Productivity_Prompts.md` | Deep Google Workspace integration relevant here |
| Any multimodal task | Native strength across text/image/audio/video |

## 5. Platform-Specific Caveats

- Multiple model tiers exist with different capability/context-window trade-offs; confirm which tier you're targeting before assuming a specific context limit.
- Search grounding availability and configuration may vary by access tier and product surface (API vs. consumer app).
- Workspace integration features are specific to certain product surfaces, not the general API — confirm which surface you're building for.

## 6. Quick Adaptation Checklist

When adapting any template for Gemini specifically:

- [ ] Confirm which specific Gemini model/tier you're targeting, since capabilities vary
- [ ] For function calling, use Gemini's uppercase type convention (`OBJECT`, `STRING`, etc.)
- [ ] For RAG/Research tasks, decide between manual context injection vs. search grounding
- [ ] Check current context window limits for the specific model tier before long-document tasks
- [ ] For Workspace-integrated workflows, confirm you're using the correct product surface

## Related Documents

- `44_AI_Model_Compatibility.md` — cross-model comparison
- `20_RAG_Prompting.md` — particularly relevant given search grounding integration
- `31_Image_Generation_Prompts.md` — relevant for Imagen-specific use

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
