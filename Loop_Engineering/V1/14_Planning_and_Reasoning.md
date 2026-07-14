# 14 — Planning and Reasoning

> 🎯 *Goal: Understand how an agent decides what to do inside a single loop iteration — the "thinking" layer that sits between Discover and Act in the lifecycle.*

---

## 🧭 Where This Fits

Look back at file 08's lifecycle diagram: `Trigger → Discover → Act → Verify → Record`. Planning and reasoning happen in the gap between Discover and Act — after the agent has gathered information about what's going on, but before it commits to a specific course of action. This file zooms into that gap specifically.

```
DISCOVER  →  [ PLANNING & REASONING ]  →  ACT
             "given what I found, what's
              the actual next step?"
```

---

## 🤔 Why This Deserves Separate Attention

It's tempting to think of "discover, then act" as one smooth motion — the agent finds a problem, then fixes it. In practice, the space between those two steps is where most of an agent's actual intelligence gets used, and where loop designers have real influence over the quality of outcomes, even though it's the least visible part of the whole system from the outside.

A weak planning step produces a loop that reacts to surface symptoms. A strong planning step produces a loop that identifies root causes, considers multiple approaches, and picks a genuinely appropriate one — closer to what you already push for in your own reverse-thinking-agent and first-principal-thinking skills.

---

## 🧱 What Good Planning Looks Like Inside a Loop

**Grounding in discovered context, not assumption.** The plan should be built from what discovery actually found — the specific CI failures, the specific open issues — not from a generic understanding of "how projects like this usually work." This is where skills (file 10, Part 3) earn their keep: a well-written skill gives the planning step accurate, project-specific grounding instead of forcing the agent to guess at your conventions.

**Considering the goal, not just the immediate symptom.** File 05 emphasized recursive *goals* over recursive *prompts* specifically because of this: a plan built only around "fix this one failing test" might produce a narrow patch, while a plan built around the actual stated goal — "the vault module passes the full security suite" — is more likely to catch that a narrow fix might break something else, the way Pass 1 did in file 13's worked example.

**Scoping correctly for isolation.** If the plan involves multiple independent pieces of work, this is the moment where a good planning step decides to split that work across separate worktrees (file 10, Part 2) rather than attempting several unrelated changes inside one unified checkout, where they're more likely to collide or become harder to verify independently.

**Anticipating what verification will check.** A plan built with zero awareness of how it will be verified tends to produce work that technically does *something*, but not necessarily the specific, checkable thing the verify stage is actually going to test for. Strong planning reasons backward from the "done" condition, not just forward from the discovered problem.

---

## 🔍 A Concrete Comparison: Weak vs. Strong Planning

```
SCENARIO: Discovery found 3 open GitHub issues tagged "bug"

❌ WEAK PLANNING:
   "There are 3 bug issues. I'll fix all 3 in this checkout, one after
   another, and open one PR when done."
   → Doesn't consider that the 3 bugs might be unrelated and independently
     verifiable, so they get bundled into one PR that's harder to review
     and riskier to merge as a single unit.

✅ STRONG PLANNING:
   "There are 3 bug issues. Issue A and Issue B touch unrelated modules
   and can be worked on in parallel, in separate worktrees, verified
   independently. Issue C depends on understanding whether Issue A's fix
   changes a shared function — so I'll resolve A first, then reassess
   whether C's original diagnosis still holds before starting on it."
   → Produces smaller, independently verifiable outcomes, correctly
     sequences a genuine dependency, and avoids polluting one worktree's
     checkout with three unrelated sets of changes.
```

The strong version isn't smarter because it used more words — it's stronger because it reasoned about *dependencies*, *isolation*, and *verifiability* before acting, rather than just listing the discovered problems and working through them mechanically in the order they were found.

---

## ⚙️ Where This Connects to Sub-agents

Planning and reasoning is also where the decision to spawn a **checker sub-agent** (file 10, Part 5) actually gets made, in practice. A strong planning step doesn't just decide *what* to build — it decides *how confident it can be* in verifying that work itself, and calls in independent verification specifically for the parts of the plan where self-assessment would be least trustworthy: security-sensitive changes, changes touching shared dependencies, or anything where the "done" condition is more subjective than a simple test pass.

---

## ⚠️ The Failure Mode Planning Exists to Prevent

Skipping a real planning step and jumping straight from discovery to action is a subtler version of the same mistake described in file 19 as "cognitive surrender" — except here, it's the *loop itself* surrendering to the first plausible-looking action, rather than a human trusting output too readily. A loop that plans well is one that occasionally decides the "obvious" first fix isn't actually the right one, and that judgment is exactly what separates a genuinely useful autonomous system from one that just moves fast in whatever direction discovery happened to point it.

---

## ➡️ Next

Continue to **`15_Tool_and_Function_Calling.md`** to see how, once a plan exists, an agent actually executes it by taking real action in the world.

---

*Loop Engineering Complete Guide | Part 14 of 22*
