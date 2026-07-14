# 10 — Core Components

> 🎯 *Goal: Understand ALL six building blocks of a loop — nothing hidden. This is the most important file in the guide; everything before it builds toward this, and everything after it assumes you know this cold.*

---

## 🧩 The Six Blocks, Named

Every credible source on loop engineering converges on the same anatomy, first laid out formally by Addy Osmani: **five active building blocks, plus one that ties them all together.**

```
Automation → Worktree → Skill → Plugin/Connector → Sub-agent
                                                          │
                                                          ▼
                                                       State
                                              (the sixth, binding block)
```

Let's take each one seriously, on its own, with real mechanics — not just a one-line definition (you already have those in file 06).

---

## Part 1: Automation

**What it is:** The mechanism that gives a loop a heartbeat — a schedule, trigger, or event that starts a run.

**Why it matters:** Without this, you don't have a loop. You have a script you run manually, which is just prompt engineering with extra steps.

**How it works in practice:** In Codex, you configure this in an Automations tab — picking the project, the prompt it runs, how often, and whether it runs on your local checkout or a background worktree. Runs that find something worth attention route to a triage inbox; runs that find nothing simply archive themselves. In Claude Code, the same capability is reached through scheduling and hooks — `/loop` for an in-session recurring prompt, `/schedule` for a persistent scheduled task, or a Routine that triggers on a schedule, webhook, or GitHub event.

```
Real internal use case: OpenAI uses automations for boring, recurring work —
daily issue triage, summarizing CI failures, writing commit briefings,
hunting for bugs someone introduced last week.
```

**Design note:** An automation should call a *skill* by reference (see Part 3), not have a giant wall of instructions pasted directly into its own configuration. Otherwise you end up with critical logic buried in a schedule config that nobody remembers to update as the project evolves.

---

## Part 2: Worktree

**What it is:** An isolated working directory on its own branch, sharing the same repository history, so that one agent's edits cannot touch another agent's checkout.

**Why it matters:** The moment you run more than one agent at once, files start colliding — and that collision is the exact same headache as two engineers committing to the same lines of code without ever talking to each other first. A worktree fixes this mechanically, not through coordination or hope.

**How it works in practice:** Codex builds worktree support directly into the product, so several parallel threads can hit the same repository at once without bumping into each other. Claude Code gives you the same isolation through the standard `git worktree` mechanism, a `--worktree` flag to open a session in its own checkout, and an `isolation: worktree` setting you can attach to a sub-agent so each helper gets a fresh, self-cleaning checkout.

**Design note — the honest caveat:** Worktrees solve the *mechanical* collision problem. They do not solve the human bottleneck underneath it: your own review bandwidth is still the actual ceiling on how many parallel agents you can responsibly run, regardless of how well-isolated their checkouts are. This is sometimes called the "orchestration tax" — the tooling removes the technical collision, but you're still the limiting factor on how much you can actually oversee.

---

## Part 3: Skill

**What it is:** Written-down project knowledge — conventions, build steps, domain expertise — stored externally so an agent doesn't have to re-infer it from scratch on every single run.

**Why it matters:** Without skills, every loop iteration starts from zero context about *how your project actually works*, which is slow, expensive, and inconsistent. With a skill, you write the knowledge down once, and every future run — across every automation that references it — benefits from that same, maintained source of truth.

**How it works in practice:** Both major tools use the same `SKILL.md` format, which is worth pausing on — it's a genuinely convergent standard, not a proprietary lock-in feature of one vendor. This is directly relevant to you: you've already built and packaged multiple skills yourself (reverse-thinking-agent, second-order-thinking, systems-thinking-verify, critical-thinking, and this very guide came from your own md-masterpiece-generator skill). You're not learning a new concept here — you're learning that the thing you've already been doing has a formal name and a formal place in a larger architecture.

**Design note:** A skill should encode the *procedure*, not the specific one-off task. "How this project runs its test suite" is a skill. "Fix bug #4471" is a one-time instruction, not a skill.

---

## Part 4: Plugin / Connector

**What it is:** The wiring that lets a loop reach out into tools and systems you already use — issue trackers, chat platforms, calendars, databases — rather than staying purely internal to the agent's own sandbox.

