# Methodology and Empirical Study

## Methodological Positioning

The project follows a design-and-evaluation methodology. The objective is to investigate a real FinOps information-delivery problem, design an appropriate Azure Data Platform, implement a prototype, and evaluate it against explicit technical and organizational criteria.

The empirical work is based on anonymized Azure FOCUS cost and usage samples, enriched through a synthetic data generation process. This allows the platform to be tested over a longer historical period without exposing confidential company data.

The study also uses an enterprise case context. The As-Is process relies on email requests, FinOps-operated Excel exports, and centrally developed Power BI reporting. The To-Be design introduces governed self-service access through RLS dashboards and certified datamarts.

## Research Design

The project follows a design science-oriented sequence:

1. Describe the current organizational and data-access problem.
2. Define functional, security, governance, and quality requirements.
3. Compare candidate platform architectures and technology stacks.
4. Design the target FinOps data product and access model.
5. Implement and validate the selected architecture.
6. Evaluate technical performance and organizational usefulness against the baseline.

## Data Sources

Primary source:

- Anonymized Azure FOCUS 1.0 Parquet datasets.

Generated source:

- Synthetic FOCUS-compatible cost and usage datasets covering 2025-01-01 to 2026-06-30.
- Incremental future batches from 2026-07-01 onward.

Future optional sources:

- Azure Price Sheet.
- Azure Advisor recommendations.
- Resource inventory.
- Resource utilization metrics.
- Organizational ownership and access-control mappings.

## Data Engineering Methods

- Dataset profiling.
- Template-based synthetic data generation.
- Controlled monthly cost scaling.
- Stable synthetic identifier generation.
- Schema preservation in Parquet format.
- Data Contract definition and validation.
- Data quality and reconciliation controls.
- Bronze, Silver, and Gold layering.
- Canonical FinOps model design.
- Dimensional modeling for analytics.
- Certified datamart and semantic-model publication.
- Role-based access and RLS testing.

## Analytical Methods

Inform:

- Cost trends.
- Cost allocation by domain, application, project, service, account, region, resource, and tags.
- Budget versus actual analysis when budget data is available.
- Showback and FinOps KPIs.

Optimize:

- Comparison of list, contracted, effective, and billed costs.
- Realized-savings analysis.
- Commitment discount analysis for Reservations and Savings Plans.
- Waste-detection or potential-savings rules only when supporting utilization or recommendation data is available.

Operate:

- Data freshness and pipeline monitoring.
- Forecasting baseline.
- Anomaly detection prototype, if feasible.
- Incremental data generation to simulate continuous operation.

## Evaluation Criteria

- Schema compatibility between source and synthetic datasets.
- Statistical credibility of synthetic data compared with anonymized samples.
- Reproducibility of generation through configuration and seed.
- Data Contract validation and controlled schema evolution.
- Data quality validation pass/fail results.
- Cost reconciliation and data freshness.
- Pipeline reliability and idempotency.
- RLS isolation between manager and domain perimeters.
- Coverage of recurring manager questions without manual extraction.
- Number of manual steps and estimated response time before and after the prototype.
- Usefulness of Inform outputs.
- Reliability of realized-savings comparisons.
- Explicit limitations for potential-savings estimates.
- Forecasting or anomaly-detection performance, if implemented.

## Limitations

- Only two source months are available, so annual seasonality cannot be learned directly from data.
- The synthetic generator uses statistical and business rules rather than a learned annual model.
- Azure is the only implemented cloud provider in the MVP.
- Some optimization use cases require additional datasets such as resource metrics, recommendations, or pricing references.
- Organizational impact cannot be claimed without an adequate user evaluation or a clearly defined scenario-based evaluation.

## Use of Generative AI

Generative AI is used as an assistive tool for brainstorming, structuring, drafting, and coding support. The final thesis must transparently document this use and preserve the student's own reasoning, decisions, implementation work, validation, and critical analysis.

Raw layout: `FinOps Data Platform/data/raw/YYYY/MM/YYYY-MM-DD.parquet`. Initial history contains 546 daily files over 18 months. Future daily generation starts on July 1, 2026; the old monthly fixtures have been deleted. Anonymized reference files are excluded from pipeline discovery.
