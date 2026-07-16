# Loop Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-15

---

## 01. Overview

Loop Prompting repeats a **cycle of generation and evaluation** against an explicit exit condition, continuing until that condition is met or a maximum iteration count is reached — rather than running a fixed, linear sequence of steps (as in Prompt Chaining) or a single pass. Each loop iteration typically involves generating or revising an output, checking it against a defined condition, and either exiting the loop (if the condition is satisfied) or feeding the result back in for another iteration.

This technique is well-suited to tasks where the "right" number of refinement passes isn't known in advance and instead depends on when a quality bar is actually met.

## 02. Purpose

- Continue refining an output dynamically until a specific, measurable condition is satisfied.
- Avoid both under-iterating (stopping too early) and over-iterating (wasting effort past the point of improvement).
- Handle tasks where the required number of passes varies case by case.
- Build a self-terminating refinement process rather than a fixed number of steps.

## 03. Use Cases

- Iterative writing refinement until a word count, tone, or quality bar is met
- Code generation with a test-run-fix loop until all tests pass
- Data cleaning that repeats until a validation check passes
- Negotiation or persuasion drafts refined until a target objection-handling coverage is achieved
- Any task where "keep improving until X is true" better describes the goal than "do these N fixed steps"

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity

## 05. Prompt Category

`Workflow` · `Iterative` · `Conditional Loop`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **Task/output goal**: What is being generated or refined
- **Exit condition**: The specific, checkable condition that ends the loop

## 08. Optional Inputs

- Maximum iteration count (safety limit)
- Evaluation method for checking the exit condition
- Instructions for what changes to make each iteration if the condition isn't yet met

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_goal}}` | Yes |
| `{{exit_condition}}` | Yes |
| `{{max_iterations}}` | No |
| `{{evaluation_method}}` | No |
| `{{revision_guidance}}` | No |

## 10. Prompt Template

```text
You will repeatedly generate and evaluate an output in a loop until a
specific exit condition is met, or until the maximum iteration count is
reached.

TASK / OUTPUT GOAL:
{{task_goal}}

EXIT CONDITION (loop stops when this is true):
{{exit_condition}}

MAXIMUM ITERATIONS (safety limit):
{{max_iterations}}

INSTRUCTIONS:
1. Generate an initial attempt at the output.
2. Evaluate the attempt using: {{evaluation_method}}
   Clearly state whether the exit condition is currently met (Yes/No).
3. If the exit condition is NOT met, revise the output using this guidance:
   {{revision_guidance}}
   Then return to Step 2.
4. If the exit condition IS met, or the maximum iteration count is reached,
   stop and present the final output, along with the number of iterations
   it took.

Label each iteration clearly (Iteration 1, Iteration 2, etc.).
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_goal}}` | What is being iteratively produced | "A persuasive email that anticipates and addresses likely objections" |
| `{{exit_condition}}` | The specific, checkable stopping criterion | "At least 3 distinct objections are explicitly addressed in the email" |
| `{{max_iterations}}` | Safety cap to prevent infinite looping | "4" |
| `{{evaluation_method}}` | How to check whether the condition is met | "Count the number of distinct objections explicitly addressed" |
| `{{revision_guidance}}` | What to change if the condition isn't yet satisfied | "Identify one likely objection not yet addressed, and add a sentence addressing it" |

## 12. Example Input

```text
TASK / OUTPUT GOAL:
Write a short email pitching a new subscription service to a potential
business client, anticipating likely objections.

EXIT CONDITION:
At least 3 distinct objections are explicitly and directly addressed.

MAXIMUM ITERATIONS: 4

INSTRUCTIONS:
Generate, evaluate objection count, revise if under 3, repeat. Stop at
condition met or 4 iterations.
```

## 13. Example Output

```text
ITERATION 1:
[Draft email addressing 1 objection: cost concerns]
Evaluation: 1 distinct objection addressed. Exit condition NOT met (need 3).
Revision guidance: Add handling for a second likely objection — e.g.,
implementation time or team adoption difficulty.

