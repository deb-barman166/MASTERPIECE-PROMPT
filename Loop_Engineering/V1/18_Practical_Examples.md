# 18 — Practical Examples

> 🎯 *Goal: Apply everything from files 01–17 by actually building loops — starting simple, ending at something genuinely useful for your own projects.*

---

## 🟢 Beginner Example: A Single-Agent, Goal-Based Loop

**Goal:** Get comfortable with rung 2 of the autonomy ladder (file 11) before touching automation or multi-agent structure at all.

**What you're building:** A loop that keeps refactoring a single, small Python module until it passes a linter and its existing tests — no scheduling, no sub-agents, just one agent, one worktree, one clear stop condition.

**Skills used:** Files 05 (recursive goal), 08 (lifecycle), 11 (goal-based rung)

**Instructions:**

1. Pick one small, self-contained module — a single utility file in RAG_Master or BUTTERFLY, not a whole subsystem.
2. Write a **verifiable** goal statement: not "clean up this file" but something checkable, e.g., "this file has zero pylint warnings and all existing tests for it still pass."
3. Run this as a goal-based invocation (`/goal` in Claude Code, or the equivalent in your own tooling) rather than prompting each individual change yourself.
4. Read the final diff carefully — this is your rung-2 verification habit forming, even though the loop itself decided when to stop.

```python
# A machine-checkable stop condition, expressed as a script the loop
# (or you) can run to decide "done":

import subprocess

def is_done() -> bool:
    lint = subprocess.run(["pylint", "target_module.py"], capture_output=True)
    tests = subprocess.run(["pytest", "test_target_module.py"], capture_output=True)
    return lint.returncode == 0 and tests.returncode == 0
```

✅ **You've succeeded when:** `is_done()` returns `True`, and you actually read and understood every change the loop made to get there — not just trusted the green checkmark.

---

## 🔵 Intermediate Example: A Two-Agent Pipeline with State

**Goal:** Build a real maker-checker pipeline (file 16) with genuine persistent state (file 12) — the first structure in this file that's actually "loop engineering" in the fullest sense, not just an automated single agent session.

**What you're building:** A loop that scans a project directory for TODO comments, drafts a resolution for each one, has a second pass independently verify that resolution against the surrounding code, and records progress in a markdown state file so re-running it doesn't redo already-resolved TODOs.

**Instructions:**

1. Design your state file format first (file 10's pro tip). A simple, working schema:

```markdown
# loop-state.md

## Resolved
- [x] `utils.py:42` — TODO: handle empty input — Resolved 2026-07-10, verified passing

## Still Open
- [ ] `parser.py:118` — TODO: support nested brackets — attempted 2026-07-11, checker rejected (broke test_deep_nesting)

## Rejected / Needs Human
- [ ] `crypto.py:9` — TODO: rotate keys automatically — flagged for human triage, security-sensitive
```

2. Build the Discoverer step: scan for `# TODO` comments not already listed as "Resolved" in state.
3. Build the Maker step: for each open TODO, draft a resolution in an isolated copy of the file (a lightweight stand-in for a real worktree if you're prototyping outside git).
4. Build the Checker step: run the relevant tests against the Maker's draft, independently, before accepting it.
5. Route anything touching security-sensitive files (like `crypto.py`) straight to the "Needs Human" section instead of letting the Checker auto-approve it — this is your Classify & Act pattern (file 17) in miniature.
6. Update `loop-state.md` after every run.

```python
# Simplified pipeline skeleton — the actual maker/checker calls would be
# your LLM API calls; this shows the control flow and state discipline.

def run_pipeline(state_path="loop-state.md"):
    state = load_state(state_path)
    todos = discover_todos(exclude=state["resolved"])

    for todo in todos:
        if is_security_sensitive(todo.file):
            state["needs_human"].append(todo)
            continue

        draft = maker_agent(todo)                 # generates a fix attempt
        verified = checker_agent(draft, todo)      # independent review

        if verified.passed:
            state["resolved"].append(todo)
        else:
            state["still_open"].append((todo, verified.reason))

    save_state(state, state_path)
```

✅ **You've succeeded when:** Running this twice in a row on the same codebase does *not* redo work from the first run — that's your proof the state layer is actually functioning, not just present.

---

## 🔴 Advanced Example: A Scheduled, Multi-Worktree Automation for BUTTERFLY

**Goal:** Assemble everything — all six components (file 10), a real trigger (rung 3, file 11), genuine worktree parallelism (file 16), and a triage escape hatch (file 08) — into something production-shaped.

**What you're building:** A nightly automation for your BUTTERFLY CLI project that checks all 19 modules for newly failing tests since the last commit, fixes what it safely can in parallel isolated worktrees, and leaves anything ambiguous for your morning review.

**Instructions:**

1. **Automation (trigger):** A scheduled job (cron, or your platform's scheduling primitive) that fires nightly and calls a `$butterfly-triage` skill by reference — not pasted instructions.
2. **Skill:** Write `butterfly-triage.md` once, documenting: how BUTTERFLY's test suite is structured, which modules are considered security-sensitive (Fernet key storage, encrypted config), and what "safe to auto-fix" means for this specific project.
3. **Discovery:** Compare current test results against `state.md`'s record of the last known-good run, across all 19 modules.
4. **Worktrees:** For each module with new failures, spin up an isolated worktree — this is where genuine parallelism matters, since fixing module 7's failure shouldn't be able to touch module 14's checkout.
5. **Maker/Checker per worktree:** Draft a fix, verify independently against that module's own tests plus the skill's project conventions.
6. **Connector:** For anything verified, open a real PR against a review branch — never auto-merge to main, regardless of how confident the checker is; that boundary belongs to you, not the loop.
7. **Triage inbox:** Anything touching the modules flagged security-sensitive in the skill routes straight here, unconditionally, no matter what the checker concludes — this is a hard rule, not a suggestion the loop can override.
8. **State update:** Record what was fixed, what's pending your PR review, and what's sitting in triage.

```
NIGHTLY RUN SUMMARY (example state output):
  ✅ 3 modules: new failures found, fixed, verified, PR opened for review
  ⏳ 1 module: fix attempted, checker rejected it twice, escalated to triage
  🔒 1 module: touched key-storage code, routed straight to triage (policy)
  📋 14 modules: no new failures, nothing to do
```

🔥 **Challenge:** Once this runs reliably for a few weeks at rung 3, consider what a genuinely earned rung-4 proactive extension would look like — for instance, the loop noticing that one specific module fails far more often than the others and proactively flagging that as a structural issue worth your attention, rather than just fixing symptoms nightly forever.

---

## ⚠️ A Note Before You Build Any of These For Real

Every example above assumes you've internalized file 19's best practices before running it against a real, important codebase — especially the advanced example. Read that file next, before you point any of this at BLACKCORE, Godfather Agent, or anything else where a wrong unattended action would actually cost you something.

---

## ➡️ Next

Continue to **`19_Best_Practices_and_Common_Mistakes.md`** before building any of the above against real, important projects.

---

*Loop Engineering Complete Guide | Part 18 of 22*
