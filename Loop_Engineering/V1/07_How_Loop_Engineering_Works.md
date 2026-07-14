# 07 — How Loop Engineering Works

> 🎯 *Goal: See the mechanics in motion — not just the vocabulary, but what actually happens, in order.*

---

## ⚙️ The Mechanical Walkthrough

Let's trace a real, concrete example end to end, using the canonical scenario described across nearly every source on this topic — a daily coding automation. This is deliberately the same example you'll see referenced again in file 18 (Practical Examples), because seeing it once here mechanically, and once there as a build-it-yourself walkthrough, cements it from two angles.

```
Step 1 → An automation fires every morning on schedule
Step 2 → Its prompt calls a "triage" skill
Step 3 → The skill reads yesterday's CI failures, open issues, recent commits
Step 4 → Findings get written to a markdown file (the state)
Step 5 → For each finding worth acting on, an isolated worktree opens
Step 6 → A sub-agent drafts a fix inside that worktree
Step 7 → A second sub-agent reviews the draft against project skills + tests
Step 8 → Connectors open a PR and update the ticket
Step 9 → Anything the loop can't resolve lands in a triage inbox for a human
Step 10 → The state file records what happened, so tomorrow picks up from here
```

Now let's slow down and explain *why* each step exists, not just what it does.

---

## 🔍 Step-by-Step Explanation

**1. The automation fires.** This is the heartbeat — without it, nothing starts. It could be a schedule (every morning), a webhook (a new PR was opened), or a manual trigger. The point is that *something* other than a human typing a message kicks things off.

**2. The prompt calls a skill, not a wall of instructions.** This is a deliberate design choice worth internalizing: instead of pasting the same giant block of instructions into the automation's configuration (which nobody will ever remember to update), the automation fires a short reference to a skill — `$triage-skill` or equivalent. The skill itself lives as a maintainable file elsewhere. Update the skill once; every future automation run picks up the change automatically.

**3–4. Discovery and recording.** The agent gathers the relevant context (what changed, what's failing, what's open) and — critically — writes it down somewhere that survives past this session. This is state creation in action, not just an abstract idea from file 05.

**5. Worktree isolation.** If more than one finding needs action, each gets its own isolated checkout. This prevents the exact failure mode described earlier in this guide: two agents editing the same file is the same headache as two engineers committing to the same lines without talking to each other first.

**6–7. Maker and checker, separated.** One sub-agent drafts. A *different* sub-agent reviews that draft independently, checking it against the project's existing skills and test suite — not just re-reading the same agent's own reasoning back to itself.

**8. Connectors take real-world action.** Once verified, the loop doesn't just report a suggestion — it opens the actual pull request and updates the actual ticket, using plugins/connectors wired into your existing tools.

**9. The escape hatch.** Not everything gets automated end to end, and that's by design, not a failure. Anything ambiguous, high-risk, or outside the loop's competence goes to a human triage inbox instead of being forced through.

**10. The loop closes by writing to memory.** The state file is described, across nearly every serious source on this topic, as "the spine of the whole thing" — it's what lets tomorrow's run know what was already tried, what already passed, and what's still open, instead of starting from zero every single day.

---

## 🎯 The Meta-Point: What You Actually Did

Here's the sentence that captures the entire shift, and it's worth sitting with: **you designed this system one time. You did not prompt any of those ten steps individually.**

That's the whole idea made concrete. Every future morning, this exact sequence runs without you typing a single instruction — because you did the harder work upfront of designing the loop, not the easier-in-the-moment work of manually prompting each step.

---

## 🔄 The Same Mechanics, Generalized

Strip the coding-specific details away and you get a pattern that applies far beyond software:

```
TRIGGER → the automation
DISCOVER → find what needs attention
ACT → do the work, isolated from other parallel work
VERIFY → an independent check, not self-grading
INTEGRATE → take real action via connectors
ESCALATE → anything uncertain goes to a human
RECORD → write the outcome to persistent state
```

This is exactly the lifecycle covered in depth in the next file — file 08 gives this sequence its own dedicated treatment, since it's important enough to deserve one.

---

## ⚠️ Where This Breaks If You Skip a Step

Understanding the mechanics also means understanding what happens when a piece is missing:

| If you skip... | What goes wrong |
|---|---|
| The verification sub-agent (step 7) | You get cognitive surrender — the loop just believes its own output |
| Worktree isolation (step 5) | Parallel agents silently overwrite each other's work |
| The state file (step 10) | Every run starts from zero, re-discovering what yesterday already found |
| The triage escape hatch (step 9) | Edge cases get force-fit through automation instead of flagged, quietly accumulating errors |
| Skills instead of pasted instructions (step 2) | The automation's behavior drifts from your actual project as it evolves, because nobody remembers to update a config buried in a schedule |

---

## ➡️ Next

Continue to **`08_Loop_Lifecycle.md`** for a dedicated, deeper look at this trigger-to-record cycle as its own subject.

---

*Loop Engineering Complete Guide | Part 7 of 22*
