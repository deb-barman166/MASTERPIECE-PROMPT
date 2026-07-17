# Claude (Anthropic) Prompting Guide

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-46 · Platform Guide

---

## Overview

This document covers platform-specific considerations for using this library's templates with Anthropic's Claude models. It's a companion to the general templates, not a replacement — apply the relevant template first, then adjust using the notes here for Claude-specific conventions.

**Note:** Anthropic updates model capabilities frequently. Verify specifics against Anthropic's current documentation for anything decision-critical, particularly around tool use schemas and context limits.

---

## 1. Platform-Specific Strengths

- Strong long-context handling, making it well-suited to RAG (Template 20), long-document Summarization (34), and extensive Data Analysis (25) tasks.
- Careful, methodical reasoning performance, benefiting Chain-of-Thought (04), Step-Back (07), and Self-Reflection (10) style prompting.
- Native tool use and computer use capability, supporting Agentic (16), ReAct (11), and Tool Use (18) workflows directly.
- Noted strength in long-form creative writing (39) and nuanced, natural-sounding prose.
- XML tag structuring is natively well-understood, useful for clearly delimiting sections within complex prompts (e.g., separating instructions from context in Template 20's RAG structure).

## 2. Tool Use Schema Notes (relevant to Template 19)

Claude's tool use API defines tools with an `input_schema` field using JSON Schema. When adapting Template 19's generic schema format:

```json
{
  "name": "create_event",
  "description": "Creates a calendar event",
  "input_schema": {
    "type": "object",
    "properties": {
      "title": { "type": "string" },
      "start_time": { "type": "string" },
      "duration_minutes": { "type": "integer" }
    },
    "required": ["title", "start_time", "duration_minutes"]
  }
}
```

This maps onto Template 19's `{{function_schemas}}` variable for Claude-specific implementations.

## 3. XML Structuring for Complex Prompts

Claude tends to parse clearly-delimited XML-style tags effectively. For templates with many distinct sections (RAG's context vs. question in Template 20, or multi-role setups in Multi-Agent Prompting Template 17), wrapping sections in descriptive tags can improve reliability:

```
<context>
[retrieved documents here]
</context>

<question>
[user question here]
</question>
```

This is a useful pattern to layer onto any template where the generic `{{variable}}` placeholders benefit from clearer structural delimitation.

## 4. Recommended Templates for This Platform

| Template | Fit Notes |
|---|---|
| `20_RAG_Prompting.md` | Strong long-context handling for large retrieved documents |
| `10_Self_Reflection.md` | Careful reasoning style well-suited to self-critique |
| `39_Creative_Writing_Prompts.md` | Noted strength in nuanced prose |
| `25_Data_Analysis_Prompts.md` | Strong when paired with code execution capability |
| `34_Summarization_Prompts.md` | Long-context strength benefits large-document summarization |
| `16_Agentic_Prompting.md` | Native tool use / computer use support |

## 5. Platform-Specific Caveats

- Context window size varies by specific model version; verify current limits for long-document tasks before assuming a document will fit in a single prompt.
- Tool use requires explicit tool definitions passed via the API; the conversational interface (claude.ai) handles some tools natively while custom tool integration requires API-level configuration.
- Computer use / agentic capabilities may require specific model versions and API access tiers — confirm availability for your specific use case.

## 6. Quick Adaptation Checklist

When adapting any template for Claude specifically:

- [ ] Confirm which specific Claude model you're targeting, since capabilities and context limits vary
- [ ] For tool use, use Claude's `input_schema` format exactly
- [ ] Consider XML-tag structuring for prompts with many distinct sections
- [ ] Check current context window limits before long-document RAG/Summarization tasks
- [ ] For agentic/computer use workflows, confirm API access tier supports the needed capability

## Related Documents

- `44_AI_Model_Compatibility.md` — cross-model comparison
- `20_RAG_Prompting.md` — particularly well-suited to Claude's long-context strength
- `19_Function_Calling.md` — the general template this guide adapts for Claude's tool use API

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
