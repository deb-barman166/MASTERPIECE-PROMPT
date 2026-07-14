# 19 — Best Practices and Common Mistakes

> 🎯 *Goal: Avoid the traps that catch nearly everyone building their first real loops — every mistake below has already been named and documented by people who found it the hard way.*

---

## ⚠️ Mistake 1: Skipping Rungs on the Autonomy Ladder

**Why it happens:** Rung 3 and 4 (time-based, proactive) are the exciting, headline-grabbing parts of loop engineering — "it just runs on its own now!" It's tempting to build straight to that from a standing start.

**What goes wrong:** A flawed "done" condition or a weak checker sub-agent, discovered at rung 2 where you're watching each run, costs you one wasted attempt to fix. The exact same flaw, undiscovered until it's running unattended every night at rung 3, can silently produce weeks of wrong outcomes before anyone notices.

```
# ❌ Wrong way:
Build the full nightly automation from file 18's advanced example
on day one, against your most important repo, unsupervised from the start.

# ✅ Right way:
Prove the goal-based version (rung 2) manually, several times, watching
every outcome closely. Only then wrap it in a schedule.
```

**The Fix:** Climb the ladder from file 11 in order, every time, for every new loop — even ones that feel similar to loops you've already validated. Each new goal condition or new codebase deserves its own trip through rung 2 before it earns rung 3.

---

## ⚠️ Mistake 2: Treating "Completed" as Proof Instead of a Claim

**Why it happens:** When a loop consistently produces correct-looking output over many runs, it's psychologically easy to stop reading closely — this is cognitive surrender (file 06), and it creeps in gradually, not all at once.

**What goes wrong:** The "completed" flag an agent produces is a self-report, not independent evidence. Without a real checker stage actually verifying against tests or standards, a loop that says "done" and a loop that's actually correct are two different things that happen to look identical from the outside — right up until they aren't.

**The Fix:** The verify stage (file 08) is never optional, and it's never satisfied by the same agent that did the work simply re-stating that it's finished. If you notice yourself reading a loop's summary instead of its actual diff, that's the specific moment to slow down.

---

## ⚠️ Mistake 3: No Hard Retry Limit on Iterative Patterns

**Why it happens:** "Loop Until Done" (file 17, pattern 5) feels safe because it's *supposed* to stop once the condition is met — so a retry limit can feel like an unnecessary extra step.

**What goes wrong:** If the condition is subtly unreachable — a flaky test, a genuinely contradictory requirement — an unlimited retry loop doesn't fail gracefully. It just keeps consuming tokens, indefinitely, until someone notices the bill or the process manually.

```
# ❌ Wrong way:
while not is_done():
    attempt_fix()  # no limit — could run forever against an unreachable goal

# ✅ Right way:
MAX_ATTEMPTS = 5
for attempt in range(MAX_ATTEMPTS):
    if is_done():
        break
    attempt_fix()
else:
    escalate_to_human_triage()  # explicit, defined exit
```

**The Fix:** Every retrying pattern needs both a stop-on-success condition *and* a stop-on-failure condition (a max attempt count), with the failure path routing to a defined human triage inbox — never silently, never indefinitely.

---

## ⚠️ Mistake 4: Bundling Independent Work Into One Worktree

**Why it happens:** Setting up multiple isolated worktrees feels like more overhead than just handling several findings sequentially in one checkout.

**What goes wrong:** As covered directly in file 09 and file 16, two agents (or even one agent handling two unrelated tasks in sequence within the same checkout) editing overlapping files without isolation reproduces the exact "two engineers committing to the same lines" collision problem worktrees exist specifically to prevent.

**The Fix:** Default to one worktree per independent unit of work, even when it feels like overkill for small tasks. The cost of an unnecessary worktree is small; the cost of a silent file collision discovered late is not.

---

## ⚠️ Mistake 5: Pasting Instructions Instead of Referencing a Skill

**Why it happens:** For a quick, one-off automation, writing the instructions directly into the automation's own config feels faster than the extra step of formalizing a separate skill file.

