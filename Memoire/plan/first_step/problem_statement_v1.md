# Problem Statement v1

> Note d'évolution — 15 septembre 2026 : ce document conserve le cadrage historique. L'affirmation ci-dessous d'une absence d'accès des managers d'autres domaines est remplacée par le contexte actuel de `chapters/01_introduction/01_02_current_process_and_diagnosis.md`. Selon l'étudiant, ces managers utilisent déjà le dashboard ; le problème comprend notamment le circuit de validation et de modification via un intervenant externe. Ne pas reprendre l'ancienne affirmation dans le mémoire final.

## Working Title

Design and Evaluation of a Governed Self-Service Azure FinOps Data Platform Supporting Inform, Optimize and Operate

## 1. Context

Cloud computing enables organizations to provision technology quickly and consume infrastructure, platforms, and software according to demand. This flexibility also changes the financial management of technology. Cloud expenditure is variable, distributed across subscriptions, services, projects, applications, environments, teams, and pricing models. It evolves continuously according to usage, architecture decisions, regions, negotiated prices, commitment discounts, and operational behavior.

FinOps addresses this challenge by combining financial accountability, engineering practices, and operational governance. Its objective is not simply to reduce cost, but to help the organization maximize the business value of technology through collaboration between finance, engineering, business, procurement, and operations. FinOps activities require reliable and timely cost and usage data to inform stakeholders, identify optimization opportunities, and operate continuous governance.

For Data Engineering, this creates a concrete platform problem. Cloud billing exports are detailed and high-volume. They contain multiple cost measures, usage quantities, dates, services, resources, accounts, tags, locations, pricing categories, and commitment-discount information. The raw data is technically rich but cannot directly provide a stable and trusted decision-support service. It must be ingested, validated, standardized, contextualized, modeled, secured, and published for different consumer profiles.

## 2. Professional Situation

The professional context of this project follows a centralized data and business intelligence operating model. A central Data Platform organization includes data engineers, data leadership, and a dedicated Power BI team. The Power BI team works with business and technical teams to build dashboards while ensuring compliance with Technip Energies standards, including design, colors, development practices, and publication rules.

FinOps is a separate domain team. When FinOps needs a dashboard or a change to an existing report, it communicates the business requirements to a Power BI specialist. The Power BI specialist implements the requested content, and the corresponding work hours are charged back to the FinOps team.

The existing Cloud Showback dashboard gives the FinOps team broad visibility into cloud consumption across projects, applications, teams, and owners. However, managers from other domains do not currently have direct visibility into the consumption associated with their own perimeter. When they need cost information, they send an email to FinOps and request total costs and detailed information for the applications and projects under their responsibility.

FinOps then extracts the relevant data, exports it to Excel, creates pivot-based analyses, and returns the requested information. These requests can be urgent and often arrive at the beginning of the month. This creates a workload peak for the FinOps team and delays the response to managers. It also makes the delivery of recurring information dependent on manual operations, even though the underlying cost data already exists.

The current model provides centralized control, but it does not provide sufficient autonomy to data consumers. The organizational problem is therefore connected to a Data Engineering problem: how to produce one trusted FinOps data foundation and distribute it securely to different consumers without losing governance, consistency, or confidentiality.

## 3. Target Direction

The target direction is a governed self-service Azure FinOps Data Platform based on certified FinOps data products.

Production and governance remain centralized. The Data Platform team continues to provide platform capabilities, engineering standards, orchestration, security, and operational support. FinOps remains responsible for cost semantics, allocation rules, FinOps indicators, savings logic, and business validation. The Power BI team remains responsible for semantic-model and dashboard standards.

Consumption becomes distributed according to user roles. Domain managers should be able to access the Cloud Showback dashboard and view only the applications, projects, teams, or cost centers within their authorized perimeter. Row-Level Security should prevent access to other domains. Authorized analysts may receive additional access to certified datamarts or semantic models when their needs go beyond standard dashboard interactions.

This approach uses selected principles associated with Data Mesh, particularly data as a product, explicit ownership, discoverability, quality expectations, and self-service consumption. However, the project does not propose a full Data Mesh. Business domains are not expected to become producers and owners of separate FinOps datasets. FinOps remains the natural owner of the certified cloud cost data product. The target is therefore better described as a hub-and-spoke or data-product-oriented platform with centralized governance and distributed consumption.

## 4. Research Problem

The school requires three proposed formulations of the same research topic. They are grouped here to make their relationship and respective emphasis explicit. They represent three complementary perspectives on one PFE rather than three separate projects.

### 4.1 Three Proposed Research Question Formulations

1. **Reliable FinOps Data Platform - technical platform angle**

   > How can an Azure-first Data Engineering platform transform FOCUS-compliant cloud cost and usage data into reliable, secure, and scalable FinOps data products?

2. **Governed Self-Service - operating model angle**

   > How can a governed self-service Azure FinOps Data Platform reduce reliance on centralized reporting by providing managers and application owners with secure access to certified cost datamarts?

3. **FinOps Decision Support - analytical value angle**

   > How can standardized and quality-controlled FinOps data products improve cloud cost visibility and decision support across Inform, Optimize, and Operate?

