# 02 — What is Loop Engineering?

---

## 🧠 The Simple Explanation

Imagine you hired an assistant, and every single morning you had to walk over to their desk and tell them exactly what to do, word for word — "check the emails," "reply to the urgent ones," "flag anything about the budget." Every day. Same instructions. Forever.

At some point, you'd stop doing that. Instead, you'd write down the instructions **once**, hand them a checklist, tell them how often to run through it, and trust them to follow the checklist on their own — checking in with you only when something doesn't fit the pattern.

**That shift — from giving instructions every single time, to designing a system that gives the instructions for you — is loop engineering.**

---

## 📖 One-Line Definition

> **Loop engineering** is the practice of designing an automated system that repeatedly prompts, monitors, and verifies an AI agent's work — so a human doesn't have to manually re-prompt the agent at every step.

---

## 🔍 Breaking That Down

Let's unpack every part of that definition, because each word is doing real work.

**"Designing a system"** — not writing a prompt. A prompt is one instruction for one moment. A system is a standing structure: it has a trigger, a set of instructions, a way to check its own work, and a place to remember what it's already done.

**"Repeatedly prompts"** — the system, not you, generates the next instruction. You wrote the meta-instruction once. The loop writes the actual prompt each time it runs.

**"Monitors and verifies"** — this is the part most casual descriptions of loop engineering skip, and it's the most important part. A loop that just fires prompts blindly is not a loop engineering — it's a spam script. A real loop checks its own output against some definition of "done" before it stops or moves on.

**"So a human doesn't have to manually re-prompt"** — this is the actual point. You're not eliminated from the process. You've moved from being the person who types the prompt to being the person who **designed the system that types the prompt**.

---

## 🎬 Where This Phrase Came From

This isn't an abstract concept someone invented in a vacuum — it has a specific origin. Google engineer Addy Osmani wrote a widely-shared essay called *"Loop Engineering"* on June 7, 2026, formalizing a pattern that senior engineers at Anthropic and OpenAI were already describing informally.

Two quotes from that period explain the shift better than any definition can:

Peter Steinberger, creator of the OpenClaw project, put it bluntly: "You shouldn't be prompting coding agents anymore. You should be designing loops that prompt your agents."

And Boris Cherny, who leads Claude Code at Anthropic, described his own day-to-day work changing in exactly this way: "I don't prompt Claude anymore. I have loops running that prompt Claude and figuring out what to do." In a CNBC interview around the same time, he elaborated: it's now an agent that prompts Claude, and he ends up "talking to that new Claude that is kind of coordinating."

---

## 💡 A Concrete Analogy You Already Understand

You've built RAG_Master. Think about the difference between:

1. **Manually querying a vector database** each time you want a document — you type the query, you read the result, you decide what to do next.
2. **A hybrid retrieval pipeline** that automatically decides which retrieval strategy to use, re-ranks results, and only surfaces something to you when confidence crosses a threshold.

Loop engineering is that same shift, but applied to the *prompting* layer instead of the *retrieval* layer. You've already internalized this pattern in a different domain — loop engineering just names it for agent orchestration specifically.

---

## ⚠️ What Loop Engineering Is *Not*

Because the term is new and gets thrown around loosely, it's worth being precise about what it doesn't mean:

- **It's not just "automation."** Running a script on a cron job that always does the exact same thing isn't a loop in this sense — a loop needs to reason, adapt, and verify, not just repeat.
- **It's not "fully autonomous AI with no human involvement."** Every credible source on this topic — including Osmani's original essay — is explicit that a human still designs the loop, still sets the verification bar, and still reviews outcomes at some checkpoint.
- **It's not a replacement for understanding your codebase or your problem.** Designing a *good* loop requires more upfront thinking than writing a one-off prompt, not less.

---

## 🌍 Where You've Probably Already Seen This

If you've used a scheduled task in an AI tool, set up a CI pipeline that re-runs tests until they pass, or built any part of Godfather Agent's God Mode pipeline that runs multiple passes without you re-typing instructions each time — you've already written something resembling a loop. This guide gives you the formal vocabulary and the missing pieces (state, verification, isolation) to do it properly and on purpose.

---

## ➡️ Next

Continue to **`03_Why_Loop_Engineering.md`** to understand *why* this shift happened now, and what problem it actually solves.

---

*Loop Engineering Complete Guide | Part 2 of 22*
