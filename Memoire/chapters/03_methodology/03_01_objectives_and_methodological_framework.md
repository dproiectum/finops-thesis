# 3.1 — Objectives and Methodological Framework

The method works backward from the intended outcome: stakeholders should be able to examine attributed cloud costs through understandable indicators. The research questions in section 1.3 are translated into capabilities, artifacts and acceptance criteria. The table follows this deduction down to its prerequisite, a suitable dataset; it does not describe the execution schedule or claim that every criterion has been met.

Each identified need is translated into an objective, a proposed artifact and a criterion for validation:

**Need → objective → proposed response/solution: an artifact → validation criterion**

| Intended outcome | Required capability | Project artifact | Acceptance criteria |
|---|---|---|---|
| Support FinOps decisions | Integrate analysis and operational monitoring | FinOps data platform | Indicator meanings and data provenance are identifiable |
| Provide stakeholder showback | Publish understandable, authorized cost views | Dashboard and documented KPIs | Business questions can be answered; totals and access boundaries are checked |
| Ensure consistent calculations | Define grain, measures and aggregation rules | Analytical model, dictionary and datamarts | Questions map to data; calculations preserve grain and reference totals |
| Maintain trust as sources evolve | Control quality, responsibilities and changes | Versioned Data Contract and quality reports | Incompatible inputs are detected; invalid publication is blocked and explained |
| Keep products updated | Automate processing and recovery | Daily/Monthly jobs and audit records | Expected periods are processed; replay avoids duplicates; failures are diagnosable |
| Establish feasibility | Test the complete chain locally | End-to-end POC | Source, transformed and displayed values agree |
| Supply experimental inputs | Generate reproducible normal and correction cases | Synthetic FOCUS corpus, generator and manifests | Schema, coverage, totals and scenario expectations are verified |

Implementation proceeds from the corpus and local POC to automated cloud processing and online consumption, with quality, governance and security accompanying each stage. Repeated build-and-test cycles are consistent with the FinOps Foundation's FOCUS adoption guidance. The sections below explain this method; architecture, implementation and evaluation are developed in chapters 4, 5, 7 and 8.

*Source: FinOps Foundation, [Adopting FOCUS, the FinOps Open Cost and Usage Specification](https://www.finops.org/wg/adopting-focus-the-finops-open-cost-and-usage-specification/) (last updated 10 December 2025).*
