# Multi-Agent Prompting

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-17

---

## 01. Overview

Multi-Agent prompting orchestrates **two or more distinct model personas or roles** that interact with each other — debating, reviewing, collaborating, or handing off work — to reach a better result than any single agent working alone. Each agent is given a distinct role, perspective, or responsibility (e.g., "Writer" and "Critic", or "Planner", "Coder", and "Reviewer"), and the prompt defines how they communicate and when the process concludes.

This differs from Self-Reflection (Template 10), where a single model critiques itself, in that Multi-Agent prompting uses genuinely distinct roles with different objectives or knowledge framings, often producing more thorough coverage through the friction of differing viewpoints — even when all roles are ultimately simulated by the same underlying model.

## 02. Purpose

- Surface disagreements and blind spots through structured role-based interaction.
- Divide complex work across specialized roles, each focused on their own concern.
- Simulate a review or debate process without needing multiple human participants.
- Improve robustness by having one role explicitly check or challenge another's output.

## 03. Use Cases

- Debate-style exploration of a contested question (Advocate vs. Skeptic)
- Collaborative content creation (Writer, Editor, Fact-Checker)
- Software development simulation (Architect, Implementer, Reviewer)
- Decision-making with structured devil's-advocate input
- Negotiation practice (simulating both sides of a discussion)

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (less common for this use case)

## 05. Prompt Category

`Agentic` · `Role-Based` · `Collaborative`

## 06. Difficulty Level

**Expert**

## 07. Required Inputs

- **Task/topic**: What the agents are collectively working on
- **Agent roles**: Two or more distinct roles with defined responsibilities/perspectives

## 08. Optional Inputs

- Interaction format (debate, sequential handoff, parallel then merge)
- Number of exchange rounds
- Resolution method (how the final answer is determined)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_topic}}` | Yes |
| `{{agent_roles}}` | Yes (2+) |
| `{{interaction_format}}` | No |
| `{{round_count}}` | No |
| `{{resolution_method}}` | No |

## 10. Prompt Template

```text
You will simulate a structured interaction between multiple distinct agents,
each with their own role and perspective, working on the same task.

TASK/TOPIC:
{{task_topic}}

AGENT ROLES:
{{agent_roles}}

INTERACTION FORMAT:
{{interaction_format}}

INSTRUCTIONS:
1. Have each agent contribute in turn, staying strictly within their defined
   role and perspective. Label each contribution clearly by agent name/role.
2. Repeat for {{round_count}} rounds of exchange, allowing agents to respond
   to each other's points where relevant.
3. After the rounds are complete, resolve the discussion using:
   {{resolution_method}}
4. Present a clear final output that reflects the outcome of the multi-agent
   process, separate from the individual role contributions.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_topic}}` | The shared subject the agents work on | "Should the company launch the product now or delay 3 months for more testing?" |
| `{{agent_roles}}` | Named roles with defined responsibilities | "Agent 1 (Growth Lead): argues for launching now. Agent 2 (QA Lead): argues for delaying." |
| `{{interaction_format}}` | How agents exchange contributions | "Alternating debate: each agent responds directly to the other's previous point" |
| `{{round_count}}` | Number of back-and-forth exchanges | "3" |
| `{{resolution_method}}` | How the process concludes | "A neutral Moderator agent synthesizes both sides into a balanced recommendation" |

## 12. Example Input

```text
TASK/TOPIC:
Should a small business prioritize paid advertising or organic content
marketing for its first year?

AGENT ROLES:
Agent 1 (Paid Media Strategist): advocates for paid advertising, focused on
speed and predictability.
Agent 2 (Content Strategist): advocates for organic content, focused on
long-term cost efficiency and trust-building.
Moderator: neutral, synthesizes both views at the end.

INTERACTION FORMAT: Alternating debate, 2 rounds each, then Moderator synthesis.
```

## 13. Example Output

```text
ROUND 1

