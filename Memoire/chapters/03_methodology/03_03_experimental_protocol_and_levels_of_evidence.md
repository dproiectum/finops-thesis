# 3.3 — Experimental Protocol and Levels of Evidence

## 3.3.1 Evaluation questions

The evaluation follows the three research questions in section 1.3. Data reliability is examined through source completeness, contract outcomes, row and monetary reconciliation, and repeatability. Governed self-service is examined through task completion and access tests at each interface. Decision support is examined through the correctness and interpretation of cost indicators. Performance and operating cost are assessed only against equivalent workloads with recorded configurations.

Each result is associated with its dataset, period, environment, software revision and procedure. A defined requirement or implemented control is evidence of design or code, whereas an execution log and output establish behavior in a particular environment. This distinction prevents a local DuckDB test from being cited as Databricks validation.

## 3.3.2 Available environments and data

The local POC contains a January 2025 synthetic billing month and provides the currently reproducible dashboard and datamart observations. The independent generator supplies Daily files through August 2026 and validated unchanged monthly billing through June 2026. The Belgium Databricks plan reports historical DEV and PROD processing through June 2026, but the run-level artifacts required to reproduce its totals are not yet indexed. A controlled cloud comparison requires the same input months, transformations and expected outputs, with compute and cache settings recorded for each run.

## 3.3.3 Evidence and inference

The project evidence register identifies local validation reports, source manifests, SQL results and the technical completion plan. For a cloud result, the record must also contain the executed revision, Job and Run IDs, task outputs, row and cost totals, and relevant billing data. Failed attempts belong in the same record because excluding them would overstate reliability. Figures derived from the synthetic corpus establish properties of that corpus and the tested implementation; they cannot estimate the host organization's actual expenditure or savings.
