# Journal partagé — travaux techniques vers le mémoire

## Objectif

Ce fichier assure la continuité entre la session consacrée à l'implémentation technique et la session consacrée à la rédaction du mémoire. Il ne remplace pas les chapitres du mémoire : il recueille les éléments techniques et les preuves qui devront ensuite être analysés et intégrés dans les sections appropriées.

## Consigne pour la session technique

Après chaque décision, implémentation ou validation importante, ajouter une entrée en suivant le modèle ci-dessous. Ne consigner que des faits vérifiables. Distinguer les résultats observés des résultats attendus et des travaux encore à réaliser.

## Modèle d'entrée

### AAAA-MM-JJ — Titre court

- **Besoin ou problème traité :**
- **Statut :** `PLANNED` / `IMPLEMENTED` / `TESTED` / `SUPERSEDED`
- **Contexte et contraintes :**
- **Solutions envisagées :**
- **Choix retenu :**
- **Justification du choix :**
- **Implémentation réalisée :**
- **Données et environnement utilisés :**
- **Validation ou tests exécutés :**
- **Résultats mesurés :**
- **Limites et risques :**
- **Alternatives ou améliorations futures :**
- **Fichiers de preuve :**
- **Décisions associées :** identifiants `ADR-xxx` ou décision à créer
- **Preuves associées :** identifiants `EVD-xxx` ou preuve à enregistrer
- **Destination probable dans le mémoire :** méthodologie / architecture / réalisation / résultats / discussion / limites / annexes
- **Informations à confirmer par l'étudiant :**

## Points à signaler systématiquement

- Choix d'un outil, d'une architecture, d'un modèle de données ou d'un algorithme.
- Abandon ou remplacement d'une solution, avec sa raison.
- Hypothèses et simplifications imposées par les données, le temps, les licences ou l'environnement.
- Volumétrie, durée d'exécution, versions logicielles et configuration des tests.
- Contrôles de qualité, réconciliation, reproductibilité, idempotence et sécurité.
- Résultats négatifs, erreurs rencontrées et corrections apportées.
- Différence entre preuve locale, démonstration Databricks et capacité de production non testée.
- Capture, rapport, requête ou artefact pouvant servir de preuve ou d'annexe.

## Entrées

Les nouvelles entrées sont ajoutées sous ce titre, de la plus récente à la plus ancienne.

### 2026-09-27 — Réorganisation du chapitre de réalisation

- **Besoin ou problème traité :** distinguer clairement les trois livrables et sortir la chronologie Frankfurt/Belgium du HLD.
- **Statut :** `IMPLEMENTED` pour la structure du mémoire ; validation technique supplémentaire non exécutée.
- **Choix retenu :** 5.1 générateur FOCUS indépendant, 5.2 POC local DuckDB/Streamlit, 5.3 plateforme cloud Databricks ; choix régionaux et comparaisons de coût réservés aux chapitres 7 et 8.
- **Implémentation réalisée :** regroupement des sept anciennes sections du chapitre 5 en trois fichiers, mise à jour du sommaire, du plan des illustrations, des renvois LLD et des décisions documentaires. La chronologie de l'extraction du générateur reste dans ADR-010.
- **Limites et risques :** la nouvelle rédaction n'ajoute aucune preuve de run Databricks ; résultats cloud, application et benchmark restent soumis aux artefacts primaires.
- **Destination dans le mémoire :** chapitres 4, 5, 7 et 8.

### 2026-09-27 — Rédaction des six mises à jour prioritaires et vérification locale

- **Besoin ou problème traité :** remplacer les trames par une rédaction académique en anglais sur les données, l'architecture, le pipeline, les résultats et le coût.
- **Statut :** `TESTED` pour les validateurs locaux ; `WORKING` pour les chapitres, qui restent à relire.
- **Validation :** 608 Daily, 3 664 261 lignes et 20 357 040 EUR jusqu'à août 2026 ; 18 billings `no_change`, 3 279 613 lignes et 18 220 080 EUR jusqu'à juin 2026.
- **Analyse locale complémentaire :** 95,98 % du coût de janvier 2025 au centre `Unknown`, 16,08 % sans owner identifié et 40,83 % pour les deux premiers services.
- **Limites :** données synthétiques ; les résultats Databricks restent rapportés sans artefacts de run indexés ; coûts DBU/GCP non disponibles pour un résultat économique chiffré.
- **Preuves associées :** EVD-011 et EVD-012 ; détail dans `audit/05_local_validation_2026_09_27.md`.
- **Destination :** chapitres 3, 4, 5, 6, 7 et 8.

### 2026-09-27 — Réconciliation documentaire après les changements cloud

