# 09 — Loop Architecture

> 🎯 *Goal: See how the pieces from files 05–08 fit together as one physical system you could actually diagram and build.*

---

## 🏗️ From Concepts to a System

You now know the mental model (file 05), the vocabulary (file 06), the mechanics of one run (file 07), and the lifecycle across many runs (file 08). This file assembles all of that into an actual architecture diagram — the thing you'd sketch on a whiteboard before writing a line of code.

```
┌──────────────────────────────────────────────────────────────────┐
│                          TRIGGER LAYER                             │
│   Schedule  │  Webhook  │  GitHub Event  │  Manual /goal command   │
└───────────────────────────────┬────────────────────────────────────┘
                                 │
                                 ▼
┌──────────────────────────────────────────────────────────────────┐
│                      ORCHESTRATOR (Main Loop)                      │
│                                                                      │
│   Reads: STATE FILE  ───────────────────────────────┐               │
│   Calls: SKILL (project knowledge, procedures)       │               │
│                                                       │               │
└───────┬───────────────────────────────────┬─────────┼───────────────┘
        │                                   │         │
        ▼                                   ▼         │
┌───────────────────┐             ┌───────────────────┐│
│   WORKTREE A        │             │   WORKTREE B       ││
│   (isolated checkout)│             │   (isolated checkout)│
│                      │             │                      │
│   SUB-AGENT (maker)  │             │   SUB-AGENT (maker)  │
│         │            │             │         │            │
│         ▼            │             │         ▼            │
│   SUB-AGENT (checker)│             │   SUB-AGENT (checker)│
└──────────┬───────────┘             └──────────┬───────────┘
           │                                    │
           ▼                                    ▼
┌──────────────────────────────────────────────────────────────────┐
│                       CONNECTORS / PLUGINS                         │
│      Opens PRs  │  Updates tickets  │  Sends notifications         │
└───────────────────────────────┬────────────────────────────────────┘
                                 │
                    ┌────────────┴────────────┐
                    ▼                          ▼
          ┌──────────────────┐      ┌──────────────────┐
          │   STATE FILE       │      │   TRIAGE INBOX     │
          │   (updated for      │      │   (human review     │
          │    next run)        │      │    for edge cases)  │
          └──────────────────┘      └──────────────────┘
```

---

## 🔍 Reading This Diagram Layer by Layer

**Trigger Layer (top).** This is file 08's "Trigger" stage, made concrete. Notice it's plural — a real system usually has more than one way to start a run, not just a single schedule.

**Orchestrator.** This is the loop's "brain" — the part that reads the state file (what happened before), pulls in the relevant skill (how this project works), and decides what needs to happen this run. Everything below this box is *dispatched* by the orchestrator, not autonomous on its own.

**Parallel worktrees.** Notice there are two side by side. This is the physical answer to the collision problem described in file 07: Worktree A and Worktree B are isolated checkouts, so an agent working inside A cannot accidentally step on files that an agent inside B is editing, even though both are working against the same underlying repository.

**Maker → Checker inside each worktree.** This is file 05's maker-checker principle, drawn as an actual pipeline: the first sub-agent does the work, and a *second, independent* sub-agent reviews it before anything leaves the worktree. Nothing skips this step in a well-architected loop.

**Connectors.** Once verified, this layer is where the loop stops being purely internal and starts taking real action in systems you actually use — opening a real pull request, updating a real ticket, sending a real notification.

**Two exits at the bottom.** This is the important architectural detail many quick explanations skip: **not everything ends up in the same place.** Verified, successful outcomes update the state file so tomorrow's orchestrator knows what happened. Anything the loop couldn't confidently resolve routes to a triage inbox instead — a human checkpoint, not a forced automation.

---

## 🧱 Why the State File Sits *Outside* the Orchestrator Box

Look closely at the diagram: the state file isn't drawn as part of the orchestrator — it's drawn as something the orchestrator *reads from and writes to*, sitting alongside it. This is deliberate and matches how it works in practice. The orchestrator itself is stateless between runs — it's just a process that starts up, does work, and shuts down. All the memory that survives between one run and the next lives in that external file, not in the orchestrator's own "head." This is the direct architectural consequence of the point made back in file 05: the agent forgets between runs; the file doesn't.

---

## 🔀 Two Common Architectural Variants

Real loops don't always look exactly like the diagram above. Two variations you'll run into constantly:

**Single-worktree loops.** For simpler tasks with no parallel work to isolate, you don't need multiple worktree boxes — one orchestrator, one worktree, one maker-checker pair is a completely legitimate, often better, starting architecture. Don't add parallelism you don't need yet.

**Nested loops.** A more advanced pattern: the orchestrator itself can be the trigger for a *smaller* loop nested inside one worktree — for instance, a sub-agent that keeps retrying a failing test up to five times before escalating, which is itself a miniature version of the whole trigger→verify→record cycle, just running at a smaller scale inside a bigger one. This is closely related to the "Dynamic Workflows" pattern covered in file 17.

---

## 📊 Architecture Decision Table

| Question | If Yes → | If No → |
|---|---|---|
| Will multiple things be worked on in the same run? | Add worktree isolation | Single worktree is fine |
| Does a wrong output carry real risk (money, security, breaking prod)? | Require human triage before connectors act | Automated connector action may be acceptable |
| Will this loop run more than once, ever? | State file is mandatory | A one-off script may be all you need — you may not need a loop at all |
| Is the "done" condition genuinely machine-checkable? | Proceed to goal-based automation | Stay at turn-based (see file 11) until you can define one |

---

## ➡️ Next

Continue to **`10_Core_Components.md`** for a dedicated, deep dive into each of the six building blocks shown in this diagram.

---

*Loop Engineering Complete Guide | Part 9 of 22*
