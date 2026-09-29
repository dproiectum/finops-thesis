# Plan des illustrations du mémoire — mise à jour du 29 septembre 2026

Document de travail pour les dix chapitres et leurs 40 sections. Le nom du fichier conserve sa date de création. Après la relecture de condensation du 29 septembre, une figure n'est retenue que si les relations, la structure ou la comparaison deviennent nettement plus compréhensibles qu'avec un court texte ou tableau. Les légendes seront en anglais académique. Une configuration ou une maquette ne prouve pas une exécution.

Contrainte de travail indiquée par l'étudiant : 60 pages ; le guide scolaire recommande environ 50 pages de corps de texte, hors compléments. Le décompte réel dépendra de l'assemblage. La sélection ci-dessous prévoit trois schémas d'architecture/modèle, une seule capture de dashboard et, si les mesures le justifient, un graphique économique. Ce n'est pas un quota à remplir. Aucune image n'est encore insérée dans les chapitres. `annexes/figures/architectures/FinOps.png` et `FinOps.svg` restent des candidats à vérifier contre le modèle cloud.

## Figures retenues pour le corps du mémoire

| ID | Emplacement précis | Figure et message | Origine et état |
|---|---|---|---|
| F2 | § 4.2, sous « Logical flow », en remplacement du bloc texte vertical | Architecture **logique** : source, conservation de la preuve, ingestion et traçabilité, porte du contrat, Silver canonique, Gold et datamarts, consommation ; qualité, audit et contrôle d'accès traversent le flux. | Dessin original possible à partir du texte et de la documentation du projet. Aucun logo ou capture fournisseur nécessaire. |
| F3 | § 4.4.1, en remplacement du bloc texte de l'architecture physique | Architecture **physique** : générateur indépendant, GCS RAW partagé, `finops_raw.landing`, `finops_dev`, `finops_prod`, `finops_ops.audit`, traitements et SQL Warehouse/App. Garder le schéma indépendant du choix régional et des résultats de coût ; marquer le chemin App comme implémenté mais en attente de validation d'exécution. | Dessin original possible à partir de `FinOps Cloud Data Platform/docs/architecture.md` et du § 4.4. Pas de capture cloud requise pour un schéma de conception. |
| F4 | § 4.5.2, après l'inventaire des tables Gold | Schéma relationnel simplifié du modèle Gold : `fact_finops_cost_usage`, dix dimensions, pont ressource/tag ; clés et grain d'une ligne de charge. L'image source est rangée dans `annexes/figures/architectures/`, puis insérée dans le chapitre, car elle est nécessaire pour comprendre le modèle. Un schéma physique complet n'irait en annexe que s'il apporte un détail utile sans répéter F4. | `FinOps.png` et `FinOps.svg` sont des candidats disponibles. Confronter leurs tables, clés et relations au SQL cloud et à l'inventaire du § 4.5 ; ne pas les insérer comme modèle cloud si elles décrivent seulement le POC. |
| F5 ou C5 | § 5.2.3 **ou** § 5.3.5 | **Une seule** capture lisible du produit : période, filtres et KPI. Privilégier l'application cloud si son déploiement, ses pages et permissions sont vérifiés ; sinon retenir le POC local vérifié de janvier 2025. | Indiquer explicitement environnement, données synthétiques et date de capture. Ne pas présenter le POC comme Databricks App. Une seconde capture va en annexe seulement si elle montre une différence utile. |
| C8 | § 8.3.3 | Un graphique du coût total et de la durée par même unité de travail, si une comparaison contrôlée existe. Ventiler DBU et infrastructure Classic sans compter une seconde fois les VM incluses dans Serverless. | Uniquement après rapprochement des consommations Databricks/GCP, tarifs datés et attribution du cluster partagé. Si quelques valeurs sont mieux présentées dans un tableau, ne pas ajouter de graphique. Le § 8.4 renvoie à cette comparaison sans la répéter. |

F2–F4 expliquent une structure et ses relations ; la capture du dashboard montre un produit effectivement exécuté. C8 ne devient un résultat qu'avec des mesures comparables. Les identifiants conservés évitent de renuméroter les remarques restantes ; les propositions supprimées ne sont plus des éléments à préparer.

## Chapitre 3 : aucune illustration supplémentaire

Les six remarques d'illustration sont retirées du chapitre 3. Le tableau déductif du § 3.1 et le texte condensé suffisent à expliquer le dataset, la gouvernance, la progression POC/cloud, l'analytique et le produit. Pas de frise pour deux périodes déjà précisées en quelques lignes, ni de schéma répétant ces étapes. Les relations de tables restent illustrées au § 4.5.2.

## Preuves à conserver en annexe si elles apportent un complément

| ID | Emplacement | Condition et contenu |
|---|---|---|
| C4 / F8 | Renvoi depuis les § 5.3 et 7.4 | Graphe réellement exécuté du Job et résultats de contrôles, avec Job/Run IDs, révision, périodes, lignes et `BilledCost`. Conserver le tableau de validation dans le corps ; ne pas le répéter en image. Une icône de succès seule ne prouve pas la réconciliation. |
| C6 | Renvoi depuis le § 7.2 | Capture ciblée de Performance Analyzer uniquement si elle complète des mesures autorisées. Le protocole et quelques valeurs se présentent dans un tableau compact ; aucune capture générale du rapport n'est nécessaire. |

