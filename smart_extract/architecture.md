
flowchart LR

    A[External Sources<br>Competitor Websites<br>Public Data Sources]

    B[Data Acquisition Layer<br>URL Management<br>Web Scraping<br>Scheduling]

    C[AI Processing Layer<br>Classification<br>Entity Extraction<br>Content Understanding]

    D[Data Engineering Layer<br>Transformation<br>Validation<br>Deduplication]

    E[Storage & Backend Layer<br>JSON / CSV<br>Database<br>Application Services]

    F[Consumption Layer<br>Dashboards<br>Reports<br>APIs]

    G[Monitoring & Observability<br>Logging<br>Error Tracking<br>Performance Metrics]

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F

    E --> G
