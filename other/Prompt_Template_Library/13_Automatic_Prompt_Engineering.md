# Automatic Prompt Engineering (APE)

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-13

---

## 01. Overview

Automatic Prompt Engineering (APE) is a systematic technique where the model is used to **generate a large set of candidate prompt variations** for a given task, **evaluate them** against sample inputs/outputs, and **select or synthesize the best-performing prompt** — largely automating the trial-and-error process that human prompt engineers would otherwise do by hand. It's a more rigorous, evaluation-driven extension of meta prompting (Template 08), which focuses on generating/improving one prompt at a time based on qualitative reasoning; APE emphasizes generating many candidates and testing them empirically.

## 02. Purpose

- Systematically discover high-performing prompts without exhaustive manual trial and error.
- Provide an empirical (test-based), not just intuitive, method for prompt selection.
- Scale prompt optimization across many candidate variations efficiently.
- Reduce reliance on prompt engineer intuition alone by grounding choices in test results.

## 03. Use Cases

- Optimizing a high-volume, repeated-use prompt (e.g., a customer service classifier run thousands of times)
- A/B testing prompt wording for measurable quality differences
- Discovering non-obvious phrasings that outperform intuitive first-draft prompts
- Building a robust, production-grade prompt where marginal accuracy gains matter significantly at scale

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (less common for this specific workflow)

## 05. Prompt Category

`Meta-Level` · `Optimization` · `Empirical Testing`

## 06. Difficulty Level

**Expert**

## 07. Required Inputs

- **Task description**: What the final prompt needs to accomplish
- **Sample input/output pairs**: A small test set to evaluate candidate prompts against
- **Candidate count**: How many prompt variations to generate

## 08. Optional Inputs

- Evaluation/scoring criteria
- Selection method (single best vs. synthesized hybrid)
- Target model for which the prompt is being optimized

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_description}}` | Yes |
| `{{sample_test_cases}}` | Yes |
| `{{candidate_count}}` | Yes |
| `{{scoring_criteria}}` | No |
| `{{selection_method}}` | No |
| `{{target_model}}` | No |

## 10. Prompt Template

```text
You are an expert prompt engineer conducting automatic prompt engineering.
Your goal is to discover the best-performing prompt for the task below.

TASK DESCRIPTION:
{{task_description}}

TARGET MODEL (if relevant):
{{target_model}}

SAMPLE TEST CASES:
{{sample_test_cases}}

INSTRUCTIONS:
1. Generate {{candidate_count}} distinct candidate prompts for this task. Vary
   their phrasing, structure, level of detail, and instructional approach
   meaningfully — not just minor wording tweaks.
2. For each candidate prompt, mentally simulate applying it to each sample
   test case, and predict the likely output.
3. Score each candidate against the following criteria: {{scoring_criteria}}
4. {{selection_method}}
5. Present the final selected/synthesized prompt in a clearly delimited block.

Show your evaluation reasoning for each candidate before presenting the
final result.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_description}}` | What the eventual prompt needs to accomplish | "Classify customer feedback as Positive, Negative, or Neutral" |
| `{{target_model}}` | The model the final prompt will run on | "GPT-4o" |
| `{{sample_test_cases}}` | A handful of representative input/expected-output pairs | 3-5 sample feedback messages with correct labels |
| `{{candidate_count}}` | Number of distinct prompt variations to generate | "5" |
| `{{scoring_criteria}}` | What makes a candidate prompt "good" | "Accuracy on sample cases, clarity, resistance to ambiguous inputs" |
| `{{selection_method}}` | How to conclude the process | "Select the single highest-scoring candidate" or "Synthesize the strongest elements of the top 2 candidates" |

## 12. Example Input

```text
TASK DESCRIPTION:
Classify short customer feedback messages as Positive, Negative, or Neutral.

SAMPLE TEST CASES:
1. "This product changed my daily routine for the better!" → Positive
2. "It broke after two days, complete waste of money." → Negative
3. "It's fine, does what it says, nothing special." → Neutral
4. "I was skeptical but it actually works great." → Positive
5. "Customer service never responded to my emails." → Negative

INSTRUCTIONS:
Generate 3 candidate prompts. Score against: accuracy on samples, clarity,
and robustness to ambiguous phrasing. Select the single best candidate.
```

## 13. Example Output

```text
CANDIDATE 1:
"Classify this feedback as Positive, Negative, or Neutral: [feedback]"
Simulated performance: Correctly handles clear cases (1, 2, 4, 5) but risks
inconsistent judgment on ambiguous/neutral cases like sample 3, since no
guidance on what qualifies as "Neutral" is given.
Score: 6/10 — functional but lacks guardrails for edge cases.

