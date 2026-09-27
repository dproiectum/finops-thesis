# Journal des changements documentaires

## 2026-09-28 — Nettoyage des liens, figures et planning du projet

- Suppression de l'unique hyperlien `.md` externe encore présent dans le cadrage historique ; ce document renvoie désormais à la section 4.3 pour la justification technologique courante.
- Conservation de `plan/` comme préparation hors PDF, avec signalement des hypothèses initiales Azure ; retrait du registre LLD resté vide.
- Centralisation des futurs fichiers image dans `annexes/figures/architectures/`. Le schéma synthétique du modèle Gold reste prévu dans la section 4.5.2, indépendamment de l'emplacement de son fichier source.
- Conservation du Gantt du 5 septembre comme base historique et création d'une version datée du 28 septembre pour préparer une éventuelle annexe de gestion de projet. Les runs Belgium y restent explicitement rapportés, non vérifiés par artefacts de run.

## 2026-09-27 — Retrait des annexes provisoires

- Suppression des deux annexes proposées, à la demande de l'étudiant : elles n'étaient pas nécessaires pour comprendre les chapitres et ne répondaient pas à la règle de complément documentaire voulue.
- Suppression de tous les renvois à ces annexes dans les sections du mémoire et dans le plan d'assemblage ; les résultats nécessaires demeurent explicités dans les chapitres concernés.
- Règle générale : figure ou contenu essentiel dans le chapitre ; détail facultatif et lisible dans une éventuelle annexe du même PDF ; aucune annexe créée pour pointer seulement vers un fichier technique.

## 2026-09-27 — Annexe A recentrée sur un complément lisible

- Remplacement de l'annexe A d'inventaire de fichiers par une note concise sur les clés et les sources du modèle Gold, complément ciblé du § 4.5.2–4.5.3.
- Déplacement des chemins et révisions Git dans `audit/07_technical_source_inventory_2026_09_27.md`, hors du PDF.
- Suppression des renvois à l'annexe A depuis les sections sans rapport avec le modèle Gold ; les résultats cloud seulement rapportés restent décrits et limités en § 7.4.
- L'annexe B conserve les résultats de validation locale et leur périmètre.

## 2026-09-27 — Préparation des renvois pour un PDF autonome

- Remplacement des liens locaux `.md` et `.sql` dans les 37 sections par des explications autonomes et des renvois internes aux annexes A et B.
- Annexe A : révisions techniques vérifiées, provenance du modèle, configuration Classic et statut seulement rapporté des exécutions cloud.
- Annexe B : méthode et résultats locaux synthétiques, dont `ContractedCost` revérifié en lecture seule dans DuckDB.
- Les URL de documentation externe restent des références bibliographiques à normaliser selon la norme imposée ; aucune exécution cloud supplémentaire revendiquée.

## 2026-09-27 — Clarification des choix techniques et du modèle de données

- Clarification du renvoi final du § 4.2 : fonctions logiques, choix de technologies, implantation physique et modèle de données ont désormais des rôles distincts.
- Ajout en § 4.3 d'un tableau par fonction séparant le POC local des environnements DEV/PROD Databricks ; les outils seulement évoqués dans la capture de travail ne sont pas présentés comme comparés.
- Introduction du § 4.4 recentrée sur les composants et leurs frontières physiques.
- Ajout du § 4.5 avec les douze noms de tables Gold et les quatorze datamarts reliés à leurs questions métier ou de contrôle, d'après la DDL et les scripts de rafraîchissement versionnés.
- Plan du mémoire, illustration F4 et registre LLD mis à jour ; aucune validation cloud supplémentaire revendiquée.

## 2026-09-27 — Trois volets de réalisation et récit de migration isolé

- Regroupement des sept anciens fichiers du chapitre 5 en trois sections : générateur FOCUS, POC local et plateforme Databricks ; 36 sections composent désormais le plan courant.
- HLD du chapitre 4 recentré sur les composants et interfaces, sans récit régional ; chronologie Frankfurt → Belgium et limites de comparaison explicitées en 8.4.2.
- Mise à jour du sommaire, du plan d'illustrations, des renvois LLD et du registre de décisions ; les entrées historiques ci-dessous conservent les numéros qu'elles avaient au moment de leur rédaction.
- Aucune nouvelle exécution cloud ni économie chiffrée revendiquée par cette réorganisation.

## 2026-09-27 — Application du code de rédaction académique

