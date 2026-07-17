# RAG Prompting (Retrieval-Augmented Generation)

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-20

---

## 01. Overview

RAG (Retrieval-Augmented Generation) prompting structures a request so the model answers **strictly grounded in retrieved documents or passages** — supplied in the prompt alongside the question — rather than relying on its own internal, potentially outdated or incomplete, training knowledge. The model is instructed to base its answer only on the provided context, cite which parts of the context support each claim, and explicitly state when the retrieved context doesn't contain enough information to answer.

This technique is central to building factual, source-grounded AI systems — search assistants, internal knowledge-base Q&A, customer support bots referencing documentation, and any application where answers must be traceable to a specific source rather than the model's general knowledge.

## 02. Purpose

- Ground answers in specific, verifiable, up-to-date source material instead of the model's training data.
- Reduce hallucination by explicitly restricting the model to provided context.
- Enable citation/attribution so answers can be traced back to their source.
- Handle information that postdates or falls outside the model's training knowledge.

## 03. Use Cases

- Internal knowledge-base or documentation Q&A systems
- Customer support bots referencing a specific product manual or policy document
- Legal or compliance Q&A grounded in specific regulations or contracts
- Research assistants summarizing or answering questions about a specific set of papers/articles
- Any application requiring answers to be traceable to a specific, auditable source

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (natively RAG-oriented via search integration)

## 05. Prompt Category

`Grounded Generation` · `Retrieval-Based` · `Factual`

## 06. Difficulty Level

**Advanced**

## 07. Required Inputs

- **User question**: What needs to be answered
- **Retrieved context**: The specific passages/documents to answer from

## 08. Optional Inputs

- Citation format requirements
- Instructions for handling insufficient context
- Source metadata (titles, dates, authors) for attribution

## 09. Variables

| Variable | Required? |
|---|---|
| `{{user_question}}` | Yes |
| `{{retrieved_context}}` | Yes |
| `{{citation_format}}` | No |
| `{{insufficient_context_instruction}}` | No |
| `{{source_metadata}}` | No |

## 10. Prompt Template

```text
Answer the question using ONLY the information in the retrieved context
below. Do not use outside knowledge, even if you believe you know the
answer from elsewhere. If the context does not contain enough information
to answer, say so explicitly rather than filling gaps with assumptions.

RETRIEVED CONTEXT:
{{retrieved_context}}

SOURCE METADATA (if available):
{{source_metadata}}

USER QUESTION:
{{user_question}}

INSTRUCTIONS:
1. Identify which parts of the retrieved context are relevant to the question.
2. Construct your answer using only that information.
3. Cite the specific part of the context that supports each claim, formatted as: {{citation_format}}
4. If the context is insufficient or partially insufficient: {{insufficient_context_instruction}}
5. Do not blend in outside knowledge, even to "fill in" a gap the context leaves open.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{retrieved_context}}` | The passages/documents retrieved for this query | Excerpts from a product manual or policy document |
| `{{source_metadata}}` | Identifying details for attribution | "Source: Employee Handbook, Section 4.2, updated March 2026" |
| `{{user_question}}` | The question to answer from context alone | "What is the company's policy on remote work for new hires?" |
| `{{citation_format}}` | How to reference supporting context | "[Source: Section X]" after each supported claim |
| `{{insufficient_context_instruction}}` | What to do if context doesn't fully answer the question | "State clearly which part of the question cannot be answered from the given context" |

## 12. Example Input

```text
RETRIEVED CONTEXT:
"Employees may work remotely up to 3 days per week after completing a
90-day probationary period. Remote work arrangements must be approved by a
direct manager. Fully remote roles (5 days/week) require separate approval
from HR and are evaluated on a case-by-case basis."

SOURCE METADATA: Employee Handbook, Section 4.2, updated March 2026

USER QUESTION:
Can a new hire work remotely starting their first week?

INSTRUCTIONS:
Answer only from context. Cite the source. State clearly if context is
insufficient for any part of the question.
```

