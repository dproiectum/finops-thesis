# 4.5 — Data Architecture and Dimensional Modeling

## 4.5.1 Canonical record and analytical grain

The data architecture separates three purposes. RAW retains the received Parquet evidence; Bronze adds technical lineage without changing source business values; and Silver contains the FOCUS representation after the versioned contract has accepted it. Gold reorganizes that canonical record for recurring analysis, while datamarts answer defined questions at coarser grains. Neither Gold nor a datamart becomes an independent source of cost truth. The same logical model is instantiated in separate DEV and PROD catalogs; the frozen local POC uses a related analytical design but a different engine.

The Gold fact, `fact_finops_cost_usage`, represents one FOCUS cost or usage charge line. It retains `billing_month` so that an authoritative monthly bill can replace the provisional Daily-fed month without adding both sources together. Its technical key is deterministic, using source lineage and logical row position; dimensional foreign keys connect a charge to its time, scope, resource, service, SKU, location, pricing and charge type. This grain permits reconciliation back to Silver and prevents a monthly summary from obscuring individual adjustments. It does not, by itself, establish the financial meaning of a difference between cost columns.

## 4.5.2 Gold table inventory and relationships

The cloud SQL defines the following Gold tables. This inventory gives each name and responsibility. A full column-by-column DDL listing is not required to interpret the model in this chapter.

| Table | Analytical responsibility |
|---|---|
| `fact_finops_cost_usage` | Charge-line measures, quantities, billing month and dimensional keys |
| `dim_date` | Reusable calendar attributes for the fact's dates |
| `dim_billing_scope` | Billing accounts, subaccounts, customers and cost-center attributes |
| `dim_resource` | Resource, resource group and application/owner attributes |
| `dim_service` | Service, provider, publisher and reseller attributes |
| `dim_sku` | SKU, meter, offer and term attributes |
| `dim_location` | Region and availability-zone attributes |
| `dim_pricing` | Pricing category, unit and currency attributes |
| `dim_commitment_discount` | Commitment identifiers and categories |
| `dim_charge_type` | Charge category, subcategory and frequency |
| `dim_tag` | Normalized tag key/value pairs |
| `bridge_resource_tag` | Many-to-many association between resources and tags |

The model has ten dimensions. The fact links directly to nine of them; tags are reached through `dim_resource`, `bridge_resource_tag` and `dim_tag`. The model's billing-scope and resource dimensions currently use Type 1 updates. Their validity columns do not prove that every past attribute value is preserved as SCD2 history. The source dataset lacks a native charge identifier and availability zone, so the implementation generates a deterministic charge identifier and uses `Unknown` for the unavailable zone. These are model limitations, not general properties of FOCUS.

<!-- Note illustration F4 : insérer ici un schéma du fait, des dix dimensions et du pont ressource/tag ; vérifier les noms et clés contre le SQL cloud exécuté. -->

## 4.5.3 Datamarts and business questions

The datamarts are analytical products derived from the canonical representation. The question column states their intended use, not a measured benefit or a claim that every cloud table has been independently validated. The paragraph after the table distinguishes products derived from Gold from those reading central Silver directly.

| Datamart | Business or control question supported |
|---|---|
| `dm_monthly_billing` | What is the billed cost for each billing month? |
| `dm_daily_billing` | How does billed cost vary by charge-start date? |
| `dm_cost_by_scope_service_month` | Which cost centers, customers and services account for monthly billed cost? |
| `dm_top_services` | Which service categories and names have the highest billed cost in the loaded data? |
| `dm_top_resources` | Which resources have the highest billed cost in the loaded data? |
| `dm_cost_by_charge_type` | How is monthly billed cost distributed across charge categories and frequencies? |
| `dm_sku_cost` | Which SKUs and meters account for the highest billed cost? |
| `dm_savings_monthly` | How do monthly List, Contracted and Effective Cost totals differ? |
| `dm_executive_summary_monthly` | What are the monthly cost totals, charge-line count, resource count and service count? |
| `dm_top_resources_monthly` | Which resources drive billed cost within a selected billing month? |
| `dm_data_quality_monthly` | How many critical nulls and ingestion batches appear in each Silver month? |
| `dm_cost_by_resource_group_month` | What are monthly billed cost and resource count by resource group? |
| `dm_cost_by_subscription_month` | What are monthly billed cost and resource count by subaccount or subscription? |
| `dm_cost_by_application_owner_month` | How are monthly billed cost and resource count attributed to applications and owners? |

`dm_savings_monthly`, `dm_executive_summary_monthly` and `dm_data_quality_monthly` read the central Silver representation because they use FOCUS fields or technical metadata not all held in the Gold fact. The remaining datamarts read Gold. The differences named as “savings” in the SQL are arithmetic cost-column comparisons; they do not establish realized savings without eligibility rules, charge-category analysis and business validation. Section 5.3.3 describes how the cloud model and datamarts are built, while chapters 6 and 7 examine their analytical meaning and validation evidence.
