# Tool Use Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-18

---

## 01. Overview

Tool Use prompting instructs a model on **when and how to invoke external tools** — calculators, search engines, code interpreters, databases, or any callable capability outside the model's own generation — as part of producing its response. Unlike ReAct (Template 11), which focuses on the interleaved reasoning loop *around* tool calls, Tool Use prompting focuses specifically on how tools are described, selected, and invoked correctly: giving the model clear tool definitions, usage rules, and guidance on choosing between multiple available tools.

This template is the foundation beneath most agentic and ReAct-style workflows — those techniques assume tools are already well-described and correctly selected; this one ensures that assumption holds.

## 02. Purpose

- Ensure the model correctly understands what each available tool does and when to use it.
- Reduce incorrect, unnecessary, or missed tool invocations.
- Provide clear rules for choosing between multiple similar tools.
- Establish safe usage boundaries (e.g., confirm before an irreversible action).

## 03. Use Cases

- Any workflow where the model has access to search, calculation, code execution, or API tools
- Systems with multiple overlapping tools where selection logic matters
- Tasks requiring precise, verified information rather than the model's internal recall
- Workflows where some tool actions are reversible (safe to try) and others aren't (require confirmation)

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later, with function calling/plugins)
- Claude (all Claude models, with tool use enabled)
- Gemini (with function calling)
- Grok (with tool access)
- Perplexity (natively search-integrated)

## 05. Prompt Category

`Agentic` · `Tool-Use` · `Functional`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **Task**: What needs to be accomplished
- **Tool definitions**: Name, purpose, and input/output format for each available tool

## 08. Optional Inputs

- Tool selection priority rules
- Actions requiring confirmation before execution
- Error-handling instructions if a tool call fails

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_description}}` | Yes |
| `{{tool_definitions}}` | Yes |
| `{{selection_rules}}` | No |
| `{{confirmation_required_actions}}` | No |
| `{{error_handling}}` | No |

## 10. Prompt Template

```text
You have access to the following tools to help complete this task. Use them
only when they add real value; do not call a tool if you already have
sufficient information to answer confidently.

TASK:
{{task_description}}

AVAILABLE TOOLS:
{{tool_definitions}}

TOOL SELECTION RULES:
{{selection_rules}}

ACTIONS REQUIRING CONFIRMATION BEFORE EXECUTION:
{{confirmation_required_actions}}

IF A TOOL CALL FAILS OR RETURNS UNEXPECTED RESULTS:
{{error_handling}}

INSTRUCTIONS:
1. Determine whether a tool call is needed at all.
2. If needed, select the most appropriate tool per the rules above.
3. State clearly which tool you are calling and why, before calling it.
4. Incorporate the tool's result into your reasoning before proceeding.
5. Provide your final answer once you have sufficient verified information.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_description}}` | The task the tools support | "Determine the current exchange rate and convert a given amount" |
| `{{tool_definitions}}` | Available tools with input/output specs | "currency_lookup(from, to) → rate; calculator(expression) → result" |
| `{{selection_rules}}` | Guidance for choosing between tools | "Use currency_lookup for the rate first, then calculator for the conversion math" |
| `{{confirmation_required_actions}}` | Actions needing explicit user approval first | "Any action that sends money or modifies an account" |
| `{{error_handling}}` | What to do if a tool fails | "Retry once; if it fails again, tell the user rather than guessing a value" |

## 12. Example Input

```text
TASK:
Convert 500 USD to EUR at today's rate and confirm the result.

AVAILABLE TOOLS:
currency_lookup(from_currency, to_currency) → exchange_rate
calculator(expression) → numeric_result

SELECTION RULES:
Always look up the current rate before calculating; never assume a
remembered rate is current.

CONFIRMATION REQUIRED: None (informational task only)

ERROR HANDLING:
If currency_lookup fails, state that a current rate could not be retrieved
rather than estimating one.
```

## 13. Example Output

```text
Determining whether a tool call is needed: Yes — exchange rates change
daily, so I need the current rate rather than relying on memory.

Calling currency_lookup(USD, EUR) to get today's rate.
[Tool result: rate returned]

Calling calculator(500 * rate) to compute the converted amount.
[Tool result: converted amount returned]

FINAL ANSWER:
500 USD converts to approximately [result] EUR at today's retrieved
exchange rate.
```

## 14. Customization Guide

- **Write precise tool definitions**: Include exact input parameters and output format — vague tool descriptions lead to malformed or incorrect calls.
- **Set explicit selection rules when tools overlap**: If two tools could plausibly handle the same request, state a clear priority or condition for choosing between them.
- **Name confirmation-required actions explicitly**: Any irreversible or consequential action (sending, deleting, purchasing) should require a stated confirmation step, not be left to the model's judgment alone.
- **Plan for failure**: Always specify what happens if a tool call fails or returns unexpected data — silent guessing is far riskier than a clear failure message.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- State the reason for each tool call before making it, not just the call itself — this keeps the process auditable.
- Avoid unnecessary tool calls when the model already has sufficient reliable information.
- Always define what "sufficient" evidence looks like, so the model doesn't call tools indefinitely.
- Separate the tool-use reasoning trace from the final answer clearly.

## 17. Common Mistakes

- Vague tool definitions that lead to malformed calls or wrong parameter usage.
- No selection rule when multiple tools could apply, causing inconsistent tool choice across runs.
- Missing error-handling guidance, resulting in the model guessing a plausible-but-fabricated result when a tool fails.
- Treating every task as requiring a tool call, even when internal knowledge is already sufficient and reliable.

## 18. Prompt Variations

- **Basic Version**: Simple tool list with minimal selection guidance.
- **Advanced Version**: Full structure with selection rules, confirmation requirements, and error handling (Section 10).
- **Expert Version**: Adds a cost/latency awareness rule — e.g., "prefer the cheaper or faster tool when either would produce an equally reliable result" — for production systems where tool calls have real resource costs.

## 19. Related Prompts

- `11_ReAct_Prompting.md` — the reasoning loop that typically wraps around tool calls defined here
- `16_Agentic_Prompting.md` — uses tool use as one component of broader autonomous goal pursuit
- `19_Function_Calling.md` — a more technical, schema-precise variant specifically for structured API/function calls

## 20. Tips

- The clarity of tool definitions is usually the single biggest lever for reliable tool use — investing time in precise input/output specs pays off more than elaborate selection logic.
- For systems with many tools, grouping them by category (informational, transactional, computational) and stating category-level rules is often more manageable than per-tool rules.

## 21. Limitations

- Entirely dependent on real tool infrastructure being available and correctly connected — this template only governs decision-making, not the underlying tool implementation.
- Model tool selection isn't infallible; ambiguous cases may still result in a suboptimal tool choice even with clear rules.
- Adds overhead compared to direct-answer prompting; only worth it when real, verifiable, or current information is genuinely required.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ (with function calling/plugins) |
| Claude | ✅ (with tool use enabled) |
| Gemini | ✅ (with function calling) |
| Grok | ✅ (with tool access) |
| Perplexity | ✅ (natively search-integrated) |
| Llama (open-source) | ⚠️ Requires tool-use fine-tuning or framework support |
| Mistral | ⚠️ Requires tool-use fine-tuning or framework support |

## 23. Tags

`#tool-use` `#function-calling` `#agentic` `#advanced` `#tool-selection`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
