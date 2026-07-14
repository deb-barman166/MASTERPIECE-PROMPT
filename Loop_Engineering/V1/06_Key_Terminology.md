# 06 — Key Terminology

> 🎯 *Every term you'll need for the rest of this guide, defined once, precisely, so later files can move fast without re-explaining basics.*

---

## 📖 Foundational Terms

**Loop**
A designed system that repeatedly prompts an AI agent toward a fixed goal, checking its own progress, without requiring a human to type each individual instruction.

**Prompt Engineering**
The craft of writing a single, well-structured instruction for a one-shot or turn-by-turn interaction with a model. The discipline loop engineering builds on top of, not replaces.

**Agent**
An LLM operating inside a loop of its own, within a single session: it calls a tool, observes the result, and decides the next action, repeating until a task is complete. Not new — the mechanism underlying agentic coding tools generally.

**Agentic Engineering**
The broader discipline of building systems that can reliably get a goal done end-to-end — covering evaluation systems, multi-agent collaboration, memory architecture, and model routing. Loop engineering is a narrower slice of this: specifically how a single loop drives itself, runs, stops, and remembers.

**Harness**
The environment a single agent runs inside — its tools, permissions, and immediate operating context. Some analysts place loop engineering *above* the harness (as the thing that decides when and how a harness gets invoked); others place it *inside* an expanded definition of harness. The disagreement matters less than understanding both views exist.

---

## 🧩 The Six Building Blocks

These six terms come directly from Addy Osmani's original framework and are used identically across Claude Code, Codex, and most serious discussion of the topic since. File 10 covers each in depth — these are the working definitions.

**Automation**
The mechanism that gives a loop a heartbeat — a schedule, trigger, or event that starts a run without a human manually initiating it. The thing that makes a loop an actual *loop*, rather than a one-time run.

**Worktree**
An isolated working directory, sharing the same repository history but on its own branch, so that one agent's edits cannot collide with another agent's edits when multiple agents work in parallel. Built on the standard `git worktree` mechanism.

**Skill**
A reusable, written-down unit of project knowledge or procedure — conventions, build steps, domain expertise — that an agent can reference instead of re-inferring context from scratch on every single run. (You already build these — this guide series itself was generated via a skill.)

**Plugin / Connector**
The wiring that lets a loop interact with tools and systems you already use — issue trackers, Slack, databases, calendars — typically standardized today via MCP (Model Context Protocol).

**Sub-agent**
A separate agent instance, spawned by the main loop, usually to divide labor or provide independent verification. The mechanism that enables maker-checker separation (see file 05).

**State**
Persistent memory that lives outside any single conversation — a markdown file, a project board, a database — recording what's been tried, what passed, and what's still open, so the next run can pick up where the last one stopped.

---

## ⚙️ Product-Specific Terms (as of July 2026)

These are specific commands and features inside current tools. Treat these as a snapshot — they're the most likely terms in this guide to change as products update. Always verify current behavior against the vendor's own documentation before relying on exact syntax.

**`/loop`** (Claude Code)
Runs a prompt or command repeatedly on an interval, within an active session.

**`/goal`** (Claude Code and Codex)
Runs an agent repeatedly until a user-defined, verifiable condition is satisfied, rather than a fixed number of times or a fixed schedule.

**`/schedule`** (Claude Code)
Sets up a persistent scheduled task that survives beyond a single session — the mechanism that turns a one-off `/loop` into something that keeps running on its own.

**Routines** (Claude Code, cloud)
Loops that trigger on a schedule, an API webhook, or a GitHub event — the "time-based" and "proactive" rungs of the autonomy ladder from file 05.

**Hooks** (Claude Code)
Shell commands or scripts that fire automatically at specific points in an agent's lifecycle (e.g., after a file edit, before a commit) — a way to inject verification or logging without the agent having to remember to do it.

**Automations tab** (Codex)
Where you configure a Codex automation: which project, which prompt, how often it runs, and whether it runs on your local checkout or a background worktree.

**Triage inbox** (Codex)
Where automation runs that *found something worth a human's attention* get routed. Runs that find nothing simply archive themselves.

---

## 🚨 Risk and Failure-Mode Terms

You'll see these throughout the guide, especially in files 03 and 19. They describe *why* loops go wrong, not how they work.

**Comprehension debt**
The gradual erosion of your own understanding of a codebase or system, caused by consistently accepting an agent's output without reading it closely — because the loop kept producing correct-looking results, so you stopped checking.

**Cognitive surrender**
Treating an agent's "completed" or "done" flag as *proof* the task succeeded, rather than as a *claim* that still needs independent verification.

**Verification debt**
The accumulated risk of skipped or shallow checks across many loop iterations — each individual skip feels harmless, but they compound.

**Orchestration tax**
A term describing the human side of running multiple parallel agents: worktrees solve the *mechanical* collision problem (agents overwriting each other's files), but your own review bandwidth — not the tooling — becomes the actual ceiling on how many agents you can responsibly run at once.

---

## 🧬 Related but Distinct Concepts

**Ralph Technique**
An earlier, simpler pattern (named after Ralph Wiggum from *The Simpsons*): running a coding agent in a plain `while` loop, feeding it the same prompt against a written specification repeatedly until the spec is satisfied. A minimal precursor to full loop engineering. See file 04.

**Dynamic Workflows**
A more recent Claude Code feature: deterministic, script-defined sequences of sub-agent calls — patterns like Fan-out & Synthesize, Classify & Act, Pipeline, Tournament, and Loop Until Done. Covered in file 17 alongside other named design patterns.

**MCP (Model Context Protocol)**
The standardized protocol most current connectors and plugins are built on, letting an agent reach external tools and services in a consistent way regardless of which underlying model or product is running it.

---

## 📊 Quick Lookup Table

| Term | One-Line Meaning |
|---|---|
| Automation | The trigger that gives a loop a heartbeat |
| Worktree | Isolated checkout so parallel agents don't collide |
| Skill | Written-down project knowledge, reused instead of re-inferred |
| Connector / Plugin | Wiring into external tools, usually via MCP |
| Sub-agent | A separate agent for division of labor or verification |
| State | Persistent memory outside any single conversation |
| Comprehension debt | Losing understanding of your own system by trusting output too readily |
| Cognitive surrender | Treating "done" as proof instead of a claim to check |

---

## ➡️ Next

Continue to **`07_How_Loop_Engineering_Works.md`** to see these terms in motion, mechanically, step by step.

---

*Loop Engineering Complete Guide | Part 6 of 22*
