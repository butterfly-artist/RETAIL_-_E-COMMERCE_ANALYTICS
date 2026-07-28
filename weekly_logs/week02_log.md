# Week 02 Log — Dataset Understanding & Documentation

**Week:** 2  
**Date Range:** [Add Dates]  
**Team:** [Team Number / Team Name]  
**Project:** P06 – CartFlow: Retail & E-Commerce Analytics

---

# 1. Sprint Goal

The goal of Week 2 was to understand the provided CartFlow datasets, document the source files and their schemas, define synthetic data assumptions, organize sample datasets for GitHub, and prepare the project for data exploration in Databricks during Week 3.

---

# 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Studied all source datasets provided in the CartFlow Data Pack | Team | Done | Project Data Pack |
| Documented source files, schemas, data types, keys, and Silver mappings in the Data Dictionary | Team | Done | `docs/data_dictionary.md` |
| Completed Synthetic Data Assumptions documentation | Team | Done | `docs/synthetic_data_assumptions.md` |
| Identified source grains, primary keys, and business purpose of each dataset | Team | Done | Data Dictionary |
| Added small raw sample datasets to the GitHub repository | Team | Done | `data_sample/raw/` |
| Reviewed streaming source files (`order_status_drop_01.json` and `order_status_drop_02.json`) for future implementation | Team | Done | Project Data Pack |
| Created Week 02 project log | Team | Done | `weekly_logs/week02_log.md` |

---

# 3. Key Decisions

- The project will preserve the original grain of every source dataset throughout the Bronze layer before performing any transformations.

- The Data Dictionary will act as the single source of truth for field definitions, business meanings, data types, and source mappings during pipeline development.

- Only small sample datasets will be stored in the GitHub repository, while the complete datasets will remain in the Databricks environment.

- Streaming event files were documented during Week 2 but their implementation will begin during the Week 10 streaming simulation.

---

# 4. Blockers / Risks

| Blocker | Impact | Help Needed |
|---|---|---|
| No major blockers during Week 2 | None | Not Required |

---

# 5. Evidence Added to GitHub

- Updated `docs/data_dictionary.md`
- Updated `docs/synthetic_data_assumptions.md`
- Added sample source files to `data_sample/raw/`
- Added `weekly_logs/week02_log.md`
- Uploaded `week02_data_dictionary_completed.png`
- Uploaded `week02_raw_sample_files.png`

---

# 6. AI Transparency Note

| Question | Response |
|---|---|
| **Where AI helped** | AI assisted in interpreting the project playbook, organizing the Data Dictionary, formatting Markdown documentation, explaining dataset relationships, and preparing the Synthetic Data Assumptions document. |
| **What we changed after AI suggestion** | All file names, row counts, source grains, field definitions, streaming information, and project assumptions were verified against the official CartFlow Project Playbook and Student Data Pack before finalizing the documentation. Unsupported assumptions and incorrect percentages were removed. |
| **What we verified manually** | Source file names, approximate row counts, field names, primary keys, business grains, streaming event schema, repository structure, and all documentation content were manually reviewed using the official project resources. |
| **What we can explain without AI** | We can explain the purpose of each source dataset, source grain, primary keys, business relationships, synthetic data boundaries, project assumptions, repository structure, and how the datasets will flow through the Bronze, Silver Candidate, Trusted Silver, Gold, and Power BI layers. |

---

# 7. Next Week Preparation

- Set up the Databricks workspace and upload the complete project datasets.
- Perform exploratory data analysis on every source dataset.
- Validate row counts, data types, and relationships.
- Identify one-to-many join risks and fan-out scenarios.
- Create temporary views for each dataset in Databricks.
- Begin Week 3 data exploration notebook development.
