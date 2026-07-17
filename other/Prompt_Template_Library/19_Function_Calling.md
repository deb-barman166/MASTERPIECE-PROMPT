# Function Calling

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-19

---

## 01. Overview

Function Calling prompting structures a request so the model produces a **precisely-typed, schema-conformant function/API call** — the exact function name and correctly-typed arguments — rather than natural language. This is the mechanism that lets a model reliably interface with external code: instead of describing what it wants to happen in prose, the model outputs a structured call (typically JSON) that a program can directly parse and execute.

Where Tool Use prompting (Template 18) governs *when and why* to call a tool, Function Calling focuses specifically on producing a *correctly formatted* call: matching parameter names, types, required vs. optional fields, and valid enum values exactly as defined in a schema.

## 02. Purpose

- Produce machine-parseable, schema-valid output instead of free-form text.
- Enable reliable integration between a model and external code/APIs.
- Reduce errors from malformed parameters, wrong types, or missing required fields.
- Support systems where the function call itself (not a text answer) is the deliverable.

## 03. Use Cases

- Integrating a model with an existing API (weather, calendar, payment, CRM, etc.)
- Structured data extraction into a defined schema
- Multi-function systems where the model must choose the correct function among several
- Any pipeline where downstream code expects a specific JSON structure, not prose

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later — native function calling support)
- Claude (all Claude models — native tool use with defined input schemas)
- Gemini (native function calling support)
- Grok (function calling support)
- Perplexity (limited; less common for this use case)

## 05. Prompt Category

`Functional` · `Structured Output` · `Schema-Based`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **User request**: The natural-language task to translate into a function call
- **Function schema(s)**: Name, description, parameters (with types and required/optional status) for each available function

## 08. Optional Inputs

- Multiple function schemas (for selection among several)
- Default values for optional parameters
- Validation rules beyond basic typing

## 09. Variables

| Variable | Required? |
|---|---|
| `{{user_request}}` | Yes |
| `{{function_schemas}}` | Yes |
| `{{default_values}}` | No |
| `{{validation_rules}}` | No |

## 10. Prompt Template

```text
Given the user request below, determine which function (if any) should be
called, and produce a valid function call matching the schema exactly.

USER REQUEST:
{{user_request}}

AVAILABLE FUNCTIONS (schema):
{{function_schemas}}

DEFAULT VALUES FOR OPTIONAL PARAMETERS (if not specified by the user):
{{default_values}}

ADDITIONAL VALIDATION RULES:
{{validation_rules}}

INSTRUCTIONS:
1. Identify which function best matches the user's request. If no function
   applies, state this clearly instead of forcing an unrelated call.
2. Extract parameter values from the user request. Use defaults only for
   optional parameters the user did not specify.
3. Ensure all required parameters are present and correctly typed before
   producing the call. If a required parameter is missing and has no
   default, ask the user for it instead of guessing.
4. Output only the function call in valid JSON, matching the schema exactly
   — no additional commentary unless a required parameter is missing.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{user_request}}` | The natural-language ask to convert into a call | "Book a meeting with Sarah next Tuesday at 2pm for 30 minutes" |
| `{{function_schemas}}` | Full schema definitions for available functions | `create_event(title: string, start_time: string [required], duration_minutes: integer [required], attendees: array [optional])` |
| `{{default_values}}` | Fallback values for unspecified optional parameters | "duration_minutes defaults to 30 if not stated" |
| `{{validation_rules}}` | Extra constraints beyond basic typing | "start_time must be in the future; reject past dates" |

## 12. Example Input

```text
USER REQUEST:
Schedule a call with the design team this Thursday at 10am for an hour.

AVAILABLE FUNCTIONS:
create_event(
  title: string [required],
  start_time: string (ISO 8601) [required],
  duration_minutes: integer [required],
  attendees: array of strings [optional]
)

DEFAULT VALUES: None specified beyond schema

VALIDATION RULES: start_time must be a future date/time.
```

## 13. Example Output

```json
{
  "function": "create_event",
  "arguments": {
    "title": "Call with Design Team",
    "start_time": "2026-07-23T10:00:00",
    "duration_minutes": 60,
    "attendees": ["design-team"]
  }
}
```

*(Note: the exact date resolved for "this Thursday" depends on the current
date at the time of the request; the model should resolve relative dates
using known current-date context.)*

## 14. Customization Guide

- **Write complete, unambiguous schemas**: Every parameter should specify its type, whether it's required, and any valid value constraints (e.g., enums, ranges) — incomplete schemas are the top cause of malformed calls.
- **Provide defaults for genuinely optional fields**: This reduces unnecessary clarifying questions for parameters that have a sensible default.
- **Add validation rules for business logic the type system can't express**: e.g., "end_time must be after start_time" isn't a type constraint but matters greatly for correctness.
- **Handle the multi-function case explicitly**: When several functions are available, state how the model should decide between them (see also `18_Tool_Use_Prompting.md`).

## 15. Output Format Options

- JSON (primary/native format for function calls)
- XML
- YAML
- Markdown (for documentation/preview purposes only, not execution)

## 16. Best Practices

- Always require the model to check for missing required parameters before producing a call, and to ask rather than guess when one is missing.
- Keep the function call output free of extra commentary or explanation unless something needs clarification — mixed prose and JSON is harder to parse reliably.
- Test schemas against ambiguous or incomplete user requests to confirm the model asks for clarification rather than fabricating values.
- Version your schemas; if a function's parameters change, old calls generated against the previous schema may no longer validate.

## 17. Common Mistakes

- Incomplete schemas that omit type or required/optional status, leading to inconsistent call formatting.
- Allowing the model to guess a missing required value rather than asking for it.
- Mixing natural-language explanation into the same output as the JSON call, complicating downstream parsing.
- Not specifying defaults, causing the model to either omit optional parameters inconsistently or invent arbitrary values for them.

## 18. Prompt Variations

- **Basic Version**: Single function schema, no defaults or extra validation rules.
- **Advanced Version**: Full schema with defaults and validation rules, single function (Section 10).
- **Expert Version**: Multiple function schemas with explicit selection logic, requiring the model to first state which function it selected and why, before producing the call — useful for auditing systems with many overlapping functions.

## 19. Related Prompts

- `18_Tool_Use_Prompting.md` — the broader decision layer (when/why to call) that Function Calling's precise schema-matching supports
- `11_ReAct_Prompting.md` — often incorporates function calls as the "Action" step in its reasoning loop
- `20_RAG_Prompting.md` — retrieval functions are a common specific case of function calling

## 20. Tips

- When designing a new function schema, writing 2-3 example user requests and their expected calls (effectively a few-shot set) before deploying is one of the fastest ways to catch schema ambiguity early.
- For parameters with a constrained set of valid values (enums), listing them explicitly in the schema dramatically reduces invalid-value errors compared to describing the constraint only in prose.

## 21. Limitations

- Entirely dependent on schema quality — an ambiguous or incomplete schema will produce unreliable calls regardless of prompt quality.
- Some models handle complex nested parameter structures less reliably than flat ones; deeply nested schemas may need additional examples to ensure correct formatting.
- Doesn't replace actual runtime validation on the receiving end — schema-conformant output from the model should still be validated before execution in production systems.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ (native function calling) |
| Claude | ✅ (native tool use with input schemas) |
| Gemini | ✅ (native function calling) |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ⚠️ Varies by fine-tuning/framework |
| Mistral | ⚠️ Varies by fine-tuning/framework |

## 23. Tags

`#function-calling` `#structured-output` `#json-schema` `#api-integration` `#advanced`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
