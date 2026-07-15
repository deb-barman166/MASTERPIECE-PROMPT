# 05 — Key Terminology

## Introduction

Every discipline has its vocabulary, and loop engineering is no exception. This file is a comprehensive reference of every important term you will encounter when designing, building, and debugging iterative AI systems. Terms are organized by category for easier navigation, and each entry includes a concise definition, a more detailed explanation, and a practical example.

This glossary complements the conceptual foundations in [04_Core_Concepts.md](04_Core_Concepts.md) and the historical context in [03_History_and_Evolution.md](03_History_and_Evolution.md). If you encounter an unfamiliar term anywhere in this library, this is the place to look it up.

---

## A

### Agent

**Definition:** An AI system that can perceive its environment, reason about goals, and take actions to accomplish tasks autonomously.

**Detailed Explanation:** In loop engineering, an agent is the entity that *executes* a loop. Unlike a passive model that responds to prompts, an agent actively decides what to do next based on its current state, available tools, and the results of previous actions. Agents range from simple (a single LLM with one tool) to complex (multi-agent systems with hierarchical delegation). The key distinction is **autonomy** — an agent makes its own decisions about which actions to take within its loop.

**Example:** A customer support agent that reads a user's complaint, decides whether to search the knowledge base or escalate to a human, takes that action, reads the result, and decides what to do next — looping until the issue is resolved.

### Agent Loop

**Definition:** The core iterative cycle of an AI agent — reasoning about what to do, taking an action, observing the result, and deciding whether to continue.

**Detailed Explanation:** The agent loop is the most common loop type in production systems. It is typically structured as Thought → Action → Observation (the ReAct pattern), though variations exist. Each pass through the agent loop is one iteration. The loop continues until a termination condition is met — the task is complete, a budget is exhausted, or an error threshold is reached.

**Example:**
```
Thought: The user wants to know today's weather in London. I should search for it.
Action: search("weather in London today")
Observation: Rain, 12°C, 80% humidity.
Thought: I have the weather data. I can answer now.
Answer: Today in London it's raining with a temperature of 12°C and 80% humidity.
```

---

## B

### Branching

**Definition:** A control flow mechanism where a loop can follow different paths based on conditions, rather than always following the same sequence.

**Detailed Explanation:** Branching in loop engineering is typically implemented using conditional edges (in LangGraph) or if/else logic in the loop's control flow. A loop might branch to different tools, different evaluation strategies, or different refinement approaches depending on the current state. Branching enables a single loop to handle a variety of situations without becoming overly complex.

**Example:** An agent loop that branches: if the user's question is factual → search the web; if it's mathematical → use a calculator; if it's creative → generate directly. The branching decision is made at each iteration based on the current state.

---

## C

### Chain-of-Thought (CoT)

**Definition:** A prompting technique where the LLM is encouraged to show its step-by-step reasoning process before producing a final answer.

**Detailed Explanation:** CoT was introduced by Wei et al. in 2022 and is one of the foundational techniques that paved the way for loop engineering. While technically a single-pass technique (the reasoning steps are in one prompt), CoT established the critical insight that *explicit reasoning improves outcomes*. This insight directly led to multi-step reasoning loops where each reasoning step becomes its own iteration. CoT can be "zero-shot" (just adding "let's think step by step") or "few-shot" (providing examples of reasoning chains).

**Example:**
```
Prompt: "If it takes 5 machines 5 minutes to make 5 widgets, how long would it take 
100 machines to make 100 widgets? Let's think step by step."

Response: "Step 1: 5 machines make 5 widgets in 5 minutes. 
Step 2: So 1 machine makes 1 widget in 5 minutes. 
Step 3: 100 machines making 100 widgets = each machine makes 1 widget. 
Step 4: Since each takes 5 minutes, the answer is 5 minutes."
```

### Convergence

**Definition:** The property of a loop making progressive, measurable improvement toward its goal over successive iterations.

**Detailed Explanation:** A converging loop produces outputs that are consistently better (by whatever quality metric is relevant) with each iteration, or at least not worse. Convergence is the ideal behavior — it means the loop is working as intended. In practice, convergence is often **asymptotic**: early iterations show large improvements, while later iterations show diminishing returns. Detecting convergence (knowing when improvements have become negligible) is a key termination strategy. See [04_Core_Concepts.md](04_Core_Concepts.md) for detailed coverage.

