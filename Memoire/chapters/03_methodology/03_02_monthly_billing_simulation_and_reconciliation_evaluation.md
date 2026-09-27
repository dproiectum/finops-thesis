# 3.2 — Monthly Billing Simulation and Reconciliation Evaluation

## 3.2.1 Why a second source representation is needed

A monthly close must distinguish provisional daily usage from a final billing statement. No real invoice-detail feed exists for the generated history, so the project constructs a second, detailed Parquet representation from each complete month of Daily files. Its purpose is to provide a controlled test fixture for close and reconciliation. It is not an independently observed financial source and cannot establish the correctness of a real Azure invoice.

Before creating a monthly file, the simulator requires every calendar day in the month and a matching daily-ledger entry. It compares the recorded and actual SHA-256 hashes, checks equality of Arrow schemas including metadata, validates row counts and confirms charge and billing periods. It also verifies EUR currency, Microsoft provider and daily `BilledCost` against the ledger. These preconditions prevent a partial month or a modified daily file from being accepted as a billing reference.

## 3.2.2 Controlled difference scenarios

The `no_change` scenario concatenates all daily rows without an adjustment. Four other scenarios create known differences: `late_usage` adds a synthetic EUR 1,500 Usage line; `cost_correction` reduces the billed amount of an eligible Usage line by EUR 200; `combined` applies both; and `unexplained_difference` changes an eligible line by EUR 50 without a supporting explanation. The amounts are configurable experimental fixtures, not company billing events. A deterministic month-level seed selects eligible rows, allowing repeatable tests.

The monthly manifest records each injected event, its original Daily file and row where applicable, the billing row, the before and after amounts, and the expected difference. This record is an evaluation oracle: after running a reconciliation algorithm, one can compare detected differences, missed changes, false positives and blocking decisions against the known intervention. The processing pipeline must not consult the oracle when deciding whether to close a month. Otherwise the experiment would test access to the answer rather than reconciliation behavior.

## 3.2.3 Publication and authority

The maintained generator writes one detailed file per month under `datasets/focus/monthly/year=YYYY/month=MM/billing-YYYY-MM.parquet`, with a manifest stored separately. Replacement requires an explicit overwrite flag; the previous file and manifest are copied to a dated local archive before replacement. Writing is performed through a temporary Parquet file, read back for equality with the intended Arrow table, then moved into place. This is local file protection, not a distributed financial approval process.

For cloud processing, a published copy must occupy the platform's RAW path `focus/monthly/billing-YYYY-MM.parquet`. File identity between generator output and GCS input should be established by a recorded hash or equivalent transfer evidence. While a month is open, its Daily files are provisional. Once the detailed monthly billing is accepted, the close replaces that month in Silver and Gold; adding Daily and billing rows together would double-count the same activity.

<!-- Note illustration F1 : insérer ici le schéma Daily → mois provisoire → facture mensuelle faisant autorité → remplacement et contrôle BEFORE/SOURCE/AFTER. Montrer le RAW partagé et les passages DEV/PROD sans suggérer que le cycle complet a déjà été validé dans le cloud. -->

## 3.2.4 Local results and limitations

On 27 September 2026, the monthly validator succeeded for 18 `no_change` bills, January 2025 through June 2026, covering 3,279,613 detailed rows and EUR 18,220,080. Each bill matched its Daily month in row count and `BilledCost`, and each file matched its manifest hash. January 2025 contained 164,145 rows and EUR 912,000. This establishes local row and amount preservation for the unchanged scenario; it does not establish cloud publication or handling of corrected billing.

The change scenarios are useful for testing exception paths, but their simplified amendments do not capture all invoice corrections, credit treatments or commitment rules. The close should accept or block differences according to explicit rules and report why. Whether those rules are financially appropriate requires FinOps review. The generator's injected labels remain unavailable to the production reconciliation logic.
