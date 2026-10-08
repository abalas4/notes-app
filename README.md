# Jot

A simple, colour-coded mobile app for capturing **notes**, **checklists** and **reminders**.
Android first, iOS later from the same React Native codebase, backed by a FastAPI service on AWS.

> **Status:** PI-1 in progress (2026-10-08 → 2026-12-16). Plans: [`00-planning/PI-1/`](00-planning/PI-1/),
> [`10-release/PI-1-release-roadmap.md`](10-release/PI-1-release-roadmap.md), RAID log
> [`00-planning/raid-log.md`](00-planning/raid-log.md). Architecture decisions: [`06-design/adr/`](06-design/adr/).
> How we work: [`CONTRIBUTING.md`](CONTRIBUTING.md).

## How this repository is organised

The project follows the SAFe ALM way of working and its mandatory folder structure:

| Folder | Contents |
|---|---|
| `00-planning/` | PI and iteration planning, RAID log |
| `01-strategy/` … `05-work-items/` | Strategic Themes, Epics, Features, Stories, Work Items |
| `06-design/` | HLD, DFMEA, LLD, ADRs, API specs, UX specs and style guide |
| `07-source-code-tests/` | Source (`src/`), tests (`tests/`), infrastructure as code (`infra/`), Docker Compose |
| `08-test-artefacts/` | Test plans, test cases, defects, closure reports |
| `09-documentation/` | User and API consumer documentation |
| `10-release/`, `11-operations/` | Release packs, SLOs, runbooks |
| `postman/`, `scripts/` | API collections, developer scripts |

A folder appears once it has content.

## Tech stack

React Native + TypeScript (Android) · Python FastAPI on AWS Lambda behind API Gateway HTTP API ·
DynamoDB · Cognito (Sign in with Google) · OpenTofu · GitHub Actions (OIDC, no stored AWS keys) ·
Espresso + Appium (Python) on emulator, a real phone and AWS Device Farm.

## One-time setup (owner)

GitHub settings (cannot be set from code):
- [ ] Branch protection on `main`: require a pull request, require status checks, block force-push and deletion, require conversation resolution
- [ ] Secret scanning and push protection: on
- [ ] Private vulnerability reporting: on (used by [`SECURITY.md`](.github/SECURITY.md))
- [ ] Actions: require approval for workflow runs from fork pull requests
- [ ] Environments `aws-admin`, `dev`, `prod`, `device-farm` with yourself as required reviewer (added when the workflows arrive)

Local:
- [ ] `pip install pre-commit` then `pre-commit install` in this folder (runs gitleaks before every commit)

AWS (later, when the infrastructure slice starts): the one-time `infra/envs/bootstrap` apply and the
SSM secret values, both with your own credentials. Everything else is created by GitHub Actions.

## Licence

Copyright © 2026 abalas4. All rights reserved.

The source is visible for reference only. No licence is granted to use, copy, modify or
distribute it.
