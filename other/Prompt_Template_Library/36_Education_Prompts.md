# Education Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-36

---

## 01. Overview

Education prompting is a domain-specific technique for producing teaching and learning content — explanations, lesson plans, practice problems, and assessments. The critical variable that separates effective educational prompting from general explanation is precise calibration to the learner's actual existing knowledge (not just age or grade level, which are imperfect proxies) and a clear pedagogical goal (build conceptual understanding, drill a specific skill, assess mastery). Effective educational content also often benefits from active learning techniques — asking questions, providing worked examples, and building from what the learner already knows — rather than pure one-way explanation.

## 02. Purpose

- Calibrate explanations precisely to a learner's actual existing knowledge, not just a generic level label.
- Match content structure to the specific pedagogical goal (understanding vs. skill drilling vs. assessment).
- Use effective teaching techniques (analogies, worked examples, checking understanding) rather than dense one-way exposition.
- Support building curricula, lesson plans, and practice materials in addition to single explanations.

## 03. Use Cases

- Explaining a concept at a specific knowledge level
- Creating lesson plans or curricula
- Generating practice problems or quiz questions
- Building study guides or exam prep materials
- Creating age-appropriate educational content for children
- Tutoring-style step-by-step problem walkthroughs

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (useful for fact-grounded educational content)

## 05. Prompt Category

`Domain-Specific` · `Education` · `Pedagogical`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Topic/concept**: What's being taught
- **Learner's existing knowledge**: What they already know/don't know

## 08. Optional Inputs

- Pedagogical goal (conceptual understanding, skill practice, assessment)
- Preferred teaching approach (analogy-heavy, example-driven, Socratic questioning)
- Format (explanation, lesson plan, practice problems, quiz)
- Length/depth
- Prior misconceptions to address

## 09. Variables

| Variable | Required? |
|---|---|
| `{{topic_concept}}` | Yes |
| `{{existing_knowledge}}` | Yes |
| `{{pedagogical_goal}}` | No |
| `{{teaching_approach}}` | No |
| `{{content_format}}` | No |
| `{{depth_length}}` | No |
| `{{known_misconceptions}}` | No |

## 10. Prompt Template

```text
Create educational content on the following topic.

TOPIC/CONCEPT:
{{topic_concept}}

LEARNER'S EXISTING KNOWLEDGE:
{{existing_knowledge}}

PEDAGOGICAL GOAL:
{{pedagogical_goal}}

PREFERRED TEACHING APPROACH:
{{teaching_approach}}

FORMAT:
{{content_format}}

DEPTH/LENGTH:
{{depth_length}}

KNOWN MISCONCEPTIONS TO ADDRESS:
{{known_misconceptions}}

INSTRUCTIONS:
- Build explicitly on what the learner already knows; don't re-explain
  foundational concepts they've already mastered, and don't assume
  knowledge they don't have.
- Use concrete examples or analogies suited to the learner's existing
  frame of reference where helpful.
- If the pedagogical goal is understanding (not just information transfer),
  consider including a brief check-for-understanding question at the end.
- If known misconceptions are listed, address them directly rather than
  hoping the correct explanation implicitly overrides them.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{topic_concept}}` | What's being taught | "Photosynthesis" |
| `{{existing_knowledge}}` | What the learner already knows | "Knows plants need sunlight and water, but doesn't know the chemical process involved" |
| `{{pedagogical_goal}}` | The learning objective | "Build conceptual understanding, not memorization of terms" |
| `{{teaching_approach}}` | Preferred method | "Use a relatable analogy, avoid heavy jargon" |
| `{{content_format}}` | Structure of the output | "A short explanation followed by 2 comprehension check questions" |
| `{{depth_length}}` | How much detail | "Keep it to about 150 words, this is a quick concept refresher" |
| `{{known_misconceptions}}` | Common wrong beliefs to correct | "Common misconception: that plants 'eat' soil for food" |

## 12. Example Input

```text
TOPIC: Compound interest
EXISTING KNOWLEDGE: Understands basic percentages and simple interest,
new to the concept of compounding
PEDAGOGICAL GOAL: Build intuition for why compounding matters over time,
not just the formula
TEACHING APPROACH: Use a concrete numeric example, avoid heavy formula-first explanation
FORMAT: Short explanation + 1 comprehension check question
DEPTH: About 150 words
KNOWN MISCONCEPTIONS: Often assumes interest just adds up linearly like
simple interest
```

