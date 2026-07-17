# Debugging Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-22

---

## 01. Overview

Debugging prompting is a domain-specific technique for diagnosing and fixing defects in existing code. Effective debugging prompts differ from code generation prompts in a key way: the model needs the *actual failing code*, the *exact error message or wrong behavior observed*, and the *expected behavior* — diagnosis is only as good as the evidence provided. A vague "this doesn't work" produces guesswork; a precise reproduction case produces a targeted fix.

This template structures a debugging request around root-cause identification first, then a fix — mirroring how an experienced engineer actually debugs, rather than jumping straight to a speculative patch.

## 02. Purpose

- Correctly diagnose the root cause of a bug, not just suppress its symptom.
- Reduce the risk of a "fix" that resolves the reported case but leaves the underlying issue intact.
- Make the debugging reasoning visible and verifiable before code is changed.
- Handle bugs ranging from clear error messages to vague "it's not working right" reports.

## 03. Use Cases

- Fixing a runtime error or exception with a stack trace
- Diagnosing incorrect output/logic errors with no explicit error message
- Investigating intermittent or hard-to-reproduce bugs
- Performance issues (slow execution, memory leaks)
- Reviewing code proactively for latent bugs before they manifest

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models — strong at code reasoning and root-cause analysis)
- Gemini
- Grok
- Perplexity (less common for direct debugging)

## 05. Prompt Category

`Domain-Specific` · `Software Development` · `Diagnostic`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **The failing code**: The actual code exhibiting the problem
- **Observed behavior**: What actually happens (error message, wrong output, crash, etc.)
- **Expected behavior**: What should happen instead

## 08. Optional Inputs

- Environment details (language version, OS, dependencies)
- Steps to reproduce
- What's already been tried
- Relevant logs or stack traces

## 09. Variables

| Variable | Required? |
|---|---|
| `{{failing_code}}` | Yes |
| `{{observed_behavior}}` | Yes |
| `{{expected_behavior}}` | Yes |
| `{{environment_details}}` | No |
| `{{reproduction_steps}}` | No |
| `{{already_tried}}` | No |
| `{{logs_stack_trace}}` | No |

## 10. Prompt Template

```text
Diagnose and fix the following bug. Identify the root cause before proposing
a fix — do not patch symptoms without explaining why the bug occurs.

FAILING CODE:
{{failing_code}}

OBSERVED BEHAVIOR:
{{observed_behavior}}

EXPECTED BEHAVIOR:
{{expected_behavior}}

ENVIRONMENT DETAILS:
{{environment_details}}

STEPS TO REPRODUCE:
{{reproduction_steps}}

WHAT HAS ALREADY BEEN TRIED:
{{already_tried}}

LOGS / STACK TRACE:
{{logs_stack_trace}}

INSTRUCTIONS:
1. Analyze the code and evidence provided to identify the most likely root
   cause. State it clearly and explain the reasoning.
2. If multiple causes are plausible given the evidence, list them ranked by
   likelihood, and state what additional information would help narrow it
   down.
3. Provide a fix that addresses the root cause, not just the symptom.
4. Briefly note any other latent issues you notice in the code, even if
   unrelated to this specific bug.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{failing_code}}` | The actual code with the bug | A function that's raising an unexpected exception |
| `{{observed_behavior}}` | What actually happens | "Throws IndexError when the input list has exactly one item" |
| `{{expected_behavior}}` | What should happen instead | "Should return the single item without error" |
| `{{environment_details}}` | Runtime/OS/dependency context | "Python 3.11, running in a Docker container, no special dependencies" |
| `{{reproduction_steps}}` | How to trigger the bug | "Call process_items([42]) — fails only with single-item lists" |
| `{{already_tried}}` | Fixes already attempted | "Tried adding a length check before the loop, error persisted" |
| `{{logs_stack_trace}}` | Raw error output | The full traceback text |

## 12. Example Input

```text
FAILING CODE:
def get_average_excluding_last(numbers):
    return sum(numbers[:-1]) / len(numbers[:-1])

OBSERVED BEHAVIOR:
Raises ZeroDivisionError when called with a list containing only one item.

EXPECTED BEHAVIOR:
Should return 0 (or a clear message) when there aren't enough items to
exclude the last one and still average something.

REPRODUCTION STEPS:
get_average_excluding_last([5]) fails; get_average_excluding_last([5, 10])
works fine and returns 5.0.
```

