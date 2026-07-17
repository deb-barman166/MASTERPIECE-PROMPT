# Tagging System

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-53 · Library Organization

---

## Overview

Every template in this library (files 01-40) includes a Section 23 "Tags" field with hashtag-style keywords. This document consolidates those tags into a master taxonomy, showing which templates share which tags, so you can navigate the library by concept rather than only by file number or category.

---

## 1. Tag Categories

Tags across the library fall into five broad categories:

### A. Difficulty Tags
`#beginner-friendly` `#intermediate` `#advanced` `#expert-level`

### B. Technique-Type Tags
`#foundational` `#reasoning` `#example-based` `#agentic` `#structured-output` `#iterative-refinement` `#self-critique` `#reliability` `#optimization`

### C. Domain Tags
`#software-development` `#database` `#marketing` `#content-writing` `#business` `#education` `#creative-writing` `#research` `#security`

### D. Format/Output Tags
`#json-schema` `#structured-output` `#grounded-answers` `#citations`

### E. Application Context Tags
`#production-systems` `#classification` `#decision-making` `#pattern-learning`

---

## 2. Master Tag Index

### #foundational
`01` Zero-Shot · `02` One-Shot · `03` Few-Shot

### #reasoning
`04` Chain-of-Thought · `05` Tree-of-Thought · `07` Step-Back · `09` Self-Consistency · `12` Least-to-Most

### #agentic
`11` ReAct · `16` Agentic Prompting · `17` Multi-Agent · `18` Tool Use · `19` Function Calling

### #example-based
`02` One-Shot · `03` Few-Shot

### #self-critique / #iterative-refinement
`10` Self-Reflection · `15` Loop Prompting · `13` Automatic Prompt Engineering

### #optimization
`08` Meta Prompting · `13` Automatic Prompt Engineering

### #software-development
`21` Code Generation · `22` Debugging · `23` SQL · `24` Web Development

### #domain-specific (applies broadly to all of 21-40)
`21` through `40` — every domain template carries this tag

### #marketing
`27` SEO · `28` Marketing · `30` Social Media

### #content-writing
`26` Content Writing · `34` Summarization · `39` Creative Writing

### #beginner-friendly
`01` Zero-Shot · `02` One-Shot · `26` Content Writing · `29` Email · `30` Social Media · `31` Image Generation · `35` Translation · `36` Education · `38` Productivity · `39` Creative Writing

### #advanced
`05` Tree-of-Thought · `08` Meta Prompting · `09` Self-Consistency · `11` ReAct · `12` Least-to-Most · `15` Loop Prompting · `18` Tool Use · `19` Function Calling · `20` RAG · `40` Security

### #expert-level
`13` Automatic Prompt Engineering · `16` Agentic · `17` Multi-Agent

### #structured-output
`19` Function Calling · Function-calling-adjacent sections of `18` Tool Use

### #grounded-answers / #citations
`20` RAG · `33` Research (implicitly, via source-citation requirements)

### #security
`40` Security Best Practices (primary) · relevant sections of `21` Code Generation, `19` Function Calling

---

## 3. Tag Combinations Worth Knowing

Some tag pairs point to particularly useful template clusters:

**`#reasoning` + `#reliability`** → Templates 04, 09, 10 (the core "trustworthy reasoning" cluster)

**`#agentic` + `#advanced`** → Templates 11, 18, 19, 20 (tool-integrated workflows below full autonomy)

**`#agentic` + `#expert-level`** → Templates 16, 17 (fully autonomous / multi-role systems)

**`#domain-specific` + `#beginner-friendly`** → Templates 26, 29, 30, 31, 35, 36, 38, 39 (accessible entry points into domain work)

**`#software-development` + `#security`** → Templates 21, 22, 40 (the production-code-safety cluster)

---

## 4. How to Use Tags for Discovery

1. **Starting from a concept, not a task:** If you know you want "something about reliability" but not which specific template, scan the `#reliability` and `#self-critique` entries above.
2. **Building a custom learning path:** Combine a difficulty tag with a technique-type tag (e.g., `#intermediate` + `#reasoning`) to find your next step up from where you are.
3. **Auditing domain coverage:** All of `21`-`40` share `#domain-specific` — if you're checking whether a particular field is covered, scan the domain tags in Category C above.

## Related Documents

- `52_Prompt_Library_Index.md` — the numerical/categorical master index this tagging system complements
- `50_Cheat_Sheet.md` — situational (task-first) lookup, as opposed to this document's concept-first lookup
- Each template's own Section 23 for its specific tag set

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release, covering tags from all 40 technique/domain templates |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
