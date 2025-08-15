# Contribuer à Obatis
- Branches: `staging` (par défaut), `main` (prod). PR obligatoires vers ces branches.
- Commits: Conventional Commits (feat|fix|chore|docs|test(scope): message).
- Tests & Lint: requis (voir CI). Couverture cible backend ≥ 70% (non bloquant au début).
- Pas de secrets/PII dans les PR (le job Guard refusera une fuite évidente).
- Toute modif DB => doc de migration dans la PR.
