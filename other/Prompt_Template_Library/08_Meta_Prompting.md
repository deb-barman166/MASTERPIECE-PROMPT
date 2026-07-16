# Meta Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-08

---

## 01. Overview

Meta prompting is the practice of using an AI model **to generate, critique, or refine prompts themselves**, rather than using the model to complete the end task directly. Instead of writing a task prompt by hand, you ask the model to design one for you — specifying the goal, and letting the model produce (or improve) the actual instructions, structure, and examples needed to achieve that goal reliably.

This is a "prompting about prompting" technique, and is especially valuable when building prompt libraries (like this one), designing prompts for non-expert users, or iteratively improving an underperforming prompt.

## 02. Purpose

- Offload the cognitive work of prompt design to the model itself.
- Systematically improve an existing prompt that isn't performing well.
- Generate prompt variations for A/B testing.
- Help non-experts produce effective prompts without needing deep prompt engineering knowledge.

## 03. Use Cases

- Building or expanding a prompt template library
- Diagnosing and fixing a prompt that produces inconsistent results
- Generating prompt variations for different skill levels (basic/advanced/expert)
- Creating prompts for a specific target model's known strengths and quirks
- Translating a vague goal ("I want better blog posts") into a structured, reusable prompt

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (less common for this use case, but functional)

## 05. Prompt Category

`Meta-Level` · `Prompt Design` · `Optimization`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **Goal description**: What the eventual task/output should achieve
- **Meta-instruction**: Direction to design or improve a prompt for that goal

## 08. Optional Inputs

- Target model (since different models respond differently to prompt structures)
- Existing prompt to critique/improve (if refining rather than generating from scratch)
- Constraints on prompt length or format

## 09. Variables

| Variable | Required? |
|---|---|
| `{{end_goal}}` | Yes |
| `{{target_model}}` | No |
| `{{existing_prompt}}` | No (required only for refinement mode) |
| `{{constraints}}` | No |

## 10. Prompt Template

```text
You are an expert prompt engineer. Your task is to design (or improve) a
prompt that will reliably achieve the following goal when given to an AI model.

END GOAL:
{{end_goal}}

TARGET MODEL (if relevant):
{{target_model}}

EXISTING PROMPT TO IMPROVE (leave blank if designing from scratch):
{{existing_prompt}}

CONSTRAINTS:
{{constraints}}

INSTRUCTIONS:
1. If an existing prompt is provided, identify its specific weaknesses
   (ambiguity, missing constraints, lack of examples, unclear format
   requirements, etc.).
2. Design a new or improved prompt that addresses these issues.
3. Explain briefly why your version is more likely to succeed.
4. Present the final prompt in a clearly delimited block, ready to copy and use.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{end_goal}}` | The outcome the final prompt should reliably produce | "Generate consistent, well-formatted product descriptions from a list of specs" |
| `{{target_model}}` | The AI model the prompt will be used with | "Claude" or "GPT-4" |
| `{{existing_prompt}}` | A prompt that isn't performing well and needs improvement | A pasted underperforming prompt |
| `{{constraints}}` | Any limits on the new prompt | "Must fit within 200 words", "Must not require any examples" |

## 12. Example Input

```text
END GOAL:
I want a prompt that turns a list of raw product specs into a consistent,
persuasive 3-sentence product description for an online store.

TARGET MODEL:
Claude

EXISTING PROMPT TO IMPROVE:
"Write a product description for this: [specs]"

CONSTRAINTS:
Must produce exactly 3 sentences every time. Must not exceed 60 words total.
```

## 13. Example Output

```text
WEAKNESSES OF THE EXISTING PROMPT:
- No sentence count or word limit specified, so output length will vary run to run
- No guidance on tone (persuasive vs. neutral vs. technical)
- No instruction on which specs to prioritize if there are many
- No format example, so structure may be inconsistent across products

IMPROVED PROMPT:

---
You are a copywriter for an online store. Write a product description using
the specs below.

SPECS:
{{product_specs}}

REQUIREMENTS:
- Exactly 3 sentences, no more, no fewer
- Maximum 60 words total
- Persuasive, benefit-focused tone (not just a spec restatement)
- Sentence 1: hook on the primary benefit
- Sentence 2: supporting feature or detail
- Sentence 3: call to action or closing appeal

Output only the 3-sentence description, nothing else.
---

WHY THIS VERSION IS MORE RELIABLE:
It fixes all four identified weaknesses: it locks the sentence count and word
limit, assigns a specific job to each sentence (reducing structural
variance), and specifies a persuasive tone so output isn't just a dry spec
list. This structure will produce far more consistent results across
different products than the original one-line prompt.
```

## 14. Customization Guide

- **Specify the target model when known**: Different models (e.g., Claude vs. GPT vs. Gemini) sometimes respond better to slightly different prompt structures — naming the target model lets the meta-prompt account for this.
- **Use refinement mode whenever an existing prompt underperforms**: Rather than starting from scratch, feeding in the current prompt and asking for a diagnosis often surfaces fixable issues faster.
- **Set hard constraints upfront**: Word limits, required sections, and format rules should be stated as constraints so the generated prompt bakes them in rather than needing manual patching afterward.
- **Iterate**: Meta prompting is often most effective as a repeated loop — generate a prompt, test it, feed the results back into another meta-prompting pass for further refinement.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Always ask the model to explain *why* its designed/improved prompt should work better, not just produce the prompt itself — the reasoning helps you evaluate and further refine it.
- When refining an existing prompt, explicitly request a list of identified weaknesses before the improved version, to make the improvement traceable.
- Test the generated prompt on 2–3 real inputs before trusting it at scale.
- Treat meta prompting as an iterative loop, not a one-shot fix.

## 17. Common Mistakes

- Accepting the first generated prompt without testing it on real inputs.
- Not providing enough context about the end goal, resulting in a generic prompt that doesn't address the specific use case.
- Skipping constraints, leading to a "better" prompt that still doesn't meet hard requirements like length or format.
- Using meta prompting for extremely simple tasks where hand-writing the prompt directly would be faster.

## 18. Prompt Variations

- **Basic Version**: "Write me a prompt that does X" with minimal structure.
- **Advanced Version**: Full weakness-diagnosis-then-improvement structure with constraints (Section 10).
- **Expert Version**: Adds a request for multiple prompt variants (e.g., a basic, advanced, and expert version of the same prompt, matching this library's own structure) plus a brief test plan suggesting what real inputs to try the new prompt on.

## 19. Related Prompts

- `13_Automatic_Prompt_Engineering.md` — a more systematic, often automated variant of meta prompting
- `10_Self_Reflection.md` — the critique step within meta prompting mirrors self-reflection applied to prompt design itself
- Every other template in this library can be fed into a meta prompt as the "existing prompt to improve"

## 20. Tips

- Meta prompting is how this very library could be extended — feed an existing template into a meta prompt asking for a new template following the same structure but for a different technique.
- Asking the model to generate 2–3 alternative phrasings of the same instruction, then testing which produces the most consistent output, is a fast way to A/B test prompt wording.

## 21. Limitations

- Adds an extra layer of indirection — you're prompting about a prompt, which takes more time upfront than writing a mediocre prompt directly.
- The model's suggested improvements still need human or empirical validation; a plausible-sounding "better" prompt isn't guaranteed to actually perform better until tested.
- Most valuable for prompts that will be reused many times; less worth the overhead for one-off tasks.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Partial (less common use case) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#meta-prompting` `#prompt-design` `#optimization` `#advanced` `#prompt-refinement`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
