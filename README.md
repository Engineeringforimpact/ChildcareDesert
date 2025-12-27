# Cloud-Native Data Platform (Foundational)  
## Childcare Supply, Demand & “Childcare Desert” Intelligence Platform (MA)

**Timeline:** 6 weeks  
**Effort:** 20 hours/week  
**Scope:** Massachusetts, ZIP/ZCTA level  
**Goal:** Finish fast, learn deeply, publish confidently  

---

## 🎯 Project Overview

This project delivers a **cloud-native, public-data lakehouse** that identifies **childcare deserts** across Massachusetts at the ZIP (ZCTA) level.

**MVP-first mindset:**  
Scope is intentionally compressed. Polish is intentionally limited. The focus is on **architecture correctness, analytical clarity, and portfolio signal**.

**Definition of Done (MVP):**

- Public GitHub repository
- Reproducible AWS-based lakehouse
- One authoritative analytical table
- One clear map + one strong table
- Uses **only public data**
- Explains childcare deserts clearly in under 2 minutes

---

## 🧱 Technology Stack

- **Cloud:** AWS  
- **Storage:** S3 (raw + curated zones)  
- **Query Engine:** Athena  
- **Data Format:** Parquet  
- **Analytics Engineering:** dbt (Athena adapter)  
- **Visualization:** Power BI or Python (Geo)  
- **AI:** Optional, minimal, last step only  

> No Redshift. No over-engineering. No unnecessary services.

---

## 📌 Core Metric

**Childcare Desert Indicator**

- `children_0_5_per_provider`
- Geography: **ZCTA**
- Supply proxy: licensed childcare providers
- Demand proxy: Census ACS population age 0–5

**Key assumptions (documented):**

- Families may cross ZIP boundaries
- Provider count is a proxy for capacity
- ZCTA chosen for Census alignment and availability

---

# 🚀 6-Week Execution Plan

## 🗓️ Week 1 — Problem Framing & Environment Setup

### Outcome
You can clearly explain:
- What a childcare desert is
- How it’s measured
- Where the data comes from

### Tasks
**Domain & Metrics (8h)**
- Define childcare desert metric
- Choose ZCTA as geography
- Document assumptions

**Repo Scaffolding (6h)**
- Create repository structure
- README skeleton
- Architecture Decision Records (ADRs):
  - Why ZCTA
  - Why provider count
  - Why AWS + Athena

**AWS Setup (6h)**
- S3 bucket
- IAM role
- Athena access
- Test S3 → Athena query

### Deliverables
- `README.md` (problem + scope)
- `docs/metric_definitions.md`
- AWS account configured

> **Pro tip:** If you can’t explain the project in 60 seconds yet, don’t write more code.

---

## 🗓️ Week 2 — Public Data Ingestion

### Outcome
Raw public datasets land in S3, reproducibly.

### Tasks
**Demand: Census ACS (8h)**
- ACS 5-year data
- Population age 0–5 by ZCTA
- Store raw files + metadata

**Supply: MA Childcare Licensing (6h)**
- Download licensing dataset
- Extract address + ZIP
- Store raw files

**Geography: ZCTA Boundaries (6h)**
- TIGER/Line ZCTA shapefile
- Store raw shapefile
- Validate counts and ZIP coverage

### Deliverables
- Raw data in S3:
  - `/raw/census/`
  - `/raw/licensing/`
  - `/raw/geography/`
- Ingestion scripts committed

> **Pro tip:** Raw = immutable. Don’t clean yet.

---

## 🗓️ Week 3 — Curated Zone & Athena

### Outcome
Clean joins run successfully in Athena.

### Tasks
**Curated Data (8h)**
- Convert raw datasets to Parquet
- Partition by year and state
- Normalize ZIP/ZCTA fields

**Glue & Athena (6h)**
- Register curated tables
- Validate schemas
- Run join queries

**Data Sanity Checks (6h)**
- ZCTA coverage checks
- Missing ZIPs
- Outlier detection

### Deliverables
- `/curated/` Parquet datasets
- Saved Athena SQL queries

> **Pro tip:** If joins fail here, stop and fix. Everything downstream depends on this.

---

## 🗓️ Week 4 — dbt Models (Core Value)

### Outcome
One clean, authoritative analytical table.

### Tasks
**dbt Setup (8h)**
- Initialize dbt project
- Configure Athena adapter
- Create staging models

**Mart Model (8h)**
- Aggregate:
  - Children age 0–5 per ZCTA
  - Providers per ZCTA
- Compute:
  - `children_per_provider`
  - `desert_flag`

**Tests & Docs (4h)**
- Non-null tests
- Uniqueness tests
- Threshold validation
- Assumptions documented

### Deliverables
- `mart_childcare_desert_zcta`
- dbt tests passing

> **Pro tip:** One perfect mart table beats ten half-finished ones.

---

## 🗓️ Week 5 — Visualization & Portfolio Polish

### Outcome
A visual that communicates instantly.

### Tasks
**Map (10h)**
- Choropleth by `children_per_provider`
- Highlight desert ZCTAs
- KPI tooltips

**Table (6h)**
- Top 20 worst ZIPs
- Best-served ZIPs
- Simple filters

**README Polish (4h)**
- Embedded screenshots
- “How to interpret this” section

### Deliverables
- Dashboard (Power BI or Python)
- Screenshots committed
- Updated README

> **Pro tip:** Assume your viewer has 2 minutes and no patience.

---

## 🗓️ Week 6 — Publish & Optional AI

### Outcome
Interview-ready, public, complete.

### Tasks
**Documentation (8h)**
- Architecture diagram
- Data sources
- Tradeoffs
- “What I’d do next”

**Optional AI Insights (6h)**
- Simple LLM prompt:
  - “Explain why this ZIP is a childcare desert”
- Grounded strictly in mart data

**Final Cleanup (6h)**
- Sample data
- Run instructions
- 3-minute demo script

### Deliverables
- Final README
- Clean GitHub repo
- Demo walkthrough

> **Pro tip:** Stop when it’s clear and complete—not perfect.

---

## 🏁 Final Result

> “In six weeks, I built a cloud-native public-data lakehouse on AWS that identifies childcare deserts in Massachusetts at ZIP-code level, integrating Census demand data, state licensing supply data, geospatial boundaries, analytics engineering with dbt, and executive-ready visualizations.”

That sentence alone justifies the project.

---

