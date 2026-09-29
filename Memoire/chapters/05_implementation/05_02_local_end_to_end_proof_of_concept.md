# 5.2 — Local End-to-End Proof of Concept

The local POC is a frozen DuckDB/Streamlit experiment. It demonstrates a processing and reporting chain for synthetic January 2025 data without implying that the later Databricks implementation runs the same physical code. Its results are treated as local evidence throughout this thesis; cloud execution is assessed separately in section 7.4.

## 5.2.1 DuckDB processing chain and data contract

The POC reads detailed monthly Parquet, processes Bronze, Silver and Gold data, and publishes analytical tables into a local DuckDB warehouse. The contract boundary checks the source before canonical Silver publication. This establishes an end-to-end local route from generated bill to queryable output, but it does not validate the behavior of the cloud contract implementation or its operational recovery controls.

For January 2025, the recorded POC outputs contain 164,145 charge lines and EUR 912,000 in `BilledCost` through Bronze, Silver and the Gold fact. The local integrity check reports no orphan foreign keys. Section 7.1 examines these results and their limits.

## 5.2.2 Gold model and subject-oriented datamarts

The local model preserves the charge-line grain and provides dimensions for recurring cost questions. DuckDB SQL templates publish fourteen materialized datamarts in the `datamart` schema; eleven feed the local dashboard. Subjects include executive cost and volume, cost-basis comparisons, top resources, quality and batch traceability, resource groups, subscriptions, and ownership attribution.

Materialization keeps repeated analytical expressions outside the interface and permits reconciliation with the local source. It also duplicates data and requires coordinated refresh. The local test establishes publication for one synthetic month; it does not establish a measured latency advantage or cloud table-level reconciliation. The cloud project implements corresponding subjects in its own versioned SQL rather than executing the DuckDB templates unchanged.

## 5.2.3 Local Streamlit dashboard

The POC's Streamlit application reads DuckDB datamarts without writing to them. Its Knowledge Base explains column names and cost formulas alongside the analytical views. Streamlit AppTest exercised eight subviews for January 2025, and the displayed EUR 912,000 billed cost and 164,145 rows reconcile with the local checks. Section 7.1 presents the validation scope. This does not establish effective cloud permissions, Row-Level Security or the behavior of the separate Databricks application.

<!-- Note illustration F5 : une seule capture de dashboard dans le corps du mémoire. Retenir ici le POC réel de janvier 2025 si aucune capture cloud validée n'est retenue en 5.3.5 ; indiquer période, filtres, KPI et données synthétiques. Une seconde capture ne va en annexe que si elle démontre une différence utile. -->