**Example:** A code generation loop where iteration 1 has 5 test failures, iteration 2 has 2 failures, iteration 3 has 0 failures. The decreasing error count demonstrates convergence.

### Context Window

**Definition:** The maximum number of tokens that an LLM can process in a single request, encompassing both input and output.

**Detailed Explanation:** The context window is a hard constraint on loop engineering because all state — conversation history, tool results, instructions, and the current reasoning — must fit within it. As a loop iterates, its state typically grows (new messages are added, tool results accumulate). If the state exceeds the context window, the loop must either compress its state (summarization, truncation) or fail. Context window management is a critical operational concern in long-running loops.

**Example:** GPT-4o has a 128,000-token context window. If a research agent's accumulated messages and search results exceed this, it must summarize earlier findings to continue looping.

### Cost Budget

**Definition:** A predefined limit on the monetary cost (typically measured in USD or token count) that a loop is allowed to consume before being terminated.

**Detailed Explanation:** Cost budgets are a practical necessity because LLM API calls cost money, and loops multiply those costs. A cost budget is typically set before the loop begins and checked at each iteration. It can be expressed as a maximum token count, a maximum dollar amount, or both. Cost budgets serve as a safety net alongside quality-based termination — even if the loop hasn't converged, it will stop when the budget is exhausted.

**Example:** A data analysis agent is given a $0.50 budget. At ~$0.0025 per iteration (GPT-4o-mini), it can iterate up to 200 times before being forcibly terminated.

---

## D

### Divergence

**Definition:** The failure mode where a loop moves away from its goal, oscillates without progress, or continues indefinitely without converging.

**Detailed Explanation:** Divergence is the opposite of convergence and one of the most important failure modes to detect and handle. Types include **oscillation** (alternating between states), **drift** (pursuing irrelevant tangents), **degradation** (each iteration makes things worse), and **runaway** (the loop never terminates). Divergence detection typically involves tracking quality metrics across iterations and looking for patterns like flat improvement curves or alternating quality scores. See [04_Core_Concepts.md](04_Core_Concepts.md) for detailed coverage.

**Example:** A code-fixing loop that fixes a bug in the login module, which causes a bug in the session module, which causes a bug in the auth module, which causes a bug in the login module — oscillating indefinitely.

---

## E

### Episode

**Definition:** A single complete execution of a loop from start to termination, including all iterations within it.

**Detailed Explanation:** An episode is to a loop what a request is to an API call — one complete unit of work. An episode begins when the loop is initiated (with initial state and input) and ends when a termination condition is met (with a final output). In reinforcement learning, this concept is called a "trajectory." In loop engineering, we use "episode" to emphasize that it's a self-contained execution that can be analyzed, logged, and compared with other episodes.

**Example:** A research agent is asked "What caused the 2008 financial crisis?" The entire process — from the first search to the final synthesized answer, including all intermediate iterations — is one episode.

---

## F

### Feedback Loop

**Definition:** A loop structure where the output (or an evaluation of it) is fed back as input to the next iteration to drive improvement.

**Detailed Explanation:** Feedback loops are one of the three primary loop types in loop engineering (alongside agent loops and reflection loops). The feedback can come from the system itself (self-critique), from an external evaluator (automated scoring), from the environment (test results, user reactions), or from a human reviewer. The quality of the feedback directly determines the loop's effectiveness — vague or inaccurate feedback leads to poor convergence or divergence.

**Example:** A writing assistant that generates a draft, runs it through a readability scorer, receives the score as feedback, and generates a revised draft targeting a higher score. The loop continues until the readability score exceeds a threshold.

---

## G

### Guardrail

**Definition:** A safety mechanism that constrains a loop's behavior to prevent harmful, costly, or unintended outcomes.

**Detailed Explanation:** Guardrails are the safety systems of loop engineering. They can take many forms: input validation (rejecting malicious prompts), output validation (checking generated content against policies), loop limits (maximum iterations, cost budgets), and behavioral constraints (preventing the agent from taking certain actions). Guardrails are especially important in production systems where loops interact with real-world systems (databases, APIs, user-facing applications). A well-guarded loop fails safely; an unguarded loop can cause production incidents.

**Example:** A customer support agent has guardrails that prevent it from: (1) deleting customer data, (2) making promises about refunds, (3) looping more than 10 times per query, (4) spending more than $0.10 per query.

---

## H

### Halting Condition

