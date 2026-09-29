# Registre des preuves

## Règle

Une affirmation de résultat destinée au mémoire doit pointer vers une preuve conservée ou vers une procédure reproductible. Le registre ne transforme pas automatiquement un artefact en preuve valide : il précise ce que cet artefact démontre et ce qu'il ne démontre pas.

| ID | Résultat ou affirmation | Type de preuve | Emplacement | Statut | Limite principale |
|---|---|---|---|---|---|
| EVD-001 | Le générateur produit un historique quotidien structuré | Données, manifeste et tests | `FinOps Data Generator/` | `VALIDATED-LOCAL` | Réalisme statistique complet non démontré |
| EVD-002 | La facturation de janvier 2025 conserve 164145 lignes, 91 colonnes, 31 jours et un total de 912000 EUR dans le scénario sans changement | Rapport de validation locale mentionné dans les notes | Répertoire de métadonnées local exclu de Git | `VALIDATED-LOCAL` à vérifier | Ne prouve pas l'exécution Databricks ni l'exactitude financière réelle |
| EVD-003 | La structure Medallion ajoute des champs techniques contrôlés | Schémas et exécutions de notebooks | À indexer | `OBSERVED` à vérifier | Les comptes de colonnes doivent être rattachés à une exécution datée |
| EVD-004 | Quatorze datamarts SQL sont publiés localement ; onze alimentent les sujets du dashboard et les mesures communes se réconcilient | Scripts SQL, inventaire DuckDB et réconciliation | `FinOps Data Platform - POC/medallion_pipeline/sql/datamarts/` et warehouse local | `VALIDATED-LOCAL` | Publication Databricks non testée ; un seul mois disponible |
| EVD-005 | Le dashboard Streamlit démarre localement et ses huit sous-vues s'exécutent uniquement sur les datamarts de janvier 2025 | AppTest Streamlit et exécution des requêtes | `FinOps Data Platform - POC/dashboard_finops/` et warehouse local | `VALIDATED-LOCAL` | Adaptateur Databricks, ergonomie utilisateur et RLS non testés |
| EVD-006 | Après extraction, le dataset partagé conserve 546 fichiers quotidiens et 18 billings `no_change`, soit 3279613 lignes et 18220080 EUR ; le billing janvier conserve son SHA-256 | Validations complètes, manifestes et tests unitaires | `FinOps Data Generator/metadata/` et suites de tests | `VALIDATED-LOCAL` | Ne prouve ni publication GCS ni exécution Databricks |
| EVD-007 | Le code cloud définit Daily, Monthly Close, Backfill, audit et archivage optionnel avec configurations DEV/PROD | Code, compilation et tests unitaires hors connexion | `FinOps Cloud Data Platform/` | `VALIDATED-LOCAL` pour le code | La preuve d'exécution cloud relève séparément d'EVD-009/EVD-010 ; l'archivage automatique est actuellement désactivé |
| EVD-008 | Le modèle cloud définit 10 dimensions, une table de pont, une fact et 14 datamarts en SQL invoqué par PySpark | DDL/DML, documentation et tests unitaires hors connexion | `FinOps Cloud Data Platform/platform/common/sql/` et `docs/data_model.md` | `VALIDATED-LOCAL` pour le code | Les résultats de publication Databricks doivent être rattachés aux artefacts de run d'EVD-009 |
| EVD-009 | Le plan technique Belgium rapporte un backfill mensuel 2025-01 à 2026-06 et des contrôles DEV/PROD réussis | Relevé de progression ; Run IDs et sorties à collecter | `FinOps Cloud Data Platform/docs/databricks_belgium_completion_plan.md` | `REPORTED-AWAITING-ARTIFACTS` | Le plan ne fournit pas encore les identifiants de runs, résultats SQL, volumes et commit exécuté ; ne pas présenter comme preuve complète dans le mémoire |
| EVD-010 | Le plan technique rapporte un premier Daily 2026-07-01 chargé en DEV seulement | Relevé de progression ; Run ID et contrôle à collecter | Même plan de finalisation Belgium | `REPORTED-AWAITING-ARTIFACTS` | Ne démontre ni la promotion PROD ni l'idempotence du Job complet |
| EVD-011 | Le générateur local valide 608 Daily du 2025-01-01 au 2026-08-31 : 3 664 261 lignes et 20 357 040 EUR ; les 18 billings `no_change` restent limités à 2025-01–2026-06 | Exécution des deux validateurs et rapports CSV | `FinOps Data Generator/metadata/` ; `audit/05_local_validation_2026_09_27.md` | `VALIDATED-LOCAL` | Ne démontre ni publication GCS ni réalisme financier ; les deux mois Daily récents n'ont pas de billing validé |
| EVD-012 | Dans le POC DuckDB de janvier 2025, 95,98 % du coût est au centre `Unknown`, 16,08 % sans owner identifié, et les deux premiers services représentent 40,83 % | Requêtes DuckDB en lecture seule, version 1.5.5 | `FinOps Data Platform - POC/duckdb_local_bi/database/finops_warehouse.duckdb` ; `audit/05_local_validation_2026_09_27.md` | `VALIDATED-LOCAL` | Un seul mois synthétique ; ne décrit pas la qualité d'allocation réelle de TEN |
| EVD-013 | La migration locale du parcours Monthly vers `monthly/billing-YYYY-MM.parquet` conserve les 18 SHA-256 ; la revalidation retrouve 3 279 613 lignes Monthly et 3 664 261 lignes Daily, avec les mêmes montants | Contrôle des hashes, cinq tests unitaires et deux validateurs, le 28 septembre 2026 | `audit/05_local_validation_2026_09_27.md`, section EVD-013 ; générateur et métadonnées locales | `VALIDATED-LOCAL` | Revalidation du parcours local, pas une nouvelle publication GCS ou exécution Databricks |

## Modèle pour une nouvelle preuve

### EVD-xxx — Titre

- **Date et environnement :**
- **Affirmation testée :**
- **Données et volumétrie :**
- **Procédure ou commande reproductible :**
- **Résultat obtenu :**
- **Résultat attendu :**
- **Artefacts :**
- **Versions logicielles :**
- **Interprétation :**
- **Ce que cette preuve ne démontre pas :**
- **Exigences M01-M10 couvertes :**
