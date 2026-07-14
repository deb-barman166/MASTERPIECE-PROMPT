# 12 — State, Context, and Memory

> 🎯 *Goal: Go deep on the block that ties every other component together — this file expands what file 10, Part 6 introduced.*

---

## 🧠 Why This Deserves Its Own File

You've already seen state introduced as "the sixth block" and called "the spine of the whole thing." That's not exaggeration for effect — of the six components, state is the one that, if broken, silently degrades *every other component's* effectiveness without necessarily causing an obvious failure. A loop with a broken automation trigger just doesn't run. A loop with broken state runs fine, every time — and just never actually gets any smarter, endlessly rediscovering the same things.

This file is dedicated to understanding why, and how to build it well.

---

## 🔑 The Core Mechanical Fact

> **The model forgets everything between runs. The memory has to be on disk, not in the context window.**

This single sentence explains nearly everything about why state exists as a distinct architectural concern, separate from "the agent's reasoning." An LLM's context window — everything it can "see" and reason about in a single session — is temporary. Once that session ends, none of that reasoning persists on its own. If something important isn't explicitly written to a file, a database, or a board that the *next* session will read, it simply doesn't exist anymore as far as the next run is concerned.

This is the exact same principle you already understand from building RAG_Master: a language model's working memory and a persistent, queryable store are fundamentally different things, and conflating them is where systems break.

---

## 📝 What Good State Actually Looks Like

State isn't a vague concept — in practice, it's usually one of two concrete formats:

**A markdown file.** Simple, human-readable, version-controllable alongside your code. Works well for smaller projects or loops where a human will frequently want to read the state directly.

**A project board (e.g., Linear).** Better for larger-scale coordination, when multiple loops or multiple humans need to see and update the same state, and when you want built-in status tracking (open, in-progress, done) rather than parsing that out of markdown yourself.

Both Claude Code and Codex support linking to either format — the choice matters less than the discipline of using it consistently.

A well-designed state file, regardless of format, answers three questions at minimum:

```
1. WHAT WAS TRIED?     — the history of attempts, even failed ones
2. WHAT PASSED?        — verified, confirmed-good outcomes
3. WHAT'S STILL OPEN?  — the actual work remaining
```

---

## 🔄 State vs. Context: A Precise Distinction

These two words get used loosely and interchangeably in casual conversation, but in loop engineering they mean genuinely different things, and conflating them causes real design mistakes.

**Context** is what's inside a single agent's active reasoning window *right now* — the conversation so far, the files it's currently looking at, the tool results it's just received. It's temporary and session-scoped.

**State** is what survives *between* sessions — written externally, read back in fresh at the start of the next run, forming the connective tissue between one loop iteration and the next.

A useful way to hold this distinction: context is what the agent knows *this run*. State is what the *loop* knows, across all runs, ever.

---

## 🏗️ How State Gets Used Across the Lifecycle

Tying this back to file 08's five-stage lifecycle directly:

| Lifecycle Stage | State's Role |
|---|---|
| Trigger | (Not directly involved — the trigger itself doesn't need state) |
| **Discover** | Read state first — "what did I already know as of the last run?" |
| Act | May reference state to avoid redundant work already recorded as done |
| Verify | Compare new outcome against what state says was expected or already tried |
| **Record** | Write the updated outcome back — this is where state gets created or updated |

Notice that Discover and Record are the two stages state actually touches directly. This is a useful mental shortcut: if you're ever unsure whether a piece of information belongs in state, ask "would the *next* run's Discover stage need this to avoid redoing work?" If yes, it belongs in state. If it's only relevant to *this* run's internal reasoning, it can stay in context and doesn't need to be externalized.

---

## ⚠️ Common State Design Mistakes

**Writing too little.** A state file that just says "ran successfully" without recording *what* was found or *what* remains open forces the next run to rediscover everything from scratch anyway — defeating the entire purpose.

**Writing too much.** A state file that grows unboundedly, appending every historical detail forever without ever summarizing or pruning, eventually becomes so large that reading it back in costs more tokens than the discovery work it was meant to save.

**Two writers, no lock.** If more than one parallel worktree or sub-agent can write to the same state file simultaneously without coordination, you get the exact same collision problem worktrees were built to solve at the file level — just moved to your memory layer instead. This is why isolated worktrees each getting their own scoped finding, aggregated back by the orchestrator, tends to work better than every parallel agent writing directly to one shared file.

---

## 💡 A Direct Connection to Your Own Work

Godfather Agent already has a **7-layer memory system** — you built this before "loop engineering" had a name, which is a genuinely good sign about your existing instincts. This file gives you a lens to audit it: for each of those seven layers, ask which lifecycle stage (Discover or Record) it actually serves, and whether it's answering all three of the core state questions above — what was tried, what passed, what's still open — or only some of them.

---

## 🧪 Mini Task

Pick one existing state-like file or memory layer from any of your projects — it could be a config file, a log, or a formal memory layer in Godfather Agent. Check it against the three-question test from earlier in this file. Does it clearly answer "what was tried," "what passed," and "what's still open" — or does it only capture one or two of those?

✅ *Expected outcome:* An honest one-paragraph audit identifying which of the three questions your existing state format answers well, and which it doesn't answer at all yet.

---

## ➡️ Next

Continue to **`13_Feedback_and_Iteration.md`** to see how a loop uses this state, together with verification, to actually get better over time rather than just repeating.

---

*Loop Engineering Complete Guide | Part 12 of 22*
