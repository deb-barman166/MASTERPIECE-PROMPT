# 20 — Comparison with Other Engineering Approaches

> 🎯 *Goal: Place loop engineering precisely relative to the other disciplines you already know, so you know exactly when to reach for each one.*

---

## 🆚 Loop Engineering vs. Prompt Engineering

This is the comparison the entire field organizes itself around, so it's worth stating with maximum precision, building on file 02's definition.

**Prompt engineering** optimizes a single, hand-written instruction, for a single turn, where a human decides both the content of the instruction and when it gets sent.

**Loop engineering** optimizes the autonomous *system* that decides what to prompt, when to prompt it, and whether the resulting output is acceptable — the human's role moves from "author of each instruction" to "designer of the system that authors instructions."

```
PROMPT ENGINEERING:                    LOOP ENGINEERING:
  Human writes prompt                    Human designs the system, once
  Human sends it                         System decides what to prompt
  Human reads response                   System verifies its own output
  Human writes next prompt   ←──────┐    System records outcome and repeats
  (repeat, manually, forever)       └────(only intervenes at triage points)
```

**When each is still the right tool:** Prompt engineering remains the right approach for genuinely one-off tasks, exploratory work where you don't yet know what "done" looks like, and any turn-based (rung 1) interaction where you specifically want to review each step. Loop engineering is not a strictly "better" successor — it's the right tool once a task is recurring, well-understood enough to define a machine-checkable goal, and worth the upfront design cost of building the system around it.

---

## 🆚 Loop Engineering vs. Agentic Engineering

File 04 already covered the historical relationship between these — worth restating as a direct comparison here.

**Agentic engineering** is the broader discipline: can this system reliably get a goal done end to end, covering evaluation systems, multi-agent collaboration, memory architecture, and model routing at a fairly macro level.

**Loop engineering** is narrower and more specific: how does a single agent (or a small orchestrated set of them) decide when to fire, what it sees when it runs, and when it stops — the mechanics of the loop itself, not the entire system surrounding it.

A useful way to hold this: agentic engineering is the *what* (can this system achieve goals autonomously at all), and loop engineering is a specific, critical slice of the *how* (the actual trigger-discover-act-verify-record mechanics that make sustained autonomy possible over time, rather than just within one session).

---

## 🆚 Loop Engineering vs. Traditional Software Automation (Cron Jobs, CI/CD)

This comparison matters because, on the surface, "an automation that runs on a schedule and takes action" sounds a lot like things you've already built without any AI involved at all.

**Traditional automation** (a cron job, a CI/CD pipeline) executes a fixed, deterministic sequence of steps every time — same input, same steps, same output, by design. Its reliability comes precisely from *not* varying its behavior.

**Loop engineering** deliberately introduces adaptive, model-driven reasoning into that same "runs on a schedule" shape — the whole point of file 05's "recursive goal, not recursive prompt" distinction is that the actual steps taken can differ meaningfully from run to run, based on what's discovered and what feedback (file 13) says about prior attempts.

**The honest trade-off:** Traditional automation is more predictable and cheaper, but can only handle situations its authors explicitly anticipated. A loop can handle genuinely novel situations within its goal's scope, but at the cost of the predictability, cost-control, and verification discipline this entire guide has spent 19 files building up — you're trading determinism for adaptability, and that trade only pays off when the situations really do vary enough to need it.

---

## 🆚 Loop Engineering vs. Traditional Workflow Automation Tools (Zapier-style)

**Workflow automation tools** connect triggers to actions through fixed, pre-defined logic — "when X happens, do Y" — with no reasoning step in between deciding *whether* Y is actually the right response to this specific instance of X.

**Loop engineering** inserts genuine reasoning (file 14) and independent verification (file 08) between trigger and action — the system doesn't just mechanically execute a pre-wired response; it evaluates the specific situation and decides what response is actually appropriate, then checks that decision before acting on it.

This is a meaningful upgrade in capability for situations with real variation, but it's also why loop engineering carries the cost and risk profile discussed throughout files 03 and 19, in a way simple "if this then that" automation never does — reasoning and verification aren't free, and a workflow tool's fixed logic, while less flexible, is also far cheaper and more predictable for genuinely simple, unvarying triggers.

---

## 📊 Full Comparison Table

| Approach | Human's Role | Adaptability | Cost | Predictability |
|---|---|---|---|---|
| Prompt engineering | Authors every instruction | High (human judgment each time) | Low per-instance | High (human-controlled) |
| Agentic engineering | Designs the overall system | High (within one session) | Medium | Medium |
| Loop engineering | Designs the recurring system | High (across many runs, over time) | Medium–High | Medium (bounded by verification quality) |
| Traditional automation (cron/CI) | Writes fixed logic once | None — same steps every time | Low | Very high |
| Workflow tools (Zapier-style) | Wires fixed trigger→action rules | Low — no reasoning step | Low | High |

---

## 🎯 The One Question That Tells You Which to Use

If you're ever unsure which discipline actually fits a given task, ask this single question: **"Does the right response to this trigger vary meaningfully based on the specific details of what's discovered, in a way I can't fully anticipate and hard-code in advance?"**

- **No** → traditional automation or a workflow tool. Cheaper, more predictable, and just as effective for genuinely fixed logic.
- **Yes, but I'll review every response myself** → prompt engineering, turn-based (rung 1).
- **Yes, and I can define a machine-checkable "done," but I still want to trigger it myself each time** → goal-based loop engineering (rung 2).
- **Yes, and I trust the goal condition enough to let it run unattended** → time-based or proactive loop engineering (rungs 3–4).

---

## ➡️ Next

Continue to **`21_Real_World_Use_Cases.md`** to see who's actually applying all of this today, and in what domains.

---

*Loop Engineering Complete Guide | Part 20 of 22*
