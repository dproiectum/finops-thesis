# Thesis assembly plan — 27 September 2026

Illustration planning for all 37 sections is in [the illustration plan](../plan/illustrations_plan_2026_09_27.md). Proposed figures remain outside the chapter files until their sources and captions are verified.

> Status: `WORKING`. The main text should be approximately 50 pages. Detailed procedures, screenshots and lengthy outputs belong in appendices.

## Argument

**Working question:** How can a reliable and governed FinOps data platform be built and evaluated for cloud-cost analysis and user autonomy? The final wording requires supervisor approval (Q-002).

The thesis distinguishes design and code, local POC validation, cloud execution supported by retained evidence, and capabilities still to be tested. Synthetic data alone cannot establish realized savings, production-grade security or superior performance.

## Chapter and section outline

### 1. General introduction and professional context

- **1.1 Professional Context and Stakeholder Roles:** organization, FinOps team, mission and confidentiality.
- **1.2 Current Process and Diagnosis:** existing users, change-request workflow, observed limitations and unmet needs.
- **1.3 Problem Statement and Research Questions:** data reliability, governed self-service and decision support.
- **1.4 Objectives, Scope and Constraints:** measurable objectives, available data and PFE boundaries.
- **1.5 Summary of Requirements:** needs and acceptance criteria; M01–M10 remain detailed in the framing documents.
- **1.6 Thesis Structure:** approach and the role of each chapter.

### 2. FinOps and cloud economics

- **2.1 FinOps as a Business and Operational Framework:** stakeholders, goals and terms.
- **2.2 Inform, Optimize and Operate in the Project:** intended use cases and demonstrated contribution.
- **2.3 Cloud Pricing and Cost Mechanisms:** List, Contracted, Effective and Billed Cost; grain and exclusions.
- **2.4 Allocation, Showback and Governed Self-Service:** allocation rules, accountability and decision quality.

### 3. Methodology, data and experimental protocol

- **3.1 Dataset Generation and Validation:** anonymized sources, synthetic assumptions, reproducibility, coverage and representativeness.
- **3.2 Monthly Billing Simulation and Reconciliation Evaluation:** scenarios, monthly authority, experimental oracle and financial limitations.
- **3.3 Experimental Protocol and Levels of Evidence:** requirements, environments, datasets, success criteria, measures and evidence retention.

### 4. General design and architecture choices

- **4.1 Design Requirements and Principles:** quality, traceability, security, cost and scope.
- **4.2 General Platform Design (Logical HLD):** source, contract, data layers, analytical products and responsibilities.
- **4.3 Technology Evaluation and Selection:** alternatives, Databricks/GCP, Raw Parquet, Delta, SQL, local DuckDB and Streamlit.
- **4.4 Selected Physical Architecture:** independent generator, frozen POC, RAW/DEV/PROD/OPS catalogs, compute configuration boundary, flow and permissions; regional choices and costs are deferred to chapters 7–8.
- **4.5 Data Architecture and Dimensional Modeling:** canonical charge-line grain, Gold table inventory, relationships and datamarts mapped to intended business questions.

### 5. Detailed design and implementation

- **5.1 Independent FOCUS Data Generator:** Daily generation, monthly billing scenarios, local validation and source publication.
  - **5.1.1 Daily Data Generation**
  - **5.1.2 Monthly Billing Simulation**
  - **5.1.3 Validation and Publication of Source Files**
- **5.2 Local End-to-End Proof of Concept:** the frozen DuckDB/Streamlit chain and its separately validated January 2025 results.
  - **5.2.1 DuckDB Processing Chain and Data Contract**
  - **5.2.2 Gold Model and Subject-Oriented Datamarts**
  - **5.2.3 Local Streamlit Dashboard**
