# P06 – CartFlow: Retail & E-Commerce Analytics

> **Student Note:** Start with `00_START_HERE.md` and `00_TEMPLATE_INDEX.md`. The placeholder files in this repository provide the required project templates.

---

## Program Information

**Program:** ZENAIZ × BVRIT Hyderabad Data Engineering Internship Program

**Track:** Data Engineering

**Duration:** 12 Weeks

**Team:** [Team Number / Team Name]

**Students:**
- Student 1
- Student 2
- Student 3

**AI Usage:** AI tools were used responsibly for learning, debugging, documentation, and code review. All generated content is manually verified and understood by the project team.

---

# 1. Project Summary

### Domain

Retail & E-Commerce Analytics

### Business Problem

Retail marketplaces generate data from multiple systems such as customer orders, order items, sellers, payments, reviews, and order status events. Since these datasets exist at different levels of detail, directly joining them can create one-to-many fan-out problems that inflate business metrics such as Gross Merchandise Value (GMV), payment totals, review counts, and order statistics.

The objective of CartFlow is to build a governed Lakehouse pipeline that preserves the original source grain, validates data quality, prevents fan-out errors, and produces trusted datasets for business analytics.

### Engineering Objective

Build an end-to-end data engineering pipeline using Databricks that:

- Ingests multiple raw source files
- Preserves source data in the Bronze layer
- Standardizes data in the Silver Candidate layer
- Applies Data Quality and Quarantine rules
- Creates Trusted Silver datasets
- Publishes Gold business tables
- Generates Power BI dashboards using only Gold data
- Demonstrates controlled streaming using incremental event files

### Pipeline Architecture

```
Raw Sources
        │
        ▼
Bronze
        │
        ▼
Silver Candidate
        │
        ▼
Data Quality & Quarantine
        │
        ▼
Trusted Silver
        │
        ▼
Gold Layer
        │
        ▼
Power BI Dashboard
```

### Source Files

- orders.csv
- order_items.parquet
- sellers.json
- payments.csv
- reviews.csv
- order_status_drop_01.json
- order_status_drop_02.json

### Final Deliverables

By the end of the internship, the repository will contain:

- Databricks notebooks
- Bronze, Silver, Trusted Silver and Gold tables
- Data Quality implementation
- Streaming simulation
- Power BI dashboard
- Weekly documentation
- Final project report
- Demo presentation

---

# 2. Technology Stack

| Tool | Purpose |
|------|---------|
| Databricks Free Edition | Spark SQL, PySpark, Lakehouse implementation |
| Spark SQL | Data transformation and analytics |
| PySpark | Data engineering and validation |
| Delta Lake | Managed Bronze, Silver and Gold tables |
| GitHub | Version control and project documentation |
| Power BI Desktop | Business dashboards |
| AI Assistant | Documentation, debugging and learning support |

---

# 3. Repository Structure

| Folder | Description |
|---------|-------------|
| docs/ | Project documentation and design documents |
| notebooks/ | Databricks notebooks for every pipeline stage |
| src/ | Helper scripts and reusable functions |
| data_sample/ | Small sample datasets for GitHub |
| dashboard/ | Power BI report and dashboard assets |
| streaming/ | Streaming design and configuration |
| screenshots/ | Weekly evidence and execution screenshots |
| weekly_logs/ | Weekly progress logs |
| final_submission/ | Final report and submission documents |

---

# 4. Project Roadmap

| Week | Focus |
|------|-------|
| Week 1 | Repository setup and project documentation |
| Week 2 | Dataset understanding and data dictionary |
| Week 3 | Data exploration and relationship analysis |
| Week 4 | Bronze layer ingestion |
| Week 5 | Silver Candidate transformations |
| Week 6 | Data Quality and Quarantine |
| Week 7 | Gold layer implementation |
| Week 8 | Power BI integration |
| Week 9 | Dashboard refinement |
| Week 10 | Streaming simulation |
| Week 11 | Integration and testing |
| Week 12 | Final demonstration and submission |

---

# 5. Project Rules

- Power BI must consume data only from the Gold layer.
- Raw, Bronze, Silver Candidate, and Quarantine datasets must never be used directly for reporting.
- All data quality failures must remain traceable through quarantine tables.
- Every project update must be committed to GitHub with supporting evidence.
- Large datasets must remain in Databricks; only small sample datasets are stored in GitHub.
- AI-generated content must be reviewed, validated, and understood by every team member before submission.

---

# 6. Expected Project Outcome

By the completion of the internship, the project aims to demonstrate:

- An end-to-end Lakehouse pipeline implemented in Databricks.
- Governed Bronze, Silver Candidate, Trusted Silver, and Gold layers.
- Data Quality validation with quarantine and reconciliation.
- Trusted business KPIs generated from Gold tables.
- A three-page Power BI dashboard built exclusively on Gold datasets.
- Structured Streaming simulation using incremental event files.
- Complete GitHub documentation, weekly evidence, and project reports.
- The ability of every team member to explain the complete data pipeline, architecture, and implementation.
