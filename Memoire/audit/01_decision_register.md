# Registre des décisions d'architecture et de conception

## Utilisation

Chaque décision structurante reçoit un identifiant stable. Une décision peut évoluer, mais son ancienne justification reste visible et passe alors au statut `SUPERSEDED` avec un lien vers la nouvelle décision.

| ID | Date | Décision | Statut | Justification disponible | Documents concernés |
|---|---|---|---|---|---|
| ADR-001 | À dater | Utiliser une architecture Medallion Raw/Bronze/Silver/Gold | `DECIDED` à confirmer | Partielle | HLD, notes Medallion |
| ADR-002 | À dater | Définir Silver comme source de vérité canonique | `DECIDED` | Oui, dans les notes | HLD, notes Medallion |
| ADR-003 | À dater | Utiliser un Data Contract FOCUS versionné | `DECIDED` | Partielle | Notes Data Contract |
| ADR-004 | À dater | Employer des données synthétiques à cause de la confidentialité et de l'historique limité | `DECIDED` | Oui, à consolider | Méthodologie |
| ADR-005 | 2026-09-06 | Conserver un notebook unique pour la simulation mensuelle et retirer le CLI redondant | `SUPERSEDED` par ADR-010 | Oui | Notes simulation mensuelle |
| ADR-006 | À dater | Matérialiser une table centrale SQL dérivée de Silver | `DECIDED` à confirmer | Oui, compromis documenté | Notes Medallion |
| ADR-007 | À décider | Retenir la pile cible face à Fabric et Azure PaaS modulaire | `WORKING` | Comparaison initiale seulement | Évaluation technologique, HLD |
| ADR-008 | À dater | Utiliser une application Streamlit unique avec adaptateurs DuckDB et Databricks | `SUPERSEDED` par ADR-011 | Oui, à consolider | Sections 4.3.8, 5.2.3 et 5.3.5, code des deux applications |
| ADR-009 | 2026-09-14 | Alimenter chaque sujet analytique du dashboard par un datamart matérialisé et réutilisable | `DECIDED` | Oui | Sections 5.2.2–5.2.3 et 5.3.3–5.3.5, scripts SQL, dashboards |
| ADR-010 | 2026-09-19 | Extraire un générateur indépendant produisant un dataset unique Daily/Monthly pour le POC et le cloud | `DECIDED` | Oui | Générateur, méthodologie, notes de réunion |
| ADR-011 | 2026-09-19 | Séparer le POC local figé de la plateforme active Databricks/GCP avec DEV et PROD sur Databricks | `DECIDED` | Oui | HLD, pipeline cloud, Bundles |
| ADR-012 | 2026-09-19 | Clôturer un mois par audit BEFORE/SOURCE/AFTER et remplacement Delta atomique ; archivage automatique initial abandonné | `PARTIALLY SUPERSEDED` par ADR-015 | Oui | Pipeline mensuel, tables ops, rétention |
| ADR-013 | 2026-09-20 | Conserver le modèle Gold et les datamarts en SQL versionné, avec PySpark comme orchestrateur d'exécution | `DECIDED` | Oui | Modèle de données cloud, DDL/DML Gold, runner SQL |
| ADR-014 | 2026-09-20 | Utiliser Serverless `STANDARD` avec un plafond de quatre exécutions simultanées par Job en DEV et reporter le benchmark Classic en fin de projet | `DECIDED` pour la configuration DEV initiale | Oui | Validation, coûts run, Bundle Databricks |
| ADR-015 | 2026-09-27 (documenté) | Laisser le RAW commun en place pour permettre une consommation indépendante par DEV et PROD | `DECIDED` dans la configuration actuelle | Oui | HLD physique, pipeline, rétention, `config/common.toml` |

### ADR-014 — Compute DEV économique et benchmark différé

- **Date :** 2026-09-20
- **Statut :** `DECIDED`
- **Contexte :** la plateforme est encore en développement ; le pipeline fonctionnel doit être stabilisé avant d'optimiser son infrastructure par scénarios concurrents.
- **Contraintes :** budget PFE limité, traitements batch, Jobs gérés par Bundle et absence actuelle de mesures comparables Serverless/Classic.
- **Options considérées :** Serverless Performance Optimized, Serverless Standard, Jobs compute Classic dimensionné manuellement.
- **Décision :** conserver Serverless en mode `STANDARD` et fixer `max_concurrent_runs` à `4` pour tous les Jobs DEV.
- **Justification :** réduire le risque de consommation inutile tout en évitant une gestion prématurée des clusters pendant la stabilisation du projet.
- **Conséquences positives :** configuration simple, reproductible et versionnée ; plusieurs essais peuvent coexister sans laisser la concurrence devenir illimitée.
- **Coûts, limites et risques :** temps de démarrage potentiellement supérieur ; taille de machine non contrôlable ; jusqu'à quatre runs concurrents par Job et donc un plafond global supérieur ; économie relative non démontrée.
- **Preuves associées :** `resources/jobs.yml` et lecture API des quatre Jobs après déploiement confirmant `STANDARD` et une concurrence maximale de `4`.
- **Amélioration future :** exécuter en fin de projet un benchmark isolé et répété contre un Jobs compute Classic de petite taille, puis comparer coût total, durée, DBU et qualité des sorties.
- **Remplace / remplacée par :** aucune.

### ADR-015 — Conservation du RAW partagé

- **Date :** état documenté le 2026-09-27 ; dater la décision technique d'origine si nécessaire.
- **Statut :** `DECIDED` dans la configuration actuelle.
- **Contexte :** DEV et PROD consomment les mêmes Parquet exposés par `finops_raw.landing`.
- **Décision :** désactiver l'archivage automatique dans `config/common.toml` et conserver les sources RAW après un traitement DEV ou une clôture.
- **Justification :** déplacer la source après DEV pourrait empêcher la promotion indépendante en PROD.
- **Conséquence :** une politique de rétention et son coût de stockage restent à définir en tenant compte de tous les consommateurs et de l'audit.
- **Preuves associées :** configuration et `docs/architecture.md` ; aucune preuve d'une politique de rétention de production.
- **Remplace / remplacée par :** remplace uniquement la partie « archivage automatique après clôture » d'ADR-012.

## Modèle pour une nouvelle décision

### ADR-xxx — Titre

- **Date :**
- **Statut :** `PROPOSED` / `DECIDED` / `SUPERSEDED`
- **Contexte :**
- **Contraintes :**
- **Options considérées :**
- **Décision :**
- **Justification :**
- **Conséquences positives :**
- **Coûts, limites et risques :**
- **Preuves associées :**
- **Remplace / remplacée par :**
