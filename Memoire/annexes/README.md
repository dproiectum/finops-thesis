# Annexes et figures

Les annexes contiendront seulement des compléments lisibles dans le PDF final et cités depuis un chapitre. Le classeur `project_management/PFE_FinOps_Gantt_2026-09-28.xlsx` conserve une WBS de 34 tâches, un Gantt quotidien du 1er au 30 septembre et une vue hebdomadaire plus compacte. Pour le PDF, exporter la vue choisie avec sa légende et expliciter que les dates historiques sont des fenêtres documentaires reconstituées. Les étapes cloud du 27 septembre sont des points de compte rendu, pas des horodatages d'exécution vérifiés. L'ancien planning du 5 septembre est conservé séparément comme base historique.

Les fichiers d'images sont conservés sous `figures/` ; les schémas techniques du modèle de données sont rangés dans `figures/architectures/`. Leur emplacement ne détermine pas leur place dans le mémoire : la figure du FinOps Framework est insérée dans la section 2.1, et `figures/architectures/data_model.svg` est inséré dans la section 4.5.2 comme vue relationnelle du POC. Sa légende précise que les types de clés ne correspondent pas au DDL cloud.

Le schéma `finops_organizational_context.svg` et son export PNG sont insérés comme figure 1.1 dans la section 1.1. Ils montrent seulement la chaîne organisationnelle utile au sujet, sans reproduire les slides internes ni les noms individuels.

Le dossier `figures/architectures/` conserve le fichier source de cette figure. Sa lisibilité doit être vérifiée lors de l'assemblage du PDF A4 ; le diagramme contient beaucoup de colonnes et pourrait nécessiter une page paysage ou une version simplifiée. Ne pas déposer les images directement à la racine de `annexes/`.

Après exécution du protocole de la section 7.5, une annexe de preuve de sécurité pourra regrouper la matrice des personas synthétiques, les résultats automatisés et trois captures ciblées : vue globale FinOps, vue filtrée d'un Application Owner et refus d'un utilisateur sans habilitation. Elle devra identifier la révision Cloud Run et la période synthétique, sans afficher de secret, jeton, assertion IAP ou adresse personnelle réelle. Aucun de ces artefacts ne doit être présenté comme preuve tant que l'implémentation n'a pas été exécutée.
