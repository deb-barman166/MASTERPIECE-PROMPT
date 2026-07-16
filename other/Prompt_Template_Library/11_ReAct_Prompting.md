# ReAct Prompting (Reasoning + Acting)

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-11

---

## 01. Overview

ReAct prompting combines **reasoning** and **acting** into an interleaved loop: the model alternates between thinking through the problem (Thought), taking an action such as using a tool or looking up information (Action), and incorporating the result of that action (Observation) before continuing its reasoning. This cycle — Thought → Action → Observation — repeats until the model has enough information to produce a final answer.

This technique is foundational to how modern AI agents interact with external tools (search engines, calculators, databases, APIs), because it gives the model a structured way to decide *when* to act, *what* action to take, and *how* to incorporate the result before proceeding.

## 02. Purpose

- Enable models to solve problems requiring external information or tools, not just internal knowledge.
- Make tool-use decisions transparent and auditable (you can see exactly why each action was taken).
- Reduce hallucination by grounding reasoning in real retrieved information rather than assumed facts.
- Support multi-step tasks where later steps depend on the results of earlier actions.

## 03. Use Cases

- Research tasks requiring web search or document lookup
- Multi-step tasks involving calculators, code execution, or database queries
- Question-answering where facts need verification before answering
- Agent-style workflows where the model must decide between multiple available tools
- Tasks combining internal reasoning with external, real-time data

## 04. Target AI Models

Most relevant to models with tool-use/function-calling capability:

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later, with tools/plugins enabled)
- Claude (all Claude models, with tool use enabled)
- Gemini (with function calling)
- Grok (with tool access)
- Perplexity (natively search-integrated)

## 05. Prompt Category

`Agentic` · `Tool-Use` · `Iterative Loop`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **Task/question**: The problem requiring reasoning and possibly external actions
- **Available actions/tools**: A list of tools the model may use (search, calculator, code execution, etc.)

## 08. Optional Inputs

- Maximum number of Thought-Action-Observation cycles
- Format for the final answer
- Rules for when to stop and answer vs. continue acting

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_question}}` | Yes |
| `{{available_tools}}` | Yes |
| `{{max_cycles}}` | No |
| `{{final_answer_format}}` | No |
| `{{stopping_rule}}` | No |

## 10. Prompt Template

```text
You will solve the following task using an interleaved Thought, Action,
Observation loop. You have access to the tools listed below. Use them only
when needed.

TASK:
{{task_question}}

AVAILABLE TOOLS:
{{available_tools}}

INSTRUCTIONS:
Repeat the following cycle as many times as necessary (up to {{max_cycles}}):

Thought: Reason about what you currently know and what you still need to
find out or verify.
Action: If you need more information, specify which tool to use and with
what input. If you have enough information, write "Action: Finish".
Observation: [The result of the action will be provided to you]

{{stopping_rule}}

Once you have sufficient information, provide your final answer, clearly
separated from the reasoning trace, formatted as: {{final_answer_format}}
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_question}}` | The problem to solve | "What is the current population of the capital city of the country that won the most recent FIFA World Cup?" |
| `{{available_tools}}` | Tools the model can invoke | "web_search(query), calculator(expression)" |
| `{{max_cycles}}` | Cap on Thought-Action-Observation loops | "5" |
| `{{stopping_rule}}` | Guidance on when to stop acting and answer | "Stop as soon as you can answer confidently; do not use tools unnecessarily" |
| `{{final_answer_format}}` | Structure for the concluding answer | "One sentence, clearly labeled 'Final Answer:'" |

## 12. Example Input

```text
TASK:
What is the population of the capital city of the country that most recently
won the FIFA World Cup?

AVAILABLE TOOLS:
web_search(query)

INSTRUCTIONS:
Use Thought/Action/Observation cycles, up to 5. Stop once confident.
Final answer format: One sentence, labeled "Final Answer:"
```

## 13. Example Output

```text
Thought: I need to first identify which country most recently won the FIFA
World Cup, then find that country's capital city, then find that capital's
current population.

