# Research Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-33

---

## 01. Overview

Research prompting is a domain-specific technique for gathering, evaluating, and synthesizing information on a topic — distinct from general question-answering in that it requires source awareness, explicit handling of conflicting information, and a clear scope boundary (what's in vs. out of the research question). Effective research prompts specify the research question precisely, the depth/rigor expected, what counts as an acceptable source, and how to handle the common reality that sources disagree or that some questions don't have a settled answer.

## 02. Purpose

- Produce well-scoped research that directly addresses the actual question, not a tangentially related overview.
- Handle source disagreement transparently rather than presenting one view as settled consensus.
- Match research depth to the actual need (quick overview vs. exhaustive literature review).
- Distinguish well-established facts from contested or emerging claims.

## 03. Use Cases

- Topic overviews and background research
- Literature review synthesis
- Competitive/market research
- Fact-finding for decision-making
- Due diligence research
- Academic or technical research question exploration

## 04. Target AI Models

Most effective when paired with web search / retrieval capability:

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later, with browsing enabled)
- Claude (all Claude models, with web search enabled)
- Gemini (with search grounding)
- Grok (with search access)
- Perplexity (natively research/search-oriented)

## 05. Prompt Category

`Domain-Specific` · `Research` · `Information Synthesis`

## 06. Difficulty Level

**Intermediate to Advanced**

## 07. Required Inputs

- **Research question**: The specific question to investigate
- **Scope boundaries**: What's included and excluded from the research

## 08. Optional Inputs

- Depth/rigor expected (quick overview vs. exhaustive)
- Source quality requirements
- Time frame relevance (e.g., only recent developments)
- Format for presenting findings
- How to handle conflicting sources

## 09. Variables

| Variable | Required? |
|---|---|
| `{{research_question}}` | Yes |
| `{{scope_boundaries}}` | Yes |
| `{{depth_rigor}}` | No |
| `{{source_quality_requirements}}` | No |
| `{{time_frame_relevance}}` | No |
| `{{conflict_handling}}` | No |

## 10. Prompt Template

```text
Research the following question thoroughly.

RESEARCH QUESTION:
{{research_question}}

SCOPE BOUNDARIES (what's in/out of scope):
{{scope_boundaries}}

DEPTH/RIGOR EXPECTED:
{{depth_rigor}}

SOURCE QUALITY REQUIREMENTS:
{{source_quality_requirements}}

TIME FRAME RELEVANCE:
{{time_frame_relevance}}

INSTRUCTIONS:
1. Gather information directly relevant to the research question, staying
   within the stated scope boundaries.
2. Distinguish well-established facts from contested, emerging, or
   single-source claims.
3. If sources disagree, present the disagreement explicitly rather than
   silently picking one view: {{conflict_handling}}
4. Cite sources for specific claims, especially statistics or contested points.
5. Note any significant gaps where the research question couldn't be fully
   answered from available information.
6. Summarize findings clearly, organized around the actual research
   question rather than a generic topic overview.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{research_question}}` | The specific question to investigate | "What are the documented health effects of intermittent fasting on metabolic markers?" |
| `{{scope_boundaries}}` | What's included/excluded | "Focus on human studies only, not animal models; exclude weight-loss claims specifically, focus on metabolic markers" |
| `{{depth_rigor}}` | How thorough the research should be | "Moderate depth — summarize key findings, not an exhaustive literature review" |
| `{{source_quality_requirements}}` | What sources are acceptable | "Prefer peer-reviewed studies and systematic reviews over general health websites" |
| `{{time_frame_relevance}}` | Recency requirements | "Prioritize studies from the last 10 years" |
| `{{conflict_handling}}` | How to present disagreement | "Present both findings with their respective sample sizes/methodology differences noted" |

## 12. Example Input

```text
RESEARCH QUESTION: What is the current scientific consensus on the
relationship between screen time and sleep quality in adolescents?

SCOPE: Focus on adolescents (13-18), sleep quality specifically (not
general wellbeing), exclude adult studies

DEPTH: Moderate — key findings summary, not exhaustive review
SOURCE QUALITY: Prefer peer-reviewed research and major health
organization guidance over general news articles
TIME FRAME: Prioritize research from the last 8 years
CONFLICT HANDLING: Present differing findings with methodology context
```

## 13. Example Output

