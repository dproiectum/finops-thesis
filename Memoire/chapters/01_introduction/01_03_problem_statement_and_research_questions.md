# 1.3 — Problem Statement and Research Questions

The project addresses the transformation of detailed FOCUS cost and usage records into reliable data products. Those products must support several consumers while preserving shared definitions, access control, traceability and confidentiality. The reported dashboard-change workflow makes the way those products are maintained and used part of the problem.

The research question is:

> How can a FinOps data platform transform FOCUS cost and usage data into reliable data products and provide governed self-service analytics to managers and application owners while supporting Inform, Optimize and Operate?

## 1.3.1 Three complementary subquestions

The central question is divided into three complementary subquestions rather than independent projects. They reflect the initial framing and organize the thesis argument.

1. Platform reliability: How can FOCUS cost and usage data become reliable, traceable and reusable data products while addressing security and scalability requirements?
2. Governed self-service: How can managers and application owners explore their authorized scope without manual FinOps extracts while preserving confidentiality and consistent indicators?
3. FinOps decision support: How can these products improve cost visibility, support analysis of optimization opportunities and enable recurring Inform, Optimize and Operate activities?

The first will be assessed through contract and quality controls, lineage, reconciliation and reproducibility, without conflating local execution with target-platform validation. The second requires user scenarios and access tests for every exposed channel; a usable interface alone does not establish secure self-service. The third requires correct and useful KPIs, separating cost differences, recommendations and measured savings.

## 1.3.2 Scope of self-service

The project aims for centralized FinOps data production and distributed consumption according to user permissions. Independent access does not require each domain to produce and maintain its own data. Section 4.2 develops this position and its relationship to Data Mesh; chapter 9 discusses its implications.

## 1.3.3 Additional design questions

Supporting questions address:

- the balance between Data Engineering depth, governance, cost and feasibility;
- the Data Contract and controls required to establish trust;
- the design of ownership, RLS and analyst access;
- the cost measures that support realized rate comparisons;
- the additional data required for potential-savings recommendations.
