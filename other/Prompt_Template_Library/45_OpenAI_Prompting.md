# OpenAI / ChatGPT Prompting Guide

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-45 · Platform Guide

---

## Overview

This document covers platform-specific considerations for using this library's templates with OpenAI's ChatGPT and API models (GPT-4, GPT-4o, GPT-4.1, and successors). It's a companion to the general templates, not a replacement — apply the relevant template first, then adjust using the notes here for OpenAI-specific conventions.

**Note:** OpenAI updates model capabilities and interfaces frequently. Verify specifics against OpenAI's current documentation for anything decision-critical, particularly around function calling schemas and rate limits.

---

## 1. Platform-Specific Strengths

- Mature, well-documented function calling / tool use API, making Templates 18 and 19 particularly reliable.
- Native DALL-E integration within ChatGPT, allowing image generation (Template 31) directly within the same conversational interface.
- Broad plugin/GPTs ecosystem for extending capability with third-party tools.
- Strong general-purpose code generation performance.
- Custom GPTs allow persistent system-level instructions, useful for deploying a template as a reusable configured assistant.

## 2. Function Calling Syntax Notes (relevant to Template 19)

OpenAI's function calling uses a `tools` array with JSON Schema-defined parameters. When adapting Template 19's generic schema format to OpenAI's actual API:

```json
{
  "type": "function",
  "function": {
    "name": "create_event",
    "description": "Creates a calendar event",
    "parameters": {
      "type": "object",
      "properties": {
        "title": { "type": "string" },
        "start_time": { "type": "string", "format": "date-time" },
        "duration_minutes": { "type": "integer" }
      },
      "required": ["title", "start_time", "duration_minutes"]
    }
  }
}
```

This maps directly onto Template 19's `{{function_schemas}}` variable — supply the schema in this format when working with OpenAI's API specifically.

## 3. Custom GPTs and System Prompts

For templates intended for repeated/production use (particularly Templates 08, 14, 16-18), consider deploying them as a Custom GPT with the template's structure embedded in the GPT's system instructions. This avoids re-pasting the full template on every use and allows the GPT's knowledge/actions to be pre-configured.

## 4. Recommended Templates for This Platform

| Template | Fit Notes |
|---|---|
| `19_Function_Calling.md` | Excellent fit — mature, well-documented API |
| `18_Tool_Use_Prompting.md` | Strong plugin/GPTs ecosystem support |
| `31_Image_Generation_Prompts.md` | Native DALL-E integration within ChatGPT |
| `21_Code_Generation_Prompts.md` | Strong general-purpose code performance |
| `16_Agentic_Prompting.md` | Well-supported via Assistants API / tool orchestration |

## 5. Platform-Specific Caveats

- Message/context length limits vary by specific model and subscription tier; verify current limits for long-document tasks (Templates 20, 25, 34).
- Rate limits and usage tiers affect how many sequential calls are practical for Prompt Chaining (14) or Loop Prompting (15) workflows at scale — check current API tier limits before designing a high-call-volume workflow.
- Custom GPT behavior can differ subtly from raw API behavior with the same underlying model; test the actual deployment surface you'll be using, not just the API in isolation.

## 6. Quick Adaptation Checklist

When adapting any template for ChatGPT/OpenAI specifically:

- [ ] Confirm which specific model (GPT-4o, GPT-4.1, etc.) you're targeting, since capabilities vary
- [ ] For function calling, use OpenAI's JSON Schema `tools` format exactly
- [ ] For image generation, confirm whether you're using DALL-E within ChatGPT or a separate API call
- [ ] Check current context window limits for the specific model before long-document tasks
- [ ] For production/repeated use, consider a Custom GPT to persist template structure

## Related Documents

- `44_AI_Model_Compatibility.md` — cross-model comparison
- `19_Function_Calling.md` — the general template this guide adapts
- `31_Image_Generation_Prompts.md` — relevant for DALL-E-specific use

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
