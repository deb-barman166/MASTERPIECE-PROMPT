# Chain-of-Thought Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-04

---

## 01. Overview

Chain-of-Thought (CoT) prompting instructs the model to reason through a problem **step by step**, making its intermediate thinking explicit before arriving at a final answer — rather than jumping straight to a conclusion. This technique dramatically improves accuracy on tasks that require logic, arithmetic, multi-step planning, or nuanced judgment, because it forces the model to build the answer incrementally instead of pattern-matching to a plausible-sounding response.

CoT can be triggered simply (e.g., "think step by step") or paired with few-shot examples that themselves demonstrate step-by-step reasoning ("few-shot CoT").

## 02. Purpose

- Improve accuracy on multi-step reasoning, math, and logic problems.
- Make the model's reasoning process visible and auditable.
- Reduce shortcut errors caused by the model jumping to conclusions.
- Provide a debugging trail — if the final answer is wrong, the reasoning steps reveal where it went wrong.

## 03. Use Cases

- Mathematical or logical word problems
- Multi-step planning or decision-making
- Root-cause or diagnostic analysis
- Complex comparisons involving multiple criteria
- Any task where the *path* to the answer matters as much as the answer itself
- Debugging why a model previously gave an incorrect answer

## 04. Target AI Models

Most effective on larger, more capable models:

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later — highly effective)
- Claude (all Claude models — highly effective, especially with extended reasoning)
- Gemini (effective, especially Pro-tier models)
- Grok
- Perplexity
- Smaller open-source models may show reduced benefit compared to frontier models

## 05. Prompt Category

`Reasoning` · `Multi-Step` · `Analytical`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Problem/question**: The task requiring reasoning
- **Reasoning instruction**: Explicit direction to think step by step

## 08. Optional Inputs

- Number of reasoning steps expected
- Format for final answer (separate from reasoning)
- Example of step-by-step reasoning (for few-shot CoT)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{problem_statement}}` | Yes |
| `{{reasoning_trigger}}` | Yes |
| `{{step_count_hint}}` | No |
| `{{final_answer_format}}` | No |
| `{{worked_example}}` | No |

## 10. Prompt Template

```text
Solve the following problem. Think through it step by step, showing your
reasoning before giving a final answer. Do not skip steps.

PROBLEM:
{{problem_statement}}

INSTRUCTIONS:
{{reasoning_trigger}}
Break your reasoning into clear, numbered steps{{step_count_hint}}.
After completing your reasoning, clearly state your final answer separately,
formatted as: {{final_answer_format}}

{{worked_example}}

Begin your step-by-step reasoning now.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{problem_statement}}` | The question or problem to solve | "A store offers 20% off, then an additional 10% off the discounted price. What is the total percentage discount?" |
| `{{reasoning_trigger}}` | The instruction that activates step-by-step thinking | "Let's think through this step by step." |
| `{{step_count_hint}}` | Optional guidance on reasoning depth | "(aim for 3–5 steps)" |
| `{{final_answer_format}}` | How the final answer should be presented | "A single percentage, labeled 'Final Answer:'" |
| `{{worked_example}}` | Optional demonstration of step-by-step reasoning (few-shot CoT) | A fully solved similar problem |

## 12. Example Input

```text
PROBLEM:
A train travels 60 miles in 1.5 hours, then travels another 90 miles in 2 hours.
What is the train's average speed for the entire trip?

INSTRUCTIONS:
Let's think through this step by step.
Break your reasoning into clear, numbered steps (aim for 3-5 steps).
After completing your reasoning, clearly state your final answer separately,
formatted as: "Final Answer: [X] mph"
```

## 13. Example Output

```text
Step 1: Calculate total distance traveled.
60 miles + 90 miles = 150 miles

Step 2: Calculate total time traveled.
1.5 hours + 2 hours = 3.5 hours

Step 3: Calculate average speed using total distance ÷ total time.
150 miles ÷ 3.5 hours = 42.857... mph

Step 4: Round to a reasonable precision.
Approximately 42.86 mph

Final Answer: 42.86 mph
```

## 14. Customization Guide

- **Adjust step granularity**: For simple problems, 3 steps may suffice; for complex multi-variable problems, allow 6–10 steps.
- **Separate reasoning from final answer clearly**: Always request a distinctly labeled final answer so downstream systems can parse it programmatically if needed.
- **Add a worked example for harder tasks**: Pairing CoT with one fully-solved example (few-shot CoT) significantly boosts accuracy on complex or unusual problem types.
- **Combine with self-consistency**: For high-stakes accuracy, run the same CoT prompt multiple times and take the majority answer (see Template 09).

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Always explicitly request numbered or clearly delineated steps — unstructured reasoning is harder to verify.
- Ask for the final answer to be clearly separated and labeled, not buried in the reasoning.
- For quantitative problems, ask the model to double-check its arithmetic in a final step.
- Use CoT selectively — for simple factual queries, it adds unnecessary length without improving accuracy.

## 17. Common Mistakes

- Using CoT for trivial tasks where it only adds verbosity without improving correctness.
- Not requesting a separately labeled final answer, making outputs hard to parse.
- Assuming visible reasoning steps guarantee correctness — the model can still make a plausible-sounding but incorrect step.
- Overly long or unconstrained reasoning chains that drift off-topic without a step limit.

## 18. Prompt Variations

- **Basic Version**: Simple "think step by step" trigger with no example (zero-shot CoT).
- **Advanced Version**: Numbered step requirement with separated final answer (Section 10).
- **Expert Version**: Few-shot CoT — includes one or two fully worked example problems with visible reasoning before presenting the real problem, plus a request to double-check the final answer against the original question.

## 19. Related Prompts

- `03_Few_Shot_Prompting.md` — combine for "few-shot CoT"
- `05_Tree_of_Thought.md` — extends CoT into exploring multiple reasoning paths
- `09_Self_Consistency.md` — runs CoT multiple times for higher reliability
- `10_Self_Reflection.md` — adds a self-critique step after the initial CoT answer

## 20. Tips

- The phrase "let's think step by step" alone (zero-shot CoT) can meaningfully improve accuracy even without any examples.
- For math and logic tasks, explicitly asking the model to verify its final answer against the original question catches many errors before they reach the user.

## 21. Limitations

- Increases response length and token cost compared to direct-answer prompting.
- Does not guarantee correctness — a flawed step early in the chain can propagate to a confidently wrong final answer.
- Less beneficial (and sometimes unnecessary) for simple factual or lookup-style questions.
- Effectiveness varies by model; smaller or less capable models may not reason as reliably even when instructed to.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ |
| Llama (open-source) | ✅ (varies by model size) |
| Mistral | ✅ (varies by model size) |
| Command R+ | ✅ |

## 23. Tags

`#chain-of-thought` `#reasoning` `#step-by-step` `#logic` `#math` `#intermediate`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
