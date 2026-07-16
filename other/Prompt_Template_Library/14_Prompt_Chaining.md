# Prompt Chaining

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-14

---

## 01. Overview

Prompt Chaining breaks a complex task into a **series of separate prompts**, where the output of one prompt becomes the input to the next. Rather than attempting to accomplish everything in a single, monolithic prompt, the task is split across multiple sequential calls to the model, each focused on one well-defined sub-task. This improves reliability, makes each step easier to verify and debug, and allows different steps to use different prompting techniques best suited to that specific sub-task.

This is the backbone of many real-world AI workflows and automation pipelines, where a single prompt would be too complex, too long, or too error-prone to handle reliably in one pass.

## 02. Purpose

- Break complex, multi-stage tasks into manageable, independently verifiable steps.
- Allow each step in the chain to use the prompting technique best suited to it.
- Make it possible to insert human review or automated validation between steps.
- Improve reliability on tasks that would overwhelm a single-prompt approach.

## 03. Use Cases

- Multi-stage content pipelines (research → outline → draft → edit)
- Data processing workflows (extract → clean → transform → summarize)
- Document generation with distinct planning and writing phases
- Any task naturally composed of sequential, dependent stages
- Workflows where intermediate outputs need human or automated review before proceeding

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity

## 05. Prompt Category

`Workflow` · `Multi-Prompt` · `Sequential`

## 06. Difficulty Level

**Intermediate to Advanced**

## 07. Required Inputs

- **Overall task**: The full, complex objective
- **Chain steps**: The defined sequence of sub-tasks that together accomplish it

## 08. Optional Inputs

- Validation criteria between steps
- Format for passing output from one step to the next
- Human review checkpoints

## 09. Variables

| Variable | Required? |
|---|---|
| `{{overall_task}}` | Yes |
| `{{chain_steps}}` | Yes (list of 2+ steps) |
| `{{handoff_format}}` | No |
| `{{validation_checkpoint}}` | No |

## 10. Prompt Template

```text
This task will be completed across a chain of sequential prompts. You are
currently on Step {{step_number}} of {{total_steps}}.

OVERALL TASK:
{{overall_task}}

CURRENT STEP:
{{current_step_instruction}}

INPUT FROM PREVIOUS STEP (if applicable):
{{previous_step_output}}

INSTRUCTIONS:
Complete only this step. Do not attempt to complete later steps in the chain.
Format your output as: {{handoff_format}}
This output will be passed directly as input to the next step in the chain.

{{validation_checkpoint}}
```

*Repeat this template once per step, substituting the step number, current
step instruction, and the previous step's output each time.*

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{overall_task}}` | The full multi-stage objective | "Produce a well-researched blog post on a given topic" |
| `{{step_number}}` / `{{total_steps}}` | Position within the chain | "Step 2 of 4" |
| `{{current_step_instruction}}` | What this specific step should accomplish | "Create a structured outline based on the research summary provided" |
| `{{previous_step_output}}` | The result passed from the prior step | A research summary generated in Step 1 |
| `{{handoff_format}}` | Structure the output should take to feed cleanly into the next step | "A bulleted outline with H2-level section titles" |
| `{{validation_checkpoint}}` | Optional review instruction before proceeding | "Pause here for user approval before continuing to Step 3" |

## 12. Example Input

```text
OVERALL TASK:
Produce a short blog post explaining a new productivity technique.

CHAIN STEPS:
1. Research and summarize key points about the technique
2. Create a structured outline from the research
3. Write the full draft based on the outline
4. Edit the draft for clarity and tone

CURRENT STEP: Step 2 of 4
CURRENT STEP INSTRUCTION: Create a structured outline based on the research
summary from Step 1.

INPUT FROM PREVIOUS STEP:
"The Pomodoro Technique involves working in focused 25-minute intervals
followed by 5-minute breaks, with a longer break after 4 intervals. It
was developed by Francesco Cirillo in the late 1980s. Benefits include
reduced mental fatigue and better focus. Common mistakes include ignoring
breaks or using intervals that are too long for the task at hand."

Handoff format: Bulleted outline with H2-level section titles.
```

## 13. Example Output

```text
## Introduction: Why Focus Is Harder Than Ever
- Brief hook about modern distraction and attention fragmentation

## What Is the Pomodoro Technique?
- Origin: developed by Francesco Cirillo, late 1980s
- Core structure: 25-minute focused intervals + 5-minute breaks
- Longer break after every 4 intervals

## Why It Works
- Reduces mental fatigue through enforced breaks
- Improves sustained focus by working in short, achievable bursts

## Common Mistakes to Avoid
- Skipping breaks entirely
- Using intervals too long for the task at hand

## Getting Started Today
- Simple first-step suggestion for readers to try it themselves

[This outline will be passed as input to Step 3: Write the full draft.]
```

## 14. Customization Guide

- **Define chain steps around natural task boundaries**: Good chain steps typically correspond to genuinely distinct cognitive modes (researching vs. structuring vs. writing vs. editing), not arbitrary splits.
- **Standardize the handoff format per step**: Consistent, predictable output formatting from each step makes the next step's prompt simpler and more reliable.
- **Insert validation checkpoints at high-risk steps**: If an early step (like research or outline) sets the direction for everything downstream, a human review checkpoint there is cheaper than discovering an error at the final step.
- **Keep each step's prompt focused**: Explicitly instruct the model not to jump ahead to later steps, keeping the chain's division of labor clean.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Design the chain around clear, distinct sub-tasks — not arbitrary splits of a single task.
- Always specify the exact handoff format so each step's output is immediately usable as the next step's input.
- Add validation checkpoints at steps where errors would be costly to discover later.
- Keep a clear record of which step number you're on, especially in longer chains, to avoid confusion or repeated steps.

## 17. Common Mistakes

- Splitting a task into steps that don't correspond to genuinely distinct sub-tasks, adding overhead without benefit.
- Inconsistent handoff formatting between steps, forcing manual reformatting between each call.
- Skipping validation at critical early steps, allowing an error to propagate through the entire chain.
- Allowing a step's prompt to drift into completing later steps, defeating the purpose of the chain's division of labor.

## 18. Prompt Variations

- **Basic Version**: A simple 2-step chain (e.g., draft → edit) with minimal handoff formatting.
- **Advanced Version**: A 4+ step chain with explicit handoff format and validation checkpoints (Section 10).
- **Expert Version**: Adds branching logic — where the output of one step determines which of several possible next steps to take (e.g., "if the research reveals the topic is highly technical, proceed to a specialized outline step; otherwise, proceed to the standard outline step").

## 19. Related Prompts

- `06_Skeleton_of_Thought.md` — a two-step chain (outline, then expand) is a specific, common case of prompt chaining
- `11_ReAct_Prompting.md` — an interleaved, tool-integrated variant of the same sequential, step-dependent philosophy
- `15_Loop_Prompting.md` — extends chaining with repeated cycles rather than a fixed linear sequence

## 20. Tips

- Prompt chaining is especially valuable when different steps benefit from entirely different prompting techniques — e.g., few-shot for classification in step 1, Chain-of-Thought for analysis in step 2.
- For production workflows, log each step's output separately; this makes it far easier to pinpoint which step introduced an error if the final result is wrong.

## 21. Limitations

- Requires more orchestration (managing multiple prompts and their handoffs) than a single-prompt approach.
- Errors in early steps propagate through the entire chain if not caught at a validation checkpoint.
- Increases total token usage and latency compared to a single combined prompt, since context often needs to be partially repeated at each step.

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

`#prompt-chaining` `#multi-step-workflow` `#sequential-prompting` `#pipeline` `#intermediate`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
