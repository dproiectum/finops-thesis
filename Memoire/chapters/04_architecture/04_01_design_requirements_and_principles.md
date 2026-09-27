# 4.1 — Design Requirements and Principles

The architecture follows the requirements in section 1.5. It must make source charges traceable, validate data before publication and serve consistent indicators to users with different access rights. The distinction between these requirements and the available tools matters because the local POC, cloud prototype and possible enterprise deployment have different operating conditions.

## Functional drivers

- ingest recurring FOCUS cost and usage data;
- preserve received evidence and its provenance;
- validate a versioned data contract before canonical publication;
- publish consistent FinOps data products for Inform, Optimize and Operate;
- support dashboard users and authorized analytical consumers;
- reconcile row counts and financial measures across transformations.

## Quality and governance drivers

- explicit ownership and definitions;
- controlled schema evolution;
- record-level and batch-level lineage;
- reproducible processing and validation;
- visibility of rejected, missing or unallocated information;
- separation between canonical data and derived analytical products.

## Security drivers

- least-privilege and read-only analytical access;
- isolation of managerial or domain perimeters;
- protection of direct SQL access in addition to dashboard filtering;
- no credentials committed to source control.

## Operational drivers

- restart and recovery information;
- observable freshness and execution status;
- maintainability by the platform and FinOps roles;
- portability between the local validation environment and the target cloud environment where feasible.

## Project constraints

The design must remain achievable within the PFE schedule and available licences. Confidentiality limits direct use of enterprise billing data. Only a restricted anonymized source is available. The local DuckDB POC, the Databricks/GCP DEV and PROD workspaces, and a possible enterprise Azure target provide different levels of evidence.
