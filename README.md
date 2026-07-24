# [PROJECT TITLE]

> **Student note:** Start with `00_START_HERE.md` and `00_TEMPLATE_INDEX.md`. The placeholder files inside this repo are the templates.


**Program:** ZENAIZ x BVRIT Hyderabad Data Engineering Internship Program  
**Track:** Data Engineering  
**Duration:** 12 Weeks  
**Team:** [Team Number / Team Name]  
**Students:** [Student 1], [Student 2], [Student 3]  
**AI Teammate:** Used responsibly for explanation, debugging, review, and documentation support.
``` markdown

## 1. Project Summary

* **Domain:** Retail & E-Commerce Operations Analytics.
* **Core engineering problem:** Raw one-to-many child table joins multiply financial metrics (such as GMV and payment totals) and review counts. The engineering objective is to build a governed lakehouse pipeline that preserves each unique source grain, captures multi-rule quality failures, and reconciles data across layers to eliminate inflating fan-out risks before publishing decision-ready dashboards.
* **Main pipeline:** Raw Sources (`orders.csv`, `order_items.parquet`, `sellers.json`, `payments.csv`, `reviews.csv`) → Bronze (`bronze_*` raw tables plus lineage metadata) → Silver Candidate (typed/standardized pre-quality tables) → Data Quality Rules Engine Router → Trusted Silver / Quarantine Tables → Gold Dimensions & Facts (with child tables aggregated independently to `order_id` before fact table creation) → Power BI Semantic Model Reports.
* **Streaming Simulation Branch:** A separate architectural path utilizes a two-drop incremental file-stream ingestion process (`order_status_drop_01.json` and `order_status_drop_02.json`) via Databricks Auto Loader and Spark Structured Streaming, incorporating an explicit schema, stable checkpoints, a 30-minute event-time watermark, deduplication, and streaming data quality routing.
* **Final outcome:** A clean, reproducible GitHub repository, runnable Databricks notebooks, governed batch and streaming lakehouse tables, a three-page decision-led Power BI dashboard, completed submission artifacts (final report, demo script, and checklists), and a recorded team presentation.

---

## 2. Tools Used

| Tool | Purpose |
| :--- | :--- |
| Databricks Free Edition | Spark SQL notebooks, light Python/PySpark, Bronze/Silver/Gold tables, streaming simulation |
| GitHub | Repository, weekly evidence, documentation, screenshots, commits |
| Power BI Desktop | Dashboard from Gold outputs |
| AI Assistant | Explanation, debugging, review, documentation support with manual verification |

---

## 3. Repository Navigation

| Folder / File | Purpose |
| :--- | :--- |
| `docs/` | Project documentation, data dictionary, DQ summary, Gold metric definitions (`problem_charter.md`, `data_dictionary.md`, `synthetic_data_assumptions.md`, `data_quality_summary.md`, `gold_metrics_definition.md`) |
| `src/` | Data generation and reusable quality helper scripts (`data_quality_rules.py`) |
| `notebooks/` | Databricks notebooks for exploration (`01_data_exploration.ipynb`), Bronze (`02_bronze_ingestion.ipynb`), Silver Candidate/DQ (`03_silver_transformations.ipynb`, `04_data_quality_checks.ipynb`), Gold (`05_gold_aggregations.ipynb`), export (`06_powerbi_export.ipynb`), and streaming (`07_streaming_simulation.ipynb`) |
| `data_sample/` | Tiny, privacy-safe GitHub extracts across three subfolders: `raw/` for initial files, `streaming/` for event drops, and `gold_exports/` for small semantic tables |
| `dashboard/` | Power BI `.pbix` file, wireframe documentation, dashboard notes, and its companion `README.md` |
| `streaming/` | Streaming framework metadata, architectural layout `structured_streaming_design.md`, and event validation parameters |
| `screenshots/` | Weekly localized evidence of functioning Spark execution plans, database counts, data model relations, and interface layouts |
| `weekly_logs/` | Weekly execution logs (`week01_log.md` through `week12_log.md`) and AI transparency notes |
| `final_submission/` | Final report, demo script, team contribution, and final submission checklist |

---

## 4. 12-Week Execution Map

| Week | Focus | Main Evidence |
| ---: | :--- | :--- |
| 1 | Project framing + GitHub | `README.md`, `docs/problem_charter.md`, finalized `week01_log.md` |
| 2 | Dataset design | Placement of safe file samples, updated `docs/data_dictionary.md`, `docs/synthetic_data_assumptions.md`, and `week02_log.md` |
| 3 | Databricks exploration | Exploration notebook, distinct reference anti-join outputs, populated `docs/pipeline_walkthrough.md`, and `week03_log.md` |
| 4 | Bronze ingestion | Complete execution of `02_bronze_ingestion.ipynb`, creation of 5 metadata-enriched raw tables, and `week04_log.md` |
| 5 | Silver standardization | Cast typed attributes safely via `try_cast`, derived logistics/time metrics, category standardizations, and `week05_log.md` |
| 6 | Data quality | Implementation of 8 core data quality check items, quarantine routing tables, validation pass, and `week06_log.md` |
| 7 | Gold metrics | Materialized star-schema dimensions/facts, single-grain summary tables, 8 distinct KPI expressions, and `week07_log.md` |
| 8 | Power BI draft | Run of `06_powerbi_export.ipynb`, established single-direction table relations, built Commerce Overview page, and `week08_log.md` |
| 9 | Dashboard refinement | Completion of dashboard pages 2-3, descriptive narrative logs, final dashboard insights documentation, and `week09_log.md` |
| 10 | Streaming simulation | Running `07_streaming_simulation.ipynb` incrementally with Drop 01 and Drop 02, checkpoint integrity proof, and `week10_log.md` |
| 11 | Integration | End-to-end integration walkthrough, runbook execution, mismatch alignment checks, finalized demo script, and `week11_log.md` |
| 12 | Final demo | Purged repository files, compiled final report, submission checklist compliance, and `week12_log.md` |

---

## 5. Important Rules

* **No Direct File Shortcuts:** Power BI must only read governed Gold layer data outputs. Connecting reports directly to raw CSVs, Bronze tables, Silver Candidate records, or Quarantine vectors is strictly prohibited.
* **Plagiarism & Authenticity:** Copying, clone-dumping, or submitting external internet GitHub repositories as original work violates compliance guidelines.
* **Reference Management:** Any external technical formulas, documentation guides, or reference modules must be explicitly logged in `docs/references.md`.
* **AI Governance:** All AI-generated PySpark, SQL blocks, or structural content must be manually verified, fully explainable by all team members, and accompanied by a detailed AI Transparency Note.
* **Continuous Integration Trails:** Every single week of the execution timeline must be verified with an active GitHub commit and a populated weekly execution log.
* **Repository Data Constraints:** Large data files must never be committed to GitHub. Maintain small samples within `data_sample/` and handle high-volume generated profiles directly inside Databricks infrastructure.

---

## 6. Final Project Proof

By Week 12, this repository proves that the team has successfully met the following exit criteria:
* **Source Dataset Architecture:** Profiled and validated 7 distinct source files, formats, physical schemas, constraints, and baseline count checksums.
* **Batch Execution Mastery:** Built a robust batch pipeline using Spark SQL and light PySpark within Databricks without modifying raw structures.
* **Bronze Data Layer Ingestion:** Established raw-preserving `bronze_*` components embedded with rich audit tracking columns and verified deterministic, duplicate-free rerun logic.
* **Silver Standardization:** Cast typed attributes safely using `try_cast`, derived logistics/time metrics, and standardized domain formats while maintaining complete trace lineage.
* **Data Quality Router:** Enforced 8 individual check criteria, captured overlapping failure attributes, isolated violations to specialized quarantine tables, and proved exact conservation rules (`Candidate = Trusted + Quarantine`).
* **Governed Gold Star Models:** Implemented unique grain dimensions, facts, and daily summaries, specifically correcting child aggregation fan-out to reconcile transaction totals within INR 0.05.
* **Analytics Interfaces:** Constructed a 3-page, fully interactive, accessible Power BI dashboard linked exclusively to Gold views, with card calculations matching independent lakehouse verification queries.
* **Structured Stream Ingestion:** Simulated an active file streaming sequence using an explicit event schema, persistent checkpoints, a 30-minute late-arrival watermark, windowed deduplication, and verified no-new-file processing stability.
* **Traceable Git Evidence Rails:** Produced a consistent history of technical changes backed by standard log arrays and clear individual work ownership.
* **Technical Presentation Competence:** Demonstrated that all three team members can fully articulate, defend, and walk through the comprehensive data lifecycle, operational limits, and architecture.

```