## 13. Example Output

```text
Based on the retrieved context, a new hire cannot work remotely starting
their first week. The policy specifies that remote work (up to 3 days per
week) is only available after completing a 90-day probationary period, and
requires direct manager approval [Source: Employee Handbook, Section 4.2].

The context does not specify whether any exceptions exist for specific
roles or circumstances during the probationary period — if that detail
matters for your situation, it isn't covered in the provided context and
would need to be confirmed separately.
```

## 14. Customization Guide

- **Always include source metadata when available**: Even simple labels (document name, section, date) make citations meaningful and let users verify claims independently.
- **Define the insufficient-context behavior explicitly**: Decide whether the model should partially answer with a caveat, or refuse entirely, when context only partially covers the question — this varies by use case and risk tolerance.
- **Set a strict citation format for downstream parsing**: If citations will be rendered as clickable links or footnotes in an application, specify the exact format (e.g., `[1]`, `(Source: X)`) the model should use.
- **Keep retrieved context focused**: Include only genuinely relevant passages; irrelevant context increases the risk of the model citing something tangential as if it were directly supportive.

## 15. Output Format Options

- Markdown
- JSON
- YAML
- Table
- Bullet List
- XML
- HTML

## 16. Best Practices

- Explicitly forbid outside knowledge, even when the model likely "knows" a plausible answer from training — the entire point of RAG is source-grounding, not just fact-recall.
- Require a citation for every substantive claim, not just a general "based on the context" disclaimer at the end.
- Instruct the model to flag partial insufficiency per sub-question, rather than an all-or-nothing sufficiency judgment for the whole answer.
- Keep retrieved context reasonably concise and relevant — dumping excessive unrelated context increases the risk of citation errors.

## 17. Common Mistakes

- Allowing the model to blend outside knowledge with retrieved context without flagging which is which.
- No citation requirement, making it impossible to verify which context supports which claim.
- Treating "the context doesn't fully answer this" as a reason to refuse entirely, when a well-caveated partial answer is often more useful.
- Including too much irrelevant retrieved context, diluting the signal and increasing the chance of citing something tangential.

## 18. Prompt Variations

- **Basic Version**: Context + question, simple "answer from this context only" instruction, no citation format.
- **Advanced Version**: Full structure with citation format and insufficient-context handling (Section 10).
- **Expert Version**: Adds a confidence/coverage statement at the end — e.g., "This answer is fully supported by the provided context" vs. "This answer is partially supported; the following aspect was not covered" — giving downstream systems a machine-readable confidence signal.

## 19. Related Prompts

- `19_Function_Calling.md` — retrieval itself is often implemented as a function call that supplies the context used here
- `18_Tool_Use_Prompting.md` — governs when to trigger a retrieval in the first place
- `34_Summarization_Prompts.md` — RAG answers are often a targeted, question-driven form of context summarization

## 20. Tips

- RAG prompting is only as good as the retrieval step feeding it — even a perfect prompt can't produce a correct answer if the retrieved context doesn't actually contain the needed information; this template governs generation, not retrieval quality itself.
- For sensitive domains (legal, medical, financial), pairing strict "context only" instructions with an explicit insufficient-context fallback is especially important to avoid the model quietly filling gaps with plausible-sounding but ungrounded content.

## 21. Limitations

- Answer quality is capped by retrieval quality — irrelevant or incomplete retrieved context leads to an incomplete or misleading answer regardless of prompt quality.
- Strict "context only" instructions can sometimes cause the model to be overly conservative on questions where a small, reasonable inference beyond the literal text would actually be helpful and low-risk.
- Long or numerous retrieved documents can strain context window limits, particularly for extensive multi-document RAG setups.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (natively RAG-oriented) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#rag` `#retrieval-augmented-generation` `#grounded-answers` `#citations` `#advanced`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
