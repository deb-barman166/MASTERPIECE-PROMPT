# Self-Reflection Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-10

---

## 01. Overview

Self-Reflection prompting asks the model to **critique and evaluate its own previous output** against a set of criteria, identify weaknesses or errors, and then produce an improved revision. This creates a built-in feedback loop within a single conversation: generate → critique → revise, without requiring a human to manually identify what's wrong first.

This technique leverages the observation that models are often better at *evaluating* a candidate answer than at generating a perfect one on the first attempt — self-reflection systematically exploits that gap to improve output quality.

## 02. Purpose

- Catch and correct errors, omissions, or weaknesses without human intervention.
- Improve output quality through a structured critique-then-revise loop.
- Make the model's own evaluation criteria explicit and checkable.
- Reduce the need for multiple back-and-forth human corrections.

## 03. Use Cases

- Reviewing and improving a first-draft piece of writing
- Checking reasoning or math for errors before finalizing an answer
- Evaluating code for bugs, edge cases, or style issues
- Improving structured outputs (reports, summaries, plans) against a quality rubric
- Any task where a "draft, then refine" workflow produces better results than one-shot generation

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity

## 05. Prompt Category

`Reasoning` · `Self-Critique` · `Iterative Refinement`

## 06. Difficulty Level

**Intermediate to Advanced**

## 07. Required Inputs

- **Original task/output**: Either the task to complete first, or an existing output to critique
- **Evaluation criteria**: What "good" looks like for this task

## 08. Optional Inputs

- Number of reflection/revision cycles
- Specific weaknesses to focus the critique on
- Format for the final revised output

## 09. Variables

| Variable | Required? |
|---|---|
| `{{original_task}}` | Yes |
| `{{evaluation_criteria}}` | Yes |
| `{{cycle_count}}` | No |
| `{{focus_areas}}` | No |
| `{{final_output_format}}` | No |

## 10. Prompt Template

```text
You will complete a task, then critique your own output, then produce an
improved version based on that critique.

TASK:
{{original_task}}

STEP 1 — INITIAL OUTPUT:
Complete the task above.

STEP 2 — SELF-CRITIQUE:
Evaluate your own output above against the following criteria: {{evaluation_criteria}}
Pay particular attention to: {{focus_areas}}
Identify specific weaknesses, errors, or areas for improvement. Be honest and
critical — do not simply praise the output.

STEP 3 — REVISION:
Based on your self-critique, produce an improved version of the output that
addresses the identified weaknesses.

{{cycle_count}}

Final output format: {{final_output_format}}
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{original_task}}` | The task to complete and then self-critique | "Write a cover letter for a marketing coordinator position" |
| `{{evaluation_criteria}}` | Standards used to judge the output's quality | "Clarity, specific examples, appropriate tone, no clichés" |
| `{{focus_areas}}` | Particular aspects to scrutinize closely | "Generic phrases that could apply to any candidate" |
| `{{cycle_count}}` | Optional instruction to repeat critique/revision more than once | "Repeat Steps 2-3 one more time before presenting the final version" |
| `{{final_output_format}}` | Structure of the final answer | "Present only the final revised version, not the intermediate draft" |

## 12. Example Input

```text
TASK:
Write a short product announcement for a new noise-cancelling headphone.

STEP 2 — SELF-CRITIQUE CRITERIA:
Clarity, avoids generic marketing clichés, specific and credible claims,
engaging opening line.

STEP 3 — REVISION:
Improve based on the critique.

Final output format: Present only the final revised version.
```

## 13. Example Output

```text
[Internal Step 1 - Initial Output, not shown to user per format instructions]
[Internal Step 2 - Self-Critique, not shown to user per format instructions]

FINAL REVISED VERSION:

Most headphones promise silence. Ours actually delivers it — blocking up to
35 decibels of ambient noise, verified in independent lab testing. The new
AeroSilent Pro uses dual-mic adaptive cancellation that recalibrates every
15 seconds to your environment, whether that's a subway car or an open-plan
office. 30-hour battery life means you won't be reaching for a charger
mid-week. Available now, starting at $179.
```

*(Note: In practice, if you want to see the intermediate critique for transparency,
simply remove "present only the final revised version" from the format instructions.)*

## 14. Customization Guide

- **Make criteria concrete, not vague**: "Good writing" is a weak criterion; "avoids clichés, uses specific numbers, opens with a hook" gives the model something actionable to check against.
- **Decide whether to show intermediate steps**: For transparency/debugging, show the critique; for a clean final deliverable, instruct the model to present only the revised version.
- **Set cycle count deliberately**: One critique-revise cycle is often sufficient; two cycles can help for especially important or complex outputs, but returns diminish quickly beyond that.
- **Target focus areas to known weak points**: If you know a model or task tends to produce a specific type of error (e.g., overly generic language, unverified claims), name it explicitly in `{{focus_areas}}`.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Give explicit, specific evaluation criteria rather than asking the model to "check if it's good."
- Instruct the model to be genuinely critical — models can default to overly generous self-assessment unless told otherwise.
- Decide upfront whether you want to see the critique itself or only the final polished result.
- Use this technique for outputs where quality matters more than speed — it roughly doubles generation length and cost.

## 17. Common Mistakes

- Vague criteria that don't give the model anything specific to check against.
- Not explicitly asking for honesty/rigor in the critique step, leading to superficial self-praise instead of real critique.
- Running excessive revision cycles for diminishing returns on already-solid output.
- Forgetting to specify whether the critique itself should be shown or hidden in the final response.

## 18. Prompt Variations

- **Basic Version**: Single "review your answer and improve it" instruction with no explicit criteria.
- **Advanced Version**: Explicit criteria, focus areas, and a single critique-revise cycle (Section 10).
- **Expert Version**: Adds a scoring rubric (e.g., rate the initial output 1–10 on each criterion before revising) and a second, final validation pass confirming the revision actually addressed each identified weakness.

## 19. Related Prompts

- `04_Chain_of_Thought.md` — self-reflection is often applied *after* a Chain-of-Thought answer to catch reasoning errors
- `09_Self_Consistency.md` — a complementary reliability technique; self-consistency samples multiple attempts, self-reflection critiques a single attempt
- `05_Tree_of_Thought.md` — can incorporate a self-reflection pass when evaluating which branch is strongest

## 20. Tips

- Self-reflection catches different error types than self-consistency: it's better for catching *qualitative* issues (clarity, tone, completeness) while self-consistency is better for catching *reasoning/logic* errors in quantitative tasks.
- Asking the model to rate its own output numerically against each criterion (not just describe it) often produces sharper, more actionable critiques.

## 21. Limitations

- Roughly doubles output length and cost compared to single-pass generation.
- Model self-critique isn't infallible — it can miss its own blind spots, especially systematic ones present across all its outputs.
- Diminishing returns after one or two cycles; additional cycles rarely improve quality much further and can even introduce unnecessary changes.

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

`#self-reflection` `#self-critique` `#iterative-refinement` `#quality-improvement` `#intermediate`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