- Relecture des 40 sections en anglais et remplacement des principales trames par une prose fondée sur les preuves disponibles.
- Suppression des statuts de travail du corps des sections ; renvois locaux et références externes vérifiés ; limites des résultats locaux et cloud maintenues.
- Correction factuelle des champs optionnels du contrat FOCUS dans 5.4 et de deux notices bibliographiques après consultation des éditeurs.
- Code de rédaction inscrit dans `Memoire/README.md` ; audit détaillé dans `audit/06_academic_writing_review_2026_09_27.md`.
- Rôle/cours personnels et norme bibliographique notés pour reprise ultérieure à la demande de l'étudiant (Q-021, Q-013, Q-007).

## 2026-09-27 — Alignement des noms de fichiers avec les titres du mémoire

- Relecture des titres des 40 fichiers de sections et des autres fichiers Markdown du dossier `Memoire`.
- Renommage de 26 fichiers de sections dont le nom abrégé ou ancien ne reprenait pas exactement le titre anglais interne ; numéros 1.1 à 10.3 conservés.
- Harmonisation des 40 libellés du plan avec les titres internes, mise à jour des références dans le registre LLD et précision de la convention de nommage.
- Aucun contenu analytique ni statut de preuve modifié par ce renommage.

## 2026-09-27 — FinOps appliqué à la plateforme Databricks

- Ajout de la section 8.4, rédigée en anglais, sur l'attribution des coûts par charge de travail, les leviers d'optimisation et leur comparaison contrôlée.
- Mise à jour du plan et des renvois en 1.6, 8.3 et 9.1. La section 7.3 conserve le protocole de performance ; 8.3 définit la mesure des coûts ; 8.4 interprète les choix d'optimisation.
- Aucune économie Databricks revendiquée : identifiants de runs, consommation tarifée, coûts GCP et équivalence des sorties restent à réunir.

## 2026-09-27 — Rédaction effective des mises à jour prioritaires

- Remplacement des simples trames par une prose académique en anglais dans les sections 3.1–3.2, 4.4, 5.1–5.3, 6.1–6.3, 7.4 et 8.3.
- Vérification locale des 608 Daily jusqu'en août 2026 et des 18 billings jusqu'en juin 2026 ; ajout d'EVD-011.
- Requêtes de lecture seule sur le POC DuckDB de janvier 2025 pour l'allocation et les services ; ajout d'EVD-012 et d'une note reproductible.
- Précision de l'atomicité Delta par table : la chaîne entière Silver/Gold/datamarts n'est pas une transaction multi-table.
- Chiffres Databricks et coûts GCP laissés non chiffrés tant que les artefacts nécessaires ne sont pas disponibles.

## 2026-09-27 — Correction de la langue du mémoire

- Traduction en anglais du plan d'assemblage et des textes de `chapters/`, y compris les nouvelles sections et les anciennes notes françaises.
- Maintien des échanges et registres internes en français lorsqu'ils ne sont pas destinés au PDF.
- Formulation de travail de la question centrale rendue indépendante d'Azure, car le prototype actif est Databricks/GCP ; validation finale par l'encadrant toujours requise.
- Aucun résultat technique nouveau ni statut de preuve modifié par cette correction éditoriale.

## 2026-09-27 — Mise à jour du plan et réconciliation avec la plateforme cloud

- Plan détaillé des dix chapitres et de leurs sections, avec trames nouvelles 3.3, 5.1, 5.2 et 7.4.
- Réécriture des sections 3.1–3.2, 4.4, 5.3 et 5.7 pour séparer générateur, POC local et plateforme Databricks/GCP.
- Correction de l'archivage RAW : désactivé pour la source partagée DEV/PROD ; ADR-012 partiellement remplacée par ADR-015.
- Actualisation des chapitres 6 à 9 : backfill cloud rapporté mais artefacts à indexer, Daily complet et clôture Classic à tester, coûts et comparaisons à mesurer.
- Ajout d'EVD-009/EVD-010 comme relevés en attente d'artefacts et des questions Q-017 à Q-020.
- Aucun nouveau résultat technique n'a été produit par cette mise à jour du mémoire.

## 2026-09-15 — Fusion des chapitres 01 et 02

- Déplacement des cinq sections de contexte/problématique dans `01_introduction`, avec renommage et titres 1.1 à 1.5.
- Ajout de la section 1.6 consacrée à l'organisation du mémoire.
- Conservation des exigences détaillées dans le cadrage ; l'introduction n'en contient qu'une synthèse.
- Conservation de la structure et des identifiants des chapitres suivants, à la demande de l'étudiant. La numérotation continue du PDF sera établie à l'assemblage.
- Aucun contenu métier, technique ou résultat des chapitres suivants n'a été modifié.

