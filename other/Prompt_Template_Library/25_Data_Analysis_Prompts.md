# Data Analysis Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-25

---

## 01. Overview

Data Analysis prompting is a domain-specific technique for extracting insights, identifying patterns, and answering questions from a dataset. Effective prompts in this domain need to specify the actual data structure (columns, types, size), the analytical question being asked, the statistical rigor expected (descriptive vs. inferential), and how to handle data quality issues (missing values, outliers) — details that determine whether the resulting analysis is trustworthy or just plausible-sounding.

## 02. Purpose

- Produce analysis grounded in the actual data provided, not generic or assumed patterns.
- Ensure appropriate statistical methods are used for the data type and question at hand.
- Surface data quality issues (missing values, outliers, skew) that affect the validity of conclusions.
- Distinguish correlation from causation and flag when a conclusion exceeds what the data supports.

## 03. Use Cases

- Exploratory analysis of a new dataset (identifying trends, distributions, anomalies)
- Answering a specific business question from data (e.g., "which segment has the highest churn?")
- Statistical hypothesis testing or significance assessment
- Building a narrative/report from raw analytical findings
- Identifying data quality issues before deeper analysis

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later, ideally with code execution)
- Claude (all Claude models, ideally with code execution / data analysis tools enabled)
- Gemini
- Grok
- Perplexity (less common for direct data analysis)

## 05. Prompt Category

`Domain-Specific` · `Analytics` · `Statistical`

## 06. Difficulty Level

**Intermediate to Advanced**

## 07. Required Inputs

- **Dataset description**: Columns, types, size, and source
- **Analytical question**: What you want to know from the data

## 08. Optional Inputs

- Known data quality issues (missing values, duplicates)
- Desired statistical rigor (descriptive summary vs. hypothesis testing)
- Segment/grouping variables of interest
- Desired output format (narrative, chart description, table)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{dataset_description}}` | Yes |
| `{{analytical_question}}` | Yes |
| `{{data_quality_notes}}` | No |
| `{{statistical_rigor}}` | No |
| `{{segment_variables}}` | No |
| `{{output_format}}` | No |

## 10. Prompt Template

```text
Analyze the dataset described below to answer the following question.

DATASET DESCRIPTION:
{{dataset_description}}

ANALYTICAL QUESTION:
{{analytical_question}}

KNOWN DATA QUALITY ISSUES:
{{data_quality_notes}}

DESIRED STATISTICAL RIGOR:
{{statistical_rigor}}

SEGMENT/GROUPING VARIABLES OF INTEREST:
{{segment_variables}}

INSTRUCTIONS:
1. Note any data quality issues that could affect the reliability of your
   analysis (missing values, small sample sizes, outliers, skew), even if
   not listed above.
2. Choose an analytical approach appropriate to the data type and question
   — state which method you're using and why.
3. Present findings clearly, distinguishing what the data shows directly
   from any interpretation or inference you're adding.
4. Explicitly flag if the question asks for a causal claim the data can
   only support correlationally.
5. State any limitations or caveats a reader should know before acting on
   this analysis.

Output format: {{output_format}}
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{dataset_description}}` | Structure and content of the data | "10,000 rows of customer transactions: customer_id, purchase_date, amount, category, region" |
| `{{analytical_question}}` | The specific question to answer | "Which product category has seen the largest revenue decline over the past 2 quarters?" |
| `{{data_quality_notes}}` | Known issues affecting the data | "region field has ~8% missing values" |
| `{{statistical_rigor}}` | Depth of statistical treatment expected | "Descriptive statistics only, no hypothesis testing needed" |
| `{{segment_variables}}` | Dimensions to break results down by | "By region and by customer tenure" |
| `{{output_format}}` | How findings should be presented | "A short narrative summary followed by a findings table" |

## 12. Example Input

```text
DATASET DESCRIPTION:
5,000 rows of monthly subscription data: user_id, signup_date, plan_tier
(Basic/Pro/Enterprise), monthly_revenue, cancelled (boolean), cancel_date
(nullable).

ANALYTICAL QUESTION:
Which plan tier has the highest cancellation rate, and is the difference
meaningful or likely just noise?

DATA QUALITY NOTES: cancel_date is null for ~60% of rows (expected — those
are active, non-cancelled users)

STATISTICAL RIGOR: Include a basic significance check, not just raw percentages
OUTPUT FORMAT: Narrative summary + findings table
```

## 13. Example Output

```text
DATA QUALITY NOTE:
The high null rate in cancel_date (~60%) is expected and consistent with
active users, not a data quality problem for this analysis — it's simply
non-applicable for non-cancelled rows.

