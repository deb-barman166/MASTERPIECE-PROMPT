# 15 — Tool and Function Calling

> 🎯 *Goal: Understand the actual mechanism by which a loop takes real action — turning a plan into something that touches real files, real APIs, real systems.*

---

## 🛠️ Where This Fits

If planning (file 14) is the "what should I do" step, tool calling is the "actually doing it" step — the literal mechanism inside the `Act` stage of the lifecycle (file 08). This isn't a new concept for you specifically — function/tool calling is foundational to everything you've already built in Godfather Agent, and this file exists to connect that existing knowledge specifically to how it operates *within* a loop, as opposed to within a single one-off agent session.

---

## 🔩 The Basic Mechanism, Refresher

At its core, tool calling is simple: the model, instead of just producing text, produces a structured request to run a specific function with specific arguments — write this file, run this command, call this API. Something executes that request, and the result gets fed back to the model, which then decides its next action based on that result. This is the same "LLM in a loop, within one session" mechanism described back in file 04 as the foundation of agentic engineering generally.

```
MODEL → "I want to call function: run_tests()"
         ↓
EXECUTOR → actually runs the test suite
         ↓
RESULT → "38 passed, 0 failed" fed back to the model
         ↓
MODEL → decides next action based on that real result
```

---

## 🔄 What Changes When This Happens *Inside* a Loop

The mechanism itself doesn't change between a one-off session and a loop iteration — but three things about *how it's used* change meaningfully, and this is the part worth focusing on.

**1. Tool calls need to be idempotent-aware.** In a single conversation, you'd notice if the model tried to run the exact same fix twice. Inside a loop that might run the same discovery-to-action cycle daily, a tool call that isn't aware of what already happened (thanks to state, file 12) risks redundant or even harmful repeated actions — re-opening a PR that already exists, for instance, or re-sending a notification about an issue that was already resolved.

**2. Tool calls increasingly go through connectors, not raw scripts.** File 10's Part 4 covered this from the architecture side; here's the mechanical version — a tool call to "open a pull request" or "update a Linear ticket" inside a loop is typically routed through an MCP-based connector rather than a hand-rolled API integration, specifically because connectors are built to be reused consistently across every automation that needs them, rather than re-implemented per-loop.

**3. Tool calls need permission boundaries that match the autonomy rung.** Recall file 11's four-rung ladder — a turn-based loop can reasonably have a tool call that does something risky, because a human reviews it before the next step happens anyway. A time-based or proactive loop running unattended at 2 AM absolutely cannot have that same permission level without a verification gate (file 08's Verify stage) sitting between the tool call being proposed and it actually executing against a real system.

---

## 🎯 Read-Actions vs. Write-Actions: The Distinction That Matters Most

This is the single most important practical distinction for safely using tool calling inside a loop, and it's worth committing to memory as its own rule, separate from everything else in this file.

**Read-actions** (checking a ticket's status, running a test suite to see results, fetching a file's contents) are low-risk. They don't change anything in the outside world — they just gather information. A loop can generally be trusted with these at almost any autonomy rung.

**Write-actions** (opening a PR, closing a ticket, sending an email, merging code, deleting a file) actually change something real. These are exactly the actions that should sit behind the verify stage, and exactly the actions where the autonomy-rung permission boundary from point 3 above matters most.

```
✅ Generally safe at any rung:        ⚠️ Requires verification gate:
   - Read a file                          - Write/edit a file
   - Run tests (read-only outcome)        - Open a PR
   - Search for open issues               - Merge code
   - Check a ticket's status              - Close/update a ticket
   - Fetch API data                       - Send a notification/email
```

---

## 🧩 How This Connects Back to Sub-agents

This distinction is also *why* the maker-checker split (file 10, Part 5) exists specifically around tool calling, not just around reasoning quality. The maker sub-agent's tool calls, inside its isolated worktree, are typically scoped to read and *local write* actions only — editing files within its own checkout. The actual connector-layer write-actions that touch the outside world — the real PR, the real ticket update — often happen only *after* the checker sub-agent has independently verified the maker's work, precisely so that a flawed first attempt never gets the chance to take an irreversible external action before a second, independent pass has looked at it.

---

## ⚠️ A Practical Warning Specific to Multi-Provider Setups

Since you already work across NVIDIA NIM, HuggingFace, OpenRouter, and Ollama in BUTTERFLY's multi-provider support — worth flagging explicitly: **not all models implement tool/function calling identically**, and this becomes a real loop-engineering concern, not just an API-compatibility concern, the moment you're running an unattended automation. A model that silently drops a tool call, hallucinates a function that doesn't exist, or formats arguments incorrectly can cause a loop to either fail loudly (annoying but safe) or, worse, fail *silently* — appearing to complete a step it never actually took, which state (file 12) would then incorrectly record as done. If you're building loops across multiple providers, this is a strong argument for keeping the verify stage's checks grounded in *actual observed outcomes* (did the file really change, did the test really run) rather than trusting the model's own report that it called a tool successfully.

---

## ➡️ Next

Continue to **`16_AI_Agents_and_Multi_Agent_Loops.md`** to see how multiple tool-calling agents, each running their own mini-loop, get orchestrated together into one larger system.

---

*Loop Engineering Complete Guide | Part 15 of 22*
