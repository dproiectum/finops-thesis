# 5.3 — Databricks Cloud Data Platform

The cloud implementation consumes the shared Parquet history but has its own processing code, SQL products and operational controls. It is a PFE platform prototype, not a deployment into Technip Energies' production systems. The technical design below identifies implemented behavior and separates it from cloud outcomes that still need run-level evidence.

## 5.3.1 RAW, DEV, PROD and OPS organization

The external `finops_raw.landing` volume exposes the same GCS source objects to DEV and PROD. Each business catalog, `finops_dev` and `finops_prod`, has separate Bronze, Silver, Gold and datamart schemas. `finops_ops.audit` keeps operational runs, month status, snapshots, reconciliations and archive events with an explicit `environment` field. Every OPS read and write must preserve that environment distinction.

Bronze retains source values with ingestion metadata, including source-file lineage and run identification. Silver is the canonical validated cost-and-usage representation. Gold provides the charge-line fact and dimensions; fourteen datamarts serve recurring analytical subjects. The central Silver serving table is a copy of the canonical representation, not a second authority. The cloud artifacts are organized under `platform/common`, `platform/serverless` and `platform/classic_compute`; chapter 8 examines what the compute variants mean for cost rather than treating either layout as proof of a cost advantage.

## 5.3.2 Daily ingestion, backfill and monthly close

The Daily pipeline accepts a source URI and rejects an empty Parquet. It writes Bronze, applies the contract, prepares Silver, requires one open billing month, and refreshes that month in Gold and the datamarts. Source-file lineage prevents a previously ingested path from adding duplicate Bronze or Silver rows. The month remains `OPEN`, and the run identifier links data writes to OPS records. A changed object at an already processed path is not treated as a valid correction; RAW immutability is an operating assumption.

The current Classic Daily Job discovers the oldest RAW Daily file absent from PROD, then processes and validates the same URI in DEV before a promotion gate can admit PROD. Choosing against PROD allows a run interrupted after DEV success to rediscover the file; DEV should then write no additional rows. The template queues runs and limits concurrency to one. It handles one candidate per run, so a backlog requires repeated runs or a sequential catch-up controller. The working completion note reports a first Daily DEV load for 1 July 2026 with PROD promotion disabled; it does not document a full promotion and replay. Section 7.4 records this evidence boundary.

For a closed month, the detailed `billing-YYYY-MM.parquet` file becomes the authoritative source. The close function lands and validates it, checks that it contains the requested month, and records `BEFORE`, `SOURCE` and `AFTER` snapshots. These include row count, monetary sums, account and resource counts, critical-null count, charge-period bounds and, when available, a Delta version. SOURCE minus BEFORE measures the change from provisional Daily data; it is not automatically an error or saving. The function replaces that month in canonical and serving Silver, verifies AFTER row count and `BilledCost` against SOURCE within tolerance, requires zero critical nulls, refreshes Gold and datamarts, and sets `CLOSED_DATA_LOADED` under the current non-archiving configuration.

Historical backfill invokes the same monthly-close function sequentially over an inclusive month range. Month-scoped Delta replacement is atomic for each target table operation, but the full sequence across Silver, Gold, datamarts and OPS is not one multi-table transaction. Audit states, reconciliation and rerun procedures are therefore needed after a failure between steps. A dedicated Classic monthly-close DEV-to-PROD Job remains to be constructed and tested. Automatic RAW archival is disabled so that a DEV close cannot remove a bill still needed by PROD; optional archive code is not part of the documented normal close.

<!-- Note illustration C4 : si nécessaire, montrer découverte du fichier, validation DEV, promotion PROD et rejeu sans doublon ; distinguer le chemin implémenté du run complet encore à prouver. -->

## 5.3.3 Data contract, Gold model and datamarts

Section 4.5 sets out the analytical grain, table inventory and intended business questions. This section identifies the cloud implementation choices and their current evidence boundary.

The versioned FOCUS contract is the gate between Bronze and Silver. It defines expected types, required fields, nullability and selected quality rules. Extra source fields are permitted, while a missing required field or incompatible type is rejected. Project-specific rules require EUR billing currency and Microsoft as provider, ordered billing and charge period boundaries, and non-null `BilledCost`. Negative billed cost remains valid for credits and adjustments. Pricing and consumed quantities and units are present but optional. These restrictions describe the Azure-derived synthetic corpus, not FOCUS as a universal provider rule.

One remediation is deliberately narrow: an Adjustment with null `ServiceName` may use non-empty `ChargeDescription`; unrelated null service names remain invalid. Contract failure prevents Silver publication for that input. Local code and tests document the rule; its exact Databricks execution outcomes still require the run records described in section 7.4.

Gold centers on `fact_finops_cost_usage` at billing-line grain, with ten dimensions for date, billing scope, resource, service, SKU, location, pricing, commitment discounts, charge type and tags, plus a resource/tag bridge. Billing-scope and resource attributes currently receive Type 1 updates; validity columns do not yet prove complete SCD2 history. Versioned cloud SQL defines and loads these structures, while Python passes validated environment identifiers and orchestrates execution. Monthly billing replaces, rather than adds to, the Daily-fed month.

The cloud project defines fourteen subject-oriented datamarts in versioned SQL under `platform/common/sql/datamarts/table_refresh`. Some read Gold; others use central Silver fields not present in the fact. Full refresh simplifies publication but repeats work after each source change. The local POC validated fourteen DuckDB datamarts; that result cannot substitute for table-level DEV/PROD output and reconciliation evidence. The Belgium completion plan reports a successful historical backfill for January 2025–June 2026, but the executed commit, Job and Run IDs, control outputs, row and cost totals, and OPS snapshots must be indexed before the thesis treats it as an independently validated cloud result.

## 5.3.4 Jobs, audit, validation and recovery

Jobs coordinate environment checks, source selection, loading, promotion and validation. OPS records run status and monthly snapshots independently of the business catalogs. The snapshot sequence distinguishes a source correction from a failed publication: reconciliation requires AFTER to match validated SOURCE, while an interrupted run may leave some downstream tables older than Silver. Recovery therefore starts by locating the run, environment, month, source URI, Delta versions and failed task, then reruns the scoped operation and its controls. A green Job status alone is insufficient evidence of cross-table consistency.

The working completion note reports DEV and PROD backfill controls, but primary run artefacts remain to be assembled. A complete Daily promotion, an idempotent replay, a Classic monthly-close Job and an interrupted-run recovery test need separate records. Section 7.4 defines the validation protocol and current evidence boundary.

## 5.3.5 Streamlit application and read-only access

The separate cloud application under `FinOps Cloud Data Platform/apps/finops_dashboard` is designed to query `finops_prod.datamart` and `finops_ops.audit` through a SQL Warehouse without writing to Unity Catalog. Its pages cover the Knowledge Base, executive overview, cost drivers, savings, allocation and accountability, resources, operations and quality, and architecture. The Knowledge Base explains column names and cost calculations; comparisons of `ListCost`, `ContractedCost`, `EffectiveCost` and `BilledCost` remain descriptive until business eligibility and exclusion rules are validated.

The deployment guide specifies narrow read permissions for the application service principal. Source code and prescribed grants do not establish effective access: deployed page behavior, Warehouse permissions, direct SQL access and any Row-Level Security claim require tests and screenshots. The local Streamlit AppTest result in section 5.2 is not evidence for this application.

<!-- Note illustration C5 : ajouter une capture de la Databricks App seulement après contrôle du déploiement, des pages et des permissions ; conserver environnement, date et période dans la preuve. -->
