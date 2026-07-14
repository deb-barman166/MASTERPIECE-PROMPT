# 08 — Loop Lifecycle

> 🎯 *Goal: Understand the full life of a loop — not one run of it, but the loop as an ongoing, evolving system.*

---

## 🔄 The Difference Between "A Run" and "The Lifecycle"

File 07 walked through *one execution* of a loop, start to finish. This file zooms out one level further: a loop isn't really "done" after one run completes. A real loop is a standing system that lives through many runs, and each run changes what the *next* run will see. That's the actual lifecycle.

```
        ┌─────────────────────────────────────────┐
        │                                           │
        ▼                                           │
   [ TRIGGER ] → [ DISCOVER ] → [ ACT ] → [ VERIFY ] → [ RECORD ]
        ▲                                           │
        │                                           │
        └───────────── next scheduled run ──────────┘
```

Five stages. Let's take each one seriously on its own.

---

## 1️⃣ Trigger

**What it is:** The event that starts a run — a schedule, a webhook, a manual invocation, or another loop's output.

**Why it matters:** This is the difference between "a loop" and "a script you happened to run once." If nothing external starts the next run, you haven't built a loop — you've just automated one single task.

**Design decision here:** How often should this fire? Too frequent, and you're burning tokens on runs that find nothing new (though even that has a soft landing — a well-designed automation with nothing to report simply archives itself instead of bothering anyone). Too infrequent, and issues sit unaddressed longer than they should. This is exactly the kind of judgment call Steinberger addressed directly when asked about cost: for many tasks, once per hour or once per day is plenty, since "waking up and doing some API calls is fairly cheap" relative to constant polling.

---

## 2️⃣ Discover

**What it is:** The agent gathers the information it needs to figure out what, if anything, needs doing — reading logs, checking a queue, scanning for changes since the last run.

**Why it matters:** This is where a loop's *memory* pays off directly. A well-built loop's discovery phase starts by checking the state file from the previous run — "what did I already know as of yesterday?" — rather than rediscovering everything from scratch every single time.

**Design decision here:** What counts as "new" versus "already handled"? This has to be answerable by checking state, not by re-reasoning about the whole history every time — otherwise your discovery phase gets slower and more expensive with every run, forever.

---

## 3️⃣ Act

**What it is:** The agent does the actual work — writes code, drafts a response, edits a file, calls a connector.

**Why it matters:** This is usually the stage people picture when they think "AI agent," but by the time you reach this stage in a well-designed loop, most of the hard design decisions have already been made upstream (what to work on, how to isolate it). Acting is often the most mechanically straightforward stage — assuming stages 1 and 2 did their job.

**Design decision here:** If more than one thing is being worked on at once, this is where worktree isolation matters (file 09 and file 10 go deep on this) — so that acting on finding A doesn't corrupt the file state that finding B's agent is relying on.

---

## 4️⃣ Verify

**What it is:** An independent check of whether the work from stage 3 actually satisfies the loop's goal — ideally performed by a different agent, process, or human than the one that did the work.

**Why it matters:** This is the single most load-bearing stage in the entire lifecycle. Every failure mode this guide warns about — cognitive surrender, verification debt, a loop that's really just a "token-burning furnace" — traces back to a weak or missing verify stage. A loop with a strong trigger, discover, and act stage but no real verification is not a safe loop; it's a system that confidently produces wrong output at scale.

**Design decision here:** What is the actual, machine-checkable bar? Tests passing? A lint check? A second agent's independent read against project skills and existing tests? This has to be decided *before* you build the loop, not discovered after something goes wrong.

---

## 5️⃣ Record

**What it is:** Writing the outcome — what was tried, what passed, what's still open — to persistent state, so the *next* trigger's discover stage has something real to build on.

**Why it matters:** Without this stage, the lifecycle isn't actually a loop — it's the same five stages happening in isolation, over and over, each one blind to what the last one learned. Recording is what turns five stages into a genuine cycle instead of a series of disconnected sprints.

**Design decision here:** What format survives best? A markdown file? A project board like Linear? Both Claude Code and Codex support both approaches — the format matters less than the discipline of actually writing to it every single time, without exception.

---

## 🔁 Why It's Drawn as a Circle, Not a List

The diagram at the top of this file isn't decorative — the arrow looping back from Record to Trigger is the entire point. A one-time script has a start and an end. A loop has a start and a *return*. Every stage exists specifically to make the next cycle through the loop better-informed than the last one — that's genuinely the difference between "I automated a task" and "I engineered a loop."

---

## 🧪 Mini Task

Take the lifecycle diagram above and map it onto something in Godfather Agent's existing 7-layer memory system or your God Mode pipeline. Which of your existing layers already does something like "Discover" (reading prior state)? Which does something like "Record" (writing outcomes forward)? If a stage is missing entirely, that's a concrete, specific place you could formalize into a real loop.

✅ *Expected outcome:* A one-paragraph mapping of your existing system onto these five stages, with at least one honest gap identified.

---

## ➡️ Next

Continue to **`09_Loop_Architecture.md`** to see how these five stages get physically assembled into a working system.

---

*Loop Engineering Complete Guide | Part 8 of 22*
