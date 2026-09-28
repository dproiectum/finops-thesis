# Mémoire PFE — espace documentaire évolutif

## Dossier de travail unique et GitHub

Le dossier de travail est `PFE/finops-thesis/Memoire/`. Le dépôt Git se trouve
dans `PFE/finops-thesis/` et son origine est
`https://github.com/dproiectum/finops-thesis.git`. Modifier les documents dans
ce dossier uniquement ; ne pas recréer une copie parallèle `PFE/Memoire/`.
Les commandes `git status`, `git pull` et `git push` se lancent depuis la
racine du dépôt `finops-thesis`.

## Langue du document final

Le mémoire final, son plan d'assemblage et tous les fichiers de `chapters/` sont rédigés en anglais. Les échanges avec l'étudiant et les registres de travail internes peuvent rester en français ; ils ne sont pas assemblés dans le PDF. Toute nouvelle section destinée au mémoire doit être rédigée en anglais dès sa création.

## Code de rédaction du mémoire

- Appuyer les affirmations importantes sur les données du projet ou des sources vérifiées. Ne créer ni résultat, chiffre, citation, page, DOI ou référence. Distinguer observation, interprétation et incertitude.
- Rédiger en anglais académique précis, avec des verbes simples, des liens logiques explicites et les détails propres au projet. Éviter les formules promotionnelles, les transitions mécaniques et les perspectives non étayées.
- Donner une idée principale à chaque paragraphe. Utiliser titres, listes, tableaux et emphase seulement lorsqu'ils facilitent la lecture. Le texte assemblé ne doit contenir ni statut de travail, consigne de rédaction, espace réservé ou balise d'audit.
- Employer de façon cohérente la norme bibliographique imposée ; vérifier que chaque source existe et soutient la phrase citée. La norme exacte reste à confirmer avec l'étudiant (Q-007).
- Relire précision, cohérence, fluidité et fidélité aux sources avant livraison. Les informations personnelles sur le rôle et les apprentissages sont à confirmer (Q-013, Q-021) plutôt qu'à inventer.

## Statut

Le projet est en phase de construction. Les documents de ce dossier constituent une base de travail auditable : ils peuvent être corrigés, déplacés, fusionnés ou remplacés lorsque l'architecture et les résultats se stabilisent. Une note technique n'est pas automatiquement une affirmation validée pour le mémoire final.

## Règles de lecture

Les statuts documentaires utilisés sont :

| Statut | Signification |
|---|---|
| `WORKING` | Contenu en cours, susceptible de changer sans validation formelle |
| `OBSERVED` | Fait constaté et associé à une preuve identifiable |
| `DECIDED` | Décision prise, avec justification et conséquences documentées |
| `VALIDATED` | Résultat vérifié par un test reproductible ou validé par la personne compétente |
| `SUPERSEDED` | Contenu conservé pour l'audit mais remplacé par une version plus récente |
| `FINAL-CANDIDATE` | Texte relu pouvant rejoindre le mémoire final |

Une capacité prévue dans le HLD ne doit jamais être présentée comme implémentée. Une exécution locale ne prouve pas une intégration Databricks ou une aptitude à la production.

## Carte du dossier

| Zone | Rôle | État actuel |
|---|---|---|
| `plan/` | Exigences scolaires, cadrage, problématique et périmètre | Documents de travail à réconcilier avec le prototype |
| `chapters/` | Plan détaillé et notes destinées aux futurs chapitres | Structure mise à jour le 27 septembre 2026 ; matière première, pas encore prose finale consolidée |
| `audit/` | Décisions, preuves, questions et changements | Source de traçabilité transversale |
| `annexes/` | Compléments retenus pour le PDF et fichiers sources des figures | L'annexe de gestion de projet reste à rédiger ; les images sont rangées dans `annexes/figures/architectures/` même lorsqu'elles sont insérées dans un chapitre |
| `references/` | Guide officiel et bibliographie | Sources à citer et vérifier |
| `audit/00_technical_work_to_thesis_log.md` | Passage de relais entre la session technique et la session mémoire | Journal d'entrée partagé |

## Sources de vérité documentaires

- Le code, les configurations et les données de test décrivent l'implémentation courante.
- Les rapports de tests et artefacts référencés dans `audit/02_evidence_register.md` étayent les résultats.
- `audit/01_decision_register.md` explique pourquoi une option a été retenue ou abandonnée.
- Les sections 4.2 et 4.4 décrivent respectivement le HLD logique et le HLD physique, en distinguant cible, prototype et hors périmètre.
- Le code et les documents techniques du projet fournissent les détails d'implémentation ; aucun registre LLD distinct n'est maintenu dans ce dossier.
- Les chapitres synthétisent ces sources dans une argumentation académique.

## Cycle de mise à jour

1. Le travail technique produit un changement, une décision ou une mesure.
2. Une entrée est ajoutée au journal partagé.
3. Toute décision structurante reçoit un identifiant `ADR-xxx` dans le registre des décisions.
4. Toute affirmation mesurée reçoit un identifiant `EVD-xxx` dans le registre des preuves.
5. Le schéma d'architecture, la section de conception ou la documentation technique concernée est mise à jour.
6. Le contenu utile est intégré au chapitre pertinent avec ses limites.
7. Les contradictions et informations manquantes sont inscrites dans les questions ouvertes.

## Convention de nommage des briques du mémoire

Chaque fichier destiné à alimenter le PDF suit la convention :

```text
CC_SS_sujet_en_snake_case.md
```

- `CC` : numéro du chapitre ;
- `SS` : numéro de la section dans le chapitre ;
- `sujet_en_snake_case` reprend le titre anglais interne après le numéro, en minuscules, sans apostrophe ni ponctuation, avec des `_` entre les mots ;
- un éventuel troisième niveau est écrit `CC_SS_TT_sujet.md` ;
- le titre interne commence par le même numéro affichable, par exemple `# 5.3 — Databricks Cloud Data Platform` pour `05_03_databricks_cloud_data_platform.md`.

Les fichiers de gouvernance placés dans `audit/` utilisent un ordre propre (`00` à `99`) et ne sont pas assemblés directement dans le PDF. Les `README.md` restent non numérotés, car ils servent uniquement à naviguer dans les dossiers.

Le PDF final doit rester compréhensible sans accès aux fichiers `.md` ou `.sql` du projet. Une information indispensable à l'argumentation est expliquée dans le chapitre, accompagnée de sa figure ou de son tableau si cela aide la lecture. Un détail utile mais non indispensable peut être adapté en annexe, sous forme de contenu réellement lisible dans le même PDF ; l'annexe n'est pas une liste de chemins de fichiers. Un document externe public est cité selon la norme bibliographique retenue. Pour un document interne non accessible au jury, le mémoire intègre le contenu nécessaire sans dépendre d'un lien local. Les chemins et révisions du code restent dans le registre de travail `audit/07_technical_source_inventory_2026_09_27.md`, hors du PDF.

## Contrôles avant intégration au mémoire final

- Le choix technique répond-il à une exigence ou à une contrainte explicite ?
- Les alternatives réellement considérées sont-elles mentionnées ?
- La preuve est-elle reproductible et son périmètre correctement formulé ?
- Les résultats observés sont-ils séparés des bénéfices attendus ?
- Les limites, coûts et risques sont-ils exposés ?
- La version finale contient-elle une citation lorsque l'affirmation dépend d'une source externe ?
