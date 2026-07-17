# SQL Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-23

---

## 01. Overview

SQL prompting is a domain-specific technique for generating correct, efficient database queries from a natural-language request. Reliable SQL generation depends heavily on details generic prompting often omits: the SQL dialect (PostgreSQL, MySQL, SQL Server, SQLite, BigQuery, etc. — syntax and functions differ meaningfully between them), the actual schema (table names, column names, types, relationships), and performance considerations like indexing and join strategy. Without the schema, a model can only guess at table/column names; without the dialect, it may generate syntax that doesn't run on the target database at all.

## 02. Purpose

- Generate queries that are both syntactically correct for the target dialect and semantically correct against the actual schema.
- Reduce hallucinated table/column names by grounding generation in real schema information.
- Produce efficient queries, not just correct ones — considering indexes, join order, and query plan implications.
- Handle the full range from simple SELECTs to complex multi-table joins, subqueries, and window functions.

## 03. Use Cases

- Writing a query to answer a specific business question from a database
- Converting a natural-language data request into SQL for a BI tool or dashboard
- Optimizing an existing slow-running query
- Writing schema migration or DDL (CREATE/ALTER TABLE) statements
- Translating a query from one SQL dialect to another

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (less common for this use case)

## 05. Prompt Category

`Domain-Specific` · `Database` · `Query Generation`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Request description**: What data/answer is needed
- **SQL dialect**: The specific database system (PostgreSQL, MySQL, SQL Server, SQLite, BigQuery, Snowflake, etc.)
- **Schema**: Relevant table names, column names, types, and relationships (foreign keys)

## 08. Optional Inputs

- Sample data or row counts (for performance context)
- Existing indexes
- Performance constraints (query must run in under X seconds)
- Desired output columns/format

## 09. Variables

| Variable | Required? |
|---|---|
| `{{request_description}}` | Yes |
| `{{sql_dialect}}` | Yes |
| `{{schema_definition}}` | Yes |
| `{{sample_data_context}}` | No |
| `{{existing_indexes}}` | No |
| `{{performance_constraints}}` | No |
| `{{desired_output}}` | No |

## 10. Prompt Template

```text
Write a SQL query for the following request.

REQUEST:
{{request_description}}

SQL DIALECT:
{{sql_dialect}}

SCHEMA:
{{schema_definition}}

EXISTING INDEXES (if relevant to performance):
{{existing_indexes}}

APPROXIMATE ROW COUNTS / DATA CONTEXT (if relevant to performance):
{{sample_data_context}}

PERFORMANCE CONSTRAINTS:
{{performance_constraints}}

DESIRED OUTPUT COLUMNS/FORMAT:
{{desired_output}}

INSTRUCTIONS:
- Use only tables and columns that exist in the schema provided; do not
  invent table or column names.
- Write syntax valid for the specified dialect specifically — note any
  dialect-specific functions used.
- Prefer explicit JOIN syntax over implicit joins in the WHERE clause.
- If the request is ambiguous (e.g., unclear date range, unclear
  aggregation level), state your assumption briefly before the query.
- Briefly note any performance considerations (e.g., missing index that
  would help, expensive operations like unindexed LIKE '%...%').
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{request_description}}` | The natural-language data request | "Find the top 5 customers by total order value in the last 90 days" |
| `{{sql_dialect}}` | The specific database system | "PostgreSQL 16" |
| `{{schema_definition}}` | Relevant tables/columns/relationships | "customers(id, name, email); orders(id, customer_id FK, order_date, total_amount)" |
| `{{existing_indexes}}` | Known indexes that affect query planning | "Index on orders(order_date), index on orders(customer_id)" |
| `{{sample_data_context}}` | Approximate scale of the data | "orders table has ~50 million rows" |
| `{{performance_constraints}}` | Speed/resource requirements | "Must run in under 2 seconds on the production dashboard" |
| `{{desired_output}}` | Specific output shape | "customer_name, total_spent, ordered as a table" |

## 12. Example Input

```text
REQUEST:
Find the top 5 customers by total order value in the last 90 days.

SQL DIALECT: PostgreSQL 16

SCHEMA:
customers(id INT PK, name TEXT, email TEXT)
orders(id INT PK, customer_id INT FK -> customers.id, order_date DATE,
total_amount NUMERIC)

EXISTING INDEXES: Index on orders(order_date), index on orders(customer_id)

PERFORMANCE CONSTRAINTS: Should use existing indexes efficiently.
DESIRED OUTPUT: customer_name, total_spent
```