APPROACH:
Calculated cancellation rate (cancelled=True / total users) per plan_tier,
then ran a chi-square test of independence to assess whether cancellation
rate differs by plan tier more than would be expected by chance.

FINDINGS:

| Plan Tier  | Users | Cancelled | Cancellation Rate |
|------------|-------|-----------|--------------------|
| Basic      | 2,400 | 552       | 23.0%              |
| Pro        | 1,800 | 270       | 15.0%              |
| Enterprise | 800   | 64        | 8.0%               |

Basic tier shows the highest cancellation rate at 23.0%, roughly 3x
Enterprise's rate. A chi-square test of independence indicates this
difference across tiers is very unlikely to be due to chance alone
(the pattern shows a clear, consistent step-down from Basic to Pro to
Enterprise, which supports a real relationship rather than random noise).

INTERPRETATION vs. DATA:
The data directly shows that cancellation rate decreases as plan tier
increases. It does NOT establish why — that could reflect price
sensitivity, feature satisfaction, customer segment differences (e.g.
Enterprise customers may have longer-term contracts with switching costs),
or another unmeasured factor. Attributing this to a single cause would be
a causal claim the data alone doesn't support.

LIMITATIONS:
- No information on subscription length/tenure is included, which could
  be a confounding factor (e.g., Enterprise customers may simply be newer,
  with less time to cancel).
- No pricing or feature-usage data is available to test specific
  explanatory hypotheses.
```

## 14. Customization Guide

- **Describe the actual dataset structure precisely**: Column names, types, and approximate size materially affect what analytical methods are appropriate — vague descriptions ("some sales data") limit the model to generic, non-actionable analysis.
- **State the desired statistical rigor explicitly**: A quick descriptive summary and a rigorous hypothesis test require very different approaches; specify which is needed to avoid over- or under-engineering the analysis.
- **Flag known data quality issues upfront**: This prevents the model from either being misled by them or spending analysis effort re-discovering something you already know.
- **Name segment variables of interest**: Without this, the model may choose different (or no) groupings than what's actually useful for your decision.

## 15. Output Format Options

- Markdown (narrative + table)
- Table
- JSON (for structured findings ingestion)
- Bullet List (for quick-scan findings)
- Chart description (for accompanying visualization)

## 16. Best Practices

- Always provide the actual column names, types, and approximate size of the dataset, not a vague description.
- Explicitly request a distinction between what the data shows directly and any interpretation layered on top.
- Ask for causal vs. correlational flagging by default — this is one of the most common and consequential analytical errors to avoid.
- State known data quality issues so analysis effort isn't wasted rediscovering them, and so findings account for them appropriately.

## 17. Common Mistakes

- Vague dataset descriptions that don't specify actual columns or types, leading to generic, non-grounded analysis.
- Not specifying statistical rigor, resulting in either an over-engineered analysis for a simple question or an under-rigorous one for a decision that actually needs significance testing.
- Accepting a causal-sounding conclusion without checking whether the data and method actually support causation, not just correlation.
- Omitting known data quality caveats, leading to conclusions that don't account for real limitations in the data.

## 18. Prompt Variations

- **Basic Version**: Dataset description + question only, descriptive statistics assumed.
- **Advanced Version**: Full structure with data quality notes, statistical rigor, and segmentation (Section 10).
- **Expert Version**: Adds a request for the model to propose what additional data (if any) would meaningfully strengthen the analysis or resolve an open causal question, useful for planning follow-up data collection.

## 19. Related Prompts

- `23_SQL_Prompts.md` — often the extraction step that produces the dataset analyzed here
- `34_Summarization_Prompts.md` — findings often need to be condensed into an executive summary after full analysis
- `04_Chain_of_Thought.md` — useful for multi-step analytical reasoning, especially when combining several findings into a single conclusion

## 20. Tips

- When working with an actual file (CSV, spreadsheet), providing the model with real, representative sample rows (not just a schema description) often catches data quality issues and type assumptions that a pure schema description would miss.
- For any finding that will inform a real decision, explicitly asking "what would change your conclusion" surfaces the sensitivity/robustness of the finding, which is often more useful than the point estimate alone.

## 21. Limitations

- Without a code execution tool, statistical calculations are based on the model's reasoning rather than actual computed results on the real dataset — for anything beyond simple descriptive statistics, pairing this template with a code execution environment substantially improves reliability.
- Analysis quality is capped by how well the dataset is described; an incomplete or inaccurate description leads to a plausible but ungrounded analysis.
- Complex statistical methods (multivariate modeling, time-series forecasting) benefit from explicit method specification rather than leaving the choice entirely to the model.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ (best with code execution enabled) |
| Claude | ✅ (best with code execution enabled) |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#data-analysis` `#statistics` `#analytics` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