```text
[Note: In actual use with search enabled, this section would contain real,
current findings with citations. The structure below illustrates the
expected shape of the output.]

SUMMARY OF FINDINGS:

There is reasonably strong consensus that screen time close to bedtime is
associated with reduced sleep quality in adolescents, primarily attributed
to two mechanisms: blue light exposure suppressing melatonin production,
and the psychologically stimulating nature of social media/gaming content
delaying sleep onset. [Citations would appear here for specific studies.]

WHERE FINDINGS DIVERGE:
Some studies find the blue-light mechanism itself has a modest, sometimes
non-significant effect once controlling for content engagement, suggesting
the psychological stimulation of content may be the larger factor rather
than light exposure alone. This is a genuinely active area of methodological
disagreement, not simply weaker vs. stronger evidence on the same
question — different studies isolate different variables.

GAPS:
Long-term causal studies (as opposed to correlational) are less common;
most available research establishes association, not proven causation, for
the specific screen-time-to-sleep-quality-decline pathway.

CONCLUSION:
The overall direction of the relationship (more evening screen time,
generally worse sleep quality) is well-supported, but the precise
mechanism and magnitude remain areas of ongoing research rather than fully
settled science.
```

## 14. Customization Guide

- **Set scope boundaries explicitly**: Research questions often have implicit boundaries the asker knows but doesn't state (e.g., a specific population, geography, or time period) — making these explicit prevents research that technically answers the question but misses the actual need.
- **Calibrate depth to the actual decision at stake**: A quick decision needs a fast overview; a high-stakes decision (medical, legal, financial, strategic) warrants requesting more rigorous, exhaustively-sourced research.
- **State source quality requirements for anything consequential**: "Any source" and "peer-reviewed only" produce very different research outputs — be explicit about what's acceptable for the stakes involved.
- **Plan for conflict handling upfront**: Most non-trivial research questions have some degree of source disagreement; deciding in advance how that should be presented (both sides, weighted by evidence quality, flagged as unresolved) avoids an artificially confident-sounding single answer.

## 15. Output Format Options

- Markdown (narrative + citations)
- Bullet List (for quick-scan findings)
- Table (for comparing multiple sources/findings)
- Annotated bibliography format

## 16. Best Practices

- State scope boundaries explicitly, even when they seem obvious from the question itself.
- Request explicit handling of source disagreement rather than allowing a single view to be presented as unanimous consensus.
- Match depth/rigor expectations to the actual stakes of the decision the research supports.
- Ask for gaps to be noted explicitly — an honest "this wasn't fully answerable from available sources" is more useful than a confident-sounding but under-supported claim.

## 17. Common Mistakes

- Vague research questions that produce a broad topic overview rather than an answer to the actual question at hand.
- Not specifying source quality requirements, resulting in research that mixes high- and low-quality sources without distinction.
- Accepting a single, confident-sounding answer without checking whether the underlying sources actually agree.
- Skipping scope boundaries, leading to research that technically covers the topic but misses the specific angle that actually mattered.

## 18. Prompt Variations

- **Basic Version**: Research question only, no scope/depth/source specification.
- **Advanced Version**: Full structure with scope, depth, source quality, and conflict handling (Section 10).
- **Expert Version**: Adds a requirement for a confidence assessment per major finding (e.g., "well-established," "emerging evidence," "contested") and a brief note on what additional research would most reduce remaining uncertainty.

## 19. Related Prompts

- `20_RAG_Prompting.md` — for research strictly grounded in a specific pre-supplied document set rather than open web research
- `25_Data_Analysis_Prompts.md` — quantitative research questions often flow into data analysis once relevant datasets are identified
- `34_Summarization_Prompts.md` — research findings often need further condensing into an executive summary

## 20. Tips

- For research questions where currency matters (recent developments, ongoing situations), explicitly requesting the most recent available sources first, then checking whether older foundational sources still hold, produces a more accurate picture than treating all sources as equally current.
- Asking "what would change this conclusion" for a research finding you intend to act on is a fast way to surface the finding's actual robustness before relying on it for a real decision.

## 21. Limitations

- Research quality is capped by what's actually retrievable — without live search/retrieval access, findings are limited to the model's training-time knowledge, which may be outdated for fast-moving topics.
- The model cannot independently verify the credibility of a source beyond general reasoning about it; source evaluation should still involve human judgment for high-stakes research.
- Complex, multi-faceted research questions often benefit from being broken into several more focused sub-questions (see Least-to-Most Prompting, Template 12) rather than answered in a single broad pass.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ (best with browsing enabled) |
| Claude | ✅ (best with web search enabled) |
| Gemini | ✅ (best with search grounding) |
| Grok | ✅ (best with search access) |
| Perplexity | ✅ (natively research-oriented) |
| Llama (open-source) | ⚠️ Limited without retrieval/search integration |
| Mistral | ⚠️ Limited without retrieval/search integration |

## 23. Tags

`#research` `#information-synthesis` `#fact-finding` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
