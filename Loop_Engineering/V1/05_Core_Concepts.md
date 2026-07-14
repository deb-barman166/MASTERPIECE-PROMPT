# 05 — Core Concepts

> 🎯 *Goal: Build the mental model every later file in this guide assumes you already have.*

---

## 🧠 The One Idea That Explains Everything Else

Here is the single sentence to internalize before anything else in this guide will make sense:

> **A loop is a recursive goal: you define a purpose once, and the AI iterates toward it repeatedly, checking its own progress, until that purpose is satisfied or a human intervenes.**

Every concept in this file is an elaboration of that one sentence. Let's take it apart piece by piece.

---

## 🔁 Concept 1: "Recursive Goal" — Not a Recursive *Prompt*

This distinction trips people up constantly, so it's worth being extremely precise.

A **recursive prompt** would be: run the exact same instruction, word for word, over and over. That's what a naive cron job does. It's brittle — it doesn't know when to stop, doesn't adapt to what it finds, and doesn't get smarter as it runs.

A **recursive goal** is different: you define *what "done" looks like*, and the system generates a *new, context-aware prompt* on every iteration based on what's already been discovered. On iteration one, the agent might investigate. On iteration two, it prompts itself differently based on what it found on iteration one. The goal stays fixed. The prompt evolves.

💡 **Example:**
```
Bad (recursive prompt):
  Every hour: "Check the repo for bugs."
  → Same instruction every time, no memory of what it already checked

Good (recursive goal):
  Goal: "All open GitHub issues tagged 'bug' should have either a fix PR
  or a triage comment within 24 hours."
  → Iteration 1: discovers 5 untriaged issues, drafts fixes for 2, comments on 3
  → Iteration 2: checks status of the 2 fix PRs, discovers 1 new issue, repeats
  → The system remembers what it already did and only acts on what's left
```

---

## 🎯 Concept 2: A Verifiable Definition of "Done"

A loop without a way to check its own work isn't a loop — it's a script that runs forever or stops arbitrarily. This is, according to essentially every serious source on the topic, the single most important design decision in building any loop.

"Done" has to be something the agent (or a second agent) can *check*, not something it just decides. Good examples: tests pass, a lint check is clean, a specific file exists with expected content, a human has approved a specific step. Bad examples: "the code looks good," "I think this is complete" — anything that relies on the same agent's unverified self-assessment as the only signal.

This is why, throughout this guide, you'll keep seeing the phrase **"a machine-checkable definition of done."** It's the difference between a loop that's trustworthy and one that's a "token-burning furnace," to borrow a phrase from one of the more skeptical analyses of the trend — without a reliable "no," a loop just keeps saying "yes" to itself.

---

## 🧩 Concept 3: The Loop Needs to Live Outside a Single Conversation

A regular chat conversation with an AI model has a hard limit: once it ends (or the context window fills up), everything the model "knew" about what it had done is gone unless it was written down somewhere else.

A loop, by definition, has to survive across many separate sessions — sometimes hours or days apart. That means **the important information cannot live only inside one conversation's context.** It has to be externalized: written to a file, a database, a project board, something that persists on disk (or equivalent) and that the *next* session can read before it starts working.

This single requirement is why "state" and "memory" show up as a core building block in every framework you'll encounter (more in file 12). The agent forgets. The repo doesn't.

---

## 🧑‍⚖️ Concept 4: Maker and Checker Should Not Be the Same Actor

If the same agent that writes a piece of code is also the *only* one that verifies it's correct, you've built a system with a blind spot — it can't catch its own mistakes any better than you'd trust a student to be the sole grader of their own exam.

Good loop design separates **execution** from **verification.** One agent (or pass) does the work. A separate agent (or pass, or human) checks that work against the original goal and the project's existing standards, independently. This "maker-checker" separation is one of the most consistently repeated principles across every credible loop engineering source, and it's the entire reason sub-agents exist as a distinct concept (file 16 goes deep on this).

---

## ⏱️ Concept 5: Loops Exist on a Spectrum of Autonomy

Not every loop needs to run fully unattended. In fact, jumping straight to "no human involved at all" is one of the most common mistakes beginners make (covered fully in file 19). Instead, think of autonomy as a ladder you climb one rung at a time, as your trust in a given loop's verification grows:

```
RUNG 1 — Turn-based:    You verify every single reply before the next step happens
RUNG 2 — Goal-based:    A verifiable condition decides when work is done, not you
RUNG 3 — Time-based:    A schedule or external event starts the loop, unattended
RUNG 4 — Proactive:     The loop decides for itself when something needs attention
```

This four-rung structure comes directly from Anthropic's own "Getting Started With Loops" documentation, and it's a genuinely useful way to think about *how much* autonomy any given loop should have — you don't have to build rung four on your first attempt, and for most tasks, you shouldn't.

---

## 📊 Quick Reference: Core Concepts Summary

| Concept | The One-Line Version |
|---|---|
| Recursive goal | Fixed purpose, evolving prompt — not a repeated instruction |
| Verifiable "done" | A machine-checkable condition, not the agent's self-assessment |
| Externalized state | Memory lives on disk, not just inside one conversation |
| Maker-checker separation | The agent that does the work shouldn't be the only one grading it |
| Autonomy spectrum | Turn-based → goal-based → time-based → proactive, climbed gradually |

---

## 🧪 Mini Task

Before moving on, try this: pick one small recurring task from one of your own projects — checking whether BUTTERFLY's encrypted key storage tests still pass, for instance — and write down, in one sentence, what a *machine-checkable* "done" condition for that task would look like. If you can't state it in a way a script could check without a human reading it, that's useful information about how hard that particular loop would be to build safely.

✅ *Expected outcome:* A one-sentence, objectively checkable "done" condition — not a vague description like "make sure it's working."

---

## ➡️ Next

Continue to **`06_Key_Terminology.md`** — every term used in the rest of this guide, defined precisely and once.

---

*Loop Engineering Complete Guide | Part 5 of 22*
