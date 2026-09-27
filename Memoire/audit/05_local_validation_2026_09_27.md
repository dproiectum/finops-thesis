# Local evidence collected on 27 September 2026

This is an internal evidence note, not a thesis chapter. It records reproducible local observations made while drafting sections 3.1, 3.2 and 6.2–6.3. It does not establish Databricks execution or real company spending.

## EVD-011 — Current Daily history

Environment: Python 3.14, pandas 3.0.5, PyArrow 24.0.0. Command from `FinOps Data Generator`: `PYTHONPATH=src python3 -m finops_generator.validate_daily_history`. The validator completed successfully and wrote `metadata/daily/daily_monthly_validation.csv`.

| Measure | Result |
|---|---:|
| Daily files | 608 |
| Period | 2025-01-01 to 2026-08-31 |
| Charge lines | 3,664,261 |
| Synthetic BilledCost | EUR 20,357,040.00 |

Monthly validation command: `PYTHONPATH=src python3 -m finops_generator.validate_monthly_history`. It completed successfully and wrote `metadata/monthly/monthly_validation.csv`.

| Measure | Result |
|---|---:|
| Detailed monthly bills | 18 |
| Period | 2025-01 to 2026-06 |
| Charge lines | 3,279,613 |
| Synthetic BilledCost | EUR 18,220,080.00 |

The 2026-07 and 2026-08 Daily files are outside the validated monthly-billing set.

## EVD-012 — January 2025 local POC analysis

Environment: DuckDB v1.5.5, read-only connection to `FinOps Data Platform - POC/duckdb_local_bi/database/finops_warehouse.duckdb`. All queries below select the only billing month available in the local POC, 2025-01. The database and source dataset are synthetic.

```sql
SELECT billing_month, charge_lines, active_resources, consumed_services,
       ROUND(billed_cost, 2), ROUND(effective_cost, 2), ROUND(list_cost, 2)
FROM datamart.dm_executive_summary_monthly;

SELECT ROUND(SUM(total_billed_cost), 2) AS unknown_center_cost,
       ROUND(100 * SUM(total_billed_cost) / 912000, 2) AS percent
FROM datamart.dm_cost_by_scope_service_month
WHERE cost_center IS NULL OR TRIM(cost_center) = ''
   OR LOWER(cost_center) IN ('unknown', 'unassigned', 'n/a');

SELECT ROUND(SUM(total_billed_cost), 2) AS missing_owner_cost,
       ROUND(100 * SUM(total_billed_cost) / 912000, 2) AS percent
FROM datamart.dm_cost_by_application_owner_month
WHERE application_owner_id IS NULL OR TRIM(application_owner_id) = ''
   OR LOWER(application_owner_id) IN ('unknown', 'unassigned', 'n/a');

SELECT service_name, ROUND(SUM(total_billed_cost), 2) AS billed_cost
FROM datamart.dm_cost_by_scope_service_month
GROUP BY service_name ORDER BY SUM(total_billed_cost) DESC LIMIT 2;
```

| Observation | Result |
|---|---:|
| BilledCost | EUR 912,000.00 |
| EffectiveCost | EUR 1,101,755.75 |
| ContractedCost | EUR 1,044,652.85 |
| ListCost | EUR 1,290,989.95 |
| Charge lines | 164,145 |
| Active resources | 22,453 |
| Consumed services | 59 |
| Unknown cost center | EUR 875,320.02 (95.98%) |
| Missing/placeholder application owner ID | EUR 146,649.15 (16.08%) |
| Virtual Machines | EUR 195,399.16 |
| Storage Accounts | EUR 176,985.27 |
| Top-two services, calculated before rounding individual values | EUR 372,384.42 (40.83%) |

The center and owner measures use different dimensions and must not be added. These results show allocation coverage and cost concentration in synthetic data, not actual company expenditure or realized savings.

`ContractedCost` was checked separately in read-only mode from `datamart.dm_savings_monthly` for `billing_month = '2025-01'`. The underlying decimal value was 1,044,652.848686590563 EUR, rounded to cents above. This verifies the value used in chapter 6; it does not validate the business interpretation of any cost-column difference.
