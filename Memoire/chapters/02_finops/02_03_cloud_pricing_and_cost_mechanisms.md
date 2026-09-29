# 2.3 — Cloud Pricing and Cost Mechanisms

## From consumption to a financial charge

A cloud charge results from the interaction of a consumed service, a pricing quantity and unit, a public rate, contractual conditions, commitment benefits, credits, corrections, taxes and billing timing. Consequently, the word “cost” is ambiguous unless the selected cost perspective and accounting basis are stated.

At line level, the simplified pricing path used for interpretation is:

```text
Consumed resource or service
        ↓ conversion to pricing quantity
Public list price
        ↓ negotiated contractual reductions
Contracted price
        ↓ allocation of commitment benefits and amortization
Effective cost
        ↓ invoice timing and covering-charge treatment
Billed cost
```

This diagram is explanatory. The equality and ordering of these values cannot be assumed for every charge category, credit, correction, tax or purchase row.

## Four FOCUS cost perspectives

| Measure | Business interpretation | Main use in the project |
|---|---|---|
| `ListCost` | Cost calculated from the provider's public list unit price and pricing quantity | Reference for rate-comparison analysis |
| `ContractedCost` | Cost calculated from the negotiated contracted unit price and pricing quantity | Isolate the effect of negotiated pricing where comparable |
| `EffectiveCost` | Economically allocated cost after relevant discounts and amortized commitment purchases | Accrual-oriented service and resource analysis |
| `BilledCost` | Charge serving as the basis for invoicing in the billing period | Invoice reconciliation, cash-oriented reporting and allocation |

These definitions follow the FOCUS 1.0 specifications for List Cost, Contracted Cost, Effective Cost and Billed Cost. `BilledCost` and `EffectiveCost` answer different questions. A commitment purchase may be billed at one time while its economic cost is allocated to covered usage over time. Their difference must therefore not automatically be labelled as a saving.

*Source: FOCUS Project, FOCUS 1.0: [List Cost](https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/list-cost/), [Contracted Cost](https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/contracted-cost/), [Effective Cost](https://focus.finops.org/docs/specification/v1-0/columns/cost-and-usage/effective-cost/) and [Billed Cost](https://focus.finops.org/docs/specification/v1-0/columns/billed-cost/).*

## Pricing quantity and unit price

Where the required fields are available and comparable:

```text
ListCost       = ListUnitPrice       × PricingQuantity
ContractedCost = ContractedUnitPrice × PricingQuantity
```

Pricing quantity can differ from consumed quantity because providers may apply block, tier or normalized pricing. Corrections are also capable of breaking a naive equality at individual-row level and must be treated according to their charge class.

## Negotiated and commitment-related effects

The following decompositions are analytical candidates, not universally valid accounting identities:

```text
Negotiated rate effect      = ListCost − ContractedCost
Additional effective effect = ContractedCost − EffectiveCost
Total effective rate effect = ListCost − EffectiveCost
```

They may be calculated only on a consistent currency, period, scope and charge population. Purchase and covered-usage records must be filtered according to a documented billed or accrual basis to avoid double counting.

## Commitment discounts

Reservations and Savings Plans exchange an obligation to consume or spend over a defined period for reduced rates. Commitment purchases may be upfront, recurring or mixed. Their cost is amortized across charge periods and allocated to eligible usage. Unused commitment is a cost of underutilization, not an additional saving, and follows a use-it-or-lose-it logic.

The prototype contains commitment-related dimensions and cost measures, but it must not claim complete commitment utilization analysis until identifiers, statuses, purchase rows, covered usage and unused portions have been validated in the dataset.

## Realized versus potential savings

- A realized rate effect can be derived retrospectively from comparable populated cost measures, with explicit exclusions.
- A potential saving estimates a future action and normally requires additional evidence such as utilization metrics, resource inventory, provider recommendations, price references or commitment coverage.

The current dashboard's `ListCost − EffectiveCost` indicator should therefore be described as an effective difference from list cost until its scope and interpretation are fully validated. It must not be presented as a verified business saving without that validation.
