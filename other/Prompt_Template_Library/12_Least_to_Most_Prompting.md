# Least-to-Most Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-12

---

## 01. Overview

Least-to-Most prompting decomposes a complex problem into a **sequence of simpler sub-problems**, ordered from easiest/most foundational to hardest, and solves them one at a time — where the solution to each sub-problem feeds into solving the next. Rather than attempting the full complex problem in one leap, the model builds up to the final answer incrementally, with each step grounded in the previously solved step.

This differs from Chain-of-Thought in that CoT reasons through a single problem in steps, while Least-to-Most explicitly breaks the *problem itself* into a hierarchy of distinct, individually solvable sub-problems, each with its own clear answer before moving to the next.

## 02. Purpose

- Make complex, multi-layered problems tractable by decomposing them first.
- Ensure foundational sub-problems are solved correctly before building on them.
- Reduce compounding errors that occur when a model attempts a complex problem in a single leap.
- Provide a clear, inspectable decomposition that reveals the problem's underlying structure.

## 03. Use Cases

- Complex word problems with multiple dependent parts
- Multi-stage planning tasks (e.g., "first determine X, then use X to calculate Y")
- Programming problems that require solving sub-tasks before integration
- Curriculum-style learning tasks that build concept by concept
- Any problem that's overwhelming as a whole but manageable when broken into ordered pieces

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity

## 05. Prompt Category

`Reasoning` · `Decomposition` · `Sequential`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **Complex problem**: The full task to ultimately solve
- **Decomposition instruction**: Direction to break it into ordered sub-problems

## 08. Optional Inputs

- Maximum number of sub-problems
- Specific format for presenting each sub-problem and its solution
- Instruction on how to combine sub-answers into the final answer

## 09. Variables

| Variable | Required? |
|---|---|
| `{{complex_problem}}` | Yes |
| `{{max_subproblems}}` | No |
| `{{subproblem_format}}` | No |
| `{{final_synthesis_instruction}}` | No |

## 10. Prompt Template

```text
You will solve a complex problem by first decomposing it into a sequence of
simpler sub-problems, ordered from easiest/most foundational to most complex.
Solve each sub-problem in order, using earlier answers to help solve later ones.

COMPLEX PROBLEM:
{{complex_problem}}

INSTRUCTIONS:
1. Decompose the problem into no more than {{max_subproblems}} sub-problems,
   ordered from simplest/foundational to most complex.
2. Solve Sub-problem 1 first, fully and clearly.
3. Using the answer to Sub-problem 1 (and any prior sub-problems), solve the
   next sub-problem in the sequence.
4. Continue until all sub-problems are solved.
5. {{final_synthesis_instruction}}

Present each sub-problem and its solution using this format: {{subproblem_format}}
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{complex_problem}}` | The full, complex task to solve | "If a recipe for 4 people uses 3 eggs, and I want to make it for 10 people, but I also want to reduce the total egg usage by 20% for a lighter version, how many eggs do I need?" |
| `{{max_subproblems}}` | Cap on how many sub-problems to create | "3" |
| `{{subproblem_format}}` | Structure for presenting each sub-problem | "Sub-problem N: [statement] → Answer: [value]" |
| `{{final_synthesis_instruction}}` | How to combine sub-answers into the final result | "Combine the sub-answers to state the final egg count clearly" |

## 12. Example Input

```text
COMPLEX PROBLEM:
A company's revenue grew 15% this year to reach $2.3 million. Next year, they
project 10% growth on top of this year's revenue, but expect to lose $150,000
due to a planned product discontinuation. What is the projected revenue for
next year?

INSTRUCTIONS:
1. Decompose into no more than 3 sub-problems.
2. Solve each in order, using earlier results.
3. Combine sub-answers into the final projected revenue.

Format: Sub-problem N: [statement] → Answer: [value]
```

## 13. Example Output

```text
Sub-problem 1: What was last year's revenue, before this year's 15% growth
brought it to $2.3 million?
→ Answer: $2.3 million ÷ 1.15 ≈ $2.0 million (used only for context; not
needed for final calculation, since we're given this year's figure directly)

Sub-problem 2: What is next year's revenue after applying 10% growth to this
year's $2.3 million?
→ Answer: $2.3 million x 1.10 = $2.53 million

Sub-problem 3: What is next year's revenue after subtracting the $150,000
loss from the discontinued product?
→ Answer: $2.53 million - $150,000 = $2.38 million

FINAL ANSWER:
Combining the sub-problem results, the projected revenue for next year is
$2.38 million.
```

## 14. Customization Guide

- **Cap sub-problem count to actual complexity**: Simple two-part problems need only 2 sub-problems; genuinely multi-layered problems may need 4–5. Avoid forcing artificial decomposition on problems that don't need it.
- **Make the ordering explicit**: If sub-problems have a clear dependency order (B needs A's answer), state this dependency in the decomposition instructions.
- **Use consistent formatting per sub-problem**: A uniform "Sub-problem N → Answer" format makes it easy to verify each step independently.
- **Add a final synthesis instruction for multi-part combination**: When the final answer isn't just the last sub-answer but a combination of several, be explicit about how they should be combined.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Reserve Least-to-Most for problems that genuinely have a natural sub-problem hierarchy — not every task benefits from forced decomposition.
- Ensure each sub-problem is fully self-contained and answerable on its own, given only the results of prior sub-problems.
- Explicitly instruct the model to use earlier sub-answers in solving later ones, rather than re-deriving from scratch each time.
- Include a clear final synthesis step so the last sub-answer isn't mistaken for the final answer when combination is actually required.

## 17. Common Mistakes

- Decomposing into sub-problems that aren't actually simpler or more foundational than the original problem.
- Solving sub-problems independently without carrying forward relevant results from earlier steps.
- Over-decomposing simple problems into unnecessary sub-steps, adding length without adding clarity.
- Forgetting a final synthesis step when the answer requires combining multiple sub-answers, not just reporting the last one.

## 18. Prompt Variations

- **Basic Version**: 2 sub-problems, minimal formatting, single-pass solve.
- **Advanced Version**: 3–4 sub-problems with explicit format and synthesis instruction (Section 10).
- **Expert Version**: Adds a validation step after synthesis where the model checks the final answer against the original complex problem statement to confirm nothing was missed or misapplied.

## 19. Related Prompts

- `04_Chain_of_Thought.md` — reasons through a single problem in steps; Least-to-Most decomposes the problem itself first
- `06_Skeleton_of_Thought.md` — similarly decomposes, but for structural/content planning rather than sequential problem-solving
- `07_Step_Back_Prompting.md` — grounds in a general principle first, which can complement decomposition into sub-problems

## 20. Tips

- Least-to-Most is especially effective for problems where a direct attempt tends to skip or mishandle an intermediate step — forcing explicit sub-problems prevents that shortcut.
- If a sub-problem still feels too complex to solve directly, it can itself be decomposed further using the same technique recursively.

## 21. Limitations

- Not every problem has a natural, clean decomposition — forcing one onto an already-simple problem adds unnecessary overhead.
- Errors in an early sub-problem will propagate to all subsequent steps that depend on it.
- More token-intensive than solving the problem directly, due to the added decomposition and per-step presentation.

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

`#least-to-most` `#decomposition` `#sequential-reasoning` `#advanced` `#problem-solving`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