Ce journal trace les réorganisations significatives du dossier `Memoire`. Les corrections éditoriales mineures pourront être retrouvées dans le contrôle de version lorsque le dossier racine sera lui-même versionné.

## 2026-09-20 — Choix du compute DEV

- Ajout d'ADR-014 pour retenir Serverless `STANDARD` et limiter chaque Job DEV à quatre exécutions simultanées.
- Ajout de la décision au HLD physique et de ses limites actuelles.
- Inscription du benchmark Serverless/Classic comme expérimentation future dans les chapitres Performance et Coûts.
- Aucun gain financier ou de performance n'est présenté comme démontré avant la campagne de mesure.

## 2026-09-14 — Optimisation du serving du dashboard

- Documentation du principe « un datamart par sujet analytique cohérent » dans la section 5.6.
- Ajout de la matrice de couverture entre les sections du dashboard et les datamarts certifiés.
- Enregistrement d'ADR-009 et consolidation des preuves EVD-004/EVD-005.
- Mise à jour du résultat local de sept à onze datamarts et ajout des réconciliations mesurées.

## 2026-09-13 — Mise en place de la documentation évolutive

### Motif

Adapter la documentation à une phase de build où les décisions et résultats peuvent changer, tout en conservant une piste d'audit exploitable pour le mémoire.

### Changements

- Création de l'index et des règles de statut dans `Memoire/README.md`.
- Création du HLD version 0.1 distinguant cible, prototype cloud et validation locale.
- Création du registre des futurs LLD.
- Création des registres de décisions, de preuves et de questions ouvertes.
- Extension du journal partagé avec les statuts et identifiants ADR/EVD.
- Adoption de la convention `CC_SS_sujet.md` pour les briques destinées au mémoire.
- Renommage des cinq sections existantes selon leur ordre futur d'assemblage.
- Déplacement du journal partagé dans `audit/` et numérotation des registres d'audit.
- Création de `chapters/README.md` comme plan d'assemblage du futur PDF unique.
- Intégration de la nouvelle note du dashboard sous le numéro 04.05 et enregistrement d'ADR-008/EVD-005.

### Choix de conservation

Les fichiers historiques de `plan/` et les notes existantes de `chapters/` n'ont pas été déplacés ni réécrits. Ils contiennent des informations encore utiles et certains liens relatifs. Ils seront consolidés progressivement, puis marqués `SUPERSEDED` si un document plus récent les remplace.

### Limites

- Le dossier `Memoire` n'est pas actuellement couvert par le dépôt Git détectable depuis la racine `/Users/dtl/Desktop/PFE` ; la traçabilité repose donc pour l'instant sur les journaux documentaires et les fichiers eux-mêmes.
- Les décisions et preuves initiales ont été recensées à partir des notes, mais plusieurs dates et emplacements d'artefacts restent à confirmer.

## 2026-09-13 — Création du chapitre métier FinOps

### Motif

Donner au métier FinOps et aux mécanismes économiques du cloud une place explicite avant la méthodologie et l'architecture technique.

### Changements

- Création du chapitre 03 avec quatre sections : cadre FinOps, Inform/Optimize/Operate, mécanismes de prix, allocation/showback/gouvernance.
- Déplacement de la méthodologie au chapitre 04.
- Déplacement des choix techniques et de l'architecture au chapitre 05.
- Création de la section 05.01 consacrée à la sélection technologique.
- Mise à jour du plan d'assemblage, du registre LLD et de la bibliographie de travail.

### Limites

- Les nouvelles sections sont au statut `WORKING` et sont encore rédigées en anglais comme les notes historiques.
- La terminologie du FinOps Framework actuel doit être articulée avec le découpage Inform/Optimize/Operate retenu par le projet.
- Les formules de comparaison de coûts nécessitent des règles d'éligibilité et d'exclusion validées sur les données avant d'être présentées comme économies réalisées.

## 2026-09-13 — Clarification du chapitre 02

- Retrait de l'expression trop large « état de l'art » du chapitre 02.
- Création de cinq sections numérotées couvrant contexte professionnel, processus actuel, problématique, périmètre et exigences.
- Séparation explicite entre le cas professionnel du chapitre 02 et le cadre métier FinOps du chapitre 03.

## 2026-09-14 — Synchronisation des datamarts et du dashboard

- Suppression des dossiers de chapitres vides `03_methodology` et `04_architecture`, vestiges de la renumérotation.
- Mise à jour des sections d'architecture avec 14 datamarts publiés et 11 datamarts consommés par Streamlit.
- Création des sections 6.1 et 6.2 pour séparer la réalisation détaillée de l'architecture générale.
- Création de la section 7.1 avec les résultats locaux, les tests et leurs limites de validité.
- Conservation explicite de l'écart négatif `ContractedCost - EffectiveCost` comme résultat à investiguer.