## 13. Example Output

```text
ROOT CAUSE:
When the input list has only one element, numbers[:-1] produces an empty
list. len([]) is 0, so the division sum([]) / 0 raises ZeroDivisionError.
This isn't a bug in the slicing logic itself — it's a missing guard for the
case where excluding the last item leaves nothing to average.

FIX:

def get_average_excluding_last(numbers: list[float]) -> float:
    remaining = numbers[:-1]
    if not remaining:
        return 0.0  # or raise a domain-specific error, depending on intended behavior
    return sum(remaining) / len(remaining)

This explicitly checks for the empty-remainder case before dividing,
preventing the ZeroDivisionError while preserving the original behavior for
all lists with 2+ items.

OTHER OBSERVATIONS:
The function doesn't currently handle a completely empty input list
(numbers = []) either — that case hits the same empty-remainder path and is
now also covered by this fix, but it's worth confirming that returning 0.0
(rather than raising an error) is the intended behavior for both the
single-item and empty-list cases, since a silent 0.0 could mask a caller
passing bad data.
```

## 14. Customization Guide

- **Always include the actual failing code, not a description of it**: "My function that sums a list sometimes breaks" gives the model nothing to diagnose against; the real code is essential.
- **Distinguish observed vs. expected clearly**: These are easy to blend together in a description; keeping them as separate fields forces precision about what's actually wrong.
- **Include the full stack trace when available**: Truncated or paraphrased error messages often omit the exact line/exception type that would immediately localize the bug.
- **State what's already been tried**: This prevents the model from re-suggesting an already-ruled-out fix and signals what evidence has already been gathered.

## 15. Output Format Options

- Markdown (root cause + fix + explanation)
- Code diff format
- Bullet List (for ranked candidate causes)
- Table (for comparing multiple candidate root causes)

## 16. Best Practices

- Require root-cause identification before any proposed fix — this catches the common failure mode of a patch that fixes the reported case but leaves the underlying flaw intact.
- Provide the actual code and actual error output, not paraphrased descriptions.
- Ask for ranked alternative causes when the evidence is ambiguous, rather than forcing a single confident-sounding diagnosis from insufficient information.
- Request a note on other latent issues spotted along the way — debugging often surfaces adjacent problems worth flagging even if out of scope for the immediate fix.

## 17. Common Mistakes

- Describing the bug in prose instead of providing the actual failing code.
- Omitting the exact error message or stack trace, forcing the model to guess at the failure mode.
- Not stating expected behavior explicitly, leaving "correct" ambiguous.
- Accepting a fix without asking for the root-cause explanation, risking a fix that only masks the symptom.

## 18. Prompt Variations

- **Basic Version**: Code + error message only, minimal structure.
- **Advanced Version**: Full structure with environment, reproduction steps, and prior attempts (Section 10).
- **Expert Version**: Adds a requirement for a regression test that specifically covers the fixed bug, plus a request to review whether the same root-cause pattern (e.g., an unguarded empty-collection case) might exist elsewhere in related code.

## 19. Related Prompts

- `21_Code_Generation_Prompts.md` — for producing new code once the fix has been diagnosed
- `04_Chain_of_Thought.md` — root-cause diagnosis benefits directly from explicit step-by-step reasoning
- `15_Loop_Prompting.md` — useful for a generate-test-fix loop that continues until all tests pass

## 20. Tips

- The single highest-leverage addition to a debugging prompt is usually the exact, unedited error message or stack trace — it often narrows the diagnosis space dramatically compared to a paraphrased description.
- For intermittent or hard-to-reproduce bugs, explicitly asking the model to list what conditions might cause the behavior to vary (timing, state, concurrency, external data) is often more useful than asking for a single definitive fix.

## 21. Limitations

- Diagnosis quality is capped by the evidence provided — a vague bug report will get a plausible-sounding but potentially wrong root-cause guess.
- The model cannot execute the code itself unless connected to a code execution tool, so its diagnosis is based on static reading, not actual runtime verification, unless paired with a tool-use setup.
- Intermittent, environment-specific, or concurrency-related bugs are inherently harder to diagnose from a static code snippet alone, even with a good prompt.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ (code-specialized variants recommended) |
| Mistral | ✅ (code-specialized variants recommended) |

## 23. Tags

`#debugging` `#root-cause-analysis` `#software-development` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
