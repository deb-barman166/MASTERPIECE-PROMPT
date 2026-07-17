# Prompt Engineering Cheat Sheet

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-50 · Quick Reference

---

## How to Use This Cheat Sheet

One-page-style quick reference for the whole library. Find your situation below, get the template number, done. For full detail, open the linked template file.

---

## By Situation

| I need to... | Use Template |
|---|---|
| Get a quick answer with no examples needed | `01` Zero-Shot |
| Show the model exactly the format I want | `02` One-Shot |
| Teach a pattern with multiple examples | `03` Few-Shot |
| Solve a math/logic problem reliably | `04` Chain-of-Thought |
| Compare multiple possible approaches | `05` Tree-of-Thought |
| Plan structure before writing something long | `06` Skeleton-of-Thought |
| Ground a specific answer in general principles | `07` Step-Back |
| Design or fix an underperforming prompt | `08` Meta Prompting |
| Get a more reliable answer via multiple attempts | `09` Self-Consistency |
| Have the model critique and improve its own output | `10` Self-Reflection |
| Combine reasoning with tool/search actions | `11` ReAct |
| Break a complex problem into ordered sub-problems | `12` Least-to-Most |
| Systematically test multiple prompt variations | `13` Automatic Prompt Engineering |
| Split a big task into a sequence of prompts | `14` Prompt Chaining |
| Keep refining until a condition is met | `15` Loop Prompting |
| Give the model an open-ended goal to pursue autonomously | `16` Agentic |
| Simulate a debate or multi-role discussion | `17` Multi-Agent |
| Set rules for when/how to use available tools | `18` Tool Use |
| Get a precise, schema-valid function call | `19` Function Calling |
| Answer strictly from provided documents/context | `20` RAG |
| Write new code | `21` Code Generation |
| Fix a bug | `22` Debugging |
| Write a database query | `23` SQL |
| Build a UI component or web page | `24` Web Development |
| Analyze a dataset | `25` Data Analysis |
| Write a blog post or long-form article | `26` Content Writing |
| Optimize for search engines | `27` SEO |
| Write ad copy or campaign messaging | `28` Marketing |
| Write a professional or marketing email | `29` Email |
| Write a platform-specific social post | `30` Social Media |
| Generate a text-to-image prompt | `31` Image Generation |
| Generate a text-to-video prompt | `32` Video Generation |
| Research a topic thoroughly | `33` Research |
| Condense long content into a summary | `34` Summarization |
| Translate text between languages | `35` Translation |
| Explain a concept to a specific learner | `36` Education |
| Build a business case or strategic document | `37` Business |
| Organize tasks or build a schedule | `38` Productivity |
| Write fiction, poetry, or creative content | `39` Creative Writing |
| Request secure code or review for security | `40` Security Best Practices |

---

## By Difficulty Level

**Beginner:** 01, 02, 26, 29, 30, 31, 35, 36, 38, 39
**Beginner-Intermediate:** 03, 24, 25
**Intermediate:** 04, 06, 07, 21, 22, 23, 27, 28, 32, 33, 34, 37
**Intermediate-Advanced:** 10, 14
**Advanced:** 05, 08, 09, 11, 12, 15, 18, 19, 20, 40
**Expert:** 13, 16, 17

---

## Common Combinations (see `43_Real_World_Case_Studies.md` for full walkthroughs)

| Combo | Use Case |
|---|---|
| Few-Shot (03) + Chain-of-Thought (04) | Reasoning-heavy classification |
| Chain-of-Thought (04) + Self-Consistency (09) | High-stakes calculations/decisions |
| Skeleton-of-Thought (06) + Prompt Chaining (14) | Long-document generation |
| ReAct (11) + Tool Use (18) | Research/lookup workflows |
| Agentic (16) + Loop Prompting (15) | Autonomous, self-terminating workflows |
| Code Generation (21) + Security Best Practices (40) | Production code handling real data |
| Debugging (22) + Chain-of-Thought (04) | Complex or time-pressured diagnosis |

---

## The Four Universal Questions

Before sending almost any prompt, answer these:

1. **What format do I want the output in?** (State it — don't assume it's obvious.)
2. **What's the minimum context the model needs that it can't already know?** (Real schema, real audience, real constraints — not paraphrases.)
3. **Does this need reasoning, or just an answer?** (If reasoning: use 04, 09, or 10.)
4. **Is this a one-off, or will it run repeatedly?** (If repeated: invest in 08/13-style refinement upfront.)

---

## Fast Links

- Full mistake list → `41_Common_Mistakes.md`
- Full best-practices list → `42_Best_Practices.md`
- Pre-flight checklist → `51_Prompt_Checklist.md`
- Complete template index → `52_Prompt_Library_Index.md`
- Platform-specific guides → `45`-`49`

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
