# Self-Consistency Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-09

---

## 01. Overview

Self-Consistency is a technique where the **same reasoning prompt is run multiple times** (typically using Chain-of-Thought), generating several independent reasoning paths and answers. The final answer is then determined by taking the most common ("majority vote") result across all runs, rather than trusting a single generation. This exploits the fact that correct reasoning tends to converge on the same answer through different paths, while errors tend to be more randomly distributed — so consensus across multiple attempts is a strong signal of correctness.

Self-Consistency is less a single prompt and more a *prompting strategy* that wraps around another technique (usually Chain-of-Thought), executed multiple times.

## 02. Purpose

- Improve reliability and accuracy on reasoning-heavy tasks beyond what a single generation achieves.
- Reduce the impact of occasional reasoning errors or "hallucinated" logical steps.
- Provide a confidence signal — strong agreement across runs indicates higher reliability; a split vote flags uncertainty.
- Catch and discard outlier or anomalous responses.

## 03. Use Cases

- Math and logic problems where a wrong step can lead to a confidently incorrect answer
- High-stakes classification tasks where a majority-vote approach improves precision
- Fact-checking or verification tasks
- Any Chain-of-Thought task where accuracy matters more than speed or cost
- Situations where you want a built-in confidence indicator alongside the answer

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity

## 05. Prompt Category

`Reasoning` · `Reliability` · `Multi-Run Strategy`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **Problem/question**: The reasoning task to solve
- **Run count**: How many independent reasoning attempts to generate

## 08. Optional Inputs

- Voting/aggregation method
- Tie-breaking instructions
- Format for reporting the final consensus

## 09. Variables

| Variable | Required? |
|---|---|
| `{{problem_statement}}` | Yes |
| `{{run_count}}` | Yes |
| `{{aggregation_method}}` | No |
| `{{tie_breaking_rule}}` | No |
| `{{final_report_format}}` | No |

## 10. Prompt Template

```text
You will solve the following problem {{run_count}} separate times, using
independent step-by-step reasoning each time. Do not let earlier attempts
influence later ones — reason through each attempt fresh, as if seeing the
problem for the first time.

PROBLEM:
{{problem_statement}}

INSTRUCTIONS:
1. Produce {{run_count}} independent, clearly labeled reasoning attempts
   (Attempt 1, Attempt 2, etc.), each ending in a specific final answer.
2. After all attempts, aggregate the results using: {{aggregation_method}}
3. If there is a tie or split result: {{tie_breaking_rule}}
4. Report the final consensus answer and how many of the {{run_count}}
   attempts agreed with it.

Final report format: {{final_report_format}}
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{problem_statement}}` | The problem requiring independent reasoning attempts | "A 3-digit number's digits sum to 15. If you reverse the digits, the new number is 396 less than the original. What is the original number?" |
| `{{run_count}}` | Number of independent attempts to generate | "5" |
| `{{aggregation_method}}` | How to determine the consensus answer | "Majority vote — the answer given by the most attempts wins" |
| `{{tie_breaking_rule}}` | What to do if there's no clear majority | "Re-examine the tied attempts' reasoning and select the one with fewer logical assumptions" |
| `{{final_report_format}}` | How to present the final result | "State the final answer, followed by a confidence score (e.g., 4/5 attempts agreed)" |

## 12. Example Input

```text
PROBLEM:
A store had 240 items. It sold 25% of them on Monday, then sold 30% of the
remaining items on Tuesday. How many items are left after Tuesday?

INSTRUCTIONS:
1. Produce 3 independent reasoning attempts.
2. Aggregate using majority vote.
3. If tied, recheck the reasoning of tied attempts for errors.
4. Report final answer with confidence score.
```

## 13. Example Output

```text
Attempt 1:
- Monday: 240 x 0.25 = 60 sold, 180 remain
- Tuesday: 180 x 0.30 = 54 sold, 126 remain
- Final Answer: 126

Attempt 2:
- Monday: 25% of 240 = 60 sold → 240 - 60 = 180 left
- Tuesday: 30% of 180 = 54 sold → 180 - 54 = 126 left
- Final Answer: 126

Attempt 3:
- Monday: 240 x 0.25 = 60, remaining = 180
- Tuesday: 30% of 180 = 54, remaining = 180 - 54 = 126
- Final Answer: 126

AGGREGATION (Majority Vote):
All 3 attempts independently arrived at 126.

FINAL ANSWER: 126 items remain.
CONFIDENCE: 3/3 attempts agreed (100% consensus).
```

## 14. Customization Guide

- **Scale run count to stakes**: 3 runs is often enough for moderate-confidence tasks; 5–10 runs suits high-stakes or especially error-prone problems.
- **Choose aggregation method by task type**: Majority vote suits problems with a single correct numeric/categorical answer; for open-ended tasks, consider "select the most detailed and well-justified attempt" instead of a literal vote.
- **Plan for ties explicitly**: Always define a tie-breaking rule in advance rather than leaving it ambiguous, especially with even run counts.
- **Report confidence, not just the answer**: Surfacing how many attempts agreed gives the end user (or downstream system) a useful reliability signal.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Use an odd number of runs (3, 5, 7) to avoid ties in binary/categorical majority votes.
- Explicitly instruct the model to reason independently each time, not to let earlier attempts bias later ones.
- Always report the consensus level, not just the winning answer — a 3/5 split is meaningfully less reliable than a 5/5 agreement.
- Reserve this technique for problems where accuracy justifies the added cost — not routine, low-stakes queries.

## 17. Common Mistakes

- Using an even run count without a tie-breaking plan.
- Treating self-consistency as necessary for every task, when it's really reserved for reasoning-heavy, error-prone, or high-stakes problems.
- Not instructing the model to reason independently each time, resulting in attempts that just repeat the same (possibly flawed) logic rather than genuinely re-deriving the answer.
- Ignoring low-consensus results — a split vote should prompt further investigation, not just an arbitrary pick.

## 18. Prompt Variations

- **Basic Version**: 3 runs, simple majority vote, no tie-breaking plan.
- **Advanced Version**: 5 runs with explicit aggregation method and tie-breaking rule (Section 10).
- **Expert Version**: Adds a final meta-review step where the model examines any disagreeing attempts specifically to identify *why* they diverged, providing insight into where the reasoning is fragile — useful for refining the original prompt afterward.

## 19. Related Prompts

- `04_Chain_of_Thought.md` — the reasoning technique self-consistency is typically layered on top of
- `10_Self_Reflection.md` — can be applied after self-consistency to critique the winning consensus answer
- `05_Tree_of_Thought.md` — explores diverse approaches deliberately, whereas self-consistency samples the *same* approach repeatedly for reliability

## 20. Tips

- Self-consistency is most valuable precisely where a single Chain-of-Thought run has shown itself to be unreliable across repeated tests.
- For numeric answers, a simple frequency count works well; for more open-ended reasoning tasks, ask the model itself to judge which attempts converge on the same underlying conclusion, even if worded differently.

## 21. Limitations

- Significantly increases token usage and cost — effectively multiplying the base prompt cost by the run count.
- Majority vote assumes correct answers are more common than any single specific error — this holds well for many reasoning tasks but isn't guaranteed for tasks with a genuinely widespread misconception.
- Doesn't help if the underlying task instructions themselves are ambiguous or flawed — all runs will share that same flaw.

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

`#self-consistency` `#majority-vote` `#reliability` `#reasoning` `#advanced`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
