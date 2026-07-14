# 16 — AI Agents and Multi-Agent Loops

> 🎯 *Goal: Bring sub-agents, worktrees, and maker-checker together into a full picture of how multi-agent orchestration works inside a loop — directly relevant to Godfather Agent's 100+ agent, 8-tier architecture.*

---

## 🧬 Single-Agent Loop vs. Multi-Agent Loop

Everything covered through file 15 works perfectly well with a single agent running the entire Discover → Act → Verify cycle by itself. Multi-agent loops exist for one specific reason: **some parts of that cycle benefit from being handled by a different agent than the one handling the rest of it** — usually because independence improves either verification quality (maker-checker) or throughput (parallel execution across worktrees).

```
SINGLE-AGENT LOOP:
  [ One agent ] handles Discover, Act, and Verify, sequentially

MULTI-AGENT LOOP:
  [ Orchestrator ] → dispatches to → [ Sub-agent 1: Discovery specialist ]
                                    → [ Sub-agent 2: Maker/implementer  ]
                                    → [ Sub-agent 3: Checker/verifier   ]
```

---

## 👥 The Three Recurring Sub-agent Roles

Across nearly every real-world loop example covered in this guide so far, sub-agents tend to specialize into one of three roles, even when the exact names differ project to project.

**The Discoverer.** Reads state, scans for what's changed, produces a structured list of findings. Often the cheapest sub-agent to run, since it's mostly reading and summarizing rather than generating substantial new work.

**The Maker.** Takes one specific finding and produces an actual attempt at resolving it — drafts the fix, writes the response, generates the content. This is where most of the "creative" or "generative" work happens, and it's the role most people picture when they think "AI agent."

**The Checker.** Independently reviews the Maker's output against the original goal, the project's skills, and existing tests — without simply re-reading the Maker's own reasoning back to itself. This is the physical embodiment of the maker-checker principle from file 05, and arguably the highest-leverage role of the three, since it's the one that actually catches mistakes before they become real-world consequences.

---

## 🏗️ Orchestration Patterns

How an orchestrator actually dispatches work to sub-agents follows a handful of recurring shapes. File 17 covers these as formally named design patterns in depth — this section previews the two most directly relevant to multi-agent structure specifically.

**Fan-out and synthesize.** The orchestrator spawns several sub-agents in parallel — often one per worktree — each working a separate piece of the discovered work independently, and then a final pass synthesizes their combined results back into one coherent outcome (one PR instead of three uncoordinated ones, for instance).

**Pipeline.** Sub-agents run in a fixed sequence, each one's output becoming the next one's input — Discoverer feeds the Maker, Maker feeds the Checker, Checker's approval feeds the connector layer. This is the shape of the canonical daily-triage example that's run through files 07, 08, and 09.

---

## 🔀 Why Parallelism Needs Worktrees, Specifically Here

This is worth restating in the specific context of multiple *agents*, not just multiple tasks: the moment an orchestrator spawns two or more Maker sub-agents to work simultaneously, each one needs its own isolated worktree (file 10, Part 2), or their edits will collide the instant they touch overlapping files — even if the two findings they're each working on seem unrelated on paper. This is precisely the setting where the `isolation: worktree` setting on a Claude Code sub-agent, or Codex's built-in per-thread worktree, stops being a nice-to-have and becomes structurally necessary.

---

## 💡 Direct Application to Godfather Agent

This is the file in the whole series most directly relevant to a system you've already built: Godfather Agent's 8-tier, 100+ agent structure is, functionally, a very large multi-agent orchestration — and the "God Mode pipeline" name suggests you already have an intuition for a top-level orchestrator dispatching to specialized lower-tier agents, similar to the pattern this file describes.

The lens this guide adds is specifically about **which of your existing tiers, if any, currently perform independent verification versus self-verification.** A useful audit question: for any given tier in your 8-tier structure, if that tier's output is wrong, does a *different* tier or agent catch it — or does the same tier's own output get trusted downstream without a second, independent pass checking it first? Wherever the answer is "no independent check," that's a specific, concrete place where formalizing a Checker role (even a lightweight one) would harden the system, using exactly the vocabulary and pattern this file just walked through.

---

## ⚠️ The Multi-Agent-Specific Cost Warning

File 03 and file 10 (Part 5) both flagged sub-agents as the most token-expensive component individually. Multi-agent loops compound that directly: a pipeline with a Discoverer, three parallel Makers, and a Checker for each Maker is running five to seven full agent passes for what might have been a single-agent, single-pass task at rung 1 of the autonomy ladder (file 11). This isn't a reason to avoid multi-agent loops — it's a reason to reserve them specifically for tasks where the independent verification or genuine parallelism they provide is worth that real, compounding cost, rather than defaulting to multi-agent structure out of habit or because it feels more sophisticated.

---

## 📊 Summary Table

| Role | Primary Job | Cost Profile | Failure Risk If Missing |
|---|---|---|---|
| Discoverer | Read state, surface what's changed | Low — mostly reading | Every run starts from zero, re-finding old issues |
| Maker | Produce the actual attempted solution | Medium–High — generative work | No progress happens at all |
| Checker | Independently verify the Maker's output | Medium — a full review pass | Cognitive surrender; unverified output ships |

---

## ➡️ Next

Continue to **`17_Loop_Design_Patterns_and_Diagrams.md`** for the formally named orchestration patterns this file previewed, laid out in full with diagrams.

---

*Loop Engineering Complete Guide | Part 16 of 22*
