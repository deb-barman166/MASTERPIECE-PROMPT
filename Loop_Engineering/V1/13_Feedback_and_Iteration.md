# 13 — Feedback and Iteration

> 🎯 *Goal: Understand how a loop actually improves across iterations — not just repeats, but converges toward a goal.*

---

## 🔁 The Difference Between "Repeating" and "Iterating"

This distinction sits right at the heart of what makes something a *loop*, rather than just a repeated task, and it connects directly back to file 05's "recursive goal" concept.

**Repeating** means doing the same thing again, regardless of outcome. A cron job that re-runs an identical script every hour is repeating.

**Iterating** means each pass is informed by the outcome of the previous pass, and moves closer to the goal because of it. This requires feedback — some signal about how the last attempt went — flowing back into the next attempt's starting point.

```
REPEATING:                      ITERATING:
  Run → Run → Run → Run           Run → Check → Adjust → Run → Check → Adjust → Run
  (same input every time)         (each run informed by the last one's outcome)
```

A loop, properly designed, is always the second kind. If yours is doing the first kind, you haven't built a loop yet — you've built a scheduled task that happens to use an AI model.

---

## 📡 Where Feedback Actually Comes From

Feedback in a loop isn't one single thing — it comes from several distinct sources, and a mature loop design draws on more than one of them.

**Verification results (file 08's "Verify" stage).** Did the tests pass? Did the checker sub-agent approve the draft? This is the most direct, most machine-checkable form of feedback, and the one every serious source treats as non-negotiable.

**State comparisons (file 12).** Comparing this run's findings against what state recorded as already-tried gives the loop feedback about *whether it's making progress* across runs, not just within one run — "we had 12 open issues last week, we have 4 now" is a feedback signal about the loop's overall trajectory.

**Human triage input.** When a run routes something to a human triage inbox and that human resolves it a specific way, that resolution is itself a feedback signal — if it's captured properly in state or in an updated skill, future runs can learn from that human judgment instead of hitting the same ambiguous case and escalating it again forever.

**Real-world outcomes.** If a loop opens a PR and that PR later gets reverted, or a drafted fix causes a new bug, that's feedback too — arguably the most valuable and most commonly neglected kind, since it requires the loop's *next* discovery phase to actually check on the downstream consequences of its own past actions, not just whether they were "approved" at the time.

---

## 🔬 A Worked Example: Iteration in Action

Let's trace how feedback actually changes behavior across three passes of the same loop, using a scenario adapted directly from your own work — hardening a cryptographic module, similar to how BLACKCORE evolved through its 38-test suite.

```
PASS 1:
  Goal: "All cryptographic functions in the vault module must pass the
         full security test suite."
  Discovery: 6 of 38 tests failing.
  Action: Sub-agent drafts fixes for all 6.
  Verify: Checker sub-agent runs the suite — 4 now pass, 2 still fail
          because the fix for one function broke a dependent function.
  Record: State updated — "4/6 resolved, 2 regressions introduced by fix
          to encrypt_vault(), needs a different approach."

PASS 2:
  Discovery: Reads state — knows NOT to repeat the same fix approach
             that caused the regression last time.
  Action: Sub-agent tries a different approach for the remaining 2,
          informed specifically by what state recorded as having failed.
  Verify: All 38 tests pass.
  Record: State updated — "38/38 passing. Approach that worked: [details]."

PASS 3 (weeks later, new automation run):
  Discovery: A new test was added to the suite as the project grew.
             State shows the module was previously fully passing, so
             this is flagged as new, not re-litigated as already-solved.
  Action: Sub-agent addresses only the new gap.
```

Notice what made this genuinely *iterative* rather than repetitive: Pass 2 didn't retry Pass 1's failed approach blindly. It used the specific feedback recorded in state — "this approach caused a regression" — to try something different. That's the entire mechanism.

---

## ⚙️ Iteration Needs a Stopping Condition, Not Just a Direction

A loop that iterates forever without a defined stopping point is just as broken as one that doesn't iterate at all — it'll keep consuming tokens indefinitely, even after the goal is genuinely met, or worse, it'll keep "improving" something that was already good enough, chasing marginal gains at real cost.

This ties directly back to file 05's emphasis on a machine-checkable "done" — iteration needs both:

1. **A direction** — feedback that tells it whether the last attempt was closer or further from the goal
2. **A stop condition** — a clear signal that says "the goal is now met, stop iterating"

Without the second, even well-designed feedback just produces a loop that runs indefinitely, technically "iterating" but never actually finishing.

---

## 📊 Feedback Sources Summary

| Feedback Source | What It Tells You | How Fast It Arrives |
|---|---|---|
| Verification results | Did this specific attempt succeed? | Immediate, within the same run |
| State comparisons | Is the loop making progress across runs? | Visible after 2+ runs |
| Human triage resolutions | How should ambiguous cases be handled? | As fast as a human responds |
| Real-world outcomes | Did the "successful" action actually hold up downstream? | Often delayed — requires deliberate follow-up checking |

---

## ➡️ Next

Continue to **`14_Planning_and_Reasoning.md`** to see how an agent decides *what to do* inside each iteration, before feedback even has a chance to kick in.

---

*Loop Engineering Complete Guide | Part 13 of 22*
