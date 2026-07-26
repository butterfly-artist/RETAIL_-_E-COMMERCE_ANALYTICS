# Problem Charter

**Week:** 1  
**Owner(s):** []  
**Project:** P06 – CartFlow: Retail & E-Commerce Analytics

---

## 1. Problem Context

CartFlow represents the operations of a fictional retail and e-commerce marketplace where customers place orders, sellers fulfill them, payments are processed, reviews are collected, and order status updates are generated throughout the delivery process.

The project uses multiple source files containing orders, order items, sellers, payments, reviews, and order status events. Since these datasets have different levels of detail (different data grains), directly joining them can create duplicate records, incorrect sales values, inaccurate payment totals, and misleading business metrics.

To solve this, the project builds a governed data engineering pipeline that preserves the original source data, performs data quality validation, prevents fan-out caused by one-to-many joins, and produces trusted business datasets.

The final analytics and dashboards are designed for:

- Commerce Operations Leads
- Seller Performance Managers
- Fulfilment Teams
- Analytics and Product Managers

These users rely on accurate business metrics to monitor order performance, seller performance, payment reconciliation, delivery status, and overall marketplace operations.

---

## 2. Engineering Problem

The project must transform multiple raw retail and e-commerce source files into a trusted Lakehouse pipeline using Databricks.

The pipeline will ingest raw source data, preserve it in the Bronze layer, standardize and validate it in the Silver Candidate layer, apply Data Quality and Quarantine rules, create Trusted Silver datasets, generate Gold business tables and KPIs, and finally deliver dashboard-ready data for Power BI while maintaining complete data lineage and preventing fan-out errors.

---

## 3. Users / Stakeholders

| User / Stakeholder | What they need from the data |
|---|---|
| Commerce Operations Lead | Monitor trusted orders, GMV, AOV, delivery performance, and cancellations |
| Seller Performance Manager | Evaluate seller performance, revenue contribution, customer ratings, and service quality |
| Fulfilment Lead | Track delivery performance, delayed shipments, returns, and fulfilment issues |
| Analytics / Product Manager | Access trusted datasets with complete data lineage for business reporting and KPI analysis |

---

## 4. Scope Inclusions

The project team will build:

- Source data ingestion from approved files
- Bronze layer for raw data preservation
- Silver Candidate layer for standardized and typed data
- Data Quality validation and Quarantine process
- Trusted Silver datasets
- Gold business facts, dimensions, summaries, and KPI calculations
- Power BI dashboard with three reporting pages
- Controlled streaming simulation using order status event files
- GitHub repository with weekly documentation, evidence, and project tracking

---

## 5. Scope Exclusions

The project will **not** include:

- Production e-commerce application development
- Real customer, seller, or payment information
- Production payment gateway integration
- Fraud detection or accounting systems
- Kafka production deployment or enterprise orchestration
- Reporting directly from raw or Bronze data
- Fake screenshots, copied project work, or unexplained AI-generated submissions

---

## 6. Success Criteria

By the end of the 12-week internship, the project will be considered successful if:

- All approved source files are successfully ingested into the Lakehouse pipeline.
- Bronze, Silver Candidate, Data Quality, Trusted Silver, Gold, and Power BI layers are implemented correctly.
- Data quality rules successfully identify, quarantine, and document invalid records.
- Gold business metrics and KPIs are generated accurately using trusted data.
- The Power BI dashboard provides meaningful business insights from Gold tables only.
- The controlled streaming simulation processes incremental order status events successfully.
- GitHub contains complete weekly documentation, evidence, commit history, and project deliverables.
- Every team member can explain the complete end-to-end architecture, data flow, and their assigned area of ownership.