**Definition:** Synonym for termination condition — the criteria that determine when a loop should stop executing. See [Termination Condition](#termination-condition).

### Human-in-the-Loop (HITL)

**Definition:** A loop architecture where a human participates in the iteration cycle, providing feedback, approvals, or corrections at one or more points.

**Detailed Explanation:** HITL loops insert human judgment into the loop cycle, typically at evaluation or approval points. The human might review the agent's output before it proceeds, provide corrections when the agent makes mistakes, or approve tool calls before they're executed. HITL improves reliability and safety but increases latency and cost (human time). It's commonly used in high-stakes domains like legal, medical, or financial applications where errors are unacceptable.

**Example:** A legal document drafting system generates a contract clause, pauses for a lawyer to review and approve it, then proceeds to the next clause. The loop cannot continue past the review point without human approval.

---

## I

### Iteration

**Definition:** A single complete pass through a loop's cycle — the atomic unit of loop execution.

**Detailed Explanation:** An iteration is one execution of the loop's core operation. In a ReAct agent, one iteration = one thought + one action + one observation. In a refinement loop, one iteration = one generation + one evaluation. The number of iterations a loop performs directly impacts cost (more iterations = more tokens) and quality (more iterations = potential for improvement, but also potential for divergence). See [04_Core_Concepts.md](04_Core_Concepts.md) for detailed coverage.

**Example:** A search-and-answer agent that searches Wikipedia, reads the result, decides it needs more info, searches again, reads that result, and then answers — that's 2 iterations.

### Iteration Budget

**Definition:** The maximum number of iterations a loop is allowed to perform before being forcibly terminated.

**Detailed Explanation:** The iteration budget is the simplest form of termination condition and serves as a hard safety limit. It prevents runaway loops and provides a predictable upper bound on cost and latency. Setting the right iteration budget requires understanding the task: simple tasks might need 1-3 iterations, while complex research tasks might need 10-20. The budget should be generous enough to allow the loop to converge but restrictive enough to prevent waste.

**Example:** A code debugging agent is given an iteration budget of 8. If it hasn't fixed all bugs after 8 fix-test cycles, it returns the best version it has produced along with a summary of remaining issues.

---

## L

### Loop

**Definition:** A repeating cycle of operations in an AI system where the output of one cycle becomes the input for the next, continuing until a termination condition is met.

**Detailed Explanation:** The loop is the fundamental structure of loop engineering. It is the computational analogue of the scientific method: hypothesize, experiment, observe, revise. Every loop has at minimum: (1) an operation to perform, (2) a way to determine the result, (3) a way to decide whether to continue, and (4) a termination condition. Loops can be simple (repeat the same operation) or complex (vary the operation based on state), shallow (one level) or deep (nested recursively).

**Example:** A ReAct agent's loop: Thought → Action → Observation → (repeat or stop).

---

## M

### Multi-Agent System

**Definition:** A system where multiple AI agents, each with their own loop, collaborate (or compete) to accomplish tasks.

**Detailed Explanation:** Multi-agent systems introduce additional loop complexity: each agent has its own loop, and there is also a coordination loop (or loops) that manages the interactions between agents. Common patterns include **sequential** (agents take turns), **parallel** (agents work simultaneously), **hierarchical** (a manager delegates to workers), and **debate** (agents argue and converge on an answer). Multi-agent systems can solve more complex problems than single-agent systems, but they multiply cost and introduce coordination challenges.

**Example:** A content creation system with three agents: a researcher (loops through web searches), a writer (loops through draft generation and refinement), and an editor (loops through review and correction). A coordinator agent manages the handoffs between them.

---

## O

### Observation

**Definition:** The result of an action — the information an agent receives after executing a tool call or taking a step.

**Detailed Explanation:** In the ReAct framework, Observation is the third element of the core loop (Thought → Action → Observation). The observation is what the agent "sees" after acting — the search results from a web search, the output of a code execution, the response from an API, or the result of any external interaction. The quality and format of observations significantly impact the agent's ability to reason effectively in subsequent iterations.

**Example:** An agent calls `search("population of Tokyo")` and receives the observation: "Tokyo's population is approximately 13.96 million as of 2024."

### Orchestrator

**Definition:** The component or agent that manages the control flow of a loop-based system, deciding which steps to execute, when to branch, and when to terminate.

**Detailed Explanation:** The orchestrator is the "conductor" of the loop. In simple systems, the orchestrator is implicit — the loop just repeats the same operation. In complex systems, the orchestrator is often a separate agent (or a rule-based controller) that reads the current state, consults a plan or policy, and determines the next action. LangGraph's conditional edges and state machine logic serve as the orchestrator in that framework.

**Example:** In a plan-and-execute system, the orchestrator maintains a task plan, assigns tasks to worker agents, collects their results, updates the plan based on results, and decides when the overall goal is achieved.

---

## P

### Plan-and-Execute

**Definition:** A loop pattern where the system first creates a complete plan (a sequence of steps) and then executes the plan step by step, with the option to replan based on intermediate results.

**Detailed Explanation:** Plan-and-Execute is an alternative to the ReAct pattern. Instead of deciding one step at a time (ReAct), the system generates an entire plan upfront and then executes it. The key advantage is that planning with full context of the task can produce better strategies than greedy step-by-step decisions. The key disadvantage is that the initial plan may be wrong, and replanning adds overhead. A hybrid approach — plan, execute a few steps, evaluate, replan if needed — combines the strengths of both patterns.

**Example:**
```
Plan:
1. Search for recent AI research papers
2. Read the top 3 papers
3. Summarize key findings
4. Identify open questions
5. Write a synthesis report

Execute Step 1 → [search results]
Execute Step 2 → [paper summaries]
Evaluate → "Finding 3 contradicts Finding 1, need to investigate"
Replan → Add step 2.5: "Compare and resolve contradiction between papers 1 and 3"
Execute Step 2.5 → [analysis]
Continue...
```

---

## R

### ReAct (Reasoning + Acting)

**Definition:** A loop pattern where an LLM alternates between reasoning (thinking about what to do) and acting (calling tools or taking actions) in an iterative cycle.

**Detailed Explanation:** ReAct, introduced by Yao et al. in 2022, is the canonical agent loop pattern and the foundation for most modern agent frameworks. The cycle is: **Thought** (the LLM reasons about the current state and decides what to do), **Action** (the LLM executes a tool call or generates output), **Observation** (the result of the action is fed back). This cycle repeats until the LLM decides the task is complete. ReAct combines the benefits of Chain-of-Thought reasoning with the capabilities of tool use.

**Example:**
```
Thought: I need to find the CEO of Tesla. Let me search for that.
Action: search("Tesla CEO 2024")
Observation: Elon Musk is the CEO of Tesla.
Thought: I have the answer now.
Answer: The CEO of Tesla is Elon Musk.
```

### Reflection Loop

**Definition:** A loop structure where the system evaluates its own output, identifies weaknesses or errors, and generates an improved version.

**Detailed Explanation:** Reflection loops are a specialized form of feedback loop where the feedback comes from the system itself (self-critique, self-evaluation). The typical cycle is: Generate → Evaluate → Critique → Refine → (repeat or stop). Reflection loops are particularly effective for writing, coding, and analytical tasks where the system can meaningfully evaluate the quality of its own output. The key challenge is designing evaluation criteria that are specific enough to drive improvement rather than just saying "make it better."

**Example:**
```
Draft 1: "AI is good and will help people a lot in many ways."
Self-critique: "Too vague. Needs specific examples and a more nuanced stance."
Draft 2: "Artificial intelligence is transforming healthcare, education, and transportation 
by enabling faster diagnosis, personalized learning, and autonomous vehicles."
Self-critique: "Better, but missing potential risks. Should address concerns."
Draft 3: "Artificial intelligence is transforming healthcare, education, and transportation, 
while raising important questions about privacy, job displacement, and algorithmic bias..."
Evaluation: Score 9/10 — sufficient quality. Terminate loop.
```

### Runaway Loop

**Definition:** A failure mode where a loop continues executing indefinitely because no termination condition is triggered.

**Detailed Explanation:** Runaway loops are one of the most serious production risks in loop engineering. They occur when: (1) no termination conditions are set, (2) termination conditions are too permissive, (3) the system fails to recognize that it should stop, or (4) the system enters a state where termination conditions can never be met. Runaway loops can consume unlimited tokens and incur unlimited costs. Prevention requires multiple, redundant termination conditions (hard iteration limits, cost budgets, time limits) — never rely on a single condition.

**Example:** An agent that keeps searching the web for "more information" without ever deciding it has enough to answer the question. Without a hard iteration limit, this loop could run for thousands of iterations.

---

## S

### State

**Definition:** The complete set of data and context that persists across loop iterations and determines the system's behavior at each step.

**Detailed Explanation:** State is the memory of a loop — everything the system knows and remembers from previous iterations. In LangGraph, state is typically a typed dictionary (`TypedDict`) that is passed between nodes and updated at each step. Good state design is critical: too little state and the system can't make informed decisions; too much state and you waste context window space. State should be structured (not unstructured text), minimal (only what's needed), and bounded (preventing unbounded growth). See [04_Core_Concepts.md](04_Core_Concepts.md) for detailed coverage.

