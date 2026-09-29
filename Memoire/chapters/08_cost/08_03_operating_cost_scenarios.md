# 8.3 — Operating-Cost Scenarios

## 8.3.1 Cost boundary and unit of analysis

The relevant economic object is the cost of operating the FinOps platform, not the cloud charges that the platform analyzes in chapter 6. A monthly estimate should include recurring ingestion and close runs, SQL Warehouse use, App hosting where billed, RAW and managed Delta storage, network charges where applicable, monitoring and human support. A run-level view is also needed to compare compute alternatives. The reference unit should be stated explicitly—for example, one historical billing month processed, one newly arrived Daily file, or one calendar month of service—because these workloads have different frequency and data volume.

Let *nᵢ* be the number of runs of workload type *i*, *Cᵢ* their measured cost per comparable run, and *Cshared* the recurring cost not assigned to a run. The monthly estimate is Σ(*nᵢ × Cᵢ*) + *Cshared*. The shared term includes SQL Warehouse and application use, storage, attributable network and monitoring charges, and human support under a stated allocation rule.

This expression defines a method; no numerical result follows from it without consumption data. Build effort from section 8.2 is added only when computing total cost over a defined horizon. Credits or trial allowances affect cash paid, while usage before credits remains relevant to a future operating model.

## 8.3.2 Measuring Databricks and GCP consumption

The project contains a monitoring SQL script that links Job runs to their task timeline and Databricks billing records. For Serverless or dedicated Job Compute, a Job ID and Run ID can identify DBU usage and list-price cost directly when those metadata are present. Billing-system records may arrive after a run; an empty immediate query result must not be interpreted as zero usage. Report both consumed DBUs and the tariff/currency used for a monetary conversion.

The Belgium Classic templates use an All-Purpose cluster. Its billing records identify the cluster but may not identify the Job run. The monitoring script therefore estimates each run's Databricks share by the time overlap between the run window and cluster billing intervals. This attribution is reliable only if other notebooks and Jobs did not share the cluster during that window; otherwise their use is mixed into the estimate. The cluster ID, run interval, competing activity and allocation rule must be recorded. Classic total cost also includes the relevant GCP Compute Engine driver and worker charges, disks and network from GCP Cloud Billing. Databricks list-price DBUs alone understate Classic cost. For Serverless, the DBU charge already includes virtual-machine cost, so adding an equivalent VM charge would double count it.

*Source: Databricks, [Billable usage system table reference](https://docs.databricks.com/gcp/en/admin/system-tables/billing), [Monitor job costs & performance with system tables](https://docs.databricks.com/gcp/en/admin/system-tables/jobs-cost) and [Best practices for cost optimization](https://docs.databricks.com/gcp/en/lakehouse-architecture/cost-optimization/best-practices).*

The RAW retention choice (section 4.4) also has a measurable consequence. Keeping one shared source for DEV and PROD avoids premature removal and supports replay, but GCS storage persists until a coordinated retention rule is introduced. DEV and PROD managed Delta tables and materialized datamarts create additional copies. Their volume and storage class should be measured rather than estimated solely from source-file size.

## 8.3.3 Scenario comparison

Three operating scenarios can be evaluated with the same model: a supervised PFE demonstration with manual runs, a pilot with scheduled Daily and monthly processing, and wider use with more users or more frequent queries. For each scenario, specify input volume, period, run frequency, concurrency, SQL Warehouse uptime, retention, App usage and human support. Sensitivity analysis should vary these drivers one at a time, particularly Daily backlog, monthly refresh frequency and Classic cluster idle time.

A Serverless-versus-Classic comparison requires the same source months, equivalent transformations and verified output equality, followed by repeated runs with recorded compute settings. Measure startup, total elapsed time, DBUs and full provider cost per processed month or million charge lines. The earlier Serverless `STANDARD` setting with `max_concurrent_runs = 4` was a development configuration; the Belgium Classic Daily Job instead limits concurrency to one. Comparing their unadjusted bills would conflate both compute mode and workload policy.

<!-- Note illustration C8 : seulement si une comparaison contrôlée et rapprochée avec les consommations Databricks/GCP devient plus claire en graphique, montrer ici coût total et durée par même unité de travail. Sinon, conserver un tableau compact. Distinguer DBU et infrastructure Classic sans recompter les VM incluses dans Serverless ; ne pas répéter la figure ailleurs. -->

## 8.3.4 Current result and interpretation

The repository supplies the costing procedure and monitoring query, but the evidence register does not yet contain the Job and Run IDs, priced DBU outputs or GCP Cloud Billing extract needed for a numeric comparison. The current result is a defined measurement method and cost boundary. A comparison will require observed consumption normalized to a common workload, raw query outputs and dated price sources. A claim about return on investment would also need a comparable baseline and measured business benefit. Section 8.4 uses this method to assess possible changes to Databricks workloads.
