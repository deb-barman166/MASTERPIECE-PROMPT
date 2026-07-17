# Common Mistakes in Prompt Engineering

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-41 · Reference Document

---

## Overview

This document consolidates the most frequent prompt engineering mistakes seen across all 40 templates in this library into a single cross-referenced guide. Each entry names the mistake, explains why it happens, shows the failure pattern, and links to the template(s) where it's addressed in depth. Use this as a fast pre-flight check before sending an important prompt, or as a diagnostic when output quality isn't meeting expectations.

---

## 1. Structural Mistakes

### 1.1 Vague or Open-Ended Instructions
**The mistake:** Requests like "make this better" or "write something about X" give the model no criteria for success.
**Why it happens:** The requester has a mental picture of the ideal output but hasn't externalized it into the prompt.
**Fix:** State what "done" looks like explicitly — format, length, tone, must-include points.
**See:** `01_Zero_Shot_Prompting.md`, `26_Content_Writing_Prompts.md`

### 1.2 Missing Output Format Specification
**The mistake:** Not stating whether output should be prose, a list, a table, JSON, etc.
**Why it happens:** The format seems "obvious" to the requester but isn't to the model.
**Fix:** Always state the desired format explicitly, even when it feels redundant.
**See:** `01_Zero_Shot_Prompting.md`, `19_Function_Calling.md`

### 1.3 Bundling Multiple Unrelated Tasks in One Prompt
**The mistake:** Asking for five different things at once dilutes quality on all five.
**Why it happens:** It feels efficient to ask everything at once.
**Fix:** Split into separate prompts or a chain (see Template 14) when tasks are genuinely distinct.
**See:** `14_Prompt_Chaining.md`

---

## 2. Example and Context Mistakes

### 2.1 Unrepresentative Examples
**The mistake:** Using an atypical, overly easy, or overly hard example that misrepresents the general task.
**Why it happens:** The first example that comes to mind is often the clearest, not the most typical.
**Fix:** Choose examples that reflect real, average-case difficulty; include at least one edge case.
**See:** `02_One_Shot_Prompting.md`, `03_Few_Shot_Prompting.md`

### 2.2 Insufficient Example Diversity
**The mistake:** All few-shot examples are too similar to each other, giving no boundary coverage.
**Why it happens:** Easy examples are faster to write than boundary-case ones.
**Fix:** Deliberately include edge cases and near-miss examples, not just clear-cut ones.
**See:** `03_Few_Shot_Prompting.md`

### 2.3 Missing Schema/Context for Structured Domains
**The mistake:** Requesting SQL, code integration, or function calls without providing the actual schema, codebase context, or parameter types.
**Why it happens:** The requester has the context in their head and forgets the model doesn't.
**Fix:** Always paste real schemas, existing code snippets, and type definitions — never paraphrase them.
**See:** `23_SQL_Prompts.md`, `19_Function_Calling.md`, `21_Code_Generation_Prompts.md`

---

## 3. Reasoning and Reliability Mistakes

### 3.1 Skipping Explicit Reasoning for Complex Problems
**The mistake:** Expecting a correct answer to a multi-step problem without requesting step-by-step reasoning.
**Why it happens:** Direct-answer prompting is faster to write.
**Fix:** Add "think step by step" or a full Chain-of-Thought structure for anything requiring logic or multi-step reasoning.
**See:** `04_Chain_of_Thought.md`

### 3.2 Trusting a Single Reasoning Pass for High-Stakes Answers
**The mistake:** Accepting one Chain-of-Thought output as final for a high-stakes calculation or decision.
**Why it happens:** One pass looks confident and complete.
**Fix:** For high-stakes reasoning, use Self-Consistency (multiple independent runs) or Self-Reflection (critique pass).
**See:** `09_Self_Consistency.md`, `10_Self_Reflection.md`

### 3.3 No Tie-Breaking or Aggregation Plan
**The mistake:** Running multiple reasoning attempts without deciding in advance how to resolve disagreement between them.
**Why it happens:** Ties feel like an edge case not worth planning for upfront.
**Fix:** Define the aggregation and tie-breaking method before running multiple attempts.
**See:** `09_Self_Consistency.md`

---

