# Conventions de branches — Obatis

## Objectif
Uniformiser les noms de branches pour améliorer la lisibilité, la recherche, les rapports et l’automatisation (labels, CI/CD, revues).

## Périmètre
S’applique à **tous les dépôts** du projet Obatis.

## Branches protégées
- `main` : production
- `staging` : pré-production / validation

> Les développements partent de **`staging`** (sauf automation explicitement autorisée).

## Format de nommage
Préfixe “type” obligatoire, puis un nom en **kebab-case** (minuscules, chiffres, tirets).
- **Types autorisés** : `feat/`, `fix/`, `chore/`, `docs/`, `refactor/`, `infra/`
- **kebab-case** : `a–z`, `0–9`, `-` (pas d’espaces, pas d’accents, pas d’underscore)

**Motif général :**
```
<type>/<kebab-case>[-gh<issueId>]
```
- Le suffixe `-gh<issueId>` est **optionnel** pour référencer une issue GitHub (ex. `-gh42`).

**Regex d’exigence :**
```
^(feat|fix|chore|docs|refactor|infra)\/[a-z0-9]+(?:-[a-z0-9]+)*(?:-gh[0-9]+)?$
```

## Exemples
✅ Valides
- `feat/gestion-avenants`
- `fix/export-compta-arrondi`
- `docs/procedure-backup`
- `refactor/service-auth-tokens`
- `infra/observabilite-grafana`
- `feat/creation-devis-rapide-gh128`

❌ Invalides (et pourquoi)
- `feature/gestion-avenants` (type inconnu)
- `feat/Gestion-Avenants` (majuscules)
- `feat/gestion_avenants` (underscore)
- `feat/` (vide)
- `hotfix/...` (type non autorisé)

## Flux de travail recommandé
1. **Créer** une branche depuis `staging`  
   ```
   git checkout staging && git pull
   git checkout -b feat/gestion-avenants
   ```
2. **Commits** petits et clairs (1 sujet par branche).
3. **Ouvrir une PR vers `staging`** (brouillon si incomplet).  
   La CI vérifie le nom de la branche et applique le label `type:*`.
4. **Revue & tests** → merge (**squash** recommandé).  
   Les branches fusionnées sont **supprimées**.

## Liens avec les labels
- Le préfixe de la branche détermine automatiquement le label `type:*` :
  - `feat/*` → `type:feat`
  - `fix/*` → `type:fix`
  - `chore/*` → `type:chore`
  - `docs/*` → `type:docs`
  - `refactor/*` → `type:refactor`
  - `infra/*` → `type:infra`

> Les labels `risk:*` et `area:*` sont ajoutés **manuellement** (ou par d’autres règles/outils).

## Exceptions
- Cas d’urgence : utiliser `fix/...` en respectant le format (pas de `hotfix/`).
- Si un besoin ponctuel sort du cadre, ouvrir une issue pour ajuster ces conventions.

## Bonnes pratiques
- Noms **courts et descriptifs** (≈ 5–6 mots max).
- Éviter les termes vagues : préférer `fix/404-sur-factures` à `fix/bug`.
- **1 PR = 1 sujet** ; si la branche dérive, scinder.
