# 17 — Loop Design Patterns & Diagrams

> 🎯 *Goal: Learn the formally named orchestration patterns you can reach for by name, each with a diagram, so you're not reinventing structure from scratch every time.*

---

## 📚 Where These Patterns Come From

Claude Code's "Dynamic Workflows" feature formalizes several of these as deterministic, script-defined sequences of sub-agent calls — meaning the *sequence itself* is fixed code, not something the model has to reason its way into fresh each time. That distinction matters: a Dynamic Workflow is predictable and auditable in a way that "just ask the agent to figure out the right approach each time" isn't. The patterns below are described generally enough to implement in any framework, including your own.

---

## 🔀 Pattern 1: Fan-out & Synthesize

**Shape:** One task splits into several independent sub-tasks, run in parallel, then recombined into a single coherent result.

```
                    ┌──→ [ Sub-agent A ] ──┐
[ Orchestrator ] ───┼──→ [ Sub-agent B ] ──┼──→ [ Synthesizer ] ──→ Final output
                    └──→ [ Sub-agent C ] ──┘
```

**When to use it:** The discovered work genuinely splits into independent pieces — three unrelated bugs, three separate documents to summarize — where working on them in parallel, each in its own worktree, is faster than sequential handling, and the pieces don't depend on each other.

**Watch out for:** Forcing fan-out onto work that *isn't* actually independent (recall file 14's example of Issue C depending on Issue A) produces a synthesis step that has to untangle conflicting or redundant changes — often more expensive than just running it as a pipeline in the first place.

---

## 🚦 Pattern 2: Classify & Act

**Shape:** An initial classification step routes each discovered item down a different path depending on its type, rather than treating everything with the same procedure.

```
[ Discovery ] → [ Classifier ] ──→ "bug"     → [ Bug-fix sub-agent  ]
                               ──→ "feature"  → [ Feature sub-agent  ]
                               ──→ "question" → [ Human triage inbox ]
```

**When to use it:** Discovered work is heterogeneous — not every finding deserves the same treatment. This maps directly onto the daily-triage example run through files 07–09: not every finding gets a fix drafted automatically; some genuinely belong straight in the triage inbox.

**Watch out for:** A weak classifier is worse than no classifier — misrouting a genuine bug to the "question, needs human" path wastes a human's time, and misrouting an ambiguous edge case to the "bug, auto-fix" path is exactly the setup for a wrong, unverified action shipping. The classification step itself often deserves its own verification pass for anything high-stakes.

---

## ⛓️ Pattern 3: Pipeline

**Shape:** A fixed sequence where each stage's output becomes the next stage's input.

```
[ Discoverer ] → [ Maker ] → [ Checker ] → [ Connector ]
```

**When to use it:** This is the default shape for most real loops, and it's the exact pattern the canonical daily-triage automation follows throughout files 07–10. Use this as your starting structure and only add fan-out or classification on top of it once you've confirmed the simple pipeline version actually works.

**Watch out for:** A pipeline with no branch for uncertainty forces every item through the same fixed sequence, including cases the Maker genuinely can't handle well — which is why the triage-inbox escape hatch (file 07, step 9) exists as an exit ramp *off* the pipeline, not a dead end within it.

---

## 🏆 Pattern 4: Tournament

**Shape:** Multiple sub-agents attempt the *same* task independently, using different approaches, and a judging step picks the best result rather than combining them.

```
                    ┌──→ [ Approach A ] ──┐
[ Same task ] ──────┼──→ [ Approach B ] ──┼──→ [ Judge ] ──→ Best result chosen
                    └──→ [ Approach C ] ──┘
```

**When to use it:** High-stakes tasks where a single attempt's quality is genuinely uncertain, and running the same problem through structurally different approaches (different reasoning strategies, different sub-skills) is worth the extra token cost to get a materially better outcome than any single attempt would produce alone.

**Watch out for:** This is the most expensive pattern per outcome by a wide margin — you're paying for N full attempts to get one result, plus a judging pass. Reserve it specifically for the highest-stakes decisions in a loop, not routine work.

---

## 🔁 Pattern 5: Loop Until Done

**Shape:** A single sub-agent retries the same step repeatedly, with feedback from each failed attempt informing the next one, until a condition is met or a retry limit is hit.

```
[ Attempt ] → fail → [ Attempt + feedback ] → fail → [ Attempt + feedback ] → pass ✅
                                                    (or: hit retry limit → escalate)
```

**When to use it:** This is the "nested loop" idea previewed back in file 09 — a smaller loop-within-a-loop, most naturally suited to something like a failing test that needs a few genuine attempts to resolve correctly, using exactly the iteration mechanics covered in file 13's worked example.

**Watch out for:** Without a hard retry limit, this pattern is the single most direct route to a runaway, token-burning process. Always pair "loop until done" with an explicit maximum attempt count and a defined escalation path (triage inbox) for when that limit is reached without success.

---

## 🔬 Pattern 6: Deep Verification

**Shape:** A dedicated, multi-step verification sub-agent that doesn't just check a single condition, but runs a genuinely thorough review — cross-referencing multiple skills, running multiple test categories, checking for side effects — before anything is allowed through to the connector layer.

```
[ Maker's output ] → [ Test suite check ] → [ Skill compliance check ] →
                      [ Side-effect scan ] → [ Final approval ] → Connector
```

**When to use it:** The highest-stakes write-actions in a loop — anything touching security, payments, or irreversible external actions — where a single pass/fail check from an ordinary Checker sub-agent isn't a thorough enough bar.

**Watch out for:** This is genuinely slow and expensive by design — that's the entire point. Don't apply Deep Verification uniformly to every action in a loop; reserve it for the subset of actions where the cost of a wrong outcome clearly outweighs the cost of a slower, more thorough check.

---

## 📊 Pattern Selection Table

| Pattern | Best For | Cost | Complexity |
|---|---|---|---|
| Fan-out & Synthesize | Genuinely independent parallel work | Medium | Medium |
| Classify & Act | Heterogeneous discovered items | Low–Medium | Low |
| Pipeline | Most default loop structures | Low | Low |
| Tournament | Single high-stakes decisions | High | Medium |
| Loop Until Done | Retryable, well-defined single steps | Low–Medium (with a hard limit) | Low |
| Deep Verification | Highest-stakes write-actions only | High | High |

---

## 🧪 Mini Task

Look back at your BUTTERFLY CLI's skill-importing feature. If you were to build a loop that automatically checks newly-imported skills for structural validity against your existing skill format, which single pattern from this file fits best — and why? (Hint: think about whether imported skills are independent of each other, and how much verification depth a malformed skill actually warrants before it's trusted.)

✅ *Expected outcome:* A one-pattern choice with a one-sentence justification tied to the actual characteristics of the task, not just picking the most sophisticated-sounding option.

---

## ➡️ Next

Continue to **`18_Practical_Examples.md`** to build one of these patterns yourself, from scratch, in full detail.

---

*Loop Engineering Complete Guide | Part 17 of 22*