## 13. Example Output

```sql
SELECT
    c.name AS customer_name,
    SUM(o.total_amount) AS total_spent
FROM customers c
JOIN orders o ON o.customer_id = c.id
WHERE o.order_date >= CURRENT_DATE - INTERVAL '90 days'
GROUP BY c.id, c.name
ORDER BY total_spent DESC
LIMIT 5;
```

```text
NOTES:
- This uses the existing index on orders(order_date) to efficiently filter
  the last 90 days before the join/aggregation, and the index on
  orders(customer_id) benefits the join itself.
- CURRENT_DATE - INTERVAL '90 days' is PostgreSQL-specific syntax; this
  would need to be rewritten (e.g., DATEADD in SQL Server, DATE_SUB in
  MySQL) if targeting a different dialect.
- Grouped by c.id in addition to c.name to ensure correct grouping
  semantics even if two customers happened to share the same name.
```

## 14. Customization Guide

- **Always specify the exact dialect**: Date arithmetic, string functions, `LIMIT` vs. `TOP`, and window function syntax all vary meaningfully between PostgreSQL, MySQL, SQL Server, SQLite, and cloud warehouses like BigQuery/Snowflake.
- **Provide the real schema, not a paraphrase**: Include actual table and column names, types, and foreign key relationships — this is the single biggest factor in avoiding hallucinated column names.
- **Include index information when performance matters**: Without knowing what's indexed, the model can't reason meaningfully about query plan efficiency.
- **State ambiguous business logic explicitly**: Terms like "top customers," "active users," or "recent orders" can mean different things (by revenue vs. by order count; last 30 vs. 90 days) — define them if precision matters.

## 15. Output Format Options

- SQL code block (dialect-tagged where applicable)
- SQL + explanatory notes
- SQL + query execution plan discussion
- Table (for schema documentation alongside queries)

## 16. Best Practices

- Provide the actual schema (DDL or table/column list) rather than describing it in prose — this is the top lever for accuracy.
- Specify the dialect explicitly, every time, even when it seems obvious from context.
- Ask for explicit JOIN syntax and clear aliasing for readability and to avoid ambiguous column references in multi-table queries.
- Request a brief note on performance implications for any query touching large tables.

## 17. Common Mistakes

- Omitting the schema, causing the model to invent plausible-sounding but incorrect table/column names.
- Not specifying the dialect, resulting in syntax that doesn't run on the actual target database.
- Leaving ambiguous business terms (e.g., "recent," "top," "active") undefined, producing a query that answers a different question than intended.
- Requesting complex aggregations without providing index/scale context, missing an opportunity to flag real performance risks.

## 18. Prompt Variations

- **Basic Version**: Request + schema only, no dialect specified, no performance discussion.
- **Advanced Version**: Full structure with dialect, indexes, and performance constraints (Section 10).
- **Expert Version**: Adds a request for the model to also provide the query's expected execution plan behavior (e.g., "this will likely use an index scan on X, followed by a hash join") and an alternative query formulation if the primary one might not scale well.

## 19. Related Prompts

- `21_Code_Generation_Prompts.md` — SQL generation shares the same core principles (version/dialect precision, existing context) applied to a different language domain
- `25_Data_Analysis_Prompts.md` — SQL is often the extraction step feeding into a broader analysis workflow
- `20_RAG_Prompting.md` — schema-grounded generation here mirrors RAG's context-grounding principle, applied to database structure instead of documents

## 20. Tips

- Pasting the actual `CREATE TABLE` statements (DDL) is often the fastest, least ambiguous way to supply schema — it conveys types and constraints precisely without needing separate prose description.
- When the dialect isn't fixed yet, asking the model to note which parts of the query are dialect-specific makes it much easier to port the query later if the target database changes.

## 21. Limitations

- Query correctness is capped by schema accuracy — an incomplete or outdated schema will produce a plausible but incorrect query.
- The model cannot verify actual query performance without an execution/tool-use environment; performance notes are based on general database principles, not measured results from your specific dataset.
- Very large or highly normalized schemas may need to be trimmed to just the relevant tables for a given request, since including an entire enterprise schema in every prompt is often impractical.

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

`#sql` `#database` `#query-generation` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
