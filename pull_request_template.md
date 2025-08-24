# PR — Gabarit Obatis

### ✅ Checklist — Conventions de branches

- [ ] **Conventions respectées** :
      `feat/<kebab-case>` | `fix/<kebab-case>` | `chore/<kebab-case>` |
      `docs/<kebab-case>` | `refactor/<kebab-case>` | `infra/<kebab-case>`
      (suffixe optionnel `-gh<issueId>`)
- Branche (copier-coller ici) : `...`
- Règles *Branches* :
  <https://github.com/Obatis/obatis-ops/blob/staging/docs/policies/branches.md>

---

## Contexte

**Issue liée** : #  
**ADR / décision** :  
**Scope principal** : Backend (Laravel/API) | Frontend (FlutterFlow) |
DB (PostgreSQL) | Infra/DevOps (Nginx, Docker, Ploi, CI/CD) |
IA/Workers (DeepSeek, Whisper, OCR) | Stockage (Wasabi/Bunny) | Sécurité/RGPD

---

## Inter-repo — PR liées / Depends on

> **Quand l’évolution touche plusieurs dépôts**, lister ici les PR sœurs (une par ligne).  
> **Formats supportés** : `owner/repo#123` · `#123` (même dépôt) · URL complète `https://github.com/owner/repo/pull/123`  
> Laisser vide si aucune dépendance.

<!-- linked_prs:start -->

<!-- linked_prs:end -->

**Meta-PR (coordination multi-repos, optionnel)** : Obatis/obatis-ops#  

---

## Impacts

- [ ] Breaking change
- [ ] Migrations DB (idempotentes + rollback)
- [ ] API publique (OpenAPI changée)
- [ ] Performance (indexes, N+1, caches)
- [ ] Sécurité (RBAC, secret handling, scopes)
- [ ] Observabilité (logs/metrics/traces)
- [ ] Compat Octane/RoadRunner (pas d’état global, pas de singletons mutables)
- [ ] Env/Config à ajuster (feature flags, variables)

**Détails d’impact** (modules/services touchés, risques business) :

---

## Critères d’acceptation

**CA-1 :**
- Given
- When
- Then

**CA-2 :**
- Given
- When
- Then

---

## Notes de test manuels (facultatif)

---

## Checklist CI

### Conventions

- [ ] *Conventional Commits* + *SemVer* appliqués  
      Règles :
      <https://github.com/Obatis/obatis-ops/blob/staging/docs/policies/commits-and-versioning.md>

### Qualité & Tests

- [ ] Linter/formatters OK (ex. PHP-CS-Fixer, ESLint)
- [ ] Tests unitaires/intégration ajoutés ou mis à jour
- [ ] Couverture ≥ 70 % backend (vérifiée par CI)
- [ ] E2E/contract tests pertinents (si API/flows)

### Build & Déploiement

- [ ] Build Docker local OK (si applicable)
- [ ] Workflows GitHub Actions verts
- [ ] Artefacts/versioning mis à jour (si applicable)

### Base de données

- [ ] `migrate` passe en staging
- [ ] `migrate:rollback` testé et documenté
- [ ] Indexes/constraints ajustés si besoin

### Sécurité & RGPD

- [ ] Aucun secret en dépôt / `.env` non committé
- [ ] RBAC/permissions revues (routes, policies, gates)
- [ ] Données perso : minimisation / masquage logs / rétention

### Perf & Observabilité

- [ ] Revue N+1 / requêtes lourdes
- [ ] Métriques/labels Prometheus ajoutés/MAJ
- [ ] Logs structurés (niveau, contexte) conformes

### Documentation

- [ ] OpenAPI/Swagger mis à jour
- [ ] Docusaurus (guides, runbooks) mis à jour
- [ ] ADR rédigée/complétée si décision d’architecture

### Gouvernance PR

- [ ] Labels appliqués (type, scope, priorité)
- [ ] CODEOWNERS requis ajoutés comme reviewers
- [ ] Changelog/Release notes préparés (si release)

---

## Risques / Rollback

**Risques identifiés** :

**Plan de rollback clair :**  
> Étapes : `php artisan down` (si nécessaire) → `migrate:rollback` →
> revert commit → `php artisan up`  
**Feature flag / kill-switch** :  
**Données à restaurer / scripts de correction** :

---

## Liens docs

**Issue / Carte** :  
**ADR** :  
**OpenAPI** :  
**Runbook / SOP** :  
**Dashboard staging / page de test** :  
**Logs/alertes (Sentry/Grafana/Prometheus)** :