## 4. Domain-Specific Mistakes

### 4.1 Not Specifying Language/Dialect Version
**The mistake:** Requesting code or SQL without specifying the exact language version or SQL dialect.
**Why it happens:** "Python" or "SQL" feels sufficiently specific, but syntax varies meaningfully by version/dialect.
**Fix:** Always name the exact version (e.g., "Python 3.12," "PostgreSQL 16").
**See:** `21_Code_Generation_Prompts.md`, `23_SQL_Prompts.md`

### 4.2 Ignoring Regional/Cultural Variation in Translation
**The mistake:** Specifying only the target language without regional dialect or formality register.
**Why it happens:** Language names feel like a complete specification.
**Fix:** Name the regional variant and formality level explicitly.
**See:** `35_Translation_Prompts.md`

### 4.3 Generic "Social Media" Content Instead of Platform-Specific
**The mistake:** Writing one version of a post and expecting it to work across all platforms.
**Why it happens:** It's more efficient to write once.
**Fix:** Name the specific platform; adapt structure and tone per platform rather than resizing the same copy.
**See:** `30_Social_Media_Prompts.md`

### 4.4 Treating All Search Intent as Uniform
**The mistake:** Optimizing for a keyword without considering what the searcher actually wants (informational vs. transactional).
**Why it happens:** The keyword itself feels like the complete signal.
**Fix:** Classify and state search intent explicitly before writing SEO content.
**See:** `27_SEO_Prompts.md`

---

## 5. Safety and Quality Mistakes

### 5.1 Including Real Sensitive Data in Prompts
**The mistake:** Pasting real credentials, API keys, or personal data into a prompt "just for this example."
**Why it happens:** It feels like a harmless one-off, and typing a placeholder feels like extra work.
**Fix:** Always use clearly-marked placeholder values, even for internal/one-off use.
**See:** `40_Security_Best_Practices.md`

### 5.2 Assuming Generated Code Is Automatically Secure
**The mistake:** Not stating security requirements explicitly, then assuming secure practices were applied by default.
**Why it happens:** Security feels like it should be a given, not something to request.
**Fix:** State security requirements explicitly as part of any code generation request handling real data or public exposure.
**See:** `40_Security_Best_Practices.md`, `21_Code_Generation_Prompts.md`

### 5.3 No Root-Cause Requirement in Debugging
**The mistake:** Accepting a proposed fix without asking why the bug occurred, risking a patch that only masks the symptom.
**Why it happens:** A working-looking fix feels sufficient.
**Fix:** Always require root-cause explanation before accepting a fix.
**See:** `22_Debugging_Prompts.md`

---

## 6. Agentic and Workflow Mistakes

### 6.1 No Definition of "Done"
**The mistake:** Giving an agent a goal without a concrete, checkable completion condition.
**Why it happens:** "Done" feels self-evident to the requester but isn't to the model.
**Fix:** Always state a specific, measurable definition of done.
**See:** `16_Agentic_Prompting.md`, `15_Loop_Prompting.md`

### 6.2 No Maximum Iteration/Step Cap
**The mistake:** Running a loop or agentic process without a safety limit on iterations.
**Why it happens:** It's assumed the process will naturally converge.
**Fix:** Always set a maximum step/iteration count as a safety net.
**See:** `15_Loop_Prompting.md`, `16_Agentic_Prompting.md`

### 6.3 Vague Autonomy Boundaries
**The mistake:** Telling an agent to "use good judgment" instead of naming specific decision types that need check-in.
**Why it happens:** Precise boundaries take more upfront thought than a general instruction.
**Fix:** Name specific, concrete decision types requiring escalation.
**See:** `16_Agentic_Prompting.md`

---

## How to Use This Document

1. Before sending an important or high-stakes prompt, scan the section most relevant to your task type.
2. If output quality is disappointing, use this as a diagnostic checklist to identify what might be missing.
3. Cross-reference the linked template for the full treatment of any mistake listed here.

## Related Documents

- `42_Best_Practices.md` — the positive counterpart to this document
- `51_Prompt_Checklist.md` — a pre-flight checklist format for quick use
- `50_Cheat_Sheet.md` — quick-reference summary of the whole library

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
