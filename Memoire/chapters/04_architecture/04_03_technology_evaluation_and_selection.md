# 4.3 — Technology Evaluation and Selection

## 4.3.1 Evaluation basis

The project's initial architecture evaluation considered Microsoft Fabric, Azure Databricks and a modular Azure PaaS solution against requirements for ingestion, contract validation, governed analytical products and reporting. It also listed maintainability, security, cost, available licences and feasibility within the PFE as criteria. The evaluation was qualitative: it contained neither weighted scores nor a measured total cost for the three candidates. It can explain which risks were considered, but it cannot support a numerical ranking.

## 4.3.2 Platform alternatives and implemented scope

Fabric groups data preparation, storage, SQL and Power BI within one service environment. The initial record treats this integration as a possible advantage and flags capacity and licensing as questions. Azure Databricks offers a lakehouse processing path with Unity Catalog and SQL serving, but the proposed Azure architecture would also require storage, identity and reporting integration. A modular Azure solution would make service boundaries explicit while increasing the number of components to configure and operate. These are design observations from the initial evaluation, not benchmark results.

The implementation subsequently converged on Databricks with GCP object storage for the active cloud prototype. Its code and catalog organization are described in sections 4.4 and 5.3; execution evidence is assessed in section 7.4. This implementation choice establishes what was built; the available decision record does not isolate the commercial, access or scheduling reason for the move from the Azure-first options. The thesis therefore does not present the GCP prototype as an approved enterprise Azure deployment or infer that it outperformed Fabric on cost.

## 4.3.3 Storage and processing choices

The independent generator publishes Parquet files as the shared RAW input. [Apache Parquet](https://parquet.apache.org/docs/overview/) specifies a column-oriented file format for storage and retrieval. The Databricks pipeline publishes managed Delta tables in Bronze, Silver and Gold, where month-level replacement and table history are required. [Delta Lake](https://docs.databricks.com/gcp/en/delta/) extends Parquet data files with a transaction log; the two formats therefore serve different roles in this design rather than being mutually exclusive alternatives. A replacement is atomic for an individual Delta table operation, while the entire multi-table pipeline needs audit and recovery logic.

Python and PyArrow support deterministic file generation and schema checks. SQL defines the Gold model and datamarts, and PySpark coordinates their execution in Databricks. YAML records the versioned data contract, while DBML documents the dimensional design. DuckDB serves the frozen local POC; its results are evidence for that environment only.

## 4.3.4 Reporting decision and remaining comparison

The POC uses Streamlit with DuckDB datamarts, whereas the cloud application is designed to query Databricks through a SQL Warehouse. The existing Power BI dashboard remains the professional reference system. The repository demonstrates local Streamlit execution, but it does not contain a controlled comparison of these reporting options or validated Row-Level Security for the new application. The selection can therefore be defended for the implemented prototype and its reproducible tests; an enterprise adoption recommendation would also require access, performance and operating-cost evidence.

## 4.3.5 Technology choices by function

The following table summarizes the tools present in the two implementations. The local POC is a separate experiment, not the DEV environment of the cloud platform. DEV and PROD use the same Databricks/GCP architecture with separate business catalogs. The table reports implementation choices and their role; it is not a scored comparison of every tool named during early exploration.

| Function | Local POC | Cloud DEV and PROD | Rationale and evidence boundary |
|---|---|---|---|
| Source files | Shared synthetic Parquet files on the local filesystem | The same published Parquet history in GCS, exposed through an external Unity Catalog volume | A common input supports comparison; publication and cloud ingestion need separate checks. |
| Data processing | Python/Pandas and local notebooks | PySpark for ingestion and contract processing; versioned SQL for Gold and datamarts | The cloud path uses distributed Spark execution, but no performance advantage follows without a comparable benchmark. |
| Processed tables | Local Delta layers and a DuckDB analytical warehouse | Managed Delta tables in Bronze, Silver, Gold and datamarts | Delta supports table-level replacement and history; DuckDB supplies local analytical tests. |
| Orchestration | Explicit local commands and notebook execution | Databricks Jobs coordinating notebooks and validation tasks | The cloud Jobs encode task dependencies; an automatic schedule does not by itself prove end-to-end operation. |
| Governance and audit | Local contract checks and test outputs | Unity Catalog namespaces and permissions; `finops_ops.audit` for operational history | Catalog organization is implemented, while effective access and recovery still require run-level tests. |
| Analytical access | DuckDB queries over local datamarts | SQL Warehouse queries over PROD datamarts and OPS audit | The Warehouse serves the application; it is not the compute engine used by every batch task. |
| Visualization | Local Streamlit application | Separate Streamlit Databricks App | The local interface is tested; cloud page behavior and permissions need their own evidence. Power BI remains the existing professional reference system. |

The initial evaluation documents Fabric, Azure Databricks and modular Azure PaaS as platform alternatives. It does not provide controlled scores for Colab, Airflow, Tableau or every other tool that could be placed in a category. Adding such products to this table would imply an evaluation that the project did not perform.
