# Prompt Engineering Knowledge Library

A rigorously structured, 60-file markdown knowledge base covering prompt engineering from foundational concepts through advanced production practices and a comprehensive technique catalog. Every file follows a consistent 19-section template — Definition, Why It Matters, Core Concepts, How It Works, Internal Mechanism, Types, Syntax, Examples (5 levels of increasing complexity), Best Practices, Common Mistakes, Real-World Applications, Comparisons, Advantages & Limitations, FAQs, Summary, Cheat Sheet, Glossary, References, and a Visual Diagram Gallery — and every file is cross-linked to the files immediately before and after it, plus relevant files throughout the series.

**Total: ~166,000 words across 60 files, 180 Mermaid/ASCII diagrams (3 per file), zero broken internal links.**

---

## How to Read This Library

The files are numbered for a reason — each builds on concepts from earlier files. Reading in order (01 → 60) is recommended for a first pass. After that, each file is self-contained enough to use as a standalone reference, and the cross-links throughout will guide you back to relevant prerequisite concepts as needed.

The library is built in two parts. **Part I (Files 1–30)** establishes the meta-layer of prompt engineering as a discipline — what a prompt is, the lifecycle around it, the roles and context it operates within. **Part II (Files 31–60)** builds a comprehensive catalog of named, concrete techniques on top of that foundation, culminating in domain-specific applications showing how it all composes in practice. File 30 closes Part I with a short retrospective before continuing into Part II; File 60 closes the entire library.

---

## Table of Contents

### Part I — Foundations, Lifecycle & Context (01–30)

#### Foundations (01–10)
| # | File | Covers |
|---|---|---|
| 01 | [What is a Prompt](./01_What_is_a_Prompt.md) | The fundamental definition — entry point for the whole series |
| 02 | [History of Prompts](./02_History_of_Prompts.md) | Evolution from rule-based NLP to modern LLM prompting |
| 03 | [Why Prompts Matter](./03_Why_Prompts_Matter.md) | The business/human case for prompt quality |
| 04 | [How LLMs Interpret Prompts](./04_How_LLMs_Interpret_Prompts.md) | The technical mechanism — tokenization, attention |
| 05 | [Prompt Components](./05_Prompt_Components.md) | The individual building blocks of a prompt |
| 06 | [Prompt Anatomy](./06_Prompt_Anatomy.md) | How components are arranged and structured |
| 07 | [Prompt Lifecycle](./07_Prompt_Lifecycle.md) | The full strategic arc — draft to retirement |
| 08 | [Prompt Workflow](./08_Prompt_Workflow.md) | The tactical, session-level working process |
| 09 | [Prompt Design Principles](./09_Prompt_Design_Principles.md) | Timeless maxims — clarity, specificity, conciseness |
| 10 | [Prompt Engineering Basics](./10_Prompt_Engineering_Basics.md) | The practical, step-by-step beginner process |

#### Quality & Craft (11–20)
| # | File | Covers |
|---|---|---|
| 11 | [Prompt Optimization](./11_Prompt_Optimization.md) | Systematic, metric-driven improvement |
| 12 | [Prompt Refinement](./12_Prompt_Refinement.md) | Manual, qualitative polishing |
| 13 | [Prompt Debugging](./13_Prompt_Debugging.md) | Reactive diagnosis of known prompt failures |
| 14 | [Prompt Testing](./14_Prompt_Testing.md) | Proactive discovery of unknown issues |
| 15 | [Prompt Evaluation](./15_Prompt_Evaluation.md) | Scoring output quality against rubrics |
| 16 | [Prompt Iteration](./16_Prompt_Iteration.md) | The ongoing cyclical improvement process |
| 17 | [Prompt Versioning](./17_Prompt_Versioning.md) | Tracking change history, enabling rollback |
| 18 | [Prompt Templates](./18_Prompt_Templates.md) | Reusable, parameterized fill-in-the-blank prompts |
| 19 | [Prompt Patterns](./19_Prompt_Patterns.md) | Named techniques — few-shot, chain-of-thought, ReAct |
| 20 | [Prompt Frameworks](./20_Prompt_Frameworks.md) | Structured methodologies — RTF, CO-STAR, RACE |

#### Roles, Context & Control (21–30)
| # | File | Covers |
|---|---|---|
| 21 | [System Prompts](./21_System_Prompts.md) | Persistent, session-level configuration |
| 22 | [User Prompts](./22_User_Prompts.md) | Individual, turn-specific requests |
| 23 | [Developer Prompts](./23_Developer_Prompts.md) | The intermediate trust tier |
| 24 | [Role Prompting](./24_Role_Prompting.md) | The persona/perspective-assignment technique |
| 25 | [Context Management](./25_Context_Management.md) | What to include and how to fit it |
| 26 | [Context Injection](./26_Context_Injection.md) | The security dimension — RAG and prompt injection defense |
| 27 | [Instruction Following](./27_Instruction_Following.md) | How models arbitrate conflicting instructions |
| 28 | [Output Control](./28_Output_Control.md) | Constraining what content appears and how much |
| 29 | [Output Formatting](./29_Output_Formatting.md) | Constraining structural organization — JSON, markdown |
| 30 | [Response Validation](./30_Response_Validation.md) | Downstream verification — closes Part I |

### Part II — Techniques & Applications (31–60)

