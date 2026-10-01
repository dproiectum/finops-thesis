# 2.4 — From Cloud Charges to Showback

## Interpreting cloud costs

A cloud charge reflects usage, a pricing quantity and unit, contractual terms, commitment benefits, credits and billing timing. The meaning of “cost” therefore depends on the measure and accounting perspective selected. FOCUS 1.0 defines four measures used in this project (FOCUS Project, 2024a, 2024b, 2024c, 2024d):

| Measure | Interpretation | Use in this study |
|---|---|---|
| `ListCost` | Cost at the public list unit price | Reference for rate comparisons |
| `ContractedCost` | Cost at the negotiated contracted unit price | Comparison with list pricing where the rows are comparable |
| `EffectiveCost` | Economically allocated cost, including applicable amortized commitment benefits | Service and resource analysis on an accrual basis |
| `BilledCost` | Amount serving as the basis for invoicing in the billing period | Reconciliation and billed-cost reporting |

For comparable rows with the required fields, `ListCost` and `ContractedCost` can be related to their respective unit prices and `PricingQuantity`. That quantity need not equal the consumed quantity. Credits, corrections, purchases and covering charges also require treatment according to their charge class. In particular, `BilledCost` and `EffectiveCost` answer different questions: a commitment purchase can be billed at one time while its economic cost is distributed over covered usage. Their difference is not automatically a saving.

Comparisons such as `ListCost − ContractedCost` or `ListCost − EffectiveCost` are analytical candidates only for a consistent currency, period, scope and charge population. They describe differences between cost perspectives, not verified business savings. A potential saving from rightsizing or a new commitment requires further evidence, including utilization, inventory, recommendations or coverage. The prototype's `ListCost − EffectiveCost` indicator is therefore an effective difference from list cost until its exclusions and interpretation have been validated. Chapter 6 applies these distinctions to the analytical results.

## Allocating costs to business responsibility

Standardized cost columns show what was charged but do not determine which business entity should be accountable. Allocation links a charge to an application, domain, project or cost center through documented rules. Shared costs need an explicit rule; charges without a reliable owner must remain visible as unallocated. Financial reconciliation alone does not establish allocation coverage (FinOps Foundation, n.d.-b).

Showback presents attributed costs to the people responsible for them. Chargeback additionally posts or recovers those costs through an accounting process; it is a different operating choice, not an automatic next step. This project prepares showback views but does not implement enterprise chargeback (FinOps Foundation, n.d.-f).

An application owner needs the relevant application view, while a domain manager needs a consolidated domain view. The analytical model must preserve the measure and allocation rule behind each figure, including an unallocated category. Access control is a separate requirement for distributing these views safely. Whether the implemented dashboard serves both audiences remains a validation question; the data model alone does not establish it.

Sources for this section (accessed 30 September 2026):

- FOCUS Project, *FOCUS 1.0 — Billed Cost*: https://focus.finops.org/docs/specification/v1-0/columns/billed-cost/
- FOCUS Project, *FOCUS 1.0 — Contracted Cost*: https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/contracted-cost/
- FOCUS Project, *FOCUS 1.0 — Effective Cost*: https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/effective-cost/
- FOCUS Project, *FOCUS 1.0 — List Cost*: https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/list-cost/
- FinOps Foundation, *Allocation*: https://www.finops.org/framework/capabilities/allocation/
- FinOps Foundation, *Invoicing & Chargeback*: https://www.finops.org/framework/capabilities/invoicing-chargeback/
