# Productivity Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-38

---

## 01. Overview

Productivity prompting is a domain-specific technique for personal and team organization tasks — task prioritization, scheduling, planning, and workflow optimization. The key variable that makes productivity prompts effective is providing the model with actual constraints and current state (real deadlines, real available time, real competing priorities) rather than asking for generic productivity advice detached from a specific situation. Effective productivity output also needs to account for realistic capacity, not just logical task sequencing, since even a perfectly prioritized list fails if it assumes more available time or energy than actually exists.

## 02. Purpose

- Produce prioritization and planning grounded in real constraints, not idealized time availability.
- Support both one-time planning (a project plan) and recurring organizational systems (weekly review structure).
- Balance urgency, importance, and realistic capacity when sequencing tasks.
- Adapt generic productivity frameworks (Eisenhower Matrix, time-blocking, etc.) to an actual specific situation.

## 03. Use Cases

- Task prioritization and to-do list organization
- Project planning and timeline creation
- Weekly/daily schedule optimization
- Meeting agenda creation
- Workflow and process improvement
- Goal-setting and milestone breakdown
- Time audit and capacity analysis

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (less common for this use case)

## 05. Prompt Category

`Domain-Specific` · `Personal Productivity` · `Planning`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Task/goal list**: What needs to get done
- **Time constraints**: Available time, deadlines

## 08. Optional Inputs

- Priority framework to apply (Eisenhower Matrix, MoSCoW, etc.)
- Energy/focus patterns (when you work best)
- Dependencies between tasks
- Non-negotiable commitments already scheduled
- Desired output format (calendar blocks, prioritized list, Gantt-style plan)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_goal_list}}` | Yes |
| `{{time_constraints}}` | Yes |
| `{{priority_framework}}` | No |
| `{{energy_patterns}}` | No |
| `{{task_dependencies}}` | No |
| `{{existing_commitments}}` | No |
| `{{output_format}}` | No |

## 10. Prompt Template

```text
Help organize/prioritize the following.

TASK/GOAL LIST:
{{task_goal_list}}

TIME CONSTRAINTS:
{{time_constraints}}

PRIORITY FRAMEWORK TO APPLY:
{{priority_framework}}

ENERGY/FOCUS PATTERNS:
{{energy_patterns}}

TASK DEPENDENCIES:
{{task_dependencies}}

EXISTING NON-NEGOTIABLE COMMITMENTS:
{{existing_commitments}}

INSTRUCTIONS:
- Work within the actual stated time constraints — do not produce a plan
  that assumes more available time or capacity than what's given.
- Respect task dependencies; don't sequence a task before its prerequisite
  is planned to be complete.
- If the task list genuinely doesn't fit within the available time, say so
  explicitly and suggest what to cut or defer, rather than silently
  cramming everything in.
- Match energy/focus patterns to task type where provided (e.g., schedule
  deep-focus work during stated high-energy periods).

Output format: {{output_format}}
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_goal_list}}` | What needs to be accomplished | "Finish quarterly report, prep for client presentation, respond to 15 pending emails, plan next sprint" |
| `{{time_constraints}}` | Real available time/deadlines | "3 working days, presentation is Thursday 2pm, report due Friday EOD" |
| `{{priority_framework}}` | Structured prioritization method | "Eisenhower Matrix (urgent/important)" |
| `{{energy_patterns}}` | When focus is best | "Best deep focus 9-11am, low energy after 3pm" |
| `{{task_dependencies}}` | What must happen before what | "Report needs data from the presentation prep to be finalized first" |
| `{{existing_commitments}}` | Already-fixed time blocks | "Daily standup 9:30-9:45am, no exceptions" |
| `{{output_format}}` | How the plan should be presented | "Day-by-day schedule with time blocks" |

## 12. Example Input

```text
TASKS: Finish quarterly report, prep client presentation, respond to
urgent emails, review team's pull requests
TIME CONSTRAINTS: 2 working days, presentation is tomorrow 2pm, report due
end of day 2
PRIORITY FRAMEWORK: Eisenhower Matrix
ENERGY PATTERNS: Sharpest 8-11am, energy dips significantly after 2pm
EXISTING COMMITMENTS: Daily standup 9:30-9:45am both days
OUTPUT FORMAT: Day-by-day time-blocked schedule
```

## 13. Example Output

```text
EISENHOWER CLASSIFICATION:
- Presentation prep: Urgent + Important (fixed deadline tomorrow 2pm)
- Quarterly report: Urgent + Important (deadline day 2)
- Urgent emails: Urgent, importance varies — will time-box rather than
  let it expand
