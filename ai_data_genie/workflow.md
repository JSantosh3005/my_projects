
# AI Data Genie Workflow

## 1. User Query Submission

The user interacts with the Flask-based web interface and submits a business question such as:

> "Show quarterly revenue trend for top customers."

The system also supports future proactive alerts and recommendation-driven interactions.

---

## 2. API Orchestration Layer

All requests are routed through a centralized API Orchestrator.

Responsibilities:

* Request validation
* Workflow routing
* Component coordination
* Error handling
* Response assembly

This acts as the central brain of the platform.

---

## 3. Input Normalization

The incoming question is standardized before processing.

Activities:

* Remove noise
* Standardize terminology
* Normalize date formats
* Resolve common aliases
* Clean user input

Example:

```text
rev by cust last qtr
```

becomes

```text
Show revenue by customer for previous quarter
```

---

## 4. Session Context & Memory Merge

The system enriches the request with contextual information.

Sources:

* Current session history
* Previous user interactions
* Business context
* User preferences

This enables conversational continuity.

Example:

```text
Show same report as last week
```

The system understands which report was previously discussed.

---

## 5. Schema Retrieval Layer

The platform identifies relevant database structures.

Retrieved information:

* Datasets
* Tables
* Columns
* Relationships
* Primary metrics

Example:

```text
Revenue
```

may map to

```sql
sales_fact.revenue_amount
```

---

## 6. Semantic Retrieval Layer

Business meaning is retrieved beyond raw schema.

Sources:

* KPI metadata
* Business glossary
* Metric definitions
* Semantic mappings

Examples:

```text
Revenue
Sales
Turnover
```

can be mapped to the same business metric.

Future versions may include:

* Vector search
* Embedding-based retrieval
* BigQuery Vector Search

---

## 7. Intent Resolution

A combination of:

* LLM reasoning
* Rule-based validation

determines:

* User objective
* Required metrics
* Filters
* Aggregation level
* Time period

Output:

```json
{
  "intent": "trend_analysis",
  "metric": "revenue",
  "period": "quarterly"
}
```

---

## 8. Query Plan Generation (AST Contract)

The request is transformed into a structured query plan.

The plan defines:

* Metrics
* Dimensions
* Filters
* Sorting
* Aggregations

This creates a deterministic contract before SQL generation.

Example:

```json
{
  "metric": "revenue",
  "group_by": "customer",
  "time_period": "quarter"
}
```

---

## 9. Template Engine Support

Predefined analytical templates can augment the plan.

Examples:

* Finance Reports
* Leadership Dashboards
* Quarterly Reviews
* Executive Summaries

This ensures consistency across enterprise reporting.

---

## 10. Deterministic SQL Compilation

The Query Plan AST is converted into SQL.

Characteristics:

* Controlled generation
* No hallucinated tables
* Schema-aware
* Reproducible output

Result:

```sql
SELECT
customer_name,
SUM(revenue_amount)
FROM sales_fact
GROUP BY customer_name
```

---

## 11. SQL Validation

Generated SQL undergoes validation checks.

Checks include:

### Static Validation

* Syntax
* Table existence
* Column existence

### Intent Validation

* Does SQL answer the question?
* Correct aggregation?
* Correct filters?

### Shape Validation

* Expected output structure
* Metric consistency

---

## 12. BigQuery Dry Run

Before execution:

* Cost estimation
* Resource estimation
* Query validation

No actual data is scanned.

Benefits:

* Reduced cost
* Faster failure detection
* Safer execution

---

## 13. Repair / Replan Loop

If validation fails:

The system automatically:

* Adjusts query plan
* Repairs SQL
* Re-validates

Future versions may support:

* Agentic SQL repair
* Confidence-based correction workflows

---

## 14. BigQuery Execution

Validated SQL is executed against BigQuery.

Output:

* Result set
* Aggregations
* KPIs
* Trends

---

## 15. Result Post Processing

Raw database results are cleaned and enriched.

Activities:

* Type formatting
* Comparison calculations
* Variance computation
* Row safety checks
* Business formatting

---

## 16. Answer Grounding & Narrative Generation

Gemini generates business-friendly insights based on actual query results.

Example:

> Revenue increased 12.4% quarter-over-quarter, primarily driven by Enterprise customers.

This step transforms data into actionable intelligence.

---

## 17. Structured Response Generation

The system produces a standardized response payload.

Example:

```json
{
  "sql": "...",
  "data": [...],
  "insights": "...",
  "visualization": {...}
}
```

---

## 18. User Presentation Layer

The Flask UI displays:

* Tables
* KPIs
* Charts
* Business insights
* Downloadable reports

---

# Continuous Learning Components

### Persistent Ask Event Logs

Every interaction is stored for:

* Auditability
* Analytics
* Performance tuning

---

### Regression Suite

Used to:

* Prevent model drift
* Validate changes
* Maintain SQL quality

---

### Semantic Sync Scripts

Regular jobs refresh:

* KPI metadata
* Business glossary
* Semantic mappings

ensuring the system stays aligned with evolving business definitions.

---

# Future Roadmap

### Proactive Alerts

* KPI anomaly detection
* Scheduled insights
* Threshold monitoring

### Vector RAG

* Semantic retrieval from embeddings
* Business knowledge search
* Metadata intelligence

### Agentic SQL Repair

* Autonomous query correction
* Confidence scoring
* Multi-step reasoning loops
