# 3.2 — Experimental Dataset Preparation

## 3.2.1 Reference data and source preparation

Two Azure FOCUS cost-and-usage files, anonymized before use, provide reference rows and schema for fictional consumption data. Microsoft's FOCUS file-schema documentation defines the fields but does not establish the provenance of these particular files. The reference inputs remain local and are not published with the project.

*Source: Microsoft, [FOCUS cost and usage details file schema](https://learn.microsoft.com/en-us/azure/cost-management-billing/dataset-schema/cost-usage-details-focus).*

The independent generator retains rows with usable charge dates and billed cost, EUR currency and Microsoft provider. The `daily-template-v2` method samples these rows, replaces selected identifiers consistently, assigns dates and scales costs to configured targets. Daily output retains the source Arrow schema and is written to `datasets/focus/daily/YYYY/MM/YYYY-MM-DD.parquet`. The same published inputs can subsequently feed different analytical engines.

A date-specific seed makes sampling independent of batch boundaries. The configuration sets an annual `BilledCost` target of EUR 12 million for 2025, monthly weights and a 1.06 growth multiplier for 2026. Targets are distributed across days in cents. These are modeling assumptions, not estimates of observed seasonality or company spending.

A configuration-and-source fingerprint and daily ledger record paths, rows, amounts and SHA-256 hashes. Resumption checks existing entries and files rather than silently replacing them. Stable synthetic identifiers preserve selected links; their substitution alone does not prove that every potentially identifying attribute has been removed.

## 3.2.2 Monthly billing and controlled scenarios

A monthly close needs a billing reference distinct from provisional Daily usage. Without a real invoice feed, the simulator constructs this reference from a complete month of Daily files. It requires every calendar day, matching ledger entries and hashes, consistent schemas and periods, and agreement on rows, currency, provider and `BilledCost`.

The `no_change` scenario concatenates rows unchanged. Other scenarios inject known differences: `late_usage` adds a EUR 1,500 Usage line; `cost_correction` reduces an eligible line by EUR 200; `combined` applies both; and `unexplained_difference` changes a line by EUR 50 without an explanation. Deterministic selection makes these interventions repeatable.

The manifest records affected rows, before/after amounts and expected differences. It serves as an evaluation oracle for detected changes, missed changes and blocking decisions, but must not inform the pipeline's decision to close a month. Financial acceptance rules require FinOps review; a known injected amount is not automatically an acceptable difference.

Monthly output is published locally at `datasets/focus/monthly/billing-YYYY-MM.parquet`, with a separate manifest. Read-back checks precede publication; explicit replacement archives the previous version. Daily and Monthly represent the same month's activity, so adding their amounts would double-count it.

## 3.2.3 Coverage and limitations

Local validation on 27 September 2026 confirmed schema, temporal and monetary consistency for 608 Daily files, January 2025–August 2026, containing 3,664,261 rows and EUR 20,357,040. The 18 `no_change` Monthly files cover January 2025–June 2026, with 3,279,613 rows and EUR 18,220,080; each matched its Daily month and manifest hash. Revalidation after path harmonization on 28 September preserved these results and the Monthly hashes.

July–August therefore belong only to the validated Daily corpus. Corrected scenarios still require downstream tests against expected outcomes. The corpus supports engineering evaluation, not claims about real resource lifecycles, invoice correctness or organizational savings; forecasting would assess behavior under the generator's assumptions.
