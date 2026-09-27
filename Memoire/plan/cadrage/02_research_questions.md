# Research Questions

The school requires three proposed formulations of the same research topic. They emphasize the technical platform, the operating model, and the FinOps decision-support value. They are presented together below for comparison and do not represent three separate projects.

## Three Proposed Research Question Formulations

1. **Reliable FinOps Data Platform - technical platform angle**

   How can an Azure-first Data Engineering platform transform FOCUS-compliant cloud cost and usage data into reliable, secure, and scalable FinOps data products?

   This formulation emphasizes ingestion, Data Contracts, data quality, layered transformations, governance, dimensional modeling, and platform reliability.

2. **Governed Self-Service - operating model angle**

   How can a governed self-service Azure FinOps Data Platform reduce reliance on centralized reporting by providing managers and application owners with secure access to certified cost datamarts?

   This formulation addresses the observed company problem: email requests, manual Excel analysis, concentrated workload, response delays, and the need for Row-Level Security.

3. **FinOps Decision Support - analytical value angle**

   How can standardized and quality-controlled FinOps data products improve cloud cost visibility and decision support across Inform, Optimize, and Operate?

   This formulation emphasizes showback, allocation, realized savings analysis, optimization, forecasting, anomaly detection, and continuous governance.

## Recommended Main Research Question

How can an Azure-first FinOps Data Platform transform FOCUS cost and usage data into reliable data products and provide governed self-service analytics to managers and application owners while supporting Inform, Optimize, and Operate?

## Architectural Positioning

The selected direction is a governed self-service platform:

- Centralized production and governance.
- Distributed and role-based consumption.
- Certified FinOps datamarts and semantic models.
- Row-Level Security for domain managers.
- Data Mesh-inspired data-product principles without implementing a full Data Mesh.

## Cross-Cutting Elements

Data Contracts support Candidates 1 and 2 by defining schema, semantics, quality expectations, compatibility, and producer-consumer responsibilities.

Savings comparison supports Candidate 3 as an Optimize use case. The MVP distinguishes realized savings derived from cost measures from potential savings, which require additional utilization or recommendation sources.

Synthetic data supports the empirical methodology by enabling reproducible testing without disclosing confidential enterprise data. It is not retained as a standalone main research question.

## Supporting Questions

- Which architecture and technology stack best balance Data Engineering depth, Azure alignment, governance, cost, maintainability, and reproducibility?
- Which Data Contract and quality controls are required to certify FinOps data products?
- How should RLS, ownership, and access levels be designed for FinOps, managers, application owners, and domain analysts?
- Which cost measures can reliably calculate realized savings, and which additional sources are needed for potential savings?
- How can the platform be evaluated through data quality, freshness, security, self-service coverage, operational reliability, and analytical usefulness?
