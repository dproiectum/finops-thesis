# 4.4 — Selected Physical Architecture

Section 4.2 defines the required functions, and section 4.3 explains the chosen technologies. This section places the implemented components in their actual storage, catalog, processing and access boundaries. It answers where data resides and how the components connect; it does not repeat the technology comparison or detail every table, which is the purpose of section 4.5.

## 4.4.1 System boundary and implementation tracks

The implementation separates three responsibilities. `FinOps Data Generator` produces a single FOCUS-based synthetic dataset, independently of any analytical engine. `FinOps Data Platform - POC` preserves the earlier DuckDB/Streamlit experiment and its January 2025 local results. `FinOps Cloud Data Platform` is the active Databricks/GCP implementation. This division preserves the value of the local validation without implying that DuckDB and Spark execute identical physical code or that local results validate cloud operation.

The cloud platform receives detailed Daily and monthly Parquet files in a shared RAW namespace, transforms them through Bronze and Silver Delta tables, builds a Gold dimensional model, and publishes subject-oriented datamarts. The repository packages the final Streamlit dashboard as a container for Google Cloud Run. The application queries PROD datamarts and operational audit through a SQL Warehouse using a read-only technical identity; its deployed behavior and effective permissions still require retained verification evidence. Read-only access does not, by itself, limit each viewer to an application or domain. The architecture is a PFE prototype with planned extensions; it is not a claim of deployment into Technip Energies production systems.

```text
Independent generator → GCS source bucket → finops_raw.landing.focus
                                           ├─ finops_dev → Bronze → Silver → Gold → datamarts
                                           └─ finops_prod → Bronze → Silver → Gold → datamarts
                       managed Delta tables and OPS audit → separate UC storage bucket
                       DEV and PROD runs → finops_ops.audit
                       PROD datamarts + audit → SQL Warehouse → Cloud Run/Streamlit
```

<!-- Note illustration F3 : remplacer le bloc ci-dessus par un schéma physique montrant le générateur, le bucket GCS des Parquet RAW, le Volume externe, DEV/PROD/OPS, le bucket distinct des tables gérées Classic, puis SQL Warehouse et Cloud Run/Streamlit. Distinguer le service principal technique du futur contrôle de périmètre par utilisateur. Ne pas représenter une comparaison de coût ou de performance. -->

## 4.4.2 Source authority, catalogs and data lifecycle

`finops_raw.landing.focus` exposes Parquet objects from `gs://dtl_finops/focus` to both environments. DEV business tables reside in `finops_dev`; PROD business tables reside in `finops_prod`. Each contains Bronze, Silver, Gold and datamart schemas. The separate `finops_ops.audit` catalog has five operational tables and records an explicit `environment` on each row. In the Classic Compute setup used for the Belgium prototype, managed catalog storage is configured under `gs://dtl_finops-unitycatalog-euw1/catalogs/`, separate from the source bucket. This arrangement permits independent data publication while maintaining a shared operational history. It also makes an environment filter essential in every audit lookup and write.

The source lifecycle follows financial meaning. Daily files populate an open month provisionally. The detailed monthly billing file becomes authoritative after close: the pipeline replaces that month separately in the two Silver tables and in the Gold fact, merges Gold dimensions, and rebuilds datamarts. These writes are not one cross-table transaction. The two source types are never added together in the fact table; replay and audit are needed if a run stops between table operations.

Automatic RAW archival is disabled in the common configuration. The earlier design would have moved processed sources after close, but a DEV close could then remove a file needed for independent PROD processing. Keeping the RAW objects allows both environments to consume the same path for replays. It does not make those objects immutable: Bronze ingestion deduplicates on `_source_file`, so replacement of an object at the same path is not detected as a new source version by that check. Source-version or checksum controls would be needed to establish immutable evidence. Retention also has a storage cost; any future move or deletion must account for every consumer and the audit period. The archival module remains optional, not an active lifecycle step.

## 4.4.3 Compute configuration boundary

