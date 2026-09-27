# 7.4 — Databricks/GCP Validation

## 7.4.1 Validation boundary

Cloud validation addresses a different claim from the local DuckDB POC: whether the shared Parquet source can be processed by Databricks, isolated into DEV and PROD catalogs, reconciled, and exposed as governed analytical products. The tests should identify the workspace, region, compute type, Photon setting, executed Git commit, source period, Job and Run IDs, and final table versions. A repository file or deployment guide establishes the intended procedure; an execution record establishes what ran. The available plan locates the work in the Belgium workspace and identifies a Classic scenario, but its summary alone does not provide these run-level details.

The acceptance criteria follow the data path. The RAW file must be readable; Bronze must preserve its rows and source lineage; contract failures must prevent invalid Silver publication; the authoritative billing month must replace rather than add to provisional Daily rows; Gold and datamarts must reconcile to Silver; and OPS must retain distinct DEV and PROD histories. The application must use permitted read access without write privileges. These criteria test both functional correctness and governance rather than interpreting a green Job icon as complete validation.

## 7.4.2 Evidence currently available

The working Belgium completion note states that the four catalogs exist, that a monthly backfill for January 2025–June 2026 and DEV/PROD controls succeeded, and that the first 1 July 2026 Daily file was loaded in DEV with `promote_to_prod=false`. Sections 3.1–3.2 independently report local validation of eighteen `no_change` billing files through June 2026 and Daily files through August 2026. These source counts can be compared with the cloud tables once the relevant Run IDs and query outputs are captured. The cloud claims remain reported execution awaiting primary artefacts, rather than independently reproduced thesis measurements.

| Capability | Current record | Evidence needed for a validated thesis claim |
|---|---|---|
| Historical DEV/PROD backfill | Reported successful in the Belgium plan | Executed commit; Job/Run IDs; dates; task outputs; rows and `BilledCost` by month; reconciliation status |
| Daily DEV load | 1 July 2026 reported in DEV only | Run ID; source URI; rows written; DEV checks and month status |
| Daily promotion to PROD | Job template and procedure exist | Complete DAG run; matching DEV/PROD outputs; OPS records; idempotent replay |
| Monthly close DEV → PROD | Module and notebook exist; dedicated Classic Job absent | Billing-arrival guard; both runs; `BEFORE/SOURCE/AFTER`; equality and failure recovery |
| Databricks App | Source and deployment guide exist | Deployment record; page checks; Warehouse and Unity Catalog permissions |

<!-- Note illustration F8 : après collecte des artefacts primaires, ajouter une vue synthétique des runs DEV/PROD : Job/Run IDs, commit, mois, volumes, BilledCost et résultat de réconciliation. Placer 1–2 captures ciblées du Job et des contrôles en annexe. Une icône de succès seule ne suffit pas. -->

## 7.4.3 Daily-to-close experiment

A complete Daily experiment should begin with a RAW file in an open month. The discovery step must choose the oldest file absent from PROD, then DEV load and validation must succeed before the promotion gate admits PROD. The same URI must reach both environments. A deliberate replay of that file should write no duplicate Bronze or Silver rows while keeping the checks green. A no-candidate run should end without loading data. Because the Job processes one candidate per run, a backlog requires repeated sequential runs or an explicit catch-up controller; schedule frequency alone does not clear many pending days quickly.

The monthly-close experiment should begin only when a detailed billing file is present. It must record the provisional `BEFORE` state, validated `SOURCE` and stored `AFTER` state for the same month and environment. The technical reconciliation passes only when AFTER row count matches SOURCE, their `BilledCost` difference is within tolerance and critical-null count is zero. This demonstrates faithful replacement of the billing candidate; it does not determine whether a nonzero SOURCE-minus-BEFORE difference is financially justified. DEV should pass before PROD is promoted, and a failed or interrupted promotion should be replayable without changing a previously closed month incorrectly. The dedicated Classic orchestration and its test results are still pending.

## 7.4.4 Limits of current validation

The currently indexed local tests demonstrate generator consistency and cloud-code behavior outside Databricks. The Belgium plan provides a credible progress record for historical cloud loading, but without primary artifacts the thesis cannot report exact cloud row counts, durations, DBUs or application behavior as measured results. No controlled Serverless/Classic performance or cost comparison follows from the presence of both configurations. RLS and direct SQL-access rules require separate access tests. These limits are carried into chapters 8 and 9 rather than filled with estimates presented as observations.
