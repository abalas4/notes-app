PI-1 objectives — Jot team

```
PI OBJECTIVES — PI-1 — Jot team                Release roadmap: 10-release/PI-1-release-roadmap.md
PI dates: 2026-10-08 → 2026-12-16 · Capacity: 00-planning/PI-1/capacity.md
Business Owner: Product Owner (@abalas4)
```

| # | Objective (business language, SMART) | Features | Committed / Uncommitted | Business Value planned (1–10) | Business Value actual (set at PI end) | Status |
|---|---------------------------------------|----------|-------------------------|-------------------------------|----------------------------------------|--------|
| 1 | By 2026-12-02 the Jot API runs in a container with health and readiness checks, one standard error body with request logging, a data layer that never loses a concurrent edit, and a published OpenAPI 3.1 contract checked by a contract test | THM01FTR06 (STR01, STR54, STR02, STR03) | Committed | 8 | — | On track |
| 2 | From iteration 01, no API change reaches `main` unless it passes the CI quality gates (types, lint, tests with coverage, dependency audit, secrets, SAST, image scan, SBOM) | THM01FTR07 (STR29) | Committed | 7 | — | On track |
| 3 | By 2026-11-04 the AWS account is bootstrapped as code: encrypted remote state with locking and the admin bootstrap, with no credentials in the repository | THM01FTR09 (STR36) | Committed | 5 | — | On track |
| 4 | Stretch: shared AWS prerequisites and the Cognito dev pool with Google sign-in exist, and the API rejects requests without a valid token | THM01FTR09 (STR37, STR40), THM01FTR01 (STR04) | Uncommitted | 6 | — | — |
| 5 | Stretch: every app change builds a debug APK in CI and passes the app quality gates | THM01FTR07 (STR30) | Uncommitted | 5 | — | — |

```
Predictability = Σ actual business value of committed objectives ÷ Σ planned business value of committed objectives
Planned (committed) = 8 + 7 + 5 = 20 · target 80–100 %
```

## Feature priority (WSJF) — PI-1 order

Scores from the Feature records (confirmed in PR #3). NFR Features ride with the Feature they protect.

| Rank | Feature | WSJF | PI-1 |
|---|---|---|---|
| 1 | THM01FTR01 Sign in with Google | 5.2 | STR04 stretch; rest PI-2+ (needs AWS prerequisites) |
| 2 | THM01FTR07 CI pipeline and quality gates | 5.0 | STR29 committed; STR30 stretch |
| 2 | THM01FTR09 AWS prerequisites as code | 5.0 | STR36 committed; STR37, STR40 stretch |
| 4 | THM01FTR02 Text notes | 4.6 | PI-2+ |
| 4 | THM01FTR06 Jot API service foundation | 4.6 | **All Stories committed** — every dependant needs it first |
| 6 | THM01FTR08 Test-execution workflows | 4.0 | PI-2+ |
| 7 | THM01FTR05 Reminders and notifications | 3.67 | PI-2+ |
| 8 | THM01FTR03 Checklists | 3.4 | PI-2+ |
| 9 | THM01FTR04 Labels and navigation drawer | 3.0 | PI-2+ |
| 10 | THM01FTR10 Search, sort, filter, multi-select | 2.75 | PI-2+ |
| — | THM01FTR11–14 (NFR) | with their Features | PI-2+ |

THM01FTR06 is taken ahead of higher-WSJF Features because they all depend on it (an Enabler takes its
dependants' Time Criticality — 10-pi-planning.md §2).

## Agreements

| Date | Agreement | Agreed by |
|---|---|---|
| 2026-10-08 | Tech-debt share 5 % in PI-1 (below the 15–20 % default): greenfield codebase with no debt yet; returns to 15 % from PI-2 | Product Owner, Architecture Lead (@abalas4) — RTE and System Architect roles held by the same person |
| 2026-10-08 | Committed load 22 pts against the new-team baseline; REL-1.0.0 date re-forecast after iteration 03 velocity | Product Owner (@abalas4) |

## Confidence vote

Fist of five: — (recorded when the PI-1 plan PR is approved; < 3 → re-plan)
