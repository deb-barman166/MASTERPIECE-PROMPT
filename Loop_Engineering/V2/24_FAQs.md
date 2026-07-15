# 24 — FAQs

> 📘 File 24 of 25 — Loop Engineering Knowledge Library
> Phase: Horizon
> Prerequisite: None strictly required, though answers assume familiarity with files 01–23's concepts

---

## 1. Introduction

### Topic Overview

This file departs from the standard 14-section template deliberately — a FAQ's value is in fast, direct answers, not extended structural analysis. It collects the questions beginners most commonly ask when first encountering Loop Engineering, answered plainly, each pointing back to the library file where the full depth lives.

### Why This Topic Matters

Not every question needs (or benefits from) the full 25-file treatment. Sometimes you just need a straight answer to "wait, is this the same as an AI agent?" This file exists for exactly those moments — a fast reference you can scan without committing to reading an entire file.

---

## 2. Definition

*(This file's format departs from the standard template — see Section 1.)*

This file is organized as a direct question-and-answer reference rather than the library's usual 14-section structure, since that structure doesn't serve a FAQ's purpose well. Sections 3–11 below present grouped questions and answers; Sections 12–14 return to the standard format for consistency with the rest of the library.

---

## Frequently Asked Questions

### General & Conceptual Questions

**Q: Is "Loop Engineering" the same thing as "AI Agents"?**
No, but they're closely related. An AI Agent is the overall *system* pursuing a goal; the *loop* is the specific repeating mechanism that agent uses to pursue that goal. You could say Loop Engineering is the engineering discipline behind building the "engine" that powers an agent. See file 01 and file 20 for the full distinction.

**Q: Do I need to know machine learning to learn Loop Engineering?**
No. Loop Engineering treats the LLM as a component you call via an API — you don't need to understand how the model itself was trained, any more than a web developer needs to understand CPU microarchitecture. You do need solid general programming skills (this library assumes Python familiarity).

**Q: Is this the same as "prompt engineering"?**
No — prompt engineering is one layer *within* loop engineering, specifically concerned with the wording of a single model call. Loop Engineering is the broader discipline of designing when and how often those calls happen, and what happens between them. See file 20 for the complete, precise comparison.

**Q: What's the difference between a "loop" and just calling an API in a for-loop?**
A genuine agentic loop has *deliberate control flow* — the number of iterations and what happens in each one is determined dynamically by the model's own reasoning and by the loop's termination logic (file 07), not by a fixed, predetermined count. A simple `for i in range(5): call_api()` is not really a Loop-Engineered system in this library's sense; it's missing state reconciliation (file 06), adaptive control flow (file 09), and genuine termination logic (file 07).

---

### Getting Started Questions

**Q: What's the single most important file to read first?**
File 01 (`What is Loop Engineering`) — everything else in this library builds on its core skeleton. If you only read one file, that's the one.

**Q: I already build agents with LangGraph/CrewAI — do I still need this library?**
Likely yes, though you can skip straight to files 09–20. Frameworks handle the mechanics *for* you, which is genuinely useful, but it also means you may not deeply understand *why* the framework behaves the way it does — which becomes a real problem the first time you hit an edge case the framework doesn't handle cleanly. This library's concept-first approach (see file 22) is designed specifically to make you framework-literate rather than framework-dependent.

**Q: Do I need to build everything from scratch, or should I use a framework?**
It depends entirely on your project's actual needs — file 22 gives you a concrete decision framework. For learning purposes, building at least one loop from scratch (using files 06–09's patterns) is strongly recommended before adopting a framework, since it makes framework abstractions genuinely legible instead of magical.

**Q: How much Python do I need to know before starting this library?**
Comfortable with functions, classes, dictionaries, and basic error handling (try/except). This library's code examples use these consistently but don't require advanced Python features.

---

### Loop Design Questions

**Q: How do I know if my task needs ReAct or Plan-and-Execute?**
The core question is predictability: if each step's outcome might genuinely change what you do next, use ReAct's interleaved reasoning. If the task is well-understood and decomposable into a reliable sequence upfront, use Plan-and-Execute. File 10's Section 8 gives the full decision guidance.

**Q: How many iterations should I allow my loop?**
There's no universal number — it depends entirely on task complexity. The important principle (file 02, file 07) is that you set *some* hard limit, start conservative, and only loosen it once you've observed the loop's actual behavior in testing. Starting with 5–10 iterations and adjusting based on real observed needs is a reasonable default for most moderately complex tasks.

**Q: Should I always use multi-agent systems for complex tasks?**
No — this is one of the most common over-engineering mistakes (file 15, Section 9). Multi-agent architecture should be justified by genuine need for specialization or parallelism, not just task complexity alone. A single, well-engineered loop can handle surprisingly complex tasks; multi-agent adds real coordination overhead that needs to be worth its cost.

**Q: My loop keeps running forever — what's wrong?**
This is almost always a missing or broken termination condition (file 02, file 07). Check: do you have a hard iteration limit? A time limit? Is your "goal achieved" check actually being triggered correctly, or is there a bug preventing it from ever returning true? File 19's pre-launch checklist has a specific testing step for exactly this failure mode.