## 2026-09-14 — Restructuration conception, choix et LLD

- Restructuration du chapitre 05 en exigences, HLD logique, évaluation technologique et HLD physique.
- Intégration de CSV, Parquet et Delta comme sous-partie de la sélection technologique.
- Déplacement de Medallion, Data Contract, Gold, datamarts et Streamlit vers le chapitre 06 de conception détaillée et réalisation.
- Intégration du HLD physique dans les fragments assemblables du mémoire au lieu d'un dossier HLD séparé.
- Mise à jour du plan, des références LLD et des décisions ADR-008/ADR-009.

## 2026-09-15 — Cadrage continu et séparation des analyses

- Application du plan approuvé : 01 introduction, 02 FinOps, 03 méthodologie, 04 architecture, 05 réalisation, 06 analyse FinOps, 07 validation/performance, 08 coûts build/run, 09 discussion/recommandations, 10 conclusion.
- Renumérotation des fichiers et titres existants : ancien 03 FinOps → 02 ; 04 méthodologie → 03 ; 05 architecture → 04 ; 06 réalisation → 05. Ancien dossier 07_results → 07_performance, section 7.1 conservée.
- Mise à jour des renvois actifs, du plan d'assemblage et de l'organisation de l'introduction. Les entrées historiques de ce journal conservent leurs anciens numéros pour l'audit.
- Création de trames WORKING pour les analyses métier, le diagnostic PBI, la comparaison des architectures, les scénarios de coût, la discussion et la conclusion.
- Confirmation par l'étudiant de l'accès possible à PBI ; aucun benchmark exécuté à cette occasion. Aucun coût humain ni tarif de plateforme supposé.
- Aucun changement de code technique ; les observations locales ne sont pas transformées en gains métier ou de performance démontrés.
- Suppression des quatre anciens dossiers devenus vides après déplacement de leurs fichiers ; aucun contenu documentaire supprimé.

## 2026-09-15 — Bilan des apprentissages dans la conclusion

- Séparation du chapitre 10 en conclusion générale (10.1), bilan des apprentissages et acquis du master (10.2), perspectives (10.3).
- Ajout d'une matrice reliant PySpark, Databricks, lakehouse, NoSQL/données semi-structurées, sécurité, gouvernance/qualité et machine learning au projet.
- Distinction explicite entre usage de JSON et déploiement d'une base NoSQL, entre code prévu et validation effective, et entre prévision ML souhaitée et résultat évalué.
- Prévision de consommation enregistrée comme travail souhaité pendant le build ; cible et historique restent à préciser. Aucun modèle développé lors de cette mise à jour.
- Plan d'assemblage et organisation du mémoire mis à jour ; bilan personnel laissé à confirmer par l'étudiant.

## 2026-09-15 — Alignement problématique, modèle d'organisation et conclusion

- Ajout en section 1.3 des trois sous-problématiques complémentaires : fiabilité, self-service gouverné et aide à la décision FinOps. La question centrale existante est conservée.
- Ajout d'une trame de réponse axe par axe en section 10.1 : objectif, réalisation, preuve, limite et degré de réponse.
- Explicitation en section 4.2 de la production centralisée et consommation distribuée, sans assimiler self-service analytique et Data Mesh complet.
- Ajout au chapitre 9 des points de discussion sur les responsabilités et les dépendances centrales.
- Ajout de la référence professionnelle fondatrice de Dehghani (2020) à la bibliographie ; aucun changement d'implémentation ni nouveau résultat validé.

## 2026-09-15 — Précision du contexte FinOps et du circuit de modification

- Source : précision de l'étudiant dans la session mémoire. Le dashboard est utilisé par FinOps, la hiérarchie et des managers de domaines/sous-domaines d'autres équipes.
- Correction en section 1.2 et dans le cadrage actif de l'ancienne généralisation d'absence d'accès des managers ; note de remplacement ajoutée au cadrage historique v1 sans effacer son texte.
- Description du circuit rapporté : retours/validation du supérieur → transmission par la manager → modifications par un intervenant externe basé en Inde. Délais signalés mais non mesurés ; localisation non traitée comme cause.
- Création de la section 9.2 sur l'apport potentiel d'un Data Engineer intégré à FinOps, incluant réactivité, manipulation directe, capitalisation, coûts et conditions de gouvernance.
- Mise en relation avec les scénarios build/run du chapitre 8 ; aucune économie humaine ou amélioration de délai revendiquée comme démontrée.
