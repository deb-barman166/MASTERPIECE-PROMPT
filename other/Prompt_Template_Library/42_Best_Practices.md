# Best Practices in Prompt Engineering

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-42 · Reference Document

---

## Overview

This document consolidates the best practices from all 40 templates in this library into a single, organized reference. It's structured as the positive counterpart to `41_Common_Mistakes.md` — where that document tells you what to avoid, this one tells you what to actively do. Each practice links back to the template(s) where it's covered in full depth.

---

## 1. Universal Practices (Apply to Almost Every Prompt)

### 1.1 State the Desired Output Format Explicitly
Never assume the model will default to the format you have in mind. Specify prose, list, table, JSON, or code block up front.
**See:** `01_Zero_Shot_Prompting.md`

### 1.2 Front-Load the Most Important Instruction
Models weight early context heavily. Put the core task before secondary details.
**See:** `01_Zero_Shot_Prompting.md`

### 1.3 Match Detail to Task Complexity
Simple tasks need simple prompts; complex, high-stakes tasks warrant fuller structure (examples, reasoning steps, validation). Don't over-engineer the trivial or under-specify the critical.
**See:** All templates — this is the organizing principle of difficulty levels across the library.

### 1.4 State Assumptions When Information Is Ambiguous
Instruct the model to flag its assumptions rather than silently resolving ambiguity, so you can catch a misinterpretation before it compounds.
**See:** `21_Code_Generation_Prompts.md`, `23_SQL_Prompts.md`, `24_Web_Development_Prompts.md`

---

## 2. Example-Based Prompting

### 2.1 Choose Representative, Not Ideal, Examples
Use examples that reflect typical difficulty — including at least one edge case — rather than the cleanest possible case.
**See:** `02_One_Shot_Prompting.md`, `03_Few_Shot_Prompting.md`

### 2.2 Balance Category Representation in Classification
For few-shot classification, include roughly equal examples per category to avoid biasing the model toward the most frequent one.
**See:** `03_Few_Shot_Prompting.md`

### 2.3 Demonstrate, Don't Just Describe, Format
When a format is hard to explain but easy to show, use one-shot or few-shot examples instead of lengthy prose description.
**See:** `02_One_Shot_Prompting.md`

---

## 3. Reasoning and Reliability

### 3.1 Require Numbered, Explicit Reasoning Steps
For math, logic, or multi-step problems, request clearly delineated steps with a separately labeled final answer.
**See:** `04_Chain_of_Thought.md`

### 3.2 Use Multiple Independent Attempts for High-Stakes Reasoning
Self-Consistency (multiple runs, majority vote) catches errors a single pass would miss.
**See:** `09_Self_Consistency.md`

### 3.3 Build In a Critique-Then-Revise Loop for Quality-Critical Output
Self-Reflection catches qualitative issues (clarity, tone, completeness) that a single generation pass often misses.
**See:** `10_Self_Reflection.md`

### 3.4 Ground Specific Answers in General Principles First
Step-Back prompting reduces errors on questions that depend on background context the model might otherwise skip.
**See:** `07_Step_Back_Prompting.md`

---

## 4. Domain-Specific Grounding

### 4.1 Always Provide Real Schema/Context, Never a Paraphrase
For SQL, code integration, and function calling, paste the actual schema, existing code, or type definitions.
**See:** `23_SQL_Prompts.md`, `19_Function_Calling.md`, `21_Code_Generation_Prompts.md`

### 4.2 Specify Exact Language/Dialect Versions
Syntax and available features differ meaningfully between versions — name them explicitly.
**See:** `21_Code_Generation_Prompts.md`, `23_SQL_Prompts.md`

### 4.3 Name the Real Audience and Their Existing Knowledge
For content, education, and business writing, describe the actual reader's expertise level and motivation, not a generic label.
**See:** `26_Content_Writing_Prompts.md`, `36_Education_Prompts.md`, `37_Business_Prompts.md`

### 4.4 Match Platform/Channel Conventions Precisely
Social media, email, and marketing content should be written for the specific platform's actual norms, not generically.
**See:** `30_Social_Media_Prompts.md`, `29_Email_Prompts.md`, `28_Marketing_Prompts.md`

---

## 5. Agentic and Tool-Based Workflows

### 5.1 Define a Concrete, Checkable "Done" Condition
Every agentic or loop-based prompt needs a specific completion criterion, not a vague quality bar.
**See:** `16_Agentic_Prompting.md`, `15_Loop_Prompting.md`

### 5.2 Set a Maximum Iteration/Step Cap
Always include a safety limit to prevent runaway or inefficient looping.
**See:** `15_Loop_Prompting.md`, `16_Agentic_Prompting.md`

### 5.3 Write Precise Tool/Function Definitions
Include exact input parameters and output formats — vague tool descriptions cause malformed calls.
**See:** `18_Tool_Use_Prompting.md`, `19_Function_Calling.md`

### 5.4 Require an Upfront Plan Before Autonomous Action
Reviewing an agent's stated plan before it starts acting catches flawed strategies early and cheaply.
**See:** `16_Agentic_Prompting.md`

---

## 6. Safety, Security, and Trust

### 6.1 Request Security-by-Default, Explicitly
Don't assume secure practices will be applied automatically — state security requirements as part of the task.
**See:** `40_Security_Best_Practices.md`

### 6.2 Use Placeholder Values for Anything Sensitive
Never include real credentials, keys, or personal data in a prompt, even for a one-off example.
**See:** `40_Security_Best_Practices.md`

### 6.3 Require Root-Cause Diagnosis Before Accepting a Fix
For debugging, always ask why a bug occurred before applying a patch.
**See:** `22_Debugging_Prompts.md`

### 6.4 Ground Answers Strictly in Provided Context for Factual Reliability
For RAG and research tasks, explicitly forbid outside knowledge blending and require citations.
**See:** `20_RAG_Prompting.md`, `33_Research_Prompts.md`

---

## 7. Iteration and Optimization

### 7.1 Test Prompts on Multiple Real Inputs Before Trusting Them
A prompt that works once may not generalize — test on 2-3 varied real inputs.
**See:** `08_Meta_Prompting.md`, `13_Automatic_Prompt_Engineering.md`

### 7.2 Use the Model to Diagnose and Improve Underperforming Prompts
Meta prompting and Automatic Prompt Engineering systematize prompt improvement rather than relying on manual trial and error alone.
**See:** `08_Meta_Prompting.md`, `13_Automatic_Prompt_Engineering.md`

### 7.3 Break Complex Tasks Into Chained or Decomposed Steps
When a single prompt is trying to do too much, split it into a chain or decompose into ordered sub-problems.
**See:** `14_Prompt_Chaining.md`, `12_Least_to_Most_Prompting.md`, `06_Skeleton_of_Thought.md`

---

## Quick-Reference Summary

| Category | Core Practice |
|---|---|
| Format | Always specify output format explicitly |
| Examples | Use representative, boundary-covering examples |
| Reasoning | Require explicit steps for complex problems |
| Reliability | Use multiple passes for high-stakes answers |
| Domain grounding | Provide real schema/context, never paraphrase |
| Agentic workflows | Define done conditions and iteration caps |
| Security | Request security explicitly, use placeholders always |
| Iteration | Test on real inputs before trusting a prompt |

## Related Documents

- `41_Common_Mistakes.md` — the negative counterpart to this document
- `51_Prompt_Checklist.md` — a pre-flight checklist format for quick use
- `50_Cheat_Sheet.md` — quick-reference summary of the whole library

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