**Why it matters:** A loop that can discover problems and draft fixes but can't actually open a PR, update a ticket, or send a notification isn't finishing the job — it's just doing internal thinking that a human still has to manually carry the rest of the way.

**How it works in practice:** Connectors in both major tools today are built predominantly on MCP (Model Context Protocol), the standardized way for an agent to reach external services regardless of the underlying model. A concrete example: both the Codex app and Claude Code can link to a project management tool like Linear — Codex via markdown or a direct connector, Claude Code via an `AGENTS.md` reference file, progress files, or MCP directly.

**Design note:** This is also your biggest real-world risk surface. A connector that can *read* a ticket is low-risk. A connector that can *close* a ticket, merge a PR, or send an email on your behalf is a very different level of trust — and should usually sit behind a verification step (Part 5) before it fires, not before automation-first without review.

---

## Part 5: Sub-agent

**What it is:** A separate, distinct agent instance spawned by the main loop, typically to divide labor or to independently verify another agent's work.

**Why it matters:** This is the mechanism that makes the maker-checker principle (file 05) physically real instead of just a nice idea. One sub-agent has the idea and does the work. A *different* sub-agent checks it — against project skills, against existing tests, against the original goal — independently.

**How it works in practice:** In a full daily-triage loop, this looks like: one sub-agent drafts a fix inside an isolated worktree, and a second sub-agent reviews that draft against the project's skills and existing tests before anything moves to the connector layer. Claude Code's more advanced "Dynamic Workflows" feature formalizes several named patterns for orchestrating multiple sub-agents deterministically — covered fully in file 17.

**Design note:** Sub-agents are the most expensive block in terms of token cost, because you're running multiple full agent passes instead of one. This is exactly where the cost warnings from file 03 bite hardest — every additional sub-agent in a pipeline is a real, compounding expense, which is why Steinberger's advice to throttle automation *frequency* (hourly or daily instead of continuous) matters even more once sub-agents are in the mix.

---

## Part 6: State — The Binding Block

**What it is:** Persistent memory that lives outside any single conversation — a markdown file, a project board like Linear, or any equivalent — recording what's been tried, what passed, and what remains open.

**Why it matters:** This is described, consistently, as "the spine of the whole thing." Every other block in this list can function correctly in isolation and *still* produce a broken system if state is missing, because without it, every single run starts from zero — rediscovering yesterday's already-solved problems, redoing already-verified work, and never actually accumulating progress across runs.

**How it works in practice:** The underlying reason state has to live *outside* the agent is simple and worth restating precisely: the model forgets everything between runs, so memory has to be on disk, not in context. Whether it's a markdown file or a Linear board matters far less than the discipline of writing to it, reliably, every single time a run completes.

**Design note:** This is why state is drawn as the *sixth* block, sitting apart from the other five in most diagrams (including file 09's architecture diagram) — it's not parallel to automation, worktrees, skills, connectors, and sub-agents. It's the thread that ties all of their outputs together across time.

---

## 📊 Full Overview Table

| Component | Purpose | Key Detail |
|---|---|---|
| Automation | Gives the loop a heartbeat | Should call a skill by reference, not embed instructions directly |
| Worktree | Isolates parallel work | Solves the mechanical collision problem; doesn't solve the human review bottleneck |
| Skill | Reusable project knowledge | Same `SKILL.md` format used across both major tools |
| Plugin / Connector | Real-world action, usually via MCP | Biggest risk surface — gate write-actions behind verification |
| Sub-agent | Division of labor + independent verification | Most token-expensive block; makes maker-checker real |
| State | Persistent cross-run memory | The spine of the system — everything else depends on this working |

---

## 🔥 Pro Tip: Build in This Order

If you're building your first real loop, the natural instinct is to start with automation (the exciting, visible part) and bolt state on at the end as an afterthought. Do the opposite: **design your state format first.** Decide exactly what "what's been done, what's still open" looks like as a file, before you write a single trigger. Every other block becomes dramatically easier to design correctly once you know precisely what it's reading from and writing to.

---

## ➡️ Next

Continue to **`11_Types_of_Loops.md`** to see how these six components combine differently depending on how much autonomy a given loop actually needs.

---

*Loop Engineering Complete Guide | Part 10 of 22*
