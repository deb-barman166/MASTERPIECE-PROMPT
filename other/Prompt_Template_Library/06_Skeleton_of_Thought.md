# Skeleton-of-Thought Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-06

---

## 01. Overview

Skeleton-of-Thought (SoT) prompting asks the model to first generate a **high-level skeleton or outline** of its answer — a short list of the main points or sections — before expanding each point into full detail. This two-phase approach (outline first, expand second) improves structural coherence, makes long-form outputs faster to produce, and gives the user (or a follow-up prompt) a chance to review and adjust the plan before the model commits to full detail.

It's conceptually similar to how a writer might draft an outline before writing a full essay, or how an engineer might sketch a system architecture before writing implementation code.

## 02. Purpose

- Improve the structural quality and completeness of long-form outputs.
- Allow early review/correction of the plan before full content is generated.
- Reduce the chance of the model wandering off-topic partway through a long response.
- Enable faster parallel expansion of each skeleton point, in workflows that support it.

## 03. Use Cases

- Long-form content (articles, reports, guides)
- Complex documents with multiple required sections
- Presentations or structured proposals
- Curriculum or lesson planning
- Any output where structure needs to be right before detail is added

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity

## 05. Prompt Category

`Structural` · `Two-Phase` · `Planning`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Topic/task**: What the final content should be about
- **Skeleton request**: Instruction to first produce an outline

## 08. Optional Inputs

- Number of skeleton points
- Expansion depth per point
- Whether to pause for approval between skeleton and expansion

## 09. Variables

| Variable | Required? |
|---|---|
| `{{topic_task}}` | Yes |
| `{{point_count}}` | No |
| `{{expansion_depth}}` | No |
| `{{pause_for_approval}}` | No |
| `{{output_format}}` | No |

## 10. Prompt Template

```text
You will produce content in two phases: first a skeleton, then full expansion.

TOPIC/TASK:
{{topic_task}}

PHASE 1 — SKELETON:
Generate a skeleton outline of {{point_count}} main points that will structure
the final output. Each point should be a short phrase (5-10 words), not a full
sentence, capturing the essence of that section only.

{{pause_for_approval}}

PHASE 2 — EXPANSION:
Expand each skeleton point into {{expansion_depth}}. Maintain logical flow
between sections. Do not introduce new top-level points not listed in the
skeleton.

Final output format: {{output_format}}
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{topic_task}}` | The subject or task for the full content | "A guide to setting up a home vegetable garden" |
| `{{point_count}}` | Number of skeleton points to generate | "5" |
| `{{expansion_depth}}` | How much detail each point should get | "2-3 paragraphs" |
| `{{pause_for_approval}}` | Optional instruction to stop and wait for confirmation | "Wait for user approval before proceeding to Phase 2." |
| `{{output_format}}` | Final structural format | "Markdown with H2 headers per section" |

## 12. Example Input

```text
TOPIC/TASK:
A beginner's guide to starting a small vegetable garden at home.

PHASE 1 — SKELETON:
Generate a skeleton outline of 5 main points. Each point should be a short
phrase (5-10 words).

PHASE 2 — EXPANSION:
Expand each skeleton point into 2-3 paragraphs. Maintain logical flow.

Final output format: Markdown with H2 headers per section.
```

## 13. Example Output

```text
SKELETON:
1. Choosing the right location and sunlight
2. Selecting beginner-friendly vegetables
3. Preparing and enriching the soil
4. Planting, watering, and early care
5. Ongoing maintenance and common pitfalls

---

## 1. Choosing the Right Location and Sunlight

Most vegetables need at least 6 hours of direct sunlight per day, so the first
step is observing your yard or balcony throughout the day to identify the
sunniest spot available...

[content continues for each of the 5 sections, following the skeleton order]
```

## 14. Customization Guide

- **Adjust point count to scope**: Short guides may need only 3–4 points; comprehensive reports may warrant 6–8.
- **Use the approval pause for high-stakes content**: For important documents, insert the pause and manually review the skeleton before allowing expansion — this catches structural issues early, when they're cheap to fix.
- **Vary expansion depth per section if needed**: Not all skeleton points deserve equal length; you can specify per-point depth for uneven emphasis (e.g., "expand point 3 in more depth than others").
- **Lock the skeleton during expansion**: Explicitly instruct the model not to add new top-level points during Phase 2, to prevent scope creep.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Keep skeleton points short and parallel in structure (similar phrasing/length across points).
- Review the skeleton before requesting expansion whenever the content is long or important.
- Explicitly forbid adding new top-level sections during expansion to preserve the approved structure.
- Use consistent formatting (e.g., H2 headers) between skeleton and final expanded output for easy comparison.

## 17. Common Mistakes

- Skipping the skeleton review step even when it's cheap and valuable to do so.
- Requesting too many skeleton points for the scope of content requested, resulting in shallow sections.
- Allowing the model to introduce new sections during expansion that weren't in the approved skeleton.
- Writing skeleton points as full sentences rather than short structural phrases, which blurs the line between planning and content.

## 18. Prompt Variations

- **Basic Version**: Skeleton and expansion requested in a single uninterrupted prompt.
- **Advanced Version**: Skeleton generated first, with an explicit pause for user approval before expansion (Section 10).
- **Expert Version**: Adds per-point word/depth targets and a final consistency pass where the model reviews the fully expanded document against the original skeleton to confirm nothing drifted off-plan.

## 19. Related Prompts

- `05_Tree_of_Thought.md` — for exploring multiple possible skeleton structures before choosing one
- `12_Least_to_Most_Prompting.md` — similarly decomposes a task, but focused on sequential sub-problems rather than parallel structural sections
- `14_Prompt_Chaining.md` — the two-phase (skeleton/expand) pattern is a specific case of a chained prompt sequence

## 20. Tips

- SoT is especially useful in multi-turn workflows: generate the skeleton in one message, get user sign-off, then expand in the next — this avoids wasted generation on a structure the user didn't want.
- For very long documents, consider expanding one section at a time across multiple prompts rather than all at once, to stay within context and maintain quality per section.

## 21. Limitations

- Adds an extra step compared to direct single-phase generation, which may be unnecessary for short content.
- If the skeleton itself is flawed, the entire expanded output inherits that flaw — that's the reason for reviewing before expanding.
- Some models may still drift from the skeleton during expansion despite instructions not to.

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

`#skeleton-of-thought` `#outlining` `#structured-content` `#long-form` `#two-phase`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