**What goes wrong:** As your project evolves — conventions change, new modules get added, security policies shift — nobody remembers to go back and update instructions buried inside an automation's schedule config. The automation silently drifts out of sync with how the project actually works.

**The Fix:** Automations should call skills by reference (file 10, Part 1 and Part 3). Update the skill once; every automation referencing it benefits immediately, and the knowledge lives somewhere you'll actually think to update it.

---

## ⚠️ Mistake 6: No Machine-Checkable Definition of Done

**Why it happens:** Some tasks genuinely feel subjective — "improve this," "clean this up" — and it's easier to just launch a loop with a vague goal than to do the harder work of operationalizing it into something checkable.

**What goes wrong:** A loop can't verify against a fuzzy goal. Without something concrete to check, the verify stage either doesn't function at all, or ends up relying on the same kind of unverified self-assessment that Mistake 2 warns against.

**The Fix:** If you can't state the goal as something a script (or an independent second agent) could check without ambiguity, you're not ready to build a loop for it yet — go back to turn-based (rung 1) until you can define one, exactly as file 05's mini task was designed to make you practice.

---

## ⚠️ Mistake 7: Ignoring the Real-World Feedback Loop

**Why it happens:** Once a checker approves an output and a connector ships it, it's tempting to consider that finding fully closed.

**What goes wrong:** As file 13 covered, real-world outcomes are a genuine feedback source that's easy to neglect — a "verified, approved" fix can still get reverted, or cause a downstream bug that only appears later. If nothing checks on the *downstream* consequences of past actions, the loop never actually learns from its real mistakes, only its immediately-caught ones.

**The Fix:** Have discovery periodically check on the actual status of past "resolved" items recorded in state — was that PR merged and kept, or reverted? — not just treat "resolved" as a permanently closed book the moment it's written.

---

## 🔥 Pro Tips: What Separates Good Loop Design From Great Loop Design

**💎 Design state before automation.** Repeated from file 10 because it's worth repeating: knowing exactly what "what was tried, what passed, what's still open" looks like as a concrete file format makes every other component easier to build correctly.

**💎 Reserve expensive patterns for expensive stakes.** Tournament and Deep Verification (file 17) exist for the genuinely high-stakes minority of decisions in a loop — applying them everywhere is a common way loops become needlessly expensive without a matching increase in quality where it doesn't matter as much.

**💎 Keep a human boundary that the loop cannot override.** File 18's advanced example hard-codes "security-sensitive modules always go to triage, regardless of what the checker concludes." Every serious loop should have at least one boundary like this — a rule the loop's own reasoning can't talk itself out of, no matter how confident a given run's checker is.

**💎 Throttle before you scale sub-agents.** If cost becomes a real concern, adjusting *frequency* (file 03's hourly-vs-continuous point) is usually a cheaper lever to pull than removing the maker-checker separation or the verification depth that keeps a loop trustworthy.

---

## 📊 Mistakes Summary Table

| Mistake | Root Cause | The Fix |
|---|---|---|
| Skipping autonomy rungs | Excitement about full automation | Climb the ladder in order, every new loop |
| Trusting "completed" as proof | Cognitive surrender over many correct runs | Independent verification, always |
| No retry limit | Assuming the condition is always reachable | Hard max attempts + defined escalation |
| Bundled worktrees | Setup feels like overhead | Default to one worktree per independent unit |
| Pasted instructions, not skills | Feels faster for one-off automations | Reference skills; update once, benefit everywhere |
| Vague "done" conditions | Some goals feel inherently subjective | Operationalize into something checkable, or stay at rung 1 |
| Ignoring downstream outcomes | "Verified" feels like a permanent closed book | Periodically re-check past "resolved" items |

---

## ➡️ Next

Continue to **`20_Comparison_with_Other_Approaches.md`** to see exactly how loop engineering relates to (and differs from) the other engineering disciplines you already know.

---

*Loop Engineering Complete Guide | Part 19 of 22*
