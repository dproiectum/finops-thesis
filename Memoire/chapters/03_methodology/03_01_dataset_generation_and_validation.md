# 3.1 — Dataset Generation and Validation

The study follows a design-and-evaluation approach. The research questions guide the requirements, architecture and implementation developed in the following chapters. This chapter specifies how that implementation is tested: a reproducible synthetic dataset, controlled processing scenarios and explicit expected outcomes provide the basis for evaluation. These data support an engineering assessment of the platform; they do not measure the host organization's actual cloud expenditure. Section 3.2 defines the monthly reconciliation scenarios, and section 3.3 specifies the evidence required to assess the results.

## 3.1.1 Source material and research constraint

The project uses two Azure FOCUS cost-and-usage files as reference input for generating fictional consumption data. The reference data were anonymized before use. Microsoft's published [FOCUS cost and usage details file schema](https://learn.microsoft.com/en-us/azure/cost-management-billing/dataset-schema/cost-usage-details-focus) documents the fields and their meanings; this schema reference is distinct from the provenance of the project's input files. The generated history is not presented as the host organization's billing history.

The independent `FinOps Data Generator` reads the reference Parquet schema and source rows, removes records without usable charge dates or billed cost, and retains only records whose billing currency is EUR and provider is Microsoft. It samples those admissible rows, replaces selected identifiers, assigns new dates and scales cost values to configured targets. This method retains source field structure and combinations of values, but does not demonstrate that the generated history represents real consumption patterns.

The generator is independent of both analytical engines used later in the project. It writes one set of source Parquet files under `datasets/focus`; the local DuckDB POC and the Databricks/GCP platform are consumers of this dataset. This separation matters experimentally: comparisons of a common period must use the same published input files rather than independently regenerated histories. The reference files remain local and are not published with the project.

## 3.1.2 Construction of the daily history

The maintained method, `daily-template-v2`, samples reference rows for each calendar day. It consistently replaces a defined set of account, resource, SKU and invoice-related identifiers with salted SHA-256-derived synthetic identifiers. Charge dates are assigned within the generated day, while billing dates span its calendar month. The output is cast back to the source Arrow schema and written as a compressed Parquet file at `daily/YYYY/MM/YYYY-MM-DD.parquet`.

Generation is deterministic at day level. A seed derived from the method, configuration seed and date makes a given day's sampled records independent of the size or boundaries of the generation batch. The configuration also defines an annual billed-cost target of EUR 12 million for 2025, monthly weights representing assumed seasonality, and a growth multiplier of 1.06 for 2026. For each day, the monthly target is divided into cents across calendar days; the generated cost columns are scaled accordingly, with a final adjustment to `BilledCost` so that the daily target is reached. These weights and the 2026 multiplier are modeling assumptions, not estimates learned from a sufficiently long real series. Row counts are generated from the configured target volume and each day's monetary target, so they too are synthetic design choices.

The generator records a configuration-and-source fingerprint and a daily ledger containing the file path, row count, target and observed billed cost, and SHA-256 hash. It refuses to silently replace a published file. On resumption, it checks existing ledger entries and file hashes, which supports reproducibility and detects missing or modified output.

## 3.1.3 Validation and observed volume

The daily validator checks contiguous dates from the configured start, absence of unexpected Parquet files, source-schema equality, charge dates within the daily boundary, correct monthly billing boundaries, non-null billed cost, row counts and agreement with both the daily target and ledger. Running that validator on 27 September 2026 succeeded for 608 daily files, from 1 January 2025 to 31 August 2026, containing 3,664,261 rows and EUR 20,357,040 of synthetic `BilledCost`. The generated validation report groups results by month. Hashes are also checked when the generator reloads its ledger. This result concerns local files and does not establish cloud ingestion.

The monthly billing corpus covers a narrower interval: 18 months from January 2025 through June 2026, with 3,279,613 rows and EUR 18,220,080 (section 3.2). July and August 2026 account for the additional 62 Daily files, 384,648 rows and EUR 2,136,960. They have not been included in the validated monthly billing corpus. This distinction also defines the input boundaries for the historical Databricks backfill and the later Daily workflow.

<!-- Note illustration C3 : placer ici une frise de couverture temporelle comparant Daily (janvier 2025–août 2026) et factures mensuelles validées (janvier 2025–juin 2026). Ce sont des périodes de données synthétiques, pas une tendance de dépense réelle. Source : audit/05_local_validation_2026_09_27.md. -->

## 3.1.4 Validity limits

The checks establish deterministic generation, schema preservation, temporal coverage and internal monetary reconciliation. They do not establish that source sampling reproduces actual resource lifecycles, day-to-day variability, real invoice semantics or business decisions. In particular, imposed monthly weights cannot be used as evidence of observed seasonality, and a forecast evaluated on this generated history would measure performance under the generator's assumptions. The thesis therefore uses these data to test engineering behavior and illustrate FinOps analyses, while treating conclusions about real organizational savings or demand as outside the dataset's evidential scope.
