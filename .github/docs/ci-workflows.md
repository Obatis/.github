📄 Documentation – CI/CD Workflows (Obatis)
1. Objectif

Mettre en place une intégration continue (CI) homogène sur tous les dépôts applicatifs (backend, frontend, infra, ops) en centralisant la logique de test et de lint dans un seul repo de référence : Obatis/.github.

2. Fonctionnement général
A. Workflows réutilisables

Définis dans Obatis/.github/.github/workflows/.

Contiennent toute la logique CI pour chaque type de projet (PHP/Laravel, Flutter, Ansible, Ops).

Déclarés avec on: workflow_call, ce qui permet à d’autres repos de les invoquer.

Noms de jobs stables (backend-ci, frontend-ci, infra-ci, ops-ci) → utilisés comme required checks dans la protection de branches.

B. Callers

Placés dans chaque repo applicatif (obatis-backend, obatis-frontend, obatis-infra, obatis-ops).

Emplacement : /.github/workflows/ci.yml.

Ces fichiers sont très courts : ils définissent les déclencheurs (push, PR, manual dispatch) et appellent les workflows réutilisables avec la syntaxe :

uses: Obatis/.github/.github/workflows/<ci-*.yml>@main


Ajoutent une logique de sécurité légère :

Concurrency (annule les runs obsolètes).

Ignore les PR en brouillon.

Permissions minimales (read + write PR/checks).

3. Emplacements
Repo central Obatis/.github
.github/workflows/
 ├── ci-backend-laravel.yml   # tests Laravel (PHP 8.3, Pest, Pint, Larastan, coverage)
 ├── ci-frontend-flutter.yml  # analyse & tests Flutter (stable channel)
 ├── ci-infra-ansible.yml     # lint Ansible + Yamllint (+ Molecule optionnel)
 ├── ci-ops.yml               # lint markdown, link check, build docs (Docusaurus)
 └── autres gardes & utilitaires (lint-actions, org-policies-guard, etc.)

Repos applicatifs

obatis-backend/.github/workflows/ci.yml

obatis-frontend/.github/workflows/ci.yml

obatis-infra/.github/workflows/ci.yml

obatis-ops/.github/workflows/ci.yml

Chaque fichier ci.yml contient le déclencheur et appelle le bon workflow réutilisable.

4. Choix & justification

Centralisation dans /.github :
Permet de maintenir un seul jeu de workflows complexes.
→ Gain de temps, cohérence entre projets.

Callers minces :
Chaque dépôt applicatif reste simple, mais déclenche la bonne CI.
→ Les devs voient tout de suite que “CI = ce fichier” sans logique lourde.

Noms stables de jobs :
(backend-ci, frontend-ci, infra-ci, ops-ci) → pratiques pour mettre en place des branch protections.

Sécurité :

Pas de secrets hérités dans les PR → réduit les risques sur les forks.

Permissions minimales → GitHub Actions “least privilege”.

Extensibilité :

Possibilité d’ajouter un tag v1 sur /.github → callers utiliseront @v1 pour figer une version.

Facile d’ajouter d’autres workflows (ex. ci-mobile.yml) si besoin.

5. Notes de dev

Runners : les jobs tournent par défaut sur [self-hosted, linux, staging].
Si besoin de GitHub-hosted, passer runner_label: ubuntu-latest depuis le caller.

Artefacts :

Backend → coverage.xml + junit.xml.

Frontend → coverage/lcov.info.

Ops → site-build.zip si Docusaurus détecté.

Options paramétrables (via inputs):

Backend → version PHP.

Frontend → channel Flutter.

Infra → activer/désactiver Molecule.

Ops → activer markdown lint, link check, build docs.

PR brouillon : les jobs sont ignorés pour éviter le bruit.

Concurrence : un run annule le précédent sur la même PR/ref → économie de runners.

Required checks recommandés (staging + main) :

backend-ci

frontend-ci

infra-ci

ops-ci

éventuellement guard (org policies).
