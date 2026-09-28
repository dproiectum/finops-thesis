# 5.1 — Independent FOCUS Data Generator

The generator is a separate project that produces one synthetic FOCUS-based source history for the local POC and the cloud platform. This is a logical account of the final system, not a claim that the generator was extracted before the POC was built. Its configuration identifies the anonymized reference data, output and ledger locations, date range, row and cost targets, monthly weights, and identifier salt. Publication to GCS is a separate step; the generator does not write DuckDB or Unity Catalog tables.

## 5.1.1 Daily data generation

The command-line interface generates the configured history, an explicit date range, the next number of days, or the remainder of the next pending month. For each date, a date-specific deterministic seed selects reference rows. The module assigns charge and billing periods, transforms supported identifiers consistently, scales cost fields, and casts the output to the source Arrow schema. It writes compressed Parquet under `datasets/focus/daily/YYYY/MM/YYYY-MM-DD.parquet`.

The file is written provisionally, hashed with SHA-256, and moved to its published local path. A ledger records its path, row count, target and actual `BilledCost`, and hash. A fingerprint of relevant settings and source hashes detects changes to the generation context. Existing output requires explicit resume behavior; resume verifies recorded files instead of silently regenerating them. A local file lock prevents concurrent generator processes from publishing to the same ledger. These controls support local reproducibility, but do not make a subsequent GCS copy a distributed transaction.

## 5.1.2 Monthly billing simulation

A monthly bill can be built only after every Daily file for the target month has been found and checked against its ledger entry, schema, currency, provider, date boundaries, and billed-cost total. In the `no_change` scenario, the detailed Daily rows are concatenated without aggregation. Four other scenarios introduce late usage, cost correction, a combination of both, or an unexplained difference. For each intervention, the manifest records the source and resulting billing row, input hashes, scenario, expected cost difference, and output hash. This manifest serves as an experimental oracle for reconciliation; the cloud pipeline does not read it to decide whether a difference is valid.

Monthly output follows `datasets/focus/monthly/billing-YYYY-MM.parquet`, matching the relative path used in GCS. Overwrite is explicit and copies the previous Parquet and manifest to a dated local archive. The replacement file is read back against the intended Arrow table before publication. This local version archive is distinct from the cloud platform's currently disabled automatic RAW archival. The generator neither closes a cloud billing month nor deletes its source files.

## 5.1.3 Validation and publication of source files

On 27 September 2026, local validation covered 608 Daily files, 3,664,261 rows and EUR 20,357,040 for January 2025–August 2026. It also covered eighteen `no_change` monthly bills through June 2026, with 3,279,613 rows and EUR 18,220,080. July and August 2026 therefore belong to the validated Daily history, not to this validated monthly-bill set. These figures establish internal consistency of synthetic files, not realistic company spending or successful cloud ingestion. Sections 3.1–3.2 describe the validation method.

The same generated Parquet files may feed the local POC and, after a controlled copy, the GCS RAW namespace. The local and cloud processing implementations are described separately in sections 5.2 and 5.3. Section 3.1 discusses the source assumptions and representativeness limit; section 7.4 identifies the cloud run evidence still required.
