# 7.2 — Existing Power BI Diagnosis and Measurement Protocol

The existing Power BI report provides the professional comparison point for reporting needs. The student's account identifies a multi-step change process, but it contains no measured report latency, refresh duration or capacity data. A slow interaction could arise from the semantic model, its source, a visual, network transfer, shared capacity or cache state. The present evidence does not identify which component dominates.

A diagnosis would fix a representative report page, filter setting, user task and expected answer before timing. Initial loading and repeated interactions should be recorded separately because cache state can change the result. Within authorized access, Power BI Performance Analyzer can separate query, visual display and other elapsed time; model and source inspection would then test a specific cause rather than assume one. Each result needs the report and model version, data volume, connection mode, capacity, hardware, date and number of repetitions. Median and dispersion are more informative than a single selected run.

*Source: Microsoft, [Use Performance Analyzer to examine report performance](https://learn.microsoft.com/en-us/power-bi/create-reports/performance-analyzer).*

<!-- Note preuve C6 : si les mesures sont réalisées, privilégier un tableau compact du protocole et des résultats. Une capture ciblée de Performance Analyzer n'ira en annexe que si elle complète la preuve ; ne pas ajouter une capture générale du rapport. -->

No such measurements are currently indexed. The comparison in section 7.3 therefore treats the existing report as an operational reference and does not claim that the local Streamlit prototype improves its response time. Refresh delay and interactive latency would also need separate measurements because they affect different user tasks.