- PR reviews: Important, not urgent — can be time-boxed into a lower-
  energy slot

DAY 1:
8:00-9:15 — Presentation prep (deep focus, your sharpest window)
9:15-9:30 — Buffer
9:30-9:45 — Standup
9:45-11:00 — Continue presentation prep (finish core content)
11:00-11:30 — Urgent emails (time-boxed, not open-ended)
11:30-1:00 — Presentation prep: polish and rehearse
1:00-2:00 — Lunch/buffer
2:00 — PRESENTATION
Afternoon (lower energy) — Light task: PR reviews, since this doesn't
need peak focus

DAY 2:
8:00-9:15 — Quarterly report (deep focus window, using presentation data
already gathered — dependency respected)
9:15-9:30 — Buffer
9:30-9:45 — Standup
9:45-12:00 — Continue report drafting
12:00-1:00 — Lunch
1:00-3:00 — Finalize report, incorporating any last details
3:00 onward (energy dip) — Remaining urgent emails, lighter follow-up tasks

NOTE:
This schedule fits within your 2-day constraint, but it's tight — there's
minimal buffer for the report if presentation prep runs long on Day 1.
If anything slips, urgent emails on Day 1 are the most flexible item to
compress further.
```

## 14. Customization Guide

- **Provide real deadlines and time availability, not idealized estimates**: A plan built on "I have all day" when meetings actually consume half of it will fail immediately — accurate constraints produce actually usable plans.
- **State energy/focus patterns if they're known**: This is often the highest-leverage detail for a genuinely useful schedule, since task-to-energy matching (deep work in high-focus windows) meaningfully affects real completion likelihood, not just theoretical task order.
- **Name dependencies explicitly**: Without this, a plan might schedule a task before something it actually depends on is complete.
- **Ask for explicit "what to cut" guidance when the list likely won't fit**: A realistic assessment that something needs to be deferred is more useful than an unrealistic plan that pretends everything fits.

## 15. Output Format Options

- Time-blocked schedule (day-by-day)
- Prioritized list (ranked order)
- Table (task, priority, deadline, status)
- Kanban-style categorization (To Do / In Progress / Done)
- Gantt-style timeline (for multi-day/week projects)

## 16. Best Practices

- Provide real, specific time constraints rather than vague availability estimates.
- State energy/focus patterns when known, since this materially improves how realistic and actually followable the resulting plan is.
- Name task dependencies explicitly so the sequencing is genuinely correct, not just plausible-looking.
- Request honest feedback on whether everything actually fits, rather than a plan that silently assumes unrealistic capacity.

## 17. Common Mistakes

- Providing idealized rather than realistic time availability, producing a plan that looks good but isn't actually followable.
- Omitting existing fixed commitments, resulting in a plan that conflicts with meetings or other non-negotiable time blocks.
- Not stating dependencies, risking a sequence that schedules a task before its prerequisite.
- Accepting an overloaded plan without asking whether the task list genuinely fits the available time.

## 18. Prompt Variations

- **Basic Version**: Task list + time constraint only, no framework/energy specification.
- **Advanced Version**: Full structure with priority framework, energy patterns, and dependencies (Section 10).
- **Expert Version**: Adds a request for a contingency plan — e.g., "if [highest-risk task] takes longer than expected, here's the fallback adjustment" — useful for plans with meaningful uncertainty in task duration.

## 19. Related Prompts

- `12_Least_to_Most_Prompting.md` — complex project planning shares the same decomposition-into-ordered-steps principle
- `37_Business_Prompts.md` — team/organizational productivity planning overlaps with broader business planning contexts
- `06_Skeleton_of_Thought.md` — useful for structuring a larger project plan before filling in day-by-day detail

## 20. Tips

- Being honest about actual energy patterns (not aspirational ones) produces meaningfully more usable schedules — a plan built on an idealized "I'll be focused all day" self-image tends to fail in practice compared to one built on real, known focus windows.
- For recurring planning needs (weekly reviews, sprint planning), saving a working version of this template with your typical constraints already filled in makes repeated use significantly faster than rebuilding the prompt from scratch each time.

## 21. Limitations

- A plan is only as good as the accuracy of the constraints provided — unrealistic inputs (assumed availability, underestimated task duration) produce an unrealistic plan regardless of prompt quality.
- The model cannot account for genuinely unpredictable disruptions (urgent unplanned issues, illness, unexpected meetings); plans should be treated as a strong starting structure, not an unchangeable commitment.
- For team-wide scheduling involving multiple people's availability, this template handles single-person planning best; multi-person scheduling may benefit from a dedicated scheduling tool integration.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#productivity` `#planning` `#time-management` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