### 4.2 Integrated Main Research Question

The three formulations are consolidated into the following main research question:

> How can an Azure-first FinOps Data Platform transform FOCUS cost and usage data into reliable data products and provide governed self-service analytics to managers and application owners while supporting Inform, Optimize, and Operate?

Three complementary dimensions structure this integrated question.

The first dimension concerns platform reliability. The solution must ingest recurring cost and usage files, preserve source traceability, enforce a versioned Data Contract, detect schema drift and quality problems, build canonical and analytical models, and publish reproducible data products.

The second dimension concerns governed self-service. The platform must provide managers with timely access while preserving confidentiality and consistent definitions. It must distinguish dashboard consumers, advanced analysts, FinOps specialists, Power BI developers, and Data Platform operators. Certified datamarts, semantic models, and Row-Level Security are central mechanisms in this dimension.

The third dimension concerns FinOps decision support. The platform must deliver useful capabilities rather than only move data between storage layers. Inform includes cost visibility, showback, allocation, trends, and accountability. Optimize includes comparison of list, contracted, effective, and billed cost, realized-savings analysis, commitment-discount analysis, and selected recommendations. Operate includes recurring ingestion, monitoring, forecasting, anomaly detection, and continuous governance.

## 5. Data and Confidentiality Constraint

Real enterprise billing data is confidential and cannot be disclosed in an academic thesis or public technical artifact. The empirical work therefore uses anonymized Azure FOCUS Parquet samples and a synthetic data generator. The generator produces fictitious but structurally compatible data over a longer historical period.

Synthetic generation is not the main research subject. It is a methodological mechanism that makes the platform reproducible and allows ingestion, Data Contracts, transformations, dimensional models, security scenarios, dashboards, savings comparisons, forecasts, and anomaly detection to be tested without exposing company information.

The limited source history must be acknowledged. Two source months cannot provide enough evidence to learn reliable annual seasonality through machine learning. The generator therefore uses controlled statistical and business rules. Its credibility must be evaluated through schema compatibility, distributions, cost totals, consistency checks, deterministic configuration, and clearly documented limitations.

## 6. Data Contracts and Certified Products

A certified FinOps datamart requires more than a Gold table or dashboard label. Consumers need a clear agreement about schema, semantics, quality, timeliness, compatibility, ownership, and permitted use. The project therefore includes a versioned FOCUS Data Contract.

The contract identifies required fields, expected data types, business rules, quality constraints, and schema-evolution policies. Automated validation should prevent malformed or incompatible data from silently reaching the canonical model, certified datamarts, dashboards, or optimization logic. Data Contract results also provide measurable evidence for the reliability of the platform.

The certification concept continues through the serving layer. Measures such as billed cost, effective cost, realized savings, and allocation coverage must have documented definitions. Certified semantic models and datamarts should provide reusable and consistent calculations for managers and analysts.

## 7. Savings Analysis

Savings comparison is retained as a principal Optimize use case. FOCUS provides several cost perspectives, including list, contracted, effective, and billed cost. These measures can support analysis of negotiated discounts, commitment-discount effects, and realized savings.

The project must distinguish realized savings from potential savings. Realized savings can be calculated from historical cost measures when the required fields are populated and semantically comparable. Potential savings generally require additional information such as utilization metrics, Azure Advisor recommendations, resource inventory, commitment coverage, or pricing references. The prototype must avoid presenting unsupported estimates as verified opportunities.

This distinction is academically useful because it demonstrates critical interpretation of financial data rather than the mechanical production of attractive indicators.

## 8. Objectives

The project objectives are:

1. Document the As-Is reporting and data-access process and define a measurable baseline.
2. Compare candidate Azure technology stacks and justify the selected architecture.
3. Define functional, security, governance, quality, and operational requirements.
4. Build a reproducible FOCUS-compatible empirical dataset without exposing confidential data.
5. Implement Data Contract validation and Bronze, Silver, and Gold processing.
6. Publish certified FinOps data products, datamarts, and semantic measures.
7. Design and test RLS-based access for domain managers.
8. Implement representative Inform, Optimize, and Operate use cases.
9. Evaluate the platform through data quality, freshness, reconciliation, security, self-service coverage, reliability, and analytical usefulness.
10. Analyze limitations and formulate prioritized recommendations for enterprise adoption.

## 9. Expected Contribution

The expected contribution is both technical and organizational. Technically, the PFE should demonstrate the design and implementation of a modern Azure Data Engineering platform using contracts, layered data processing, dimensional modeling, governance, security, and analytical serving. Organizationally, it should evaluate how governed self-service can reduce repetitive manual delivery while preserving centralized standards and FinOps ownership.

The project does not assume that more decentralization is always better. It seeks to identify the appropriate level of autonomy for each consumer profile. Managers may be satisfied by an RLS-protected dashboard, while domain analysts may require a certified datamart. FinOps and Data Platform teams retain broader access and governance responsibilities.

The final result should demonstrate that trusted FinOps data products can connect complex cloud billing data with timely, secure, and actionable decision support, while remaining realistic about confidentiality, organizational maturity, data availability, and implementation cost.
