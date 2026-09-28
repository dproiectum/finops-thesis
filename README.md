# FinOps thesis

Le mémoire et ses documents de travail se trouvent dans [Memoire](Memoire/README.md).
Ce dépôt est l'unique dossier de travail pour le mémoire ; les projets techniques
possèdent leurs propres dépôts.

## Mise à jour

Depuis la racine de `finops-thesis`, avant de commencer sur un autre ordinateur :

```bash
git status
git pull --ff-only origin main
```

Après modification et vérification des documents :

```bash
git diff --stat
git add README.md Memoire
git commit -m "Update thesis manuscript"
git push origin main
```

Si `git status` indique des modifications locales, les conserver ou les valider
avant le pull. Ne pas forcer un push pour résoudre un conflit.
