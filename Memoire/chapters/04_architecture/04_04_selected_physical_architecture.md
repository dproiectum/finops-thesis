# 4.4 — Selected Physical Architecture

Section 4.2 defines the required functions, and section 4.3 explains the chosen technologies. This section places the implemented components in their actual storage, catalog, processing and access boundaries. It answers where data resides and how the components connect; it does not repeat the technology comparison or detail every table, which is the purpose of section 4.5.

## 4.4.1 System boundary and implementation tracks

The implementation separates three responsibilities. `FinOps Data Generator` produces a single FOCUS-based synthetic dataset, independently of any analytical engine. `FinOps Data Platform - POC` preserves the earlier DuckDB/Streamlit experiment and its January 2025 local results. `FinOps Cloud Data Platform` is the active Databricks/GCP implementation. This division preserves the value of the local validation without implying that DuckDB and Spark execute identical physical code or that local results validate cloud operation.

The cloud platform receives detailed Daily and monthly Parquet files in a shared RAW namespace, transforms them through Bronze and Silver Delta tables, builds a Gold dimensional model, and publishes subject-oriented datamarts. Its read-only application consumes the datamarts and operational audit through a SQL Warehouse. The architecture is an implemented PFE prototype with planned extensions; it is not a claim of deployment into Technip Energies production systems.

```text
Independent generator → GCS RAW Parquet → finops_raw.landing
                                          ├─ DEV → Bronze → Silver → Gold → datamarts
                                          └─ PROD → Bronze → Silver → Gold → datamarts
                              DEV and PROD runs → finops_ops.audit
                              PROD datamarts + audit → SQL Warehouse → App
```

<!-- Note illustration F3 : remplacer le bloc ci-dessus par le schéma physique du générateur, GCS RAW partagé, finops_raw, finops_dev, finops_prod, finops_ops et SQL Warehouse/App. Montrer la frontière des responsabilités sans attribuer ici une région ni un résultat de performance. Vérifier chaque lien dans la documentation d'architecture et le code. -->

## 4.4.2 Source authority, catalogs and data lifecycle

`finops_raw.landing` exposes the same GCS objects to both environments. DEV business tables reside in `finops_dev`; PROD business tables reside in `finops_prod`. Each contains Bronze, Silver, Gold and datamart schemas. The separate `finops_ops.audit` catalog has five operational tables and records an explicit `environment` on each row. This arrangement permits independent data publication while maintaining a shared operational history. It also makes an environment filter essential in every audit lookup and write.

The source lifecycle follows financial meaning. Daily files populate an open month provisionally. The detailed monthly billing file becomes authoritative after close and replaces that month's Silver and Gold contents. The two source types are never added together in the fact table. A monthly replacement is therefore a correction of the canonical state rather than another batch of cost on top of Daily activity.

Automatic RAW archival is disabled in the common configuration. The earlier design would have moved processed sources after close, but a DEV close could then remove a file needed for independent PROD processing. Keeping the RAW objects allows both environments to consume the same input and preserves the evidence used for replays. This choice has a storage and lifecycle cost: a future retention rule must identify every consumer and the audit period before moving or deleting any source. The archival module remains in the codebase as an optional capability, not an active lifecycle step.

## 4.4.3 Compute configuration boundary

The repository separates common processing logic from compute-specific deployment artifacts. `platform/common` contains shared notebooks and SQL. `platform/serverless` and `platform/classic_compute` contain the respective setup and Job adapters. Both scenarios target the same logical RAW-to-datamart flow, while catalog storage configuration, compute lifecycle and billing attribution differ. This separation allows the implementation to change compute without redefining the data contract or analytical grain.

This architecture section records the physical components and their interfaces, not the chronology of workspace decisions or a claim that either compute mode is more economical. Chapter 7 records execution evidence and chapter 8 examines the later location and compute choices as an operating-cost case study.

## 4.4.4 Analytical and consumption layers

Silver retains the canonical FOCUS representation after contract validation. Gold and the fourteen datamarts are stored separately in each business catalog. Versioned SQL defines and refreshes these products; Python orchestrates execution and supplies validated environment identifiers. Some datamarts read central Silver fields absent from the Gold fact, while others read Gold. Section 4.5 specifies the tables, their grain and the business questions they are designed to address. A full datamart refresh favors simple publication in the current version at the expense of extra work after each monthly replacement.

The frozen local dashboard demonstrated that eleven of fourteen local datamarts support its views. The active Databricks App is a separate implementation designed to read PROD datamarts and OPS audit in read-only mode. Its service principal is intended to receive only the Unity Catalog and Warehouse permissions required for that use. Actual effective permissions, direct SQL access and Row-Level Security require their own tests; interface behavior alone cannot establish them.

## 4.4.5 Architectural trade-offs and evidence boundary

The design prioritizes a single source history, explicit environment isolation, a canonical Silver layer and reproducible SQL products. It accepts duplicated DEV/PROD data, materialized datamarts and retained RAW objects to make testing, promotion and audit easier. These choices incur storage, refresh and operational costs that chapter 8 must quantify. Chapter 7 must establish which cloud paths ran successfully and how they compare with the POC. The existence of two compute configurations alone cannot establish a cost or latency advantage.
