# Agentic Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-16

---

## 01. Overview

Agentic prompting configures a model to operate as an **autonomous agent**: given a goal rather than a single instruction, it plans a sequence of steps, decides which actions to take (including tool use), monitors its own progress, and continues working — often across multiple internal iterations — until the goal is achieved or a stopping condition is reached. Unlike a single-turn prompt that produces one output, an agentic prompt establishes an operating loop: plan → act → observe → adjust → repeat, with the model largely self-directing between the start and the final result.

This is the conceptual umbrella above several other techniques in this library. ReAct (Template 11) supplies the act/observe mechanics; Loop Prompting (Template 15) supplies the repeat-until-condition logic; Prompt Chaining (Template 14) supplies staged handoffs. Agentic prompting is what you reach for when the task is a *goal*, not a fixed procedure.

## 02. Purpose

- Let the model handle open-ended goals where the exact steps aren't known in advance.
- Reduce the need for a human to manually orchestrate each step.
- Allow the model to adapt its plan mid-task based on what it discovers along the way.
- Provide a consistent structure (goal, constraints, tools, autonomy level) for building repeatable agent behaviors.

## 03. Use Cases

- Open-ended research tasks ("find out X and compile findings")
- Multi-step task completion where the path depends on intermediate results
- Autonomous coding tasks (plan a feature, implement it, test it, fix issues)
- Long-running assistants that manage a goal across many turns
- Workflow automation where the agent must decide, not just execute, each next step

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later, with tools enabled)
- Claude (all Claude models, especially with tool use / computer use enabled)
- Gemini (with function calling / agent frameworks)
- Grok (with tool access)
- Perplexity (for research-agent style tasks)

## 05. Prompt Category

`Agentic` · `Autonomous` · `Goal-Directed`

## 06. Difficulty Level

**Expert**

## 07. Required Inputs

- **Goal statement**: The outcome to achieve, not a fixed procedure
- **Autonomy boundaries**: What the agent may decide on its own vs. what requires check-in

## 08. Optional Inputs

- Available tools
- Maximum steps/budget
- Definition of "done"
- Escalation rule for when the agent gets stuck

## 09. Variables

| Variable | Required? |
|---|---|
| `{{goal_statement}}` | Yes |
| `{{autonomy_boundaries}}` | Yes |
| `{{available_tools}}` | No |
| `{{max_steps}}` | No |
| `{{definition_of_done}}` | No |
| `{{escalation_rule}}` | No |

## 10. Prompt Template

```text
You are operating as an autonomous agent working toward a goal, not
following a fixed script. Plan your own steps, take actions as needed, and
adapt based on what you learn.

GOAL:
{{goal_statement}}

TOOLS AVAILABLE:
{{available_tools}}

AUTONOMY BOUNDARIES:
{{autonomy_boundaries}}

DEFINITION OF DONE:
{{definition_of_done}}

MAXIMUM STEPS: {{max_steps}}

INSTRUCTIONS:
1. Before acting, state a brief plan: the sequence of steps you currently
   believe will achieve the goal.
2. Execute the plan step by step. After each step, briefly note what you
   learned and whether it changes your remaining plan.
3. If you encounter a decision outside your autonomy boundaries: {{escalation_rule}}
4. Stop when the definition of done is met, or when you reach the maximum
   step count — whichever comes first.
5. Conclude with a summary of what was done and the final result.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{goal_statement}}` | The outcome to achieve | "Identify the top 3 competitors for our product and summarize their pricing models" |
| `{{available_tools}}` | Tools the agent can call | "web_search, web_fetch, calculator" |
| `{{autonomy_boundaries}}` | What the agent may decide alone vs. must check in on | "May choose which sources to consult; must ask before finalizing pricing figures used in a public document" |
| `{{definition_of_done}}` | The concrete condition marking completion | "3 named competitors, each with a summarized pricing tier structure" |
| `{{max_steps}}` | Safety cap on total actions | "10" |
| `{{escalation_rule}}` | What to do when stuck or outside bounds | "State the blocker clearly and ask the user for guidance rather than guessing" |

## 12. Example Input

```text
GOAL:
Find three well-reviewed project management tools suitable for a 5-person
startup team and summarize their strengths and pricing.

TOOLS AVAILABLE: web_search, web_fetch

AUTONOMY BOUNDARIES:
May choose which tools to research and which sources to trust. Must not
recommend a paid tool without stating its price clearly.

DEFINITION OF DONE:
3 tools identified, each with strengths and current pricing summarized.

MAXIMUM STEPS: 8
```

