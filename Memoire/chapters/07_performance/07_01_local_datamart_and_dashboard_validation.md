# 7.1 — Local Datamart and Dashboard Validation

This section summarizes local validation of the January 2025 synthetic dataset and the DuckDB and Streamlit prototype. The results apply only to this setting.

## Test environment

- dataset: January 2025 monthly billing;
- charge lines: 164,145;
- local analytical engine: DuckDB 1.5.5;
- dashboard framework: Streamlit 1.63.0;
- serving objects: 14 materialized SQL datamarts, including 11 queried by the dashboard.

## Reconciliation results

The executive datamart and the existing monthly-billing datamart both report a billed cost of EUR 912,000.00. The executive charge-line count and the monthly quality row count both equal 164,145. The quality table reports zero null values for BilledCost, BillingCurrency and ServiceName, and one ingestion batch for the selected month.

## Application validation

Streamlit AppTest executed the initial FinOps page, four Cost Analysis views and four Data & Architecture views. All eight navigable subviews completed with zero application exceptions and zero Streamlit warning elements. Python compilation completed successfully. The existing automated suites also completed successfully: one synthetic-generator test and nine billing-notebook regression tests.

## Cost-comparison observations

| Indicator | January 2025 result |
|---|---:|
| List cost | EUR 1,290,989.95 |
| Contracted cost | EUR 1,044,652.85 |
| Effective cost | EUR 1,101,755.75 |
| List minus contracted | EUR 246,337.10 |
| Contracted minus effective | EUR -57,102.90 |
| List minus effective | EUR 189,234.20 |
| List-to-effective difference rate | 14.66% |

The negative contracted-to-effective difference prevents this component from being accepted as demonstrated commitment savings. The result is retained as an analytical observation requiring semantic validation, not corrected or hidden to produce a favorable KPI.

## Validity boundary

These results demonstrate local technical execution and reconciliation for one synthetic month. They do not demonstrate Databricks SQL compatibility, production performance, enterprise certification, Row-Level Security, actual organizational savings or forecasting capability.
