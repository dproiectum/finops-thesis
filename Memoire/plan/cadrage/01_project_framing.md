# Project Framing

## Working Title

Design and Evaluation of a Governed Self-Service Azure FinOps Data Platform Supporting Inform, Optimize and Operate

## Professional Context

The organization currently follows a centralized data and business intelligence operating model. A central Data Platform team includes data engineers, data leadership, and a dedicated Power BI team responsible for building dashboards with the visual and technical standards of Technip Energies.

The FinOps team is a separate domain team. To create or modify a dashboard, FinOps communicates its requirements to a Power BI specialist, whose work is then charged back to the FinOps team. The current Cloud Showback dashboard was created for FinOps and gives the FinOps team a consolidated view of cloud consumption.

Correction du contexte par l'étudiant le 15 septembre 2026 : le dashboard est déjà utilisé par FinOps, sa hiérarchie et des managers de domaines/sous-domaines d'autres équipes. Il n'est donc pas établi que ces managers n'ont aucun accès direct. La couverture des besoins, les droits et les demandes complémentaires par email/Excel restent à préciser.

Le supérieur valide d'abord le dashboard et formule ses retours ; la manager transmet les demandes à un intervenant externe basé en Inde. L'étudiant rapporte un circuit comportant trop d'étapes et un temps de correction important, sans mesure chiffrée à ce stade. Voir la description actuelle en section 1.2 et la discussion du rôle d'un Data Engineer intégré à FinOps en section 9.2.

## Main Problem

The current process provides centralized control, but dashboard consultation must be distinguished from autonomy to extend analyses and implement changes. The project investigates both governed consumer access and the ability of FinOps to manipulate its data products more directly, without bypassing business validation or enterprise standards.

The project investigates how an Azure FinOps Data Platform can move from centralized reporting requests toward governed self-service analytics. Domain managers should be able to consult their own cost perimeter through a Row-Level Security-enabled dashboard. Authorized analysts may additionally consume certified FinOps datamarts or semantic models for more advanced analysis.

## Target Platform Type

The target is a governed self-service FinOps Data Platform based on certified data products:

- Production and governance remain centralized under the Data Platform, FinOps, and Power BI responsibilities.
- Consumption is distributed to managers, application owners, and authorized analysts.
- Row-Level Security protects domain, project, and application boundaries.
- Certified datamarts and semantic models provide consistent definitions and reusable measures.
- Data Contracts and automated quality controls protect downstream consumers.
- Data Mesh principles inform the design, but the project does not implement a full decentralized Data Mesh operating model.

This positioning can be described as a hub-and-spoke or data-product-oriented platform with centralized governance and distributed consumption.

## Research Contribution

The project combines three complementary contributions:

1. A reliable Azure-first Data Engineering platform for FOCUS cost and usage data.
2. A governed self-service consumption model based on certified FinOps data products, datamarts, semantic models, and Row-Level Security.
3. Measurable FinOps decision-support use cases across Inform, Optimize, and Operate.

Synthetic data generation is a methodological enabler for confidentiality and reproducibility. It is not the primary research subject. Data Mesh is used as a conceptual reference, not as the target operating model.

## Project Scope

Included in the MVP:

- Anonymized and synthetic Azure FOCUS cost and usage data.
- Data profiling and validation.
- Versioned Data Contracts and schema controls.
- Bronze, Silver, and Gold data layers.
- Canonical FinOps cost and usage model.
- Certified FinOps datamarts and semantic model.
- Showback dashboard with a conceptual and testable RLS design.
- Inform analytics for cost visibility and allocation.
- Optimize analysis including realized savings comparisons.
- Selected Operate capabilities such as forecasting, anomaly detection, or continuous monitoring.
- Evaluation of data quality, security, reproducibility, self-service coverage, and analytical usefulness.

Excluded from the MVP:

- A full enterprise Data Mesh implementation.
- Transfer of FinOps data-product ownership to every business domain.
- Direct use or disclosure of confidential enterprise billing data.
- Full multi-cloud implementation.
- Precise potential-savings recommendations without the additional utilization, pricing, or Azure Advisor data required to support them.

## Expected Value

The platform should reduce repetitive manual extraction and Excel manipulation, shorten access time for domain managers, preserve consistent FinOps definitions, and provide a reusable foundation for cost optimization and continuous governance.
