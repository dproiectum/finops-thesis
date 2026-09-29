# 3.5 — Analytical Preparation

Each business question determines a measure, population, period and allocation scope. For example, monthly cost by application requires a stated cost basis and attribution rule. Indicator specifications record source fields, formula, unit, grain, filters, exclusions and missing-value treatment, using the financial definitions in chapter 2.

These specifications guide the dimensional model and subject-oriented datamarts. Joins and aggregations must preserve the intended charge population without multiplying costs. Each datamart is compared with a reference calculation on the same scope; displayed indicators are then checked against the datamart read by the dashboard. Section 4.5 defines the concrete model and maps its products to business questions, while chapter 6 examines their analytical interpretation.