Action: web_search("most recent FIFA World Cup winner")
Observation: [Search result indicates the most recent winning country]

Thought: Now I know the winning country. I need to identify its capital city.

Action: web_search("capital city of [winning country]")
Observation: [Search result confirms the capital city]

Thought: Now I need the current population of that capital city.

Action: web_search("population of [capital city] [current year]")
Observation: [Search result provides population figure]

Thought: I now have all the information needed to answer confidently.

Action: Finish

Final Answer: The capital city of the most recent World Cup-winning country
has an estimated population as reported by the most recent search result.
```

*(Note: This example shows the ReAct structural pattern. In actual use, the
model would substitute real search results into the Observation steps and
name specific countries/cities/figures.)*

## 14. Customization Guide

- **List tools precisely**: Include exact function names/signatures if this will be used in an actual tool-calling system, not just descriptive names.
- **Set a reasonable max cycle count**: Too low risks cutting off a task that genuinely needs more steps; too high risks unnecessary tool calls. 3–7 cycles suits most tasks.
- **Define a clear stopping rule**: Explicitly discourage unnecessary tool use once enough information is available, to keep the process efficient.
- **Adjust for multi-tool scenarios**: When multiple tools are available, consider adding guidance on which tool suits which sub-problem type.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Always clearly label each Thought, Action, and Observation to keep the trace auditable.
- Instruct the model not to fabricate Observation content — it should only reflect real tool results, not assumed ones.
- Set an explicit stopping condition so the model doesn't over-use tools when it already has sufficient information.
- Keep the final answer clearly separated from the reasoning trace for easy extraction.

## 17. Common Mistakes

- Not providing a clear tool list/signature, leading to inconsistent or invalid action calls.
- Allowing unlimited cycles, which can result in inefficient or looping behavior.
- Failing to distinguish between the reasoning trace and the final answer in the output.
- Using ReAct for tasks that don't actually require external information — this adds unnecessary complexity over simple Chain-of-Thought.

## 18. Prompt Variations

- **Basic Version**: Single tool, unlimited cycles, minimal structure.
- **Advanced Version**: Multiple tools, capped cycles, explicit stopping rule (Section 10).
- **Expert Version**: Adds a self-consistency-style check where the model reflects on whether its gathered observations are sufficient and consistent before finalizing, and explicitly notes any remaining uncertainty in the final answer.

## 19. Related Prompts

- `04_Chain_of_Thought.md` — the reasoning foundation ReAct builds on, extended with external actions
- `14_Prompt_Chaining.md` — ReAct can be seen as a specific, tool-integrated form of prompt chaining
- `10_Self_Reflection.md` — can be added as a final check on whether gathered observations support the answer

## 20. Tips

- ReAct is the backbone of most "agentic" AI systems — understanding this pattern helps in designing more complex multi-tool workflows.
- Explicitly logging each Observation (even if verbose) makes debugging much easier when the final answer seems wrong — you can trace exactly which step introduced the error.

## 21. Limitations

- Requires actual tool/function-calling infrastructure to be genuinely useful — without real tools, the "Action" step is just simulated and provides no real informational benefit.
- More complex to set up and interpret than single-pass prompting techniques.
- Errors in early Observations (e.g., a bad search result) can propagate through the rest of the reasoning chain.
- Token-intensive, since it includes full reasoning traces alongside tool interactions.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ (with tools/plugins) |
| Claude | ✅ (with tool use enabled) |
| Gemini | ✅ (with function calling) |
| Grok | ✅ (with tool access) |
| Perplexity | ✅ (natively search-integrated) |
| Llama (open-source) | ⚠️ Requires tool-use fine-tuning or framework support |
| Mistral | ⚠️ Requires tool-use fine-tuning or framework support |

## 23. Tags

`#react-prompting` `#tool-use` `#agentic` `#reasoning-and-acting` `#advanced`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