**Example:**
```python
class AgentState(TypedDict):
    messages: list           # Conversation history
    search_results: list     # Accumulated search findings
    current_step: str        # What the agent is currently doing
    errors: list[str]        # Errors encountered so far
    iteration: int           # Loop counter
```

### State Machine

**Definition:** A computational model consisting of a finite number of states, transitions between those states, and actions associated with transitions.

**Detailed Explanation:** State machines are a foundational pattern in loop engineering for implementing structured control flow. Instead of an unstructured while-loop, the system's behavior is defined as a set of explicit states (e.g., `PLANNING`, `EXECUTING`, `REVIEWING`, `RETRYING`, `DONE`) with defined transitions between them. LangGraph's `StateGraph` is essentially a state machine with LLM-powered transitions. State machines make loops more debuggable, more predictable, and easier to reason about.

**Example:**
```
States: PLANNING → EXECUTING → REVIEWING → (PASS → DONE | FAIL → EXECUTING)
Transitions:
  PLANNING → EXECUTING (always, after plan is created)
  EXECUTING → REVIEWING (always, after action is taken)
  REVIEWING → DONE (if quality check passes)
  REVIEWING → EXECUTING (if quality check fails, up to 3 times)
  REVIEWING → DONE (after 3 failures, return best result)
```

