# Prompt Engineering Template Library

> **Compiled by:** Deb Barman
> **Total Templates:** 15
> **Format:** Markdown (.md)

---

## About This Library

This is a structured collection of 15 prompt engineering technique templates,
each documenting a distinct prompting strategy — from foundational
(Zero-Shot) to expert-level (Automatic Prompt Engineering). Every template
follows an identical 25-section structure, making the library easy to
navigate, compare, and extend.

Each template is written for **universal application** — the prompt
structures use domain-agnostic placeholders so they can be adapted to
writing, coding, business analysis, research, education, or any other field.

## How to Use This Library

1. **Browse by difficulty**: Start with Beginner templates (01–03) if you're
   new to prompt engineering, then progress toward Advanced/Expert templates.
2. **Copy the template**: Each file's Section 10 ("Prompt Template") contains
   a ready-to-use template with `{{variable}}` placeholders.
3. **Fill in the variables**: Use Section 11 ("Placeholder Explanation") to
   understand what each variable needs.
4. **Check the example**: Sections 12–13 show a worked example input/output
   for reference.
5. **Combine techniques**: Section 19 ("Related Prompts") in each file points
   to complementary techniques — many advanced workflows combine 2–3
   techniques together (e.g., Few-Shot + Chain-of-Thought).

## Template Index

| # | Template | Difficulty | Category |
|---|---|---|---|
| 01 | [Zero-Shot Prompting](01_Zero_Shot_Prompting.md) | Beginner | Foundational |
| 02 | [One-Shot Prompting](02_One_Shot_Prompting.md) | Beginner | Example-Based |
| 03 | [Few-Shot Prompting](03_Few_Shot_Prompting.md) | Beginner–Intermediate | Example-Based |
| 04 | [Chain-of-Thought](04_Chain_of_Thought.md) | Intermediate | Reasoning |
| 05 | [Tree-of-Thought](05_Tree_of_Thought.md) | Advanced | Multi-Path Reasoning |
| 06 | [Skeleton-of-Thought](06_Skeleton_of_Thought.md) | Intermediate | Structural |
| 07 | [Step-Back Prompting](07_Step_Back_Prompting.md) | Intermediate | Conceptual Grounding |
| 08 | [Meta Prompting](08_Meta_Prompting.md) | Advanced | Prompt Design |
| 09 | [Self-Consistency](09_Self_Consistency.md) | Advanced | Reliability |
| 10 | [Self-Reflection](10_Self_Reflection.md) | Intermediate–Advanced | Self-Critique |
| 11 | [ReAct Prompting](11_ReAct_Prompting.md) | Advanced | Agentic / Tool-Use |
| 12 | [Least-to-Most Prompting](12_Least_to_Most_Prompting.md) | Advanced | Decomposition |
| 13 | [Automatic Prompt Engineering](13_Automatic_Prompt_Engineering.md) | Expert | Optimization |
| 14 | [Prompt Chaining](14_Prompt_Chaining.md) | Intermediate–Advanced | Workflow |
| 15 | [Loop Prompting](15_Loop_Prompting.md) | Advanced | Conditional Loop |

## Recommended Learning Path

**Beginner track:** 01 → 02 → 03 → 04
**Reasoning track:** 04 → 05 → 07 → 12
**Reliability track:** 04 → 09 → 10
**Workflow/agentic track:** 06 → 14 → 11 → 15
**Meta/optimization track:** 08 → 13

## Common Combinations

- **Few-Shot + Chain-of-Thought**: Multiple examples that each show step-by-step
  reasoning ("few-shot CoT") — one of the most effective known combinations.
- **Chain-of-Thought + Self-Consistency**: Run CoT multiple times and take the
  majority answer for higher-reliability reasoning tasks.
- **Skeleton-of-Thought + Prompt Chaining**: Generate an outline as one chain
  step, then expand it in a subsequent step.
- **ReAct + Prompt Chaining**: Tool-use loops often sit inside a larger chained
  workflow (e.g., research phase uses ReAct, then hands off to a writing phase).
- **Self-Reflection + Loop Prompting**: Repeat a critique-revise cycle until a
  specific, measurable quality bar is met.

## File Structure

Each template file follows this consistent structure:

```
01. Overview                    09. Variables                17. Common Mistakes
02. Purpose                     10. Prompt Template           18. Prompt Variations
03. Use Cases                   11. Placeholder Explanation   19. Related Prompts
04. Target AI Models            12. Example Input             20. Tips
05. Prompt Category              13. Example Output           21. Limitations
06. Difficulty Level             14. Customization Guide      22. Model Compatibility
07. Required Inputs              15. Output Format Options    23. Tags
08. Optional Inputs              16. Best Practices           24. Version History
                                                               25. License / Credits
```

## License

This library is compiled by **Deb Barman** and is free to use, adapt, and
share with attribution.

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release — 15 templates covering foundational through expert-level prompting techniques |