CANDIDATE 2:
"Classify the sentiment of this customer feedback. Positive = clear
satisfaction or praise. Negative = clear complaint or dissatisfaction.
Neutral = factual, mixed, or lacking clear emotional signal. Feedback:
[feedback]"
Simulated performance: Explicit category definitions correctly guide sample
3 toward Neutral by clarifying what qualifies. Clear cases remain correctly
classified.
Score: 9/10 — clear definitions reduce ambiguity significantly.

CANDIDATE 3:
"Read the feedback and output only one word: Positive, Negative, or Neutral.
Feedback: [feedback]"
Simulated performance: Correct for clear cases, but the lack of category
definitions creates the same ambiguity risk as Candidate 1, despite cleaner
output formatting.
Score: 6.5/10 — good output format constraint, but same definitional gap
as Candidate 1.

SELECTED PROMPT (Candidate 2, refined with Candidate 3's output constraint):

---
Classify the sentiment of this customer feedback. Output only one word.

Positive = clear satisfaction or praise
Negative = clear complaint or dissatisfaction
Neutral = factual, mixed, or lacking clear emotional signal

Feedback: {{feedback_text}}
---

This hybrid combines Candidate 2's category definitions (which correctly
resolved the ambiguous Neutral case) with Candidate 3's strict output
format constraint (single-word output, easier to parse programmatically).
```

## 14. Customization Guide

- **Provide genuinely representative test cases**: Include at least one ambiguous or edge-case example per category — testing only "easy" cases won't reveal meaningful differences between candidates.
- **Scale candidate count to how much time/tokens you can spend**: 3–5 candidates is typical for manual review; more can be generated for higher-stakes, high-volume production prompts.
- **Choose synthesis over single-pick when candidates have complementary strengths**: As shown in the example, the best final prompt is often a hybrid of two candidates' distinct strengths, not necessarily any single candidate as-is.
- **Name the target model when known**: Some phrasings perform differently across models; specifying the target model helps tailor candidate generation accordingly.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Always include ambiguous/edge-case test samples, not just clear-cut examples, to meaningfully differentiate candidate quality.
- Require the model to show its simulated reasoning for each candidate, not just a final score, so the evaluation is auditable.
- Treat this as a starting point for real empirical testing — mentally simulated performance is a useful heuristic, but actual testing against real model outputs remains valuable before production deployment.
- Prefer synthesis over rigid single-selection when candidates show complementary strengths.

## 17. Common Mistakes

- Using only easy/unambiguous test cases, which fails to differentiate meaningfully between candidate prompts.
- Generating candidates that are only superficially different (same structure, different wording) rather than genuinely distinct approaches.
- Skipping the "why" behind each candidate's score, making the final selection feel arbitrary.
- Treating the mentally-simulated evaluation as a substitute for real-world testing at scale, for high-stakes production use cases.

## 18. Prompt Variations

- **Basic Version**: 3 candidates, simple accuracy check against samples, pick the best.
- **Advanced Version**: 5 candidates with explicit scoring criteria and reasoning (Section 10).
- **Expert Version**: Adds an iterative refinement loop — after selecting/synthesizing the top prompt, generate a new round of candidates that are variations *on* the winner, repeating until performance plateaus across rounds.

## 19. Related Prompts

- `08_Meta_Prompting.md` — the qualitative, single-prompt-focused predecessor to this more systematic, test-driven technique
- `09_Self_Consistency.md` — shares the "generate multiple, then converge" philosophy, applied to answers rather than prompts
- `03_Few_Shot_Prompting.md` — sample test cases used here overlap conceptually with few-shot examples

## 20. Tips

- APE is most worth the overhead for prompts that will run at scale (thousands of times) — the effort to optimize pays off proportionally to usage volume.
- Keep a running library of "winning" prompt patterns discovered through APE, since certain structural choices (e.g., explicit category definitions) often generalize well across similar future tasks.

## 21. Limitations

- Mentally simulated candidate evaluation is not a substitute for actual empirical testing against a real model and real test data, especially for production deployments.
- Significant token/time investment relative to simply writing a prompt directly — best reserved for high-value, repeated-use prompts.
- Quality of the final result still depends on the quality and representativeness of the sample test cases provided.

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

`#automatic-prompt-engineering` `#ape` `#optimization` `#expert-level` `#empirical-testing`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