### Step

**Definition:** A single logical operation within a loop iteration — one reasoning step, one tool call, or one evaluation.

**Detailed Explanation:** While an **iteration** is a complete pass through the loop, a **step** is a finer-grained unit. One iteration may contain multiple steps (e.g., in a plan-and-execute system, one iteration might involve executing multiple planned steps). The distinction matters for cost accounting (each step may involve an LLM call) and for debugging (knowing which specific step failed).

**Example:** In a ReAct loop, one iteration contains three steps: one Thought step, one Action step, and one Observation step.

---

## T

### Termination Condition

**Definition:** The criteria (one or more) that determine when a loop should stop iterating and produce its final output.

**Detailed Explanation:** Termination conditions are arguably the most critical design element in loop engineering. Every loop must have at least one termination condition, and production systems should have multiple redundant conditions. Common types include: goal achievement (the task is done), iteration limit (hard maximum), convergence detection (improvement has plateaued), budget exhaustion (tokens or money), and error threshold (too many failures). The art of termination is setting conditions that are tight enough to prevent waste but loose enough to allow the loop to achieve quality. See [04_Core_Concepts.md](04_Core_Concepts.md) for detailed coverage.

**Example:**
```python
# Multiple termination conditions (any one triggers stop)
def should_terminate(state):
    return (
        state["quality_score"] >= 0.9    # Goal achieved
        or state["iteration"] >= 10       # Hard limit
        or state["tokens_used"] >= 50000  # Budget
        or state["errors"] >= 3           # Error threshold
        or state["improvement"] < 0.01    # Convergence plateau
    )
```

### Token Budget

**Definition:** A predefined maximum number of LLM tokens that a loop is allowed to consume across all its iterations.

**Detailed Explanation:** Token budget is a specific form of cost budget expressed in tokens rather than dollars. It serves the same purpose: preventing runaway costs. Token budgets are particularly important because they directly map to context window pressure — as the token count grows, the state may need to be compressed to fit within the model's context window. A well-designed system tracks token usage per iteration and can predict how many iterations remain within budget.

**Example:** A loop with a 30,000-token budget. If each iteration consumes approximately 3,000 tokens (input + output), the system knows it can iterate approximately 10 times before the budget is exhausted.

### Tool Loop

**Definition:** A loop structure centered around the repeated calling of external tools (APIs, search engines, code interpreters, databases) as part of the workflow.

**Detailed Explanation:** Tool loops are the most common form of agent loop in practice. The cycle is: decide which tool to call → call it → process the result → decide whether to call another tool or produce a final answer. Tool loops are the mechanism by which AI systems interact with the external world — fetching data, executing code, sending emails, updating databases. The reliability of a tool loop depends heavily on error handling (what happens when a tool fails or returns unexpected results) and on the agent's ability to select the right tool for each situation.

