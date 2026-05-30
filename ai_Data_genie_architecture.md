flowchart TD
    User["User (Business / Analyst)"]
    FutureAlerts["Future Scope: Proactive\nalerts & scheduled digests"]
    FlaskUI["Flask UI\n(Chat + Crosstab + Charts + Insights)"]
    APIOrch["/api/chat/ask\n(Backend Orchestrator)"]

    User --> FlaskUI
    FutureAlerts -.-> FlaskUI
    FlaskUI --> APIOrch

    APIOrch --> InputNorm["1. Input Normalization"]
    APIOrch --> EventLogs["Persistent Ask Event Logs\n(jsonl)"]

    InputNorm --> SessionCtx["2. Session Context +\nMemory Merge"]
    EventLogs --> Regression["Regression Suite + Golden\nRules + Tuning"]

    SessionCtx --> SchemaLayer["3. Schema Retrieval Layer"]

    Regression --> SemSync["Semantics Sync Scripts\n(metadata/kpi refresh)"]
    FutureRAG["Future Scope: Embedding\nRAG in BigQuery Vector"]

    SchemaLayer --> SemanticLayer["4. Semantic Retrieval Layer"]
    SemSync --> SemanticLayer
    FutureRAG -.-> SemanticLayer

    SemanticLayer --> IntentRes["5. Intent Resolution\n(LLM + Rules)"]

    TemplateEngine["Template Engine\n(Finance / Leadership / Quarterly)"]
    FutureRAG --> TemplateEngine

    IntentRes --> QueryPlan["6. Query Plan AST\n(Contract)"]
    TemplateEngine --> QueryPlan

    QueryPlan --> SQLCompiler["7. Deterministic SQL\nCompiler"]
    SQLCompiler --> SQLValid["8. SQL Validation\n(Static + Intent/Shape Checks)"]
    SQLValid --> BQDryRun["9. BigQuery Dry-Run"]

    FutureAgentic["Future Scope: Agentic SQL\nrepair with confidence gating"]
    FutureAgentic -.-> RepairLoop

    BQDryRun --> RepairLoop["10. Repair / Replan Loop\n(if needed)"]
    RepairLoop --> ExecuteBQ["11. Execute BigQuery\nQuery"]
    ExecuteBQ --> PostProc["Result Post-Processing\n(shape, compare fields, row safety)"]
    PostProc --> Grounding["Answer Grounding +\nGemini Narrative"]
    Grounding --> StructuredJSON["Structured Response JSON"]

    StructuredJSON --> FlaskUI

    style FutureAlerts stroke-dasharray: 5 5
    style FutureRAG stroke-dasharray: 5 5
    style FutureAgentic stroke-dasharray: 5 5
