# Initial Bibliography

This initial bibliography supports the first academic framing of the PFE. It combines official FinOps/FOCUS sources and scientific or academic references. The final thesis bibliography must be refined and formatted consistently.

## Official and Professional References

1. FinOps Foundation. (2026). *FinOps Framework*. https://www.finops.org/framework/
   - Use: Defines FinOps as an operating model and cultural practice; supports the Inform, Optimize, Operate positioning.

2. FinOps Foundation. (2026). *FinOps Open Cost and Usage Specification*. https://www.finops.org/topic/focus/
   - Use: Explains FOCUS as a common billing data foundation for reporting, allocation and benchmarking.

3. FOCUS Project. (2026). *FOCUS: FinOps Open Cost and Usage Specification*. https://focus.finops.org/
   - Use: Official source for the FOCUS specification, data model and provider support.

4. FinOps Foundation. (2024). *Adopting FOCUS, the FinOps Open Cost and Usage Specification*. https://www.finops.org/wg/adopting-focus-the-finops-open-cost-and-usage-specification/
   - Use: Supports the implementation approach: decide, design, build, test and launch FOCUS adoption.

5. FinOps Open Cost and Usage Specification. (2026). *FOCUS_Spec GitHub repository*. https://github.com/FinOps-Open-Cost-and-Usage-Spec/FOCUS_Spec
   - Use: Technical reference for FOCUS as an open specification and for schema evolution discussion.

6. FOCUS Project. (2024). *FOCUS 1.0 — Billed Cost*. https://focus.finops.org/docs/specification/v1-0/columns/billed-cost/
   - Use: Defines the invoiced cost perspective used for reconciliation and cash-oriented reporting.

7. FOCUS Project. (2024). *FOCUS 1.0 — Contracted Cost*. https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/contracted-cost/
   - Use: Defines the negotiated-price cost perspective and its aggregation precautions.

8. FOCUS Project. (2024). *FOCUS 1.0 — List Cost*. https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/list-cost/
   - Use: Defines the public-price reference used for rate-effect comparisons.

## Scientific and Academic References

9. Qu, Z., Dawande, M., & Janakiraman, G. (2023). Technical Note - Cloud Cost Optimization: Model, Bounds, and Asymptotics. *Operations Research, 72*(1), 132-150. https://doi.org/10.1287/opre.2022.0362
   - Use: Academic support for cloud cost optimization as a formal decision problem.

10. Smendowski, M., & Nawrocki, P. (2024). Optimizing multi-time series forecasting for enhanced cloud resource utilization based on machine learning. *Knowledge-Based Systems, 304*, 112489. https://doi.org/10.1016/j.knosys.2024.112489
   - Use: Supports the Operate phase: forecasting, anomaly detection and resource reservation planning.

11. Nawrocki, P., & Sus, W. (2022). Anomaly detection in the context of long-term cloud resource usage planning. *Knowledge and Information Systems, 64*, 2689-2711. https://doi.org/10.1007/s10115-022-01721-5
   - Use: Supports anomaly detection and long-term resource planning in cloud environments.

12. Osypanka, P., & Nawrocki, P. (2022). Resource usage cost optimization in cloud computing using machine learning. *IEEE Transactions on Cloud Computing, 10*(3), 2079-2089. https://doi.org/10.1109/TCC.2020.3015769
   - Use: Supports cloud resource optimization using machine learning, anomaly detection and closed-loop optimization.

13. Sus, W., & Nawrocki, P. (2024). Signature-based Adaptive Cloud Resource Usage Prediction Using Machine Learning and Anomaly Detection. *Journal of Grid Computing, 22*, article 46. https://doi.org/10.1007/s10723-024-09764-4
   - Use: Supports adaptive prediction and anomaly-aware cloud resource planning.

14. Manurung, H., & Aji, R. F. (2026). Evaluating the Implementation of the FinOps Framework for Cloud Infrastructure Cost Management: A Case Study of Technology Companies in Indonesia. *Scientific Journal of Informatics, 12*(4), 709–720. https://doi.org/10.15294/sji.v12i4.36226
   - Use: Supports FinOps adoption and maturity evaluation in real organizations.

15. Cho, C.-H. (2026). FinOps-Aware Budget-Constrained Optimization for Cloud Resource Management. *Applied Sciences, 16*(7), 3302. https://doi.org/10.3390/app16073302
   - Use: Supports budget-constrained optimization as part of FinOps governance.

## Additional Databricks Platform References

16. Databricks. (n.d.). *Billable usage system table reference*. https://docs.databricks.com/gcp/en/admin/system-tables/billing (accessed 27 September 2026).
   - Use: DBU usage records, billing metadata, data freshness and the attribution limits of All-Purpose compute in sections 8.3–8.4.

17. Databricks. (n.d.). *Monitor job costs with system tables*. https://docs.databricks.com/gcp/en/admin/system-tables/jobs-cost (accessed 27 September 2026).
   - Use: Scope of standard Job-cost monitoring and the distinction between Jobs Compute and All-Purpose workloads.

18. Databricks. (n.d.). *Choose compute for your workloads*. https://docs.databricks.com/gcp/en/compute/choose-compute (accessed 27 September 2026).
   - Use: Compute-mode options to compare in section 8.4; vendor guidance is not treated as a project result.

19. Databricks. (n.d.). *Cost optimization best practices*. https://docs.databricks.com/gcp/en/lakehouse-architecture/cost-optimization/best-practices (accessed 27 September 2026).
   - Use: Candidate levers for sizing, lifecycle and workload efficiency, subject to measured validation.

20. FOCUS Project. (2024). *FOCUS 1.0 — Effective Cost*. https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/effective-cost/ (accessed 27 September 2026).
   - Use: Distinguishes amortized economic cost from billed cost in section 2.3.

21. FinOps Foundation. (n.d.). *FinOps Phases*. https://www.finops.org/framework/phases/ (accessed 27 September 2026).
   - Use: The recurring Inform, Optimize and Operate framing in section 2.2.

22. Apache Parquet. (n.d.). *Overview*. https://parquet.apache.org/docs/overview/ (accessed 27 September 2026).
   - Use: File-format properties discussed in section 4.3.

23. Databricks. (n.d.). *What is Delta Lake in Databricks?* https://docs.databricks.com/gcp/en/delta/ (accessed 27 September 2026).
   - Use: Relationship between Delta and Parquet and the scope of table transactions in section 4.3.

24. Microsoft. (n.d.). *Use Performance Analyzer to examine report performance*. https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-performance-analyzer (accessed 27 September 2026).
   - Use: Measurement categories in the proposed Power BI diagnosis in section 7.2.

## Minimum Requirement Check

Référence professionnelle complémentaire ajoutée le 15 septembre 2026 :

- Dehghani, Z. (2020, 3 décembre). *Data Mesh Principles and Logical Architecture*. MartinFowler.com. [Article](https://martinfowler.com/articles/data-mesh-principles.html). Consulté le 15 septembre 2026.
  - Usage : distinguer autonomie de consommation, autonomie de production et principes du Data Mesh dans la section 4.2. Source professionnelle fondatrice, non comptée comme article scientifique.

- Total references listed: 25.
- Scientific/academic references: 7.
- Official/professional references: 18.

The school requires 10 references including at least 5 scientific articles. This initial bibliography satisfies the quantity requirement, but the final thesis should still refine source quality, in-text citation style, and relevance by chapter.
