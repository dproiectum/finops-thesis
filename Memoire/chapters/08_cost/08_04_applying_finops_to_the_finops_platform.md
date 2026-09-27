# 8.4 — Applying FinOps to the FinOps Platform

## 8.4.1 Applying FinOps to the platform itself

The platform exists to improve the interpretation of cloud expenditure, but its own processing and reporting generate expenditure. This creates a second FinOps scope: the cost data being analyzed are the business object, while Databricks, GCP storage and compute are the cost of producing the analysis. Optimizing the latter should not weaken the former. A cheaper run that omits contract checks, delays monthly close beyond an agreed deadline or produces inconsistent datamarts would not be an acceptable improvement.

The first step is attribution. For each workload—historical backfill, one Daily file, monthly close, datamart refresh and dashboard query—record the source volume, Job or Warehouse identity, elapsed time, DBUs, applicable Databricks charge, GCP infrastructure charge and output quality. Useful unit measures are cost per processed billing month, cost per million charge lines and cost per successful Daily file, always paired with processing time and reconciliation status. These measures allow workload growth to be separated from a change in unit efficiency.

Databricks provides `system.billing.usage`, historical list prices and Job timeline tables for this analysis. Billing records may arrive after the run, so data freshness must be checked before treating a missing usage row as zero cost. The standard Job-cost queries do not attribute Jobs that run on an All-Purpose cluster as ordinary Job Compute; the project's Belgium Classic run therefore needs the cluster/time-overlap estimate described in section 8.3 and the associated GCP bill. The method and its attribution uncertainty must be stated alongside any comparison. [Databricks billable-usage reference](https://docs.databricks.com/gcp/en/admin/system-tables/billing); [Databricks Job-cost monitoring](https://docs.databricks.com/gcp/en/admin/system-tables/jobs-cost).

## 8.4.2 Workspace location and compute migration

According to the project owner's account, the platform was first exercised in a Frankfurt Databricks workspace with Serverless compute. After the team examined the platform's own consumption, the execution environment was rebuilt in a Belgium workspace using Classic compute. The current repository documents the latter configuration, but the earlier workspace and billing records still need to be archived for a fully traceable chronology. The available records do not establish the monetary saving attributable to location, compute mode or sizing individually. Earlier run identifiers, dates, SKU charges and GCP infrastructure charges must be retained before a numerical before-and-after claim is made.

The migration preserved the logical contract: the same external GCS RAW source and the catalog names `finops_raw`, `finops_dev`, `finops_prod` and `finops_ops`. The Classic deployment added a separate GCS bucket for Unity Catalog managed Delta storage and explicit catalog `MANAGED LOCATION` clauses, while the source bucket remained external and unchanged. A catalog's managed storage location is not the external FOCUS path read through `finops_raw.landing`. The storage change affected platform setup and compute-specific Job adapters, while common transformations and analytical products remained shared. The working completion note reports historical loading in the new workspace, subject to the evidence limits in section 7.4.

This migration is therefore a case of applying FinOps to the data platform itself, but it is not yet a controlled experiment. Region, Serverless versus Classic pricing, cluster size and lifecycle, Photon, concurrent-run policy and the timing of the runs may all affect the observed bill. Section 8.4.4 specifies how to separate these factors in a comparison.

## 8.4.3 Optimization levers relevant to this project

| Lever | Project-specific question | Measurement and trade-off |
|---|---|---|
| Compute choice | Should repeated batch Jobs use Serverless, dedicated Classic Jobs Compute or the current Classic All-Purpose cluster? | Compare full cost and duration for identical output; include GCP VM/disk cost for Classic and idle time for All-Purpose. |
| Cluster lifecycle | How much paid time occurs before, between and after batch tasks? | Measure idle intervals and evaluate auto-termination or task-level Jobs Compute without missing the next processing window. |
| Sizing and Photon | Does a larger or Photon-enabled run reduce total cost per successful month, despite a different rate? | Repeat the same workload with one setting changed, record DBUs, GCP resources, elapsed time and output equality. |
| Job schedule and concurrency | Does processing one Daily file per run cause repeated startup or a slow backlog? | Compare controlled sequential catch-up with the current single-file Job; protect month-level writes and track freshness. |
| SQL Warehouse and datamarts | Are Warehouse uptime and full refresh of fourteen datamarts justified by dashboard use? | Measure query latency, refresh time, Warehouse active time and table freshness before changing auto-stop or refresh scope. |
| Data retention | How much do shared RAW objects and DEV/PROD Delta copies cost? | Measure stored bytes and access needs; retain sources until every consumer and audit requirement is satisfied. |

These are hypotheses, not universal prescriptions. Databricks recommends matching compute to workload, using Jobs Compute for automated workloads where suitable, terminating idle Classic resources, and testing whether Photon improves cost per workload rather than duration alone. The project's current All-Purpose Classic configuration is a useful development and migration environment but merits measurement against alternatives once the pipeline is stable. [Databricks compute selection](https://docs.databricks.com/gcp/en/compute/choose-compute); [Databricks cost-optimization practices](https://docs.databricks.com/gcp/en/lakehouse-architecture/cost-optimization/best-practices).

## 8.4.4 Controlled comparison and decision rule

An optimization claim requires an A/B experiment on the same billing files and code revision, with isolated destination tables and identical validation queries. Record region, runtime, cluster or Serverless mode, Photon, worker configuration, concurrency, Warehouse settings, cache state and run order. Repeat runs so that one unusually slow startup or temporary cloud condition does not determine the conclusion. The two Classic backfill templates labeled “with Photon” and “without Photon” do not alone prove a Photon effect if they also differ by environment or input; the setting must be isolated in a comparable test.

For each candidate, compare total provider cost, not only DBUs: Databricks consumption plus GCP Compute Engine, disks, network and storage where applicable, while avoiding double counting infrastructure already included in a Serverless SKU. Then compare cost with elapsed time, data freshness, job failure rate, and equality of Silver, Gold and datamart outputs. A candidate is preferable only if it meets the required quality and operational constraints and improves the chosen cost-performance measure. If the business requires faster availability, a more expensive but much faster configuration may still be justified; the service objective should be stated rather than silently assumed.

## 8.4.5 Current conclusion

<!-- Note illustration C8 : si la comparaison chiffrée du § 8.3.3 est réalisée, y renvoyer ici pour discuter les leviers ; ne pas dupliquer le même graphique. -->

The project already exposes several concrete opportunities: an All-Purpose Classic cluster may incur idle cost; the Daily Job processes one candidate per run; DEV and PROD retain separate Delta products; and the first cloud version refreshes all datamarts. At present, however, the evidence register lacks the priced run-level and GCP records needed to rank these levers or quantify a saving. The immediate FinOps action is to establish the measured baseline in section 8.3, then test one change at a time under the protocol in section 7.3. Chapter 9 will distinguish a measured recommendation from an untested deployment option.
