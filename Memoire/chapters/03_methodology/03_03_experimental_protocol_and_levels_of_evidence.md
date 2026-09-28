# 3.3 — Experimental Protocol and Levels of Evidence

## 3.3.1 Method and evaluation questions

The method connects the requirements in section 1.3 to tests with observable outcomes. A requirement is first translated into an expected behavior, such as rejecting an invalid source before publication or preserving a month's billed amount across transformations. The implementation is then executed with identified inputs, and its output is compared with that expectation. A failed result leads to diagnosis, a recorded change and a new test. This sequence evaluates the implemented artifact rather than treating the presence of code as evidence that a requirement has been met.

The three subquestions in section 1.3 organize the evaluation. Performance and operating cost provide an additional assessment of implementation feasibility.

| Evaluation dimension | Test or comparison | Evidence required |
|---|---|---|
| Platform reliability | Source completeness, contract acceptance and rejection, row and monetary reconciliation, and repeated processing without duplicate activity | Identified source files, expected totals, quality results, execution outputs and before/after controls |
| Governed self-service | Completion of defined analytical tasks within an authorized scope, and refusal of access outside that scope | Task outputs and access-test results for each exposed interface; user feedback where collected |
| FinOps decision support | Agreement of displayed indicators with reference calculations, and interpretation consistent with the selected cost measure | Reference queries, calculated values, dashboard outputs and explicit analytical limitations |
| Performance and operating cost | Equivalent input periods and transformations executed with recorded compute configurations | Run and task durations, output checks, consumption records, pricing basis and documented cost attribution |

Each result is associated with its dataset, period, environment, software revision and procedure. A defined requirement or implemented control is evidence of design or code, whereas an execution log and output establish behavior in a particular environment. This distinction prevents a local DuckDB test from being cited as Databricks validation.

## 3.3.2 Available environments and data

The local POC contains a January 2025 synthetic billing month and provides the reproducible dashboard and datamart observations recorded on 27 September 2026. The independent generator supplies Daily files through August 2026 and validated unchanged monthly billing through June 2026. The Belgium Databricks plan reports historical DEV and PROD processing through June 2026, but the run-level artifacts required to reproduce its totals are not yet indexed. These environments therefore provide different evidence, rather than interchangeable repetitions of one experiment.

The cloud protocol distinguishes historical monthly backfill from Daily incremental processing and subsequent monthly replacement. For each workflow, the expected period, source files, output totals and handling of a repeated execution must be specified before its result is assessed. DEV validation precedes PROD processing, but success in DEV is not itself evidence of a successful PROD execution.

A controlled compute comparison requires the same input months, software revision, transformations and expected outputs, with compute and cache settings recorded for each run. Elapsed time and DBU consumption are reported separately from monetary cost. The pricing basis and infrastructure charges included in that cost must be stated. Cluster activity outside task execution, including idle or shared intervals, must not be silently attributed to one Job run. Where inputs, cache state or cost attribution differ, the comparison is reported as an operational observation rather than a controlled performance result.

## 3.3.3 Evidence and inference

The project evidence register identifies local validation reports, source manifests, SQL results and the technical completion plan. For a cloud result, the record must also contain the executed revision, Job and Run IDs, task outputs, row and cost totals, and relevant billing data. Failed attempts belong in the same record because excluding them would overstate reliability. Figures derived from the synthetic corpus establish properties of that corpus and the tested implementation; they cannot estimate the host organization's actual expenditure or savings.
