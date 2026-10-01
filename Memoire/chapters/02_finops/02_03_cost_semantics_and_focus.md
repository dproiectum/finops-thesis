# 2.3 — Cost Semantics and FOCUS

## A common language for billing data

Cloud billing exports differ in their column names and in the meanings attached to usage, discounts and charges. The FinOps Open Cost and Usage Specification (FOCUS) defines a common structure and semantic requirements for technology cost-and-usage datasets. It gives data generators a specification for publishing billing data and data consumers a reference for interpreting it. FOCUS is neither a billing service nor a dashboard; adopting its vocabulary does not remove the need to check the contents of each export (FOCUS Project, n.d.-d).

FOCUS is an open specification initiative of the Linux Foundation, organized as a Joint Development Foundation specification project. Its steering committee approves the specification, while contributors and maintainers develop it through an open process. The FinOps Foundation provides support, but FOCUS is not a format owned by a single cloud provider (FOCUS Project, n.d.-a).

## Provider support and specification versions

The FOCUS Project's provider index lists FOCUS datasets from AWS, Microsoft Azure and Google Cloud, as well as other cloud and technology vendors. On 30 September 2026, the index listed version 1.2 for those three providers. The specification itself had reached version 1.4 by that date. Provider support therefore needs to be checked by export and version; the existence of a FOCUS export does not establish that all providers publish the same release or that a particular dataset satisfies every requirement (FOCUS Project, n.d.-c; FOCUS Project, n.d.-d).

## Scope of FOCUS in this study

The professional setting at Technip Energies motivates the need for consistent showback definitions, but the available evidence does not establish whether the existing company reporting flow uses a FOCUS export or which version it might use. This study does not make that claim. Its experimental input is different: two anonymized Azure FOCUS files provide reference data for a generator that produces fictional cost-and-usage records. The project's configuration identifies the target specification as FOCUS 1.0; its own data contract is versioned 1.0.0. These numbers refer to different artifacts. Microsoft documents the Azure FOCUS schema, but that documentation alone does not establish the provenance of the two reference files (Microsoft, n.d.-a).

The generated records are processed on a Databricks platform hosted on Google Cloud. That processing environment does not change the cloud provider represented by the reference billing data. The contract's Microsoft-provider and EUR-currency checks describe this experimental corpus, not universal FOCUS requirements. They also do not constitute an independent certification of full FOCUS conformance. Chapter 3 explains how the versioned contract controls data quality and future schema changes; section 2.4 examines the cost measures whose meanings the analytical model must preserve.

Sources for this section (accessed 30 September 2026):

- FOCUS Project, *About the FOCUS Project*: https://focus.finops.org/about-focus/
- FOCUS Project, *Get Started with FOCUS Datasets*: https://focus.finops.org/docs/implementation/get-started/get-started-with-focus-datasets/
- FOCUS Project, *What is FOCUS?*: https://focus.finops.org/what-is-focus/
- Microsoft, *FOCUS cost and usage details file schema*: https://learn.microsoft.com/en-us/azure/cost-management-billing/dataset-schema/cost-usage-details-focus