**Q: My agent seems to "forget" things it found earlier — why?**
This is almost always a state reconciliation bug (file 06, file 11) — check whether your code is *overwriting* state instead of *appending* to it. This is one of the most common, subtle bugs in loop engineering, and file 06's Section 7 shows the exact broken-vs-correct pattern to check against.

---

### Tool & Safety Questions

**Q: How do I stop my agent from doing something destructive (deleting files, sending real emails)?**
Use risk-tiered tool gating (file 14) — classify your tools by risk level, and require explicit human approval before executing anything irreversible. File 07's suspension pattern is the mechanism that makes this pause-for-approval flow actually work.

**Q: Is it safe to let an agent execute arbitrary code it generates?**
Only with proper sandboxing (file 14, Section 7's advanced example) — hard time limits, restricted filesystem/network access, and bounded output capture are the minimum safeguards. Running generated code with full system access is a serious security risk regardless of how "safe" the code looks.

**Q: How do I know if my agent is hallucinating tool results or genuinely getting them?**
You can't know this from the model's output alone — this is exactly why file 02 and file 09 emphasize independent verification over trusting self-report. If a tool call genuinely executed, its result should be traceable in your logs (file 08's observability layer); if you can't find that trace, investigate whether the tool call actually ran.

---

### Production & Reliability Questions

**Q: My loop works great in testing but breaks in production — why?**
This is extremely common, and file 19's Pre-Launch checklist exists specifically to catch it. The most frequent cause: testing only covers the "happy path," while production reliably surfaces edge cases (tool errors, malformed model output, resource exhaustion) that were never deliberately tested. File 19's checklist explicitly requires testing failure paths, not just success paths.

**Q: How do I debug a multi-agent system when something goes wrong?**
Start with communication logging (file 15, file 08) — without a clear record of every handoff and every agent's input/output, multi-agent debugging is nearly intractable. If you don't already have this logging in place, add it before attempting to debug further.

**Q: My agent's costs are higher than expected — what should I check first?**
Check for unnecessarily high iteration counts, unbounded context (file 11's context rot discussion — larger context means more tokens per call), and whether you're using an expensive multi-agent pattern (like Debate, file 16) where a cheaper single-loop approach would suffice.

**Q: How often should I re-evaluate my framework choice?**
Periodically, especially given how fast this landscape moves (file 22, file 23) — but don't churn framework choices reflexively. Re-evaluate when your actual requirements change meaningfully, or when your current framework's status changes significantly (e.g., moves to maintenance mode), not simply because a newer option exists.

---

### Learning Path Questions

**Q: I only have time to read a few files — which ones matter most?**
For a working understanding: files 01, 04, 09, 10, and 14 give you the core mental model and the most load-bearing mechanics. For production readiness specifically: add files 02, 07, and 19.

**Q: I want to specialize in multi-agent systems specifically — what's the fastest path?**
Files 09 (components) → 15 (multi-agent fundamentals) → 16 (named patterns) → 21 (real-world domain applications). You can skip most of files 11–14's single-loop-internals depth on a first pass, though understanding them eventually will make your multi-agent systems' individual sub-agents more reliable.

**Q: Is this library still relevant if I'm working with a completely different framework than the ones covered in file 22?**
Yes — this library is deliberately concept-first (see file 04's six pillars, file 09's four components). Any framework, including ones not covered here, is an implementation of those same underlying concepts. File 05's Category 7 terminology table is specifically designed to help you translate an unfamiliar framework's vocabulary back to concepts you already know.

---

## 12. Summary

### Key Takeaways

- This file departs from the library's standard 14-section format because a FAQ's value is fast, scannable, direct answers — not structural analysis
- Questions are grouped into five categories: General & Conceptual, Getting Started, Loop Design, Tool & Safety, Production & Reliability, and Learning Path
- Every answer points back to the specific library file(s) where the full depth lives — this file is a fast index, not a replacement for the library's deeper treatment
- The most common beginner confusions — Loop Engineering vs. Agents, ReAct vs. Plan-and-Execute, state overwriting bugs, over-eager multi-agent adoption — are directly addressed here with their root-cause files identified

### Cheat Sheet

```
FASTEST ANSWERS TO THE MOST COMMON QUESTIONS:

"Loop Eng. vs Agents?"        → file 01, 20 (loop is the engine, agent is the whole car)
"Which pattern do I need?"    → file 10 (predictability = ReAct; well-understood = Plan-Execute)
"Agent won't stop looping?"   → file 02, 07 (check your termination conditions)
"Agent 'forgets' things?"     → file 06, 11 (check for state OVERWRITE instead of APPEND)
"Need multi-agent?"           → file 15 (only if genuinely justified — don't default to it)
"Works in testing, not prod?" → file 19 (test FAILURE paths, not just the happy path)
```

---

## 13. Glossary

*(This file applies terminology from across the library — see file 05 for the complete glossary.)*

---

## 14. References & Further Reading

### Where to Go Next in This Library

- Previous file: `23_Future_of_Loop_Engineering.md`
- Next file: `25_References_and_Further_Reading.md` — the final file, collecting every citation and reference across the entire library
- Related: This file references nearly every prior file — use it as a fast index back into the library whenever a specific question arises

---

*This is File 24 of 25 in the Loop Engineering Knowledge Library. See `README.md` for the full index and suggested reading paths.*
