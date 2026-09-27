# MVP Scope and Acceptance Criteria

## Status

Historical framing proposal. It records the options considered before the local POC and the Databricks/GCP implementation. Its Azure/Databricks Free assumptions and proposed tests must not be read as the current project status. Sections 4.3 and 5.3 of the thesis describe the current choices and implementation.

## Demonstration Scenario

A domain manager consults the total cost and application/project breakdown for a selected period without asking FinOps to prepare an Excel extract. An authorized analyst creates an additional analysis from the same certified datamart. Both users see only their authorized perimeter. FinOps retains consolidated visibility and ownership of cost definitions.

The historical dataset covers 2025-01-01 to 2026-06-30. A manually triggered subsequent batch demonstrates incremental operation. Daily synthetic files are generated locally in manually requested batches. Daily granularity is implemented; scheduled daily freshness remains to be demonstrated by the platform. Each view exposes its latest available data date.

## Users and Responsibilities

| Persona | Prototype access | Responsibility |
|---|---|---|
| Domain manager | Dashboard for authorized domains | Consult total and detailed costs |
| Domain analyst | Read-only certified datamart access within authorized domains | Produce additional analysis |
| FinOps | Consolidated cost data and quality results | Define measures, allocation rules, and product acceptance |
| Platform operator | Pipeline execution and technical logs | Ingestion, reliability, and access configuration |

Use at least two synthetic domains, two manager identities, and one analyst identity. Organizational ownership and identity mappings are required supporting fixtures, even if the Parquet files do not contain them. Unmapped users have no access; unmapped costs remain visible to FinOps as unallocated costs.

## Scope and Evidence

| ID | Research angle | Required capability | Acceptance evidence |
|---|---|---|---|
| M01 | Reliable platform | Historical ingestion and subsequent batch | Batch manifest with source identity, period, row counts, and run status; subsequent batch preserves historical totals |
| M02 | Reliable platform | Versioned FOCUS Data Contract | Valid fixture accepted; missing required field, incompatible type, and broken business rule rejected or quarantined according to documented policy |
| M03 | Reliable platform | Bronze, canonical Silver, and dimensional Gold | Traceable transformations; published grain, keys, dimensions, and measures; duplicate dimension keys and orphan fact references detected |
| M04 | Reliable platform | Reconciliation and repeatable execution | Reprocessing the same batch changes neither row counts nor monetary totals; totals reconcile by period and currency at each layer, with exclusions and rounding explicitly accounted for |
| M05 | Governed self-service | Certified datamart | Versioned schema, owner role, measure definitions, freshness, lineage, access policy, and passing quality evidence recorded before publication |
| M06 | Governed self-service | Dashboard and analyst isolation | Separate identities tested on dashboard, export, and direct datamart access; zero unauthorized rows in the test suite; default-deny and changed membership tested |
| M07 | Governed self-service | Manager and analyst autonomy | Manager answers total-cost and application/project-breakdown tasks; analyst builds one new aggregation from the certified mart without FinOps preparing an extract |
| M08 | Decision support: Inform | Showback and period comparison | Dashboard results match reference SQL for selected periods, domains, applications, and projects; unallocated costs explicitly shown |
| M09 | Decision support: Optimize | Cost comparison and supported realized savings | Formula, reference cost, currency, charge scope, and exclusions documented; fixture calculations verified; missing or incomparable values marked unavailable; no unsupported potential-savings claims |
| M10 | Decision support: Operate | Pipeline status, freshness, and recovery | Successful and failed runs logged; invalid input cannot silently replace certified output; corrected batch can be retried successfully |

Certification here means the project's documented acceptance process. It does not imply enterprise approval or a vendor certification badge. Dashboard RLS alone does not secure direct SQL access; the selected serving layer must enforce the analyst's perimeter too.

## Optional Extensions

- Forecasting baseline and anomaly detection, after required acceptance scenarios pass.
- Budget-versus-actual analysis when a documented budget fixture is available.
- Automated scheduling after the manual end-to-end execution is repeatable.
- Additional optimization sources such as utilization metrics or recommendations.

Full Data Mesh, multi-cloud implementation, production deployment at Technip Energies, and automated infrastructure remediation are outside this MVP.

## Evaluation Protocol for the Thesis

1. Define fixed reference tasks: period total, application/project breakdown, previous-period comparison, and one analyst aggregation.
2. Document the current email/export/pivot process from the student's observations. Collect actual timings or request volumes only when available and authorized; otherwise mark them unknown.
3. Run the prototype tasks on a fixed dataset and record completion, manual steps, response times, access identity, and correctness against reference queries.
4. Record environment, data volume, software versions, quotas, and cold/warm execution conditions when comparing performance. Report measured timings before proposing an SLA.
5. Separate real organizational observations, controlled scenario measurements, and hypothetical benefits. Synthetic-data tests do not demonstrate actual savings or a measured reduction in company workload.

Suggested evidence package: batch manifests, contract/quality results, reconciliation tables, access-test matrix, screenshots, timed task records, and limitations. Every evidence item should reference an M01-M10 requirement.

## Technology Decision Gate

Compare candidate stacks against M01-M10, especially durable storage, direct analyst access isolation, BI connectivity, reproducibility, and continued use beyond trial expiry. Existing resources are approximately EUR 30 Azure credit and Databricks Free Edition with a 2XS SQL warehouse; subscription and license details remain to be verified.

Databricks Free plus BI is a candidate, not a validated integration. Azure SQL is justified only if it serves a documented access or publication requirement. The feasibility test must establish connectivity and security before stack approval. Do not assume an enterprise Azure deployment is equivalent to Databricks Free Edition.

## Next Discussion

Implement independent daily-to-monthly consolidation and distinguish daily data granularity from scheduled enterprise freshness. Establish whether an authorized domain analyst represents an observed user need or a research scenario. Then resolve BI access and run the bounded stack feasibility test once implementation is authorized.

## Related Documents

- [Research formulations](02_research_questions.md)
- [Methodology](03_methodology_and_empirical_study.md)

The current technology rationale is summarized in thesis section 4.3. This historical planning note is not an annex or a dependency of the final PDF.

Raw layout: `FinOps Data Platform/data/raw/YYYY/MM/YYYY-MM-DD.parquet`. Initial history contains 546 daily files over 18 months. Future daily generation starts on July 1, 2026; the old monthly fixtures have been deleted. Anonymized reference files are excluded from pipeline discovery.
