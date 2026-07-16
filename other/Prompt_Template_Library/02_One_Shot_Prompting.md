# One-Shot Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-02

---

## 01. Overview

One-shot prompting provides the model with **exactly one worked example** of an input/output pair before asking it to perform the same task on new content. That single example acts as a calibration point — showing the model not just what to do, but precisely how the output should look, in terms of format, tone, structure, and level of detail.

It sits between zero-shot (no examples) and few-shot (multiple examples), offering a lightweight way to steer output style without the token overhead of several examples.

## 02. Purpose

- Demonstrate the exact output format expected, rather than describing it in words.
- Reduce ambiguity for tasks where the "right" structure is hard to explain but easy to show.
- Calibrate tone, length, and style with minimal added prompt length.
- Improve consistency over zero-shot for moderately nuanced tasks.

## 03. Use Cases

- Formatting tasks where a written description of the format is clumsier than showing it
- Style transfer (e.g., "write like this example")
- Data extraction into a specific structure
- Classification where one labeled example clarifies the category boundaries
- Tasks with a specific idiom, tone, or structure that's easier demonstrated than described

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity
- Open-source instruction-tuned models (Llama, Mistral, Qwen, etc.)

## 05. Prompt Category

`Foundational` · `Example-Based` · `Single-Turn`

## 06. Difficulty Level

**Beginner**

## 07. Required Inputs

- **Task description**: What the model should do
- **One example**: A complete, correct input → output pair
- **New input**: The actual content to apply the task to

## 08. Optional Inputs

- Output format
- Tone/style notes
- Constraints

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_instruction}}` | Yes |
| `{{example_input}}` | Yes |
| `{{example_output}}` | Yes |
| `{{new_input}}` | Yes |
| `{{output_format}}` | No |
| `{{constraints}}` | No |

## 10. Prompt Template

```text
You will complete a task. Study the example below carefully, then apply the same
approach, format, and style to the new input.

TASK:
{{task_instruction}}

EXAMPLE INPUT:
{{example_input}}

EXAMPLE OUTPUT:
{{example_output}}

NOW APPLY THE SAME APPROACH TO THIS NEW INPUT:
{{new_input}}

Additional requirements:
- Output format: {{output_format}}
- Constraints: {{constraints}}

Match the structure, tone, and level of detail shown in the example output.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_instruction}}` | The general task being demonstrated | "Rewrite the customer complaint as a polite response" |
| `{{example_input}}` | The sample input for the worked example | A sample complaint email |
| `{{example_output}}` | The correct/desired output for that input | The ideal polite reply |
| `{{new_input}}` | The real content to process | A new, different complaint email |
| `{{output_format}}` | Structural requirements | "Email format with greeting and sign-off" |
| `{{constraints}}` | Rules the output must follow | "Keep under 120 words" |

## 12. Example Input

```text
TASK:
Convert a casual meeting note into a formal action-item summary.

EXAMPLE INPUT:
"talked about the budget thing, marketing needs more $ for q3, sarah said she'd send
numbers by friday, also need to fix the website bug before launch"

EXAMPLE OUTPUT:
Action Items:
1. Marketing to submit updated Q3 budget request.
2. Sarah to provide supporting figures by Friday.
3. Website bug to be resolved prior to launch.

NEW INPUT:
"went over the hiring plan, need two more engineers by march, jake is drafting the
job posts, also client wants a demo before signing, mike's setting that up next week"
```

## 13. Example Output

```text
Action Items:
1. Finalize hiring plan for two additional engineers, target start date March.
2. Jake to draft job postings.
3. Mike to schedule client demo ahead of contract signing, planned for next week.
```

## 14. Customization Guide

- **Choose a representative example**: The example should reflect typical difficulty, not the easiest possible case — otherwise the model may under-perform on harder new inputs.
- **Match example length to expected output length**: If you want short outputs, use a short example; the model tends to mirror example length closely.
- **Use a real-feeling example**: Fabricated or overly clean examples sometimes produce output that feels artificial in the same way.
- **Swap the example when task drifts**: If you're reusing this template for a subtly different task, always update the example — a stale example anchors the model to the wrong pattern.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Clearly separate the example from the new input using labels or delimiters.
- Keep the example close in complexity to the real task — not simpler, not harder.
- If format matters more than content, make the example format flawless — the model will copy it precisely.
- Test with two or three different new inputs to confirm the example generalizes well.

## 17. Common Mistakes

- Using an atypical or edge-case example that misrepresents the general task.
- Making the example too long relative to the new input, causing bloated output.
- Forgetting to label which block is the example and which is the new input, causing confusion.
- Assuming one example fixes every ambiguity — some tasks genuinely need few-shot (Template 03).

## 18. Prompt Variations

- **Basic Version**: Task + one example + new input, no format constraints.
- **Advanced Version**: Adds explicit output format and constraints (as shown in Section 10).
- **Expert Version**: Adds a brief annotation explaining *why* the example output is structured that way, helping the model generalize the underlying rule rather than just the surface pattern.

## 19. Related Prompts

- `01_Zero_Shot_Prompting.md` — the no-example baseline
- `03_Few_Shot_Prompting.md` — extends this with multiple examples
- `09_Self_Consistency.md` — can be combined with one-shot for higher reliability

## 20. Tips

- One-shot is often the sweet spot for tasks where the "shape" of the answer matters more than exhaustive pattern coverage.
- If the model's output style drifts from the example on the first try, try re-ordering: place the example immediately before the new input with minimal instruction text between them.

## 21. Limitations

- A single example can't capture edge cases or category boundaries the way multiple examples can.
- Risk of the model overfitting to superficial features of the one example (e.g., exact wording) rather than the general principle.
- Less effective than few-shot for classification tasks with more than two or three possible categories.

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
| Command R+ | ✅ |

## 23. Tags

`#one-shot` `#prompt-engineering` `#example-based` `#calibration` `#beginner-friendly`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
