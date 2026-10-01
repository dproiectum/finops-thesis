# Thesis assembly plan — 29 September 2026

Illustration planning for the 42 current sections is in [the illustration plan](../plan/illustrations_plan_2026_09_27.md). Chapter 3 uses its explanatory table without additional figures. Remaining editorial comments elsewhere identify only selected figure or appendix-evidence locations and must be excluded from the final PDF.

> Status: `WORKING`. The school recommends approximately 50 pages for the main text. Draft each argument for clarity and concision before adjusting the final layout; detailed procedures, screenshots and lengthy outputs belong in appendices.

The student sets a working limit of 60 pages. The school guide recommends approximately 50 pages for the main body, excluding supplementary matter. The final page count must be checked after assembly; no page total is inferred from Markdown length alone.

## Argument

**Working question:** How can a governed FinOps data platform transform FOCUS cost-and-usage data into reliable analytical products for cloud showback, and what operational added value does the resulting system demonstrate? The final wording requires supervisor approval (Q-002).

The thesis distinguishes design and code, local POC validation, cloud execution supported by retained evidence, and capabilities still to be tested. Synthetic data alone cannot establish realized savings, production-grade security or superior performance.

## Chapter and section outline

### 1. General introduction and professional context

- **1.1 Professional Context and the FinOps Team:** host organization, team roles, author's position and Cloud Showback.
- **1.2 Current Reporting Process and Observed Difficulties:** change dependencies, dashboard latency, data quality and scoped distribution.
- **1.3 Problem Statement and Research Question:** one question and the operational meaning of added value.
- **1.4 Objectives, Implemented Artifacts and Scope:** implemented artifacts and limits of the synthetic study.
- **1.5 Assessment Criteria and Evidence Boundaries:** what the project can substantiate and what still needs measurement.
- **1.6 Thesis Structure:** the role of each subsequent chapter.

### 2. FinOps and cloud economics

- **2.1 FinOps as a Business and Operational Framework:** stakeholders, goals and terms.
- **2.2 Inform, Optimize and Operate in the Project:** intended use cases and demonstrated contribution.
- **2.3 Cost Semantics and FOCUS:** specification, governance, provider adoption, versioning and the project's experimental scope.
- **2.4 From Cloud Charges to Showback:** List, Contracted, Effective and Billed Cost; interpretation limits, allocation, and the boundary between showback and chargeback.
- **2.5 FinOps Team Activities and Outputs:** measurement, planning, optimization and governance tasks described in an internal presentation, followed by the PFE boundary.

### 3. Methodology and evaluation framework

- **3.1 Objectives and Methodological Framework:** backward reasoning from desired FinOps outcomes to required capabilities, artifacts and acceptance criteria, ending with the experimental dataset.
- **3.2 Experimental Dataset Preparation:** reference data, reproducible Daily generation, local Monthly simulation, controlled scenarios, publication, validated coverage and representativeness limits.
- **3.3 Data Quality, Governance and Change Control:** quality criteria, the versioned Data Contract, responsibilities, compatible additions, incompatible drift and reviewed evolution.
- **3.4 Progressive Implementation and Automation:** local POC, cloud extension, historical and incremental workflows, recovery, evaluation and levels of evidence.
- **3.5 Analytical Preparation:** business questions, measures and grain, analytical model, datamarts and publication checks; the concrete model remains in section 4.5.
- **3.6 FinOps Data Product Delivery and Operation:** dashboard and datamarts as analytical products, platform support, delivery, access, operational visibility and acceptance.

### 4. General design and architecture choices

- **4.1 Design Requirements and Principles:** quality, traceability, security, cost and scope.
- **4.2 General Platform Design (Logical HLD):** source, contract, data layers, analytical products and responsibilities.
- **4.3 Technology Options and Implemented Choices:** alternatives considered without a numerical ranking; Databricks/GCP, RAW Parquet, Delta, SQL, local DuckDB and Streamlit used in the project.
- **4.4 Selected Physical Architecture:** independent generator, frozen POC, RAW/DEV/PROD/OPS catalogs, compute configuration boundary, Cloud Run consumption and the proposed dashboard identity/authorization boundary; regional choices and costs are deferred to chapters 7–8.
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
  - **5.3.5 Cloud Run Streamlit Application and Read-Only Data Access**
  - **5.3.6 Proposed Role- and Scope-Based Dashboard Authorization**

### 6. FinOps analysis of results

- **6.1 Scope and Method for FinOps KPI Analysis:** formulas, scopes, sources, exclusions and level of evidence.
- **6.2 Analysis of Costs and Pricing Mechanisms:** List/Contracted/Effective/Billed observations; semantic validation before any savings claim.
- **6.3 Allocation and Resource Analysis:** distribution, concentration, ownership coverage and possible actions.

### 7. Technical validation and performance

- **7.1 Local Datamart and Dashboard Validation:** quality, reconciliation and dashboard results for January 2025.
- **7.2 Existing Power BI Diagnosis and Measurement Protocol:** permitted measurements and comparability limits.
- **7.3 Architecture Comparison and Performance Levers:** equivalent data and results; direct query versus datamart; Serverless versus Classic where comparable.
- **7.4 Databricks/GCP Validation:** historical DEV/PROD load, Daily cycle, close, idempotence and backend permissions; results supported by Run IDs and artifacts.
- **7.5 Dashboard Access-Control Validation:** controlled synthetic personas, denial by default, role/scope isolation and the separate evidence required for IAP authentication.

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

The earlier 40-section draft received an academic-language and evidence review, recorded in `audit/06_academic_writing_review_2026_09_27.md`. Consolidating chapter 5 and adding section 4.5 then left 37 sections. On 29 September, chapter 3 was reorganized into six sections following the approved objective-led method, bringing the total to 40. Two additions to chapter 2 on 30 September, one on FOCUS and one on the FinOps team's work, brought the total to 42; merging cloud-cost interpretation and allocation into section 2.4 brought it back to 41. The dashboard access-control validation added on 1 October brings the current total to 42. The revisions still require the final supervisor review. Local validation covers 608 Daily files through August 2026 and 18 unchanged monthly bills through June 2026; January 2025 POC cost and allocation results are documented separately. The Belgium completion plan reports a successful DEV/PROD backfill from January 2025 through June 2026. Its Run IDs, control outputs, screenshots and executed commit must be indexed before that run is presented as an independently validated thesis result. The complete Daily DEV-to-PROD cycle, Classic monthly close, Cloud Run dashboard permissions, persona authorization tests and economic benchmark still require verification.

Chapter 6 concerns the cloud costs being analyzed; chapter 8 concerns the cost of the platform itself. Chapter 5 explains implementation; chapter 7 evaluates it. If the main text substantially exceeds 50 pages, chapters 6–8 may be condensed during assembly without dropping their research questions.

## Final assembly

Files named `CC_SS_topic.md` are assembled in numeric order. Appendices are added only when they contain substantive material that complements a specific chapter and is included in the same PDF; the project timeline is a candidate, pending figure export and review. Audit registers and source-code inventories remain working sources and are not assembled as chapters. The chapter text must not depend on local `.md` or `.sql` hyperlinks. Only reviewed text marked `FINAL-CANDIDATE` enters the final PDF. Each result must identify its environment, period, volume, evidence and validity limit.
