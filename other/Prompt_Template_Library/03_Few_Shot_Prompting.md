# Few-Shot Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-03

---

## 01. Overview

Few-shot prompting provides the model with **multiple worked examples** (typically 2–8) before presenting the real task. Where one-shot gives a single calibration point, few-shot lets the model infer the *underlying pattern or rule* across varied examples — including edge cases, category boundaries, and stylistic range — rather than anchoring to one specific case.

This is one of the most powerful and widely used prompting techniques, particularly for classification, structured extraction, and tasks with nuanced rules that are difficult to state explicitly but easy to demonstrate repeatedly.

## 02. Purpose

- Teach the model a pattern through repetition rather than explanation.
- Cover edge cases and boundary conditions that a single example would miss.
- Improve consistency and accuracy on tasks with subtle distinctions (e.g., sentiment shades, formatting rules).
- Reduce the need for lengthy, hard-to-write natural-language instructions.

## 03. Use Cases

- Text classification (sentiment, topic, intent, priority level)
- Structured data extraction with varying input formats
- Style or tone matching across diverse content types
- Named entity recognition or tagging
- Translation or transformation tasks with nuanced rules
- Any task where "show, don't tell" produces more reliable results than instructions alone

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity
- Open-source instruction-tuned models (Llama, Mistral, Qwen, etc.)

## 05. Prompt Category

`Foundational` · `Example-Based` · `Pattern-Learning`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Task description**
- **3 or more examples** (input/output pairs), covering varied cases
- **New input** to apply the task to

## 08. Optional Inputs

- Output format
- Explicit list of categories/labels (for classification tasks)
- Constraints

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_instruction}}` | Yes |
| `{{example_set}}` | Yes (3+ pairs) |
| `{{new_input}}` | Yes |
| `{{category_list}}` | No |
| `{{output_format}}` | No |
| `{{constraints}}` | No |

## 10. Prompt Template

```text
You will perform a task consistently across varied inputs. Study the examples
below to understand the pattern, then apply it to the new input.

TASK:
{{task_instruction}}

CATEGORIES/LABELS (if applicable):
{{category_list}}

EXAMPLES:

Example 1
Input: {{example_input_1}}
Output: {{example_output_1}}

Example 2
Input: {{example_input_2}}
Output: {{example_output_2}}

Example 3
Input: {{example_input_3}}
Output: {{example_output_3}}

[Add more examples as needed]

NEW INPUT:
{{new_input}}

Requirements:
- Output format: {{output_format}}
- Constraints: {{constraints}}

Apply the same pattern shown in the examples above. Do not introduce a new
format or style not demonstrated.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_instruction}}` | The task being demonstrated | "Classify the urgency of each support ticket" |
| `{{category_list}}` | Valid output categories, if classifying | "Low, Medium, High, Critical" |
| `{{example_input_N}}` | The Nth sample input | A sample support ticket |
| `{{example_output_N}}` | The correct output for the Nth input | "High" |
| `{{new_input}}` | The real content to classify/process | A new support ticket |
| `{{output_format}}` | Structural requirement | "Return only the category label" |
| `{{constraints}}` | Rules to follow | "If uncertain, default to Medium" |

## 12. Example Input

```text
TASK:
Classify each customer message by urgency.

CATEGORIES:
Low, Medium, High, Critical

EXAMPLES:

Example 1
Input: "Just wondering if you have this in a different color?"
Output: Low

Example 2
Input: "My order hasn't arrived and it's been two weeks, getting worried."
Output: Medium

Example 3
Input: "The app is completely down and my whole team can't work, we're losing money every minute."
Output: Critical

NEW INPUT:
"I was charged twice for my subscription this month, can someone look into it?"
```

## 13. Example Output

```text
Medium
```

*(The model correctly infers that a billing error affecting one customer, while important, does not meet the "Critical" threshold demonstrated by the operational outage example, nor is it as low-priority as a general product question.)*

## 14. Customization Guide

- **Vary example difficulty**: Include at least one clear-cut case and one borderline case per category so the model learns boundaries, not just obvious examples.
- **Balance category representation**: For classification, include roughly equal examples per category to avoid biasing the model toward whichever category appears most often.
- **Order matters less than coverage**: Unlike one-shot, exact example order has a smaller effect in few-shot — but variety across examples matters a great deal.
- **Scale example count to task difficulty**: Simple binary classification may need only 3–4 examples; nuanced multi-class tasks often benefit from 6–8.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Use a consistent format across all examples — mismatched formatting between examples confuses the pattern.
- Include edge cases deliberately, not just "easy" examples.
- Number or clearly separate each example to avoid the model blending them together.
- Keep the new input in the same format/style as the example inputs.
- Periodically test with an example removed to check if fewer examples still perform adequately (helps optimize prompt length/cost).

## 17. Common Mistakes

- All examples being too similar to each other (no boundary coverage).
- Inconsistent formatting between examples, which the model may replicate as noise.
- Overloading with too many examples, increasing token cost without meaningfully improving accuracy past a certain point.
- Forgetting to specify what happens with ambiguous or out-of-scope inputs.

## 18. Prompt Variations

- **Basic Version**: 3 examples, minimal formatting.
- **Advanced Version**: 5–8 examples with explicit categories and constraints (Section 10).
- **Expert Version**: Adds a brief rationale line after each example output (e.g., "→ Critical because service is fully down for multiple users") to teach the *reasoning*, not just the label — often combined with Chain-of-Thought (Template 04).

## 19. Related Prompts

- `02_One_Shot_Prompting.md` — the single-example predecessor
- `04_Chain_of_Thought.md` — combine with few-shot for "few-shot CoT," a highly effective hybrid
- `09_Self_Consistency.md` — often paired with few-shot for classification reliability

## 20. Tips

- If output quality plateaus, more examples usually won't help — the bottleneck is likely example diversity, not quantity.
- For classification tasks, an explicit category list plus few-shot examples together outperform either alone.

## 21. Limitations

- Longer prompts increase token usage and cost, which matters at scale.
- Very large example sets can approach context window limits for some models.
- If examples are inconsistent or contain errors, the model will reliably learn the wrong pattern.
- Not a substitute for genuine reasoning tasks — pairs best with Chain-of-Thought for anything requiring multi-step logic.

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

`#few-shot` `#prompt-engineering` `#classification` `#pattern-learning` `#example-based`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