## 13. Example Output

```text
You already know simple interest: if you have $100 and earn 10% a year,
you get $10 every year, forever — that's linear growth.

Compound interest works differently: instead of always earning 10% of your
original $100, you earn 10% of whatever you currently have. So:

Year 1: $100 → $110 (earned $10)
Year 2: $110 → $121 (earned $11, not $10 — because you're now earning 10%
of $110, not $100)
Year 3: $121 → $133.10 (earned $12.10)

Notice the amount you earn each year keeps growing, even though the rate
stays the same at 10%. That's the key difference from simple interest: your
past earnings start earning their own interest too. Over many years, this
compounding effect becomes dramatically larger than simple interest would
produce.

CHECK YOUR UNDERSTANDING:
If you started with $100 at 10% simple interest instead, how much would
you have after 3 years — and how does that compare to the $133.10 you'd
have with compound interest?
```

## 14. Customization Guide

- **Describe existing knowledge specifically, not just a grade/age level**: "5th grader" is a weak proxy; "knows basic multiplication but hasn't been introduced to fractions yet" gives the model something concrete to calibrate against.
- **State the pedagogical goal explicitly**: Understanding, memorization, and assessment call for genuinely different content structures — a request for "an explanation" is ambiguous between these.
- **Name known misconceptions when they exist**: Directly addressing a common wrong belief is more effective than hoping a correct explanation alone will overwrite it.
- **Match teaching approach to the learner's actual interests when possible**: An analogy connected to something the learner already cares about (sports, a hobby, a game) often lands better than a generic analogy.

## 15. Output Format Options

- Narrative explanation
- Structured lesson plan (objectives, content, activities, assessment)
- Quiz/practice problem set (with or without answer key)
- Step-by-step worked example
- Flashcard-style Q&A pairs

## 16. Best Practices

- Describe the learner's existing knowledge specifically rather than relying on a vague level label.
- State the pedagogical goal explicitly — understanding, skill practice, and assessment need different structures.
- Include a comprehension check when the goal is genuine understanding, not just information delivery.
- Address known misconceptions directly rather than assuming a correct explanation alone will override a prior wrong belief.

## 17. Common Mistakes

- Relying on a vague grade/age level instead of describing actual existing knowledge, leading to content pitched at the wrong level.
- Not specifying the pedagogical goal, resulting in content that informs but doesn't actually build the intended skill or understanding.
- Overloading an explanation with jargon before establishing the underlying intuition.
- Ignoring known misconceptions, missing the chance to directly correct a wrong belief that will otherwise persist.

## 18. Prompt Variations

- **Basic Version**: Topic + existing knowledge only, no format/goal specification.
- **Advanced Version**: Full structure with pedagogical goal, teaching approach, and misconceptions (Section 10).
- **Expert Version**: Adds a request for a follow-up "if the learner struggles with X, try explaining it this alternative way" fallback, useful for building adaptive tutoring-style content that anticipates where understanding might break down.

## 19. Related Prompts

- `07_Step_Back_Prompting.md` — grounding a specific explanation in the broader principle first is a core educational technique
- `04_Chain_of_Thought.md` — worked-example step-by-step reasoning directly supports teaching problem-solving skills
- `26_Content_Writing_Prompts.md` — longer educational content (study guides, articles) shares long-form writing structuring principles

## 20. Tips

- For genuinely effective teaching (not just accurate explanation), asking the model to build the explanation from an analogy or example the learner already understands, then bridge to the new concept, tends to produce more durable understanding than starting with abstract definitions.
- When creating practice problems, explicitly requesting a range of difficulty levels (not just uniform difficulty) better supports learners at different points in mastering a skill.

## 21. Limitations

- Effective teaching often benefits from real-time adaptation based on how a learner responds, which a single static prompt can't fully replicate — for genuinely adaptive tutoring, a multi-turn conversation checking understanding along the way outperforms a one-shot explanation.
- Content for young children requires extra care regarding age-appropriateness beyond just knowledge-level calibration; content should be reviewed by a responsible adult before use with children.
- Subject-matter accuracy remains essential — for specialized or advanced academic content, verification against authoritative sources or subject-matter expert review is worthwhile, especially for content that will be used at scale.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (useful for fact-grounded content) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#education` `#teaching` `#tutoring` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