## Relecture de toutes les sections

La mention « sans figure » signifie que le passage est mieux servi par son texte ou tableau actuel ; ce n'est pas un manque à remplir par une photo décorative.

| Chapitre | Sections relues et décision |
|---|---|
| **1–3. Introduction, FinOps et méthode** | Pas de nouvelle figure. Le processus métier, les définitions et la méthode sont compréhensibles dans le texte et les tableaux. |
| **4. Architecture** | **4.1** Sans figure : les exigences sont déjà classées. **4.2** F2, schéma logique. **4.3** Conserver le tableau de synthèse sans score inventé. **4.4** F3, schéma physique distinct de F2. **4.5** F4 pour les relations Gold ; la correspondance datamart/question métier reste un tableau. |
| **5. Réalisation** | Une capture du dashboard : F5 **ou** C5. Le graphe de tâches réellement exécuté va en annexe si utile, pas dans un second schéma d'architecture. |
| **6. Analyse FinOps** | Pas de graphique pour répéter quatre montants ou deux pourcentages déjà expliqués. Conserver les valeurs, les dénominateurs et leurs limites dans le texte ou un tableau compact. |
| **7. Validation et performance** | Tableaux de résultats dans le corps, preuves primaires ciblées en annexe. Une éventuelle comparaison économique est illustrée une seule fois en chapitre 8. |
| **8. Coût de la plateforme** | **8.1** Sans figure : préciser la frontière économique en texte/formule. **8.2** Tableau d'effort seulement après journal et taux autorisé ; pas d'histogramme vide. **8.3** C8 après factures et unités comparables. **8.4** Même C8, sans seconde figure redondante ; le tableau des leviers existe déjà. |
| **9. Discussion** | Pas de nouvelle figure : interpréter les résultats et discuter le processus sans schéma redondant. |
| **10. Conclusion** | **10.1–10.3** Aucune nouvelle figure : conclure, expliciter les apprentissages vérifiés et les travaux futurs à partir des résultats déjà présentés. |

## Recherche demandée à l'étudiant

**Priorité 1 — preuve cloud (F8).** Rassembler les captures ou exports des Jobs de backfill DEV et PROD (Job ID, Run ID, date, statut, tâches, commit exécuté), les résultats SQL ou exports pour chaque mois (`row_count`, `BilledCost`, statut de réconciliation) et les enregistrements `finops_ops.audit` correspondants. Pour la validation Daily/clôture, fournir aussi un run DEV → PROD, un rejeu, et les snapshots `BEFORE/SOURCE/AFTER` si ces expériences ont réellement eu lieu. Indiquer la région, le type de compute et le mois source. Les valeurs sensibles peuvent être masquées, mais les identifiants nécessaires à la traçabilité doivent rester consignés dans un registre privé.

**Priorité 2 — interfaces réelles (C5, C6).** Pour la Databricks App, capturer une page représentative après déploiement avec date, environnement, filtres et valeurs, ainsi que la preuve d'un accès autorisé en lecture si ce test est fait. Pour Power BI, recueillir les mesures Performance Analyzer avec page, filtres, version, mode de connexion, cache et répétitions ; une capture ciblée reste un complément éventuel d'annexe. Ne pas envoyer de factures réelles ni d'identifiants personnels visibles dans les images du mémoire.

**Priorité 3 — coûts propres à la plateforme (C8).** Extraire, pour des runs équivalents, les durées, DBU et montants Databricks avec Job/Run ou cluster ID ; récupérer la part GCP Compute Engine, disques, réseau et stockage liée au Classic, puis l'usage du SQL Warehouse et des données stockées. Fournir les tarifs datés, devise, crédits/discounts et la règle qui attribue le coût d'un cluster partagé. Sans ces éléments, C8 reste un protocole de mesure.

**Priorité 4 — processus métier.** Confirmer la chaîne réelle d'une demande de modification du rapport : qui formule, valide, transmet, développe, teste et accepte ; obtenir, si possible, quelques dates et temps actifs d'exemples comparables. Cette collecte étaye le texte, sans imposer d'image supplémentaire.

## Règles de préparation finale

- Dessiner les schémas et graphiques en vectoriel ou en haute résolution ; captures recadrées sur le résultat, avec police lisible à l'impression.
- Dans la légende anglaise : nom de l'objet, environnement, période, source vérifiable, et mention « synthetic » quand le corpus est généré. Décrire les conventions de flèches et les étapes non encore validées dans la figure ou son commentaire.
- Éviter les photos génériques de cloud, de serveurs ou de bureaux et les logos décoratifs. Une capture d'interface ou d'exécution vaut seulement pour l'état précis qu'elle montre.
- Ne pas mettre d'artefact provisoire ou de note éditoriale dans les chapitres publiés. Le présent plan garde les demandes de collecte et les conditions de publication hors du corps du mémoire ; les commentaires HTML des sources doivent être masqués ou retirés à l'export.
