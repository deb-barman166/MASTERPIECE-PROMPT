# Code Generation Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-21

---

## 01. Overview

Code Generation prompting is a domain-specific technique for producing working, idiomatic source code from a natural-language specification. Unlike generic task prompting, effective code generation requires specifying the language, version/runtime, style conventions, existing codebase context, error-handling expectations, and testing requirements — details that meaningfully change what "correct" output looks like in software, unlike in prose generation.

This template captures the specific parameters that separate a vague "write me a function" request from a prompt that reliably produces production-usable code on the first pass.

## 02. Purpose

- Produce syntactically correct, idiomatic code in a specified language and style.
- Reduce back-and-forth caused by missing context (language version, dependencies, conventions).
- Ensure generated code handles edge cases and errors appropriately, not just the happy path.
- Make generated code consistent with an existing codebase's conventions where relevant.

## 03. Use Cases

- Writing new functions, classes, or modules from a specification
- Implementing an algorithm or data structure
- Generating boilerplate (CRUD operations, API clients, configuration files)
- Converting pseudocode or a written spec into working code
- Scaffolding a new project structure

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models — strong code generation performance)
- Gemini
- Grok
- Perplexity (less common for code generation specifically)

## 05. Prompt Category

`Domain-Specific` · `Software Development` · `Code Generation`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Functionality description**: What the code should do
- **Language and version**: e.g., Python 3.12, TypeScript 5.x, Java 21

## 08. Optional Inputs

- Framework/library constraints (e.g., must use pandas, React, Express)
- Style guide or linting conventions (PEP 8, Airbnb style guide, etc.)
- Existing code context (surrounding functions, class structure)
- Error-handling and input-validation expectations
- Required test coverage

## 09. Variables

| Variable | Required? |
|---|---|
| `{{functionality_description}}` | Yes |
| `{{language_version}}` | Yes |
| `{{framework_constraints}}` | No |
| `{{style_guide}}` | No |
| `{{existing_code_context}}` | No |
| `{{error_handling_requirements}}` | No |
| `{{test_requirements}}` | No |

## 10. Prompt Template

```text
Write code that performs the following functionality.

FUNCTIONALITY:
{{functionality_description}}

LANGUAGE / VERSION:
{{language_version}}

FRAMEWORK / LIBRARY CONSTRAINTS:
{{framework_constraints}}

STYLE GUIDE / CONVENTIONS:
{{style_guide}}

EXISTING CODE CONTEXT (if integrating with existing code):
{{existing_code_context}}

ERROR HANDLING / INPUT VALIDATION REQUIREMENTS:
{{error_handling_requirements}}

TEST REQUIREMENTS:
{{test_requirements}}

INSTRUCTIONS:
- Write clean, idiomatic code following the specified language conventions
  and style guide.
- Include appropriate comments only where logic isn't self-evident from
  naming — do not over-comment obvious lines.
- Handle edge cases and invalid input according to the requirements above.
- If any part of the specification is ambiguous, state your assumption
  briefly above the code rather than guessing silently.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{functionality_description}}` | What the code should accomplish | "A function that validates a US phone number and returns it in E.164 format" |
| `{{language_version}}` | Target language and version | "Python 3.12" |
| `{{framework_constraints}}` | Required libraries/frameworks | "Use only the standard library, no external dependencies" |
| `{{style_guide}}` | Formatting/naming conventions | "PEP 8, type hints required" |
| `{{existing_code_context}}` | Relevant surrounding code | A snippet of the class this function will belong to |
| `{{error_handling_requirements}}` | How invalid input/errors should be handled | "Raise a ValueError with a descriptive message for invalid formats" |
| `{{test_requirements}}` | Testing expectations | "Include 3-5 pytest unit tests covering valid input, invalid input, and edge cases" |

## 12. Example Input

```text
FUNCTIONALITY:
A function that takes a list of transaction amounts (floats) and returns
the total, but raises an error if any transaction is negative.

LANGUAGE / VERSION: Python 3.12
FRAMEWORK CONSTRAINTS: Standard library only
STYLE GUIDE: PEP 8, use type hints
ERROR HANDLING: Raise ValueError with a message identifying the invalid amount
TEST REQUIREMENTS: Include pytest tests for valid list, empty list, and a
list containing a negative value
```

