# 4.2 — General Platform Design (Logical HLD)

## System boundary

The system begins with cost and usage datasets delivered by a billing-data producer and ends with governed information exposed to FinOps, managers and authorized analysts. Provider billing generation, enterprise accounting, resource remediation and production identity administration remain external responsibilities.

## Logical flow

```text
Cost and usage sources
        ↓
Evidence preservation
        ↓
Ingestion and lineage
        ↓
Contract and quality validation
        ↓
Canonical cost and usage data
        ↓
Dimensional and subject-oriented data products
        ↓
Governed dashboards and analytical access
```

Quality, reconciliation, security, metadata and observability apply across the complete flow.

<!-- Note illustration F2 : remplacer le bloc de flux texte ci-dessus par un schéma vectoriel logique. Montrer source, preuve, ingestion, contrat, Silver, Gold/datamarts et accès, avec qualité/audit/sécurité transversaux. Ce schéma décrit les fonctions, sans noms de services physiques. -->

## Logical components

| Component | Responsibility |
|---|---|
| Source interface | Receive periodic cost and usage data with identifiable origin and period |
| Evidence store | Preserve the received representation without hidden business transformation |
| Ingestion service | Register the batch and add technical lineage |
| Contract gate | Reject or quarantine incompatible structure and invalid mandatory values |
| Canonical repository | Provide the authoritative standardized FinOps representation |
| Analytical model | Organize detailed charges by time, scope, resource, service, price and commitment |
| Data-product layer | Publish stable subjects and common measures for consumption |
| Consumption layer | Provide role-appropriate dashboards and analytical access |
| Operational control | Track executions, freshness, failures, reconciliation and recovery |

## Architectural principles

- The immutable evidence layer and the canonical repository have different responsibilities.
- Validation occurs before data becomes authoritative.
- Derived products do not become independent sources of truth.
- Consumers use stable products rather than storage-specific implementation details.
- Access control applies at every exposed interface.
- Claims of reliability require reproducible evidence, not only an architecture diagram.

## Operating model: centralized production and distributed consumption

The proposed operating model gives managers access to their cost scope and authorized analysts access to further analysis. The Data Platform retains shared technical capabilities; FinOps owns business definitions and product validation; domains consume only their authorized scope. These responsibilities describe the target design and require organizational confirmation.

Here, “data factory” denotes a centralized production organization, not the Azure Data Factory service. Centralized production can coexist with autonomous access. The issue under study is dependency on repeated requests for changes.

Data Mesh combines domain ownership, data as a product, self-service infrastructure and federated governance. Its autonomy extends to producing teams, beyond report consumption. Physical data location alone does not define it. [Dehghani, 2020](https://martinfowler.com/articles/data-mesh-principles.html).

The target adopts product-oriented practices—definitions, quality, ownership and stable interfaces—without autonomous production by several domains or full federated governance. It is therefore not described as a complete Data Mesh. Chapter 9 will revisit this choice against the evidence collected.

This section describes what the platform must do without assigning those responsibilities to products. Section 4.3 compares the documented technology options and identifies the tools used in the prototypes. Section 4.4 maps the logical flow to deployed components; section 4.5 explains the data model and the analytical products.