The repository separates common processing logic from compute-specific deployment artifacts. `platform/common` contains shared notebooks and SQL. `platform/serverless` and `platform/classic_compute` contain the respective setup and Job adapters. The Belgium implementation uses the Classic setup with explicit GCS managed locations; the Serverless setup remains a distinct execution scenario using Default Storage. Both target the same logical RAW-to-datamart flow, but their catalog storage configuration, compute lifecycle and billing attribution differ. The separation avoids redefining the data contract or analytical grain when adapting the deployment.

This architecture section records the physical components and their interfaces, not the chronology of workspace decisions or a claim that either compute mode is more economical. Chapter 7 records execution evidence and chapter 8 examines the later location and compute choices as an operating-cost case study.

## 4.4.4 Analytical and consumption layers

Silver retains the canonical FOCUS representation after contract validation. Gold and the fourteen datamarts are stored separately in each business catalog. Versioned SQL defines and refreshes these products; Python orchestrates execution and supplies validated environment identifiers. Some datamarts read central Silver fields absent from the Gold fact, while others read Gold. Section 4.5 specifies the tables, their grain and the business questions they are designed to address. Each datamart is fully refreshed in the current implementation; this simplifies publication but adds work after a monthly replacement and can restate historical groupings when Type 1 dimension attributes change.

The frozen local dashboard's query definitions reference ten of the fourteen local datamarts; this count describes code usage, not a separate execution result. The cloud dashboard is a separate Streamlit implementation packaged for Cloud Run and designed to read PROD datamarts and OPS audit in read-only mode. Its technical identity can restrict the application to serving objects, but it does not identify which viewer is a domain manager, application owner or project manager. No viewer-specific perimeter policy is implemented in the repository at the time of this design update. Access must therefore remain limited to synthetic demonstration data or trusted project users until the proposed authorization controls are implemented and tested. Effective grants and direct SQL access still require verification; interface behavior alone cannot establish them.

## 4.4.5 Dashboard identity and authorization boundary

The proposed access-control extension separates authentication from business authorization. In the production target, Google Identity-Aware Proxy authenticates a viewer before a request reaches Cloud Run. The application must validate the signed IAP assertion rather than trust an email supplied by a form or an unsigned header. It then resolves the verified email against two managed control tables in a new `finops_ops.security` schema. `user_entitlement` associates a principal with a role and scope, while `business_scope` relates domains, subdomains, applications and projects to attributes available in the FinOps products. The application service principal remains read-only and receives no RAW, DEV or write privilege.

The PFE demonstration uses the same authorization logic with a fixed list of synthetic personas. A configuration value selects either `demo`, in which a predefined persona can be chosen, or `iap`, in which no selector is exposed and the signed identity is mandatory. A free-text email field is excluded because it would allow a viewer to assert another identity. The demonstration can therefore test role and scope behavior without being presented as enterprise authentication. The planned roles are FinOps administrator, domain manager, subdomain manager, application owner and project manager; an identity without an active entitlement must be denied by default.

*Source: Google Cloud, Configure IAP for Cloud Run and Getting the user's identity (accessed 1 October 2026).*

This boundary is an architectural decision and validation target, not yet an implemented result. Section 5.3 defines the intended implementation and Section 7.5 defines the evidence required before the thesis can claim successful role- and scope-based isolation.

## 4.4.6 Architectural trade-offs and evidence boundary

The design prioritizes a shared source path, separate DEV and PROD catalogs, a canonical Silver layer and reproducible SQL products. It accepts duplicated business data, materialized datamarts and retained RAW objects to make testing, promotion and audit easier. It does not yet guarantee source immutability or user-specific showback access. The proposed persona simulation reduces implementation risk and demonstrates authorization logic, but only validated IAP integration and organizational identities could support a production authentication claim. These choices incur storage, refresh and operational costs that chapter 8 must quantify. Chapter 7 must establish which cloud paths ran successfully and how they compare with the POC. The existence of two compute configurations alone cannot establish a cost or latency advantage.