## 13. Example Output

```text
PLAN:
1. Search for well-reviewed project management tools for small teams
2. Shortlist 3 candidates based on review consensus
3. Look up pricing for each
4. Summarize strengths and pricing per tool

STEP 1: [search executed]
Learned: Several tools consistently recommended for small teams; narrowing
to those with strong small-team reviews specifically, not enterprise focus.

STEP 2: Shortlisted 3 tools based on small-team fit and review consistency.

STEP 3: [pricing looked up for each of the 3]
Learned: Pricing tiers vary by per-seat vs. flat-rate models; noting this
distinction for the summary.

STEP 4: Compiled strengths and pricing for each.

DEFINITION OF DONE MET: 3 tools identified with strengths and pricing.

SUMMARY:
[Tool A] — strongest for visual task boards, per-seat pricing starting at $X/user/month.
[Tool B] — strongest for small-team simplicity, flat-rate pricing at $X/month.
[Tool C] — strongest for integrations, per-seat pricing starting at $X/user/month.
Completed in 4 of 8 maximum steps.
```

## 14. Customization Guide

- **Set autonomy boundaries precisely**: Vague boundaries ("use good judgment") lead to inconsistent escalation behavior. Name the specific decision types that require check-in.
- **Always define "done" concretely**: An agent without a clear completion condition will either stop too early or keep working past the point of usefulness.
- **Size the step budget to task complexity**: Simple goals may need 3–5 steps; complex research or build tasks may need 15–20.
- **Add the escalation rule explicitly**: Without one, an agent facing ambiguity may guess rather than pause — naming the rule up front prevents silent wrong turns.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Require an upfront plan before any action — this catches flawed strategies before they're executed.
- Keep autonomy boundaries specific and example-driven, not abstract principles.
- Log each step's outcome, not just the final result, so the process is auditable.
- Always include a step budget as a safety mechanism against runaway loops.

## 17. Common Mistakes

- Leaving autonomy boundaries vague, causing either excessive check-ins or risky unsupervised decisions.
- No definition of done, leading to premature stopping or unnecessary over-working.
- Treating agentic prompting as necessary for simple tasks that a single direct prompt would handle fine.
- Failing to set a maximum step count, risking inefficient or looping behavior.

## 18. Prompt Variations

- **Basic Version**: Goal + tools only, no explicit autonomy boundaries or step cap.
- **Advanced Version**: Full structure with autonomy boundaries, definition of done, and step cap (Section 10).
- **Expert Version**: Adds a mid-task checkpoint where the agent must summarize progress and explicitly re-confirm its plan is still valid, useful for long-running or high-stakes agentic tasks.

## 19. Related Prompts

- `11_ReAct_Prompting.md` — supplies the act/observe mechanics used within each agentic step
- `15_Loop_Prompting.md` — supplies the repeat-until-condition logic
- `17_Multi_Agent_Prompting.md` — extends agentic prompting to multiple coordinating agents
- `14_Prompt_Chaining.md` — a more fixed, less autonomous alternative for well-understood procedures

## 20. Tips

- Agentic prompting is for goals, not procedures — if you already know the exact steps, Prompt Chaining (Template 14) is simpler and more predictable.
- Reviewing the agent's stated plan before it starts acting is the single highest-leverage checkpoint — most costly failures trace back to a flawed initial plan, not a flawed individual step.

## 21. Limitations

- Higher variance than fixed-procedure prompting — the same goal can be pursued via different, not always equally good, plans.
- Requires real tool infrastructure to be genuinely autonomous; without tools, "actions" are simulated and limited to what the model already knows.
- Harder to predict cost/time in advance compared to a fixed-step chain.
- Autonomy boundaries and escalation rules must be well-designed, or the agent may make consequential decisions without appropriate oversight.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ (with tools/agent frameworks) |
| Claude | ✅ (with tool use / computer use) |
| Gemini | ✅ (with function calling) |
| Grok | ✅ (with tool access) |
| Perplexity | ⚠️ Partial (best for research-style agentic tasks) |
| Llama (open-source) | ⚠️ Requires agent framework support |
| Mistral | ⚠️ Requires agent framework support |

## 23. Tags

`#agentic-prompting` `#autonomous-agents` `#goal-directed` `#expert-level` `#tool-use`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