**Example:** A data analysis agent that loops through: query database → read results → identify needed follow-up → query again → read results → generate chart → write summary. Each database query and chart generation is a tool call within the loop.

### Trajectory

**Definition:** The complete sequence of states, actions, and observations from the start of a loop episode to its termination.

**Detailed Explanation:** A trajectory is a record of everything that happened during one complete execution of a loop. It includes the initial state, every intermediate state, every action taken, every observation received, and the final state/output. Trajectories are essential for debugging (replaying what went wrong), for training (using successful trajectories as few-shot examples), and for evaluation (comparing trajectories to find the most efficient paths). LangSmith and similar observability tools capture and display trajectories.

**Example:** A trajectory for a research agent might be: `[start] → [search: "AI trends 2024"] → [read: 3 results] → [search: "LLM market size"] → [read: 2 results] → [synthesize] → [end]` — a 6-step trajectory.

---

## Quick Reference Table

| Term | Category | One-Line Summary |
|---|---|---|
| **Agent** | Architecture | Autonomous AI system that reasons, acts, and observes in a loop |
| **Agent Loop** | Loop Type | Core iterative cycle: Thought → Action → Observation |
| **Branching** | Control Flow | Following different paths based on conditions |
| **Chain-of-Thought** | Prompting | Showing step-by-step reasoning to improve outputs |
| **Convergence** | Behavior | Loop making progressive improvement toward goal |
| **Context Window** | Constraint | Maximum tokens the LLM can process per request |
| **Cost Budget** | Constraint | Maximum money/tokens allowed for a loop episode |
| **Divergence** | Behavior | Loop moving away from goal or making no progress |
| **Episode** | Execution | One complete execution of a loop from start to termination |
| **Feedback Loop** | Loop Type | Output evaluation fed back to drive improvement |
| **Guardrail** | Safety | Constraint preventing harmful or costly outcomes |
| **Halting Condition** | Control Flow | See Termination Condition |
| **Human-in-the-Loop** | Architecture | Human provides feedback/approval within the loop |
| **Iteration** | Fundamentals | Single complete pass through the loop cycle |
| **Iteration Budget** | Constraint | Maximum iterations allowed before forced stop |
| **Loop** | Fundamentals | Repeating cycle of operations until termination |
| **Multi-Agent System** | Architecture | Multiple agents with individual loops collaborating |
| **Observation** | ReAct | Result received after executing an action |
| **Orchestrator** | Architecture | Component managing loop control flow |
| **Plan-and-Execute** | Pattern | Plan complete strategy first, then execute step by step |
| **ReAct** | Pattern | Reasoning + Acting — canonical agent loop pattern |
| **Reflection Loop** | Loop Type | System evaluates and refines its own output |
| **Runaway Loop** | Failure | Loop executing indefinitely without terminating |
| **State** | Fundamentals | Data persisting across loop iterations |
| **State Machine** | Pattern | Explicit states with defined transitions |
| **Step** | Fundamentals | Single logical operation within an iteration |
| **Termination Condition** | Control Flow | Criteria that determine when to stop looping |
| **Token Budget** | Constraint | Maximum tokens allowed for a loop episode |
| **Tool Loop** | Loop Type | Loop centered on repeated external tool calls |
| **Trajectory** | Execution | Complete record of a loop episode from start to end |

---

## References & Further Reading

- **LangGraph Glossary**: [https://langchain-ai.github.io/langgraph/concepts/](https://langchain-ai.github.io/langgraph/concepts/) — Official LangGraph concept definitions
- **LangChain Glossary**: [https://python.langchain.com/docs/concepts/](https://python.langchain.com/docs/concepts/) — Official LangChain terminology
- **"ReAct: Synergizing Reasoning and Acting in Language Models"** — Yao et al. (2022): [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)
- **"Reflexion: Language Agents with Verbal Reinforcement Learning"** — Shinn et al. (2023): [https://arxiv.org/abs/2303.11366](https://arxiv.org/abs/2303.11366)
- **"Self-Refine: Iterative Refinement with Self-Feedback"** — Madaan et al. (2023): [https://arxiv.org/abs/2303.17651](https://arxiv.org/abs/2303.17651)
- **"LLM Powered Autonomous Agents"** by Lilian Weng: [https://lilianweng.github.io/posts/2023-06-23-agent/](https://lilianweng.github.io/posts/2023-06-23-agent/)