- **Besoin ou problème traité :** aligner le mémoire sur la séparation générateur/POC/plateforme et sur les configurations Databricks actuelles.
- **Statut :** `IMPLEMENTED` pour la mise à jour documentaire ; validation technique supplémentaire non exécutée ici.
- **État documenté :** RAW partagé entre DEV et PROD, archivage automatique désactivé ; scénarios Serverless et Classic avec notebooks/SQL communs ; backfill historique DEV/PROD et premier Daily DEV rapportés par le plan de finalisation Belgium.
- **Limites :** Run IDs, sorties des contrôles, commit exécuté et mesures de coûts/performance non encore indexés dans le mémoire ; Daily complet DEV → PROD, clôture Classic et App Databricks à vérifier.
- **Décisions associées :** ADR-012 révisée, ADR-015 ajoutée ; ADR-014 replacée dans son contexte DEV initial.
- **Preuves associées :** EVD-009 et EVD-010 enregistrées comme résultats rapportés en attente d'artefacts, sans promotion au statut `VALIDATED`.
- **Destination dans le mémoire :** 3.3, 4.4, 5.3, 7.4, 8.3 et 9.1.

### 2026-09-20 — Choix du compute DEV et comparaison FinOps différée

- **Besoin ou problème traité :** maîtriser le coût des Jobs Databricks pendant la stabilisation fonctionnelle sans multiplier prématurément les environnements de calcul.
- **Statut :** `TESTED`
- **Contexte et contraintes :** Jobs déployés par Bundle et verrouillés dans l'interface ; traitements batch ; budget PFE limité.
- **Solutions envisagées :** Serverless Performance Optimized, Serverless Standard et Classic dimensionné manuellement.
- **Choix retenu :** Serverless `STANDARD` avec `max_concurrent_runs = 4` pour les quatre Jobs DEV.
- **Justification du choix :** privilégier la maîtrise des coûts et la simplicité d'exploitation pendant le développement.
- **Implémentation réalisée :** ajout des deux paramètres à chaque ressource Job dans `resources/jobs.yml`.
- **Validation ou tests exécutés :** Bundle validé, 15 tests unitaires réussis, déploiement des quatre Jobs et lecture de leur configuration par l'API Databricks.
- **Résultats mesurés :** les quatre Jobs exposent `performance_target = STANDARD` et `max_concurrent_runs = 4` ; aucun benchmark de coût ou de performance à ce stade.
- **Limites et risques :** le mode Standard peut augmenter le temps de démarrage ; quatre runs par Job peuvent accroître fortement la consommation globale ; la comparaison économique avec Classic reste inconnue.
- **Alternatives ou améliorations futures :** benchmark contrôlé Serverless/Classic sur la même source, avec destinations isolées, archivage désactivé et coûts Databricks/GCP consolidés.
- **Fichiers de preuve :** `FinOps Cloud Data Platform/resources/jobs.yml`.
- **Décisions associées :** ADR-014.
- **Destination probable dans le mémoire :** validation/performance, coûts d'exploitation et discussion ; le HLD reste indépendant de la chronologie des choix de compute.

### 2026-09-19 — Séparation POC, générateur partagé et plateforme cloud

- **Besoin ou problème traité :** éviter de forcer une parité artificielle DuckDB/Spark et préparer une exécution DEV/PROD homogène sur Databricks.
- **Statut :** `IMPLEMENTED` localement, intégration cloud non testée.
- **Choix retenu :** trois projets frères : générateur indépendant, POC local figé et plateforme active Databricks/GCP.
- **Justification du choix :** conserver les preuves locales, produire un seul dataset Daily/Monthly et utiliser le même moteur Delta/Spark en DEV et PROD.
- **Implémentation réalisée :** déplacement sans régénération des données ; format `focus/daily/year=YYYY/month=MM/day=DD` et `focus/monthly/billing-YYYY-MM.parquet` ; CLI Python Daily/Monthly/Monthly Range ; configuration cloud DEV/PROD ; jobs Daily, Monthly Close et Backfill ; snapshots `BEFORE`, `SOURCE`, `AFTER` ; remplacement Delta mensuel ; Gold initial et datamarts ; archivage vers `gs://dtl_finops/focus_archive` avec reprise.
- **Données et environnement utilisés :** données synthétiques locales existantes, Python 3.14 pour la validation du générateur ; aucun workspace Databricks ni bucket GCS contacté.
- **Validation ou tests exécutés :** 4 tests du générateur, 5 tests unitaires cloud, compilation Python, validation exhaustive des 546 Parquet et contrôle du hash du billing janvier.
- **Résultats mesurés :** 546 jours du 2025-01-01 au 2026-06-30, 3279613 lignes, 18220080 EUR ; 18 billings mensuels `no_change` validés sur la même période et les mêmes totaux ; janvier 2025 : 31 fichiers, 164145 lignes, SHA-256 `60c161051fb027935c3817db8fb6f85447b032700a4a500169f0ff3f4d38ea8b` inchangé.
- **Limites et risques :** configuration Runtime, OAuth, Unity Catalog, External Volumes, permissions GCS, syntaxe Delta réelle, concurrence et performance restent à tester dans Databricks DEV.
- **Fichiers de preuve :** `FinOps Data Generator/`, `FinOps Cloud Data Platform/`, `FinOps Data Platform - POC/`.
- **Décisions associées :** ADR-010, ADR-011, ADR-012.
- **Preuves associées :** EVD-006, EVD-007.
- **Destination probable dans le mémoire :** méthodologie, architecture, réalisation, validation, limites et annexes.

