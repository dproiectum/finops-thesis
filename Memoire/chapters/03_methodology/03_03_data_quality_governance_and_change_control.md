# 3.3 — Data Quality, Governance and Change Control

Quality controls cover schema, required values, periods, monetary reconciliation and repeatability. Technical validity is assessed separately from business attribution: a reconciled total can still lack an application or owner. Missing allocation attributes remain visible, and negative amounts are not rejected solely by sign because they may represent credits. EUR and Microsoft delimit this corpus, not all FOCUS inputs.

The versioned Data Contract declares fields, types, nullability and selected rules. Failed validation must block invalid canonical publication and identify the input and rule for diagnosis. Passing this project contract is not certification of complete FOCUS conformance. Governance also requires traceable revisions, corrections and access decisions. The proposed responsibilities assign business definitions to FinOps and technical controls to data engineering; organizational confirmation remains necessary.

Specification and contract versions are explicit because FOCUS version numbers do not guarantee compatibility, as stated in the official repository (FinOps Open Cost and Usage Specification, n.d.). The project's compatibility policy permits additional fields, but rejects missing required fields and incompatible type changes. Intentional evolution requires review of field meanings, a versioned adaptation and regression tests of dependent calculations. Schema detection does not automatically revise the contract or detect every semantic change.

Access tests cover files, queries, dashboards and exports. Public synthetic demonstrations and authorized stakeholder services are assessed separately; chapter 7 reports the available security evidence.

Source for this section (accessed 30 September 2026):

- FinOps Open Cost and Usage Specification, *FOCUS_Spec repository*, “Versioning the Specification”: https://github.com/FinOps-Open-Cost-and-Usage-Spec/FOCUS_Spec#versioning-the-specification
