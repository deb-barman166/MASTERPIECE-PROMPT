# 11 — Types of Loops

> 🎯 *Goal: Understand the four-rung autonomy ladder in enough depth to know which rung any loop you're designing actually belongs on.*

---

## 🪜 Recap: The Ladder

File 05 introduced this ladder briefly as one of the core concepts. This file gives it the full treatment it deserves, because choosing the wrong rung is one of the most common — and most consequential — mistakes in loop design (more on that in file 19).

This four-rung progression comes directly from Anthropic's own Claude Code documentation, "Getting Started With Loops," published in late June 2026 alongside OpenAI's equivalent piece on the Codex agent loop.

```
RUNG 1 ─── Turn-based
RUNG 2 ─── Goal-based
RUNG 3 ─── Time-based
RUNG 4 ─── Proactive
```

---

## 1️⃣ Turn-Based Loops

**Definition:** You verify every single reply before the next step happens. The agent takes one action, stops, and waits for your explicit go-ahead.

**What this actually is:** If you're honest, this is just a regular agentic coding session — the "agent" concept from file 04's second stage, not really loop engineering in the fuller sense yet. But it's the correct, honest starting point for any new task, and it's included here specifically because skipping it is where most beginner mistakes happen.

**When to use it:** Any task where the cost of a wrong action is high, where you don't yet trust the agent's judgment on this specific type of work, or — most importantly — any task where you haven't yet figured out what a machine-checkable "done" condition would even look like.

💡 **Example:** You're using BUTTERFLY to test a new cryptographic function in BLACKCORE. Every single change gets reviewed by you before the next one happens. No automation, no schedule — you're still the one deciding when "next" happens.

---

## 2️⃣ Goal-Based Loops

**Definition:** A verifiable success condition — not a human — decides when work is done. You still typically start the run yourself, but you no longer verify every intermediate step; you verify the final outcome against a condition you defined in advance.

**What this actually is:** This is the first rung that's genuinely "loop engineering" rather than ordinary agentic use. The mechanism in Claude Code and Codex is literally called `/goal` in both tools — you give it a condition, and it runs until that condition holds, rather than requiring a prompt at each step.

**When to use it:** Tasks with a clear, machine-checkable finish line — tests pass, a build succeeds, a specific file matches an expected schema — where you trust the agent to handle the *intermediate* steps but still want to decide *when* the whole thing starts.

💡 **Example:** "Keep refactoring this module in RAG_Master's hybrid retrieval pipeline until the full test suite passes and the lint check is clean." You run it once. It iterates on its own until the condition is met, then stops and reports back.

---

## 3️⃣ Time-Based Loops

**Definition:** An external schedule or event starts the loop, unattended — you're no longer even the one clicking "run."

**What this actually is:** This is where automation (file 10, Part 1) becomes essential, not optional. The mechanism in Claude Code is `/schedule` or a Routine; in Codex, it's the Automations tab. The loop now has its own heartbeat, independent of you being at the keyboard.

**When to use it:** Recurring, well-understood tasks where you've already validated the goal-based version (rung 2) enough times to trust it running without you present to kick it off — daily CI triage, nightly documentation updates, weekly dependency checks.

💡 **Example:** Every night at 2 AM, an automation checks whether any of your 19 BUTTERFLY modules have new failing tests since the last commit, and if so, drafts a fix and opens a PR for your morning review.

---

## 4️⃣ Proactive Loops

**Definition:** The loop decides *for itself* when something needs attention, rather than waiting on a fixed schedule or a specific external event.

**What this actually is:** The most advanced rung, and genuinely rare to see done well as of mid-2026. This typically involves a loop continuously (or very frequently) monitoring a broader signal — usage patterns, error rates, sentiment — and deciding on its own that a threshold has been crossed and action is warranted, rather than waiting for a clock or a webhook to tell it to check.

**When to use it:** Only after you've built real trust across rungs 1–3 on a specific, well-scoped task category. This is not a starting point for a first loop, ever — it's the top of a ladder you climb, not a rung you jump to.

💡 **Example:** A loop monitoring feedback about your AI/ML content channel that notices engagement dropping on a specific content type *before* you'd have thought to check, and flags it — without you having scheduled that specific check.

---

## 📊 Comparison Table

| Rung | Who Starts It | Who Decides "Done" | Risk Level | Good First Loop? |
|---|---|---|---|---|
| 1. Turn-based | You, every time | You, every time | Lowest | This is where everyone should start |
| 2. Goal-based | You, once per run | A verifiable condition | Low–Medium | Yes — the real starting point for "a loop" |
| 3. Time-based | A schedule/event | A verifiable condition | Medium | Only after goal-based is proven reliable |
| 4. Proactive | The loop itself | A verifiable condition | Highest | No — advanced, earned through the other three |

---

## ⚠️ The Mistake This Ladder Exists to Prevent

The single most common beginner error, covered fully in file 19, is jumping straight from rung 1 to rung 3 or 4 — building a fully scheduled, unattended loop before you've validated, at rung 2, that your "done" condition actually works the way you think it does. A goal-based loop that runs once, where you can immediately see and correct a flawed verification condition, is dramatically cheaper to fix than the same flaw discovered three weeks into an unattended nightly automation.

**Climb the ladder in order. Don't skip rungs to get to the exciting part faster.**

---

## ➡️ Next

Continue to **`12_State_Context_and_Memory.md`** for a deep dive into the block that makes every rung above turn-based possible at all.

---

*Loop Engineering Complete Guide | Part 11 of 22*