ITERATION 2:
[Revised email now addressing 2 objections: cost concerns, implementation time]
Evaluation: 2 distinct objections addressed. Exit condition NOT met (need 3).
Revision guidance: Add handling for a third likely objection — e.g.,
whether the service integrates with their existing tools.

ITERATION 3:
[Revised email now addressing 3 objections: cost concerns, implementation
time, tool integration]
Evaluation: 3 distinct objections addressed. Exit condition MET.

FINAL OUTPUT (after 3 iterations):
[Full final email text addressing all 3 objections, presented in full]

Loop completed in 3 of 4 maximum iterations.
```

## 14. Customization Guide

- **Make the exit condition genuinely checkable**: Vague conditions ("the email is persuasive enough") don't work well for looping; specific, countable/verifiable conditions ("addresses at least 3 objections", "passes all provided test cases") work far better.
- **Always set a maximum iteration safety limit**: Without one, a poorly defined exit condition could cause excessive, costly looping. 3–5 iterations is a reasonable default for most tasks.
- **Tie revision guidance to what's actually missing**: Rather than "make it better," instruct the model to identify specifically what's still lacking relative to the exit condition, and address just that gap each iteration.
- **Use for tasks with a measurable finish line**: Loop Prompting works best when "done" can be objectively defined, not just subjectively judged.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Define the exit condition as specifically and measurably as possible before starting the loop.
- Always include a maximum iteration cap as a safety net against infinite or excessive looping.
- Have the model explicitly state Yes/No on whether the condition is met at each iteration, not just describe progress vaguely.
- Focus each revision on the specific gap identified, rather than open-ended "improve this" instructions that could change unrelated aspects of the output.

## 17. Common Mistakes

- Defining an exit condition that's too subjective to reliably evaluate ("make it good enough").
- Omitting a maximum iteration limit, risking wasted cost on a loop that never cleanly resolves.
- Making sweeping, unfocused revisions each iteration instead of targeting the specific identified gap.
- Not clearly labeling each iteration, making it hard to track progress or debug where the loop went wrong.

## 18. Prompt Variations

- **Basic Version**: Single exit condition, no iteration cap, minimal evaluation detail.
- **Advanced Version**: Explicit exit condition, iteration cap, and targeted revision guidance (Section 10).
- **Expert Version**: Adds a secondary "diminishing returns" check — if two consecutive iterations show no meaningful improvement toward the exit condition, the loop exits early even if the condition itself isn't fully met, with a note explaining why.

## 19. Related Prompts

- `14_Prompt_Chaining.md` — a fixed, linear sequence of steps, versus Loop Prompting's repeated cycle until a condition is met
- `10_Self_Reflection.md` — a single critique-revise cycle; Loop Prompting extends this into a repeated, condition-driven cycle
- `09_Self_Consistency.md` — runs the same prompt multiple times for reliability, whereas Loop Prompting iterates and *changes* the output each time toward a goal

## 20. Tips

- Loop Prompting is especially useful in code-generation contexts: generate code, run tests, and loop until all tests pass or a max iteration count is hit.
- When possible, use an automated (not just model-judged) evaluation method for the exit condition — e.g., an actual word count, an actual test suite result — rather than relying solely on the model's own self-assessment of whether the condition is met.

## 21. Limitations

- Requires a genuinely measurable exit condition to work well; vague conditions undermine the entire technique.
- Can be costly in tokens/time if the exit condition is hard to satisfy or poorly calibrated.
- Without careful revision guidance, iterations can churn without making real progress toward the exit condition.
- The model's own self-evaluation of whether the condition is met isn't infallible — pairing with an external, automated check (where possible) improves reliability significantly.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#loop-prompting` `#iterative-refinement` `#conditional-loop` `#advanced` `#self-terminating`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