- **5.3 Databricks Cloud Data Platform:** independent cloud implementation and its pending run-level evidence.
  - **5.3.1 RAW, DEV, PROD and OPS Organization**
  - **5.3.2 Daily Ingestion, Backfill and Monthly Close**
  - **5.3.3 Data Contract, Gold Model and Datamarts**
  - **5.3.4 Jobs, Audit, Validation and Recovery**
  - **5.3.5 Streamlit Application and Read-Only Access**

### 6. FinOps analysis of results

- **6.1 Scope and Method for FinOps KPI Analysis:** formulas, scopes, sources, exclusions and level of evidence.
- **6.2 Analysis of Costs and Pricing Mechanisms:** List/Contracted/Effective/Billed observations; semantic validation before any savings claim.
- **6.3 Allocation and Resource Analysis:** distribution, concentration, ownership coverage and possible actions.

### 7. Technical validation and performance

- **7.1 Local Datamart and Dashboard Validation:** quality, reconciliation and dashboard results for January 2025.
- **7.2 Existing Power BI Diagnosis and Measurement Protocol:** permitted measurements and comparability limits.
- **7.3 Architecture Comparison and Performance Levers:** equivalent data and results; direct query versus datamart; Serverless versus Classic where comparable.
- **7.4 Databricks/GCP Validation:** historical DEV/PROD load, Daily cycle, close, idempotence, permissions and App; results supported by Run IDs and artifacts.

### 8. Economic analysis of the solution

- **8.1 Costing Scope and Method:** cost boundaries, horizon, assumptions and dated price sources.
- **8.2 Build-Cost Scenarios:** human effort and build resources.
- **8.3 Operating-Cost Scenarios:** DBUs, GCP infrastructure, storage, SQL Warehouse, App, maintenance and scenarios.
- **8.4 Applying FinOps to the FinOps Platform:** workload-level attribution, compute and scheduling levers, controlled comparisons and decision criteria.

### 9. Discussion, limitations and recommendations

- **9.1 Discussion, Limitations and Recommendations:** research-question answers, internal/external validity, security and prioritized recommendations.
- **9.2 Potential Contribution of a Data Engineer Embedded in FinOps:** autonomy, delays and organizational cost to assess without presumed gains.

### 10. General conclusion and outlook

- **10.1 General Conclusion:** objective, implementation, evidence and limit for each axis.
- **10.2 Learning Outcomes and Application of Master's Coursework:** personal contribution, applied skills and critical reflection.
- **10.3 Future Work:** security/RLS, operations, optimization, possible forecasting and broader deployment.

## Draft status and missing evidence

The previous 40-section draft received an academic-language and evidence review, recorded in `audit/06_academic_writing_review_2026_09_27.md`. Chapter 5 was then consolidated into three sections and section 4.5 was added, leaving 37 current sections; the revisions still require the final supervisor review. Local validation covers 608 Daily files through August 2026 and 18 unchanged monthly bills through June 2026; January 2025 POC cost and allocation results are documented separately. The Belgium completion plan reports a successful DEV/PROD backfill from January 2025 through June 2026. Its Run IDs, control outputs, screenshots and executed commit must be indexed before that run is presented as an independently validated thesis result. The complete Daily DEV-to-PROD cycle, Classic monthly close, Databricks App and economic benchmark still require verification.

Chapter 6 concerns the cloud costs being analyzed; chapter 8 concerns the cost of the platform itself. Chapter 5 explains implementation; chapter 7 evaluates it. If the main text substantially exceeds 50 pages, chapters 6–8 may be condensed during assembly without dropping their research questions.

## Final assembly

Files named `CC_SS_topic.md` are assembled in numeric order. Appendices are added only when they contain substantive material that complements a specific chapter and is included in the same PDF; the project timeline is a candidate, pending figure export and review. Audit registers and source-code inventories remain working sources and are not assembled as chapters. The chapter text must not depend on local `.md` or `.sql` hyperlinks. Only reviewed text marked `FINAL-CANDIDATE` enters the final PDF. Each result must identify its environment, period, volume, evidence and validity limit.