#### Structural Techniques (31–37)
| # | File | Covers |
|---|---|---|
| 31 | [Constraints](./31_Constraints.md) | The general umbrella concept of any limiting rule |
| 32 | [Guardrails](./32_Guardrails.md) | The safety/ethics-specific subtype of constraint |
| 33 | [Delimiters](./33_Delimiters.md) | Deep-dive on boundary markers — quotes, XML, fences |
| 34 | [Variables](./34_Variables.md) | The conceptual data layer — type, source, trust |
| 35 | [Placeholders](./35_Placeholders.md) | The concrete syntax layer — `{{brackets}}` and collision risk |
| 36 | [Tone Control](./36_Tone_Control.md) | Shaping voice and register, independent of role |
| 37 | [Persona Design](./37_Persona_Design.md) | Building a complete, reusable, documented identity |

#### The Shot Spectrum (38–40)
| # | File | Covers |
|---|---|---|
| 38 | [Few-Shot Prompting](./38_Few_Shot_Prompting.md) | Multiple varied examples enabling pattern generalization |
| 39 | [One-Shot Prompting](./39_One_Shot_Prompting.md) | A single example for format-anchoring, not rule inference |
| 40 | [Zero-Shot Prompting](./40_Zero_Shot_Prompting.md) | Instruction alone — the efficient default to try first |

#### The Reasoning-Elicitation Family (41–45)
| # | File | Covers |
|---|---|---|
| 41 | [Chain of Thought](./41_Chain_of_Thought.md) | Linear, step-by-step reasoning before a final answer |
| 42 | [Tree of Thought](./42_Tree_of_Thought.md) | Branching, backtracking exploration of competing approaches |
| 43 | [Skeleton of Thought](./43_Skeleton_of_Thought.md) | Parallel expansion of independent parts, for latency |
| 44 | [Step-Back Prompting](./44_Step_Back_Prompting.md) | Deriving a general principle before applying it |
| 45 | [Meta-Prompting](./45_Meta_Prompting.md) | Using a model to help write, critique, or improve prompts |

#### Reliability & Optimization (46–50)
| # | File | Covers |
|---|---|---|
| 46 | [Self-Consistency](./46_Self_Consistency.md) | Multiple independent attempts, majority voting |
| 47 | [Self-Reflection](./47_Self_Reflection.md) | A single response critiquing and revising itself |
| 48 | [ReAct Prompting](./48_ReAct_Prompting.md) | Interleaving reasoning with real external actions |
| 49 | [Least-to-Most Prompting](./49_Least_to_Most_Prompting.md) | Decomposing into sequentially-dependent sub-problems |
| 50 | [Automatic Prompt Engineering](./50_Automatic_Prompt_Engineering.md) | The automated, closed-loop version of meta-prompting |

#### Composition & Agentic Systems (51–56)
| # | File | Covers |
|---|---|---|
| 51 | [Prompt Chaining](./51_Prompt_Chaining.md) | Connecting separately-scoped prompts in sequence |
| 52 | [Loop Prompting](./52_Loop_Prompting.md) | Cyclical repetition with a dynamic stopping condition |
| 53 | [Agentic Prompting](./53_Agentic_Prompting.md) | The umbrella: goal-directed, autonomous operation |
| 54 | [Multi-Agent Prompting](./54_Multi_Agent_Prompting.md) | Scaling to multiple coordinating agent instances |
| 55 | [Tool Use Prompting](./55_Tool_Use_Prompting.md) | The general capability and design discipline |
| 56 | [Function Calling](./56_Function_Calling.md) | The specific, structured, typed technical protocol |

#### Domain-Specific Applications (57–60)
| # | File | Covers |
|---|---|---|
| 57 | [RAG Prompting](./57_RAG_Prompting.md) | Grounding, citation, and retrieval-gap handling |
| 58 | [Code Generation Prompts](./58_Code_Generation_Prompts.md) | General techniques applied to producing source code |
| 59 | [Debugging Prompts](./59_Debugging_Prompts.md) | Using prompts to diagnose and fix broken code |
| 60 | [SQL Prompts](./60_SQL_Prompts.md) | Schema dependency and write-operation safety — closes the library |

---

## Key Throughlines

A few themes recur across many files, deliberately:

- **Stakes calibration** (introduced in File 3): not every technique is needed for every task — match rigor to actual consequence.
- **The trust hierarchy** (Files 21, 23, 26, 27): system > developer > user > injected content, and why this is trained behavior, not an architectural given.
- **Defense-in-depth** (Files 26, 27, 30, 32, 60): no single prompt-level technique is an absolute guarantee — layer prompt design with application-level safeguards, most concretely realized in SQL's preview-before-destructive-action pattern.
- **The quality-assurance triad** (Files 13–15): debugging (reactive), testing (proactive), evaluation (graded) work together, not interchangeably.
- **Careful scoping of near-synonym pairs** (Part II especially): few-shot vs. one-shot vs. zero-shot; chain-of-thought vs. tree-of-thought vs. skeleton-of-thought vs. step-back; tool use vs. function calling; prompt debugging (File 13) vs. debugging prompts (File 59). Each pair shares surface similarity but differs in genuine, load-bearing ways — every file's "Comparison with Related Concepts" section spells out exactly where the line sits.
- **The agentic taxonomy layers cleanly** (Files 48, 53–56): agentic prompting is the umbrella; ReAct is a specific reasoning pattern within it; tool use is a capability it depends on; function calling is that capability's technical protocol; multi-agent is a scaling dimension.

---

*Built as a fully cross-linked, single knowledge system — not 60 independent documents.*