## 13. Example Output

```python
def sum_transactions(amounts: list[float]) -> float:
    """
    Sum a list of transaction amounts.

    Raises:
        ValueError: If any amount is negative.
    """
    for amount in amounts:
        if amount < 0:
            raise ValueError(f"Invalid negative transaction amount: {amount}")
    return sum(amounts)


# --- Tests ---
import pytest


def test_sum_transactions_valid_list():
    assert sum_transactions([10.0, 20.5, 5.25]) == 35.75


def test_sum_transactions_empty_list():
    assert sum_transactions([]) == 0


def test_sum_transactions_negative_raises():
    with pytest.raises(ValueError, match="Invalid negative transaction amount: -5"):
        sum_transactions([10.0, -5.0, 20.0])
```

## 14. Customization Guide

- **Always specify the exact language version**: Syntax and available features differ meaningfully between, e.g., Python 3.8 and 3.12, or ES2015 and ES2023 — vague "JavaScript" or "Python" requests risk version-incompatible output.
- **State framework constraints even when the answer is "none"**: Explicitly saying "standard library only" prevents the model from reaching for a convenient but unwanted dependency.
- **Provide existing code context for integration tasks**: A function meant to fit into an existing class or module should be shown that surrounding context so naming, patterns, and imports stay consistent.
- **Be specific about error handling philosophy**: Different codebases handle errors differently (exceptions vs. return codes vs. Result types) — state the convention explicitly rather than letting the model default to its own preference.

## 15. Output Format Options

- Raw code block (language-tagged, e.g., ` ```python `)
- Code + inline comments
- Code + separate test file
- Code + accompanying documentation/docstring
- Diff format (for modifying existing code)

## 16. Best Practices

- Specify language version, style guide, and framework constraints even when they seem obvious — assumptions here are a leading cause of unusable first-pass code.
- Ask for tests alongside the implementation when correctness matters, not as a separate follow-up request.
- Request that ambiguous parts of the spec be flagged rather than silently resolved with a guess.
- For integration tasks, always provide the relevant surrounding code context rather than expecting the model to infer conventions from nothing.

## 17. Common Mistakes

- Omitting the language version, leading to syntax that doesn't match the actual target runtime.
- Not stating framework/dependency constraints, resulting in code that pulls in an unwanted library.
- Requesting code without also requesting tests, then discovering edge cases weren't handled only after deployment.
- Providing no existing code context for an integration task, producing code that doesn't match the codebase's naming or structural conventions.

## 18. Prompt Variations

- **Basic Version**: Functionality description + language only, no style guide or tests.
- **Advanced Version**: Full structure with style guide, error handling, and test requirements (Section 10).
- **Expert Version**: Adds a requirement for the model to also state Big-O time/space complexity of the solution and to propose one alternative implementation approach with its own trade-offs, useful for performance-sensitive or interview-prep contexts.

## 19. Related Prompts

- `22_Debugging_Prompts.md` — for fixing issues in code that's already been generated or written
- `23_SQL_Prompts.md` — a specialized code-generation case for database queries
- `04_Chain_of_Thought.md` — useful for algorithmically complex functions where reasoning through the approach before coding improves correctness

## 20. Tips

- For any code involving business logic (pricing, dates, currency), explicitly listing edge cases you care about (leap years, zero/negative values, empty inputs) in the prompt catches far more issues than a generic "handle edge cases" instruction.
- When working within an existing codebase, pasting a short representative example of an existing similar function is often more effective than describing the style guide in words.

## 21. Limitations

- Generated code should always be reviewed and tested before production use — even well-specified prompts can produce subtly incorrect logic, especially for complex algorithms.
- Model knowledge of very new language features, libraries, or framework versions may be incomplete or outdated relative to the model's training cutoff.
- Long or complex existing-code context may exceed what can be usefully included in a single prompt; very large integrations may need to be broken into smaller, chained requests (see `14_Prompt_Chaining.md`).

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less specialized for code generation) |
| Llama (open-source) | ✅ (code-specialized variants recommended) |
| Mistral | ✅ (code-specialized variants recommended) |

## 23. Tags

`#code-generation` `#software-development` `#programming` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
