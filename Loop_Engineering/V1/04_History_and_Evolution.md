# 04 — History and Evolution

---

## 🗺️ The Big Picture Timeline

Loop engineering didn't appear out of nowhere. It's the latest stage in a fairly clean progression, and understanding that progression makes the current moment much easier to reason about.

```
PROMPT ENGINEERING
    ↓  (agents get tool access + can act, not just answer)
AGENTIC ENGINEERING
    ↓  (agents get reliable enough to run unsupervised for hours)
LOOP ENGINEERING
    ↓  (still forming — see file 22 for where this goes next)
???
```

Let's walk through each stage properly.

---

## 1️⃣ Stage One: Prompt Engineering

For years, the dominant skill in working with LLMs was **prompt engineering** — the craft of writing a single, well-structured instruction to get the best possible one-shot response. Techniques like few-shot examples, chain-of-thought instructions, and structured output formatting all belong to this era.

The defining trait of this stage: **a human wrote every prompt, one at a time, for every interaction.** The model was a tool you held and operated directly, turn by turn.

---

## 2️⃣ Stage Two: Agentic Engineering

As models gained the ability to call tools — run code, search the web, edit files — a new discipline formed around building "agents": LLMs that don't just answer once, but take actions, observe the results, and decide what to do next in a loop *within a single session*.

This is worth being precise about, because it's easy to conflate with loop engineering: **an "agent" being "an LLM in a loop" refers to a single conversation or session** where the model calls a tool, sees the result, and calls another tool, repeating until the task is done. This is not new — the best coding agents have been doing exactly this for a while, and it's the foundation everything after it builds on.

Agentic engineering added the machinery around that: error handling and retries, observability (tracing what the agent did and why), and tool-calling protocols like MCP (Model Context Protocol) that let agents reach external systems in a standardized way.

---

## 3️⃣ Stage Three: Loop Engineering

Loop engineering is what happens when you zoom out **one level further** — from "how does a single agent behave within one session" to "what triggers a session in the first place, and what happens *between* sessions."

One helpful way to see this distinction, from an engineer who analyzed Osmani's essay in depth, breaks the whole stack down like this:

```
agentic engineering
└── harness engineering
    ├── tool calls and feedback
    ├── error handling and retries
    ├── observability
    └── Loop Engineering  ← the loop itself
        ├── automation   (when does it fire)
        ├── worktree     (parallel isolation)
        ├── skill        (reusable context assembly)
        ├── plugin       (wiring up existing tools)
        ├── sub-agent    (verification and division of labor)
        └── state        (cross-loop memory)
```

The value of naming loop engineering as its own thing, in this view, is that it pulls "the loop itself" — when it fires, what it remembers, when it stops — out of the general "harness" bucket where it used to be buried, unstudied as its own object. Before it had a name, this layer was fragmented across ad-hoc scripts, cron jobs, and one-off automations that nobody thought of as a coherent discipline.

---

## 📅 The Actual Timeline, Month by Month

| When | What Happened |
|---|---|
| Prior years | Prompt engineering matures as a discipline; few-shot prompting, CoT, structured outputs become standard practice |
| Earlier 2026 | Agentic coding tools (Claude Code, Codex, and similar) become reliable enough for extended tool-use sessions |
| **June 7, 2026** | Addy Osmani publishes the essay *"Loop Engineering"* on his blog, formally naming the pattern and defining its five-plus-one component anatomy |
| **Mid-late June 2026** | The term spreads rapidly — Slashdot, Business Insider, and others cover it; Boris Cherny's comments about no longer prompting Claude directly circulate widely |
| **Late June 2026** | Both frontier labs ship official documentation on the pattern in the same week: Anthropic publishes *"Getting Started With Loops"* and OpenAI publishes *"Unrolling the Codex Agent Loop"* |
| **July 2026 (now)** | The idea has moved from community argument to something both major labs treat as documented, supported practice |

That last point matters a lot: when two competing frontier labs ship the *same* concept as official product documentation in the same week, it's a strong signal that this isn't just influencer hype — it reflects a real shift in how their own engineering teams were already working internally.

---

## 🧬 A Related Technique You Should Know: The Ralph Technique

Before "loop engineering" had a name, a related pattern already existed informally, and it's worth knowing about because it's simpler and a good stepping stone. Named by Geoffrey Huntley in early 2026, after Ralph Wiggum from *The Simpsons*, the **Ralph technique** runs a coding agent inside a plain `while` loop: the same prompt gets fed to the agent repeatedly against a written specification, with the agent making incremental progress each pass until the spec is satisfied.

The Ralph technique is loop engineering in its most stripped-down form — no worktrees, no sub-agents, no fancy state management, just "keep running the same prompt against the same goal until done." It's a useful mental anchor: everything more sophisticated in this guide is an elaboration on that basic idea, adding isolation, verification, and memory on top.

---

## 🔮 Why This History Matters for You

Notice the pattern across all three stages: **each stage didn't replace the previous one — it wrapped around it.** Loop engineering doesn't make prompt engineering or agentic engineering obsolete. A loop still needs well-designed prompts inside it, and it still needs solid tool-calling and error handling underneath it. It just adds a new layer of design *above* those, deciding when and how they get invoked.

This matters for how you approach the rest of this guide: you're not learning a replacement for skills you already have in building Godfather Agent or RAG_Master. You're learning the layer that sits above them.

---

## ➡️ Next

Continue to **`05_Core_Concepts.md`** to build the mental model that every other file in this guide assumes you have.

---

*Loop Engineering Complete Guide | Part 4 of 22*