### 2026-09-14 — Datamarts orientés sujets pour le dashboard

- **Besoin ou problème traité :** éviter que les sections interactives interrogent directement la table centrale et garantir une définition stable des indicateurs.
- **Statut :** `TESTED`
- **Choix retenu :** un datamart matérialisé par sujet analytique cohérent, réutilisable par plusieurs KPI ou graphiques.
- **Justification du choix :** réduire les scans et jointures au runtime, centraliser les règles métier et conserver le même contrat SQL entre DuckDB et Databricks.
- **Implémentation réalisée :** ajout de `dm_executive_summary_monthly`, `dm_top_resources_monthly` et `dm_data_quality_monthly`; utilisation de `dm_savings_monthly`; redirection de toutes les requêtes Streamlit vers les datamarts.
- **Données et environnement utilisés :** DuckDB 1.5.5, données synthétiques de janvier 2025, 164145 lignes.
- **Validation ou tests exécutés :** publication des quatorze scripts SQL, inventaire des tables, réconciliation croisée, compilation Python et Streamlit AppTest sur les huit sous-vues navigables.
- **Résultats mesurés :** 14 datamarts publiés, dont 11 consommés par le dashboard ; coût facturé de 912000 EUR identique dans les datamarts Executive et Monthly Billing ; 164145 lignes identiques dans Executive et Data Quality ; huit sous-vues testées, zéro exception et zéro élément d'avertissement Streamlit. Les suites existantes exécutent également 1 test du générateur et 9 tests de facturation avec succès.
- **Limites et risques :** un seul mois; portabilité SQL Databricks conçue mais non exécutée; les comparaisons de coûts ne constituent pas encore une preuve d'économies métier réalisées.
- **Fichiers de preuve :** `FinOps Data Platform/medallion_pipeline/sql/datamarts/`, `FinOps Data Platform/dashboard_finops/`, warehouse DuckDB local.
- **Décisions associées :** ADR-009.
- **Preuves associées :** EVD-004, EVD-005.
- **Destination probable dans le mémoire :** conception technique, optimisation, réalisation, validation et limites.
- **Observation métier complémentaire :** `ContractedCost - EffectiveCost` vaut -57102,90 EUR en janvier 2025 ; cet écart ne peut pas être qualifié d'économie d'engagement sans analyse sémantique des lignes éligibles et des exclusions.

### 2026-09-13 — Consultation du dashboard Streamlit local

- **Besoin ou problème traité :** vérifier que la nouvelle brique Inform est consultable et exploite les datamarts produits.
- **Statut :** `TESTED`
- **Contexte et contraintes :** application Streamlit portable et warehouse DuckDB local disponible ; accès visuel finalement établi avec Microsoft Edge autorisé dans ChatGPT Computer Use.
- **Solutions envisagées :** lecture du code, contrôle HTTP du serveur, exécution directe des requêtes et inspection visuelle interactive.
- **Choix retenu :** combiner contrôle du démarrage, validation des requêtes contre DuckDB et navigation dans les quatre onglets.
- **Justification du choix :** vérifier le backend et les données sans confondre cette preuve avec une validation visuelle ou Databricks.
- **Implémentation réalisée :** aucune modification fonctionnelle du dashboard.
- **Données et environnement utilisés :** DuckDB local, période 2025-01, Streamlit 1.63.0, DuckDB 1.5.5.
- **Validation ou tests exécutés :** réponse HTTP 200, endpoint de santé `ok`, requêtes mois, synthèse, tendances, services, centres de coûts, ressources, charges et qualité ; consultation des onglets Tendances, Allocation, Ressources et Qualité.
- **Résultats mesurés :** 164145 lignes, 22453 ressources, 59 services et coût facturé proche de 912000 EUR avant formatage ; 31 lignes quotidiennes et un mois disponible.
- **Limites et risques :** un seul mois ; l'axe du graphique mensuel affiche des timestamps inadaptés ; pas de test de l'adaptateur Databricks, de Databricks Apps ou de la RLS.
- **Alternatives ou améliorations futures :** test visuel et captures, validation de portabilité Databricks, scénarios multi-mois et tests de sécurité.
- **Fichiers de preuve :** `FinOps Data Platform/dashboard_finops/` et `duckdb_local_bi/database/finops_warehouse.duckdb`.
- **Décisions associées :** ADR-008.
- **Preuves associées :** EVD-005.
- **Destination probable dans le mémoire :** architecture, réalisation, résultats, limites et annexes.
- **Informations à confirmer par l'étudiant :** exigences métier et niveau de lisibilité attendu par les utilisateurs visés.