Paid Media Strategist: Paid advertising gets the business in front of
customers immediately, which matters most in year one when there's no
existing audience or brand recognition to rely on.

Content Strategist: Immediate visibility is valuable, but paid traffic
disappears the moment spending stops. Organic content compounds over time
and builds durable trust that paid ads alone can't replicate.

ROUND 2

Paid Media Strategist: True, but a new business often can't afford to wait
months for organic content to gain traction — cash flow in year one depends
on faster results.

Content Strategist: That's a fair concern, which suggests the real answer
may not be either/or — a modest paid budget to bridge the gap while organic
content builds could address both concerns.

MODERATOR SYNTHESIS:
Both perspectives converge on a practical middle path: use a modest,
tightly measured paid advertising budget to generate early revenue and
validate messaging, while simultaneously investing in organic content that
will reduce customer acquisition costs over time. Treat paid spend as a
bridge, not a permanent strategy, and plan to shift the budget mix toward
organic as content assets mature.
```

## 14. Customization Guide

- **Define roles with genuinely different objectives**: Roles that are too similar produce redundant contributions rather than productive friction.
- **Cap round count to avoid diminishing returns**: 2–3 rounds usually surfaces the core disagreement; more rounds often just restate positions.
- **Choose a resolution method matching the goal**: Use a neutral Moderator for balanced synthesis; use "one role must concede" for forcing a decision; use "present both views unresolved" when the goal is simply to map the disagreement, not settle it.
- **Name roles descriptively**: "Agent 1" and "Agent 2" are harder to follow than named, purpose-labeled roles like "Growth Lead" and "QA Lead."

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Give each role a clearly distinct objective or perspective, not just a different name.
- Label every contribution clearly by role so the exchange is easy to follow.
- Include a neutral synthesis or resolution step rather than leaving the reader to adjudicate an unresolved debate, unless an open debate is the explicit goal.
- Keep round count proportional to topic complexity — simple topics rarely need more than 2 rounds.

## 17. Common Mistakes

- Roles that are too similar, producing repetitive rather than genuinely differentiated contributions.
- No resolution step, leaving the user without a clear takeaway from the exchange.
- Excessive rounds that restate the same points without adding new substance.
- Not specifying the interaction format, resulting in an unstructured, hard-to-follow exchange.

## 18. Prompt Variations

- **Basic Version**: 2 roles, single round, no formal resolution step.
- **Advanced Version**: 2-3 roles, multiple rounds, neutral Moderator synthesis (Section 10).
- **Expert Version**: Adds a scoring rubric where the Moderator explicitly rates the strength of each role's arguments against defined criteria before synthesizing, making the resolution more rigorous and traceable.

## 19. Related Prompts

- `16_Agentic_Prompting.md` — the single-agent, goal-directed foundation this technique extends into multiple roles
- `05_Tree_of_Thought.md` — explores multiple perspectives within one agent; Multi-Agent externalizes this into distinct interacting roles
- `10_Self_Reflection.md` — a single-agent critique loop, versus genuinely distinct role-based interaction here

## 20. Tips

- Multi-Agent prompting is especially effective for surfacing considerations a single-perspective prompt would miss — assigning a dedicated "Skeptic" or "Risk Assessor" role often catches issues a purely constructive single-role prompt overlooks.
- For decision-support use cases, explicitly instruct the Moderator role to state trade-offs rather than declaring one side simply "right," since most real debates involve genuine trade-offs rather than a clean winner.

## 21. Limitations

- All roles are ultimately simulated by the same underlying model, so the "disagreement" is a structured framing device, not genuinely independent reasoning from separate systems.
- More token-intensive than a single-perspective prompt, due to multiple rounds and roles.
- Quality depends heavily on how distinctly the roles are defined — poorly differentiated roles produce shallow, redundant exchanges.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Partial (less common use case) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#multi-agent` `#role-based-prompting` `#debate` `#collaborative-ai` `#expert-level`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
