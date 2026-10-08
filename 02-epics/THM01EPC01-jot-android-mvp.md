THM01EPC01 — Jot Android MVP: notes, checklists and reminders

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[EPIC] THM01EPC01 — Jot Android MVP: notes, checklists and reminders
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Capability : THM01CAP01
Type              : Business
Product Stage     : MVP
Surfaces          : API / backend: Yes (component apis/jot-api)
                    Web UI: No
                    Mobile app: Yes (Android; cross-platform React Native, component mobile/jot)
                                iOS: Later (REL-1.1 — trigger: REL-1.0.0 released and Apple developer account in place)
Epic Owner        : Product Owner (@abalas4)
Architecture Lead : Architecture Lead (@abalas4)
Description       : Build the first release of Jot for Android: sign in with Google, write
                    colour-coded text notes and checklists, pin, archive and delete them with
                    undo, organise them with labels, search, sort and multi-select, and set
                    date / time reminders that arrive as notifications with Mark done, Snooze and
                    Open. Notes are stored by a small cloud API so they survive a reinstall or a new
                    phone. The owner is the only user; the design follows the Jot design system
                    (screens W1–W12).

Lean Business Case
  Problem Statement  : Notes, to-do lists and reminders are spread over several apps; reminders get
                       missed and notes are hard to find again.
  Solution Overview  : A React Native Android app (iOS-ready codebase) backed by a FastAPI service on
                       AWS Lambda behind API Gateway HTTP API, DynamoDB for storage and Cognito with
                       Google sign-in. Reminders are local notifications scheduled on the phone, so
                       they fire without a network connection. Online-only in the MVP (D-07).
  Leading Indicators : The owner creates notes in Jot on ≥ 5 of the first 7 days after install;
                       first reminders fire on time on the personal phone during UAT.
  Non-Financial      : One trusted place for notes and reminders; fewer forgotten tasks.
  Financial          : Run cost ≤ US$1 per month (AWS always-free tier + cents for API Gateway,
                       DynamoDB on-demand requests and ECR). Device Farm uses the one-time free
                       minutes (≈ 200 of 981.77 planned). Investment: the owner's time; no licences.
  Go/No-Go Threshold : 60 days after REL-1.0.0: ≥ 3 notes or checklists created per week, no data-loss
                       incident, and reminder reliability ≥ 95 %.
  Pivot/Persevere    : Persevere if the threshold is met. If notes are lost or edits fail because the
                       network drops, pivot to offline-first (L-01) before new features. Stop if
                       adoption stays < 1 note per week at 90 days.

MVP Definition    : REL-1.0.0 on Android: Google sign-in; text notes (8 colours, pin, archive, delete
                    with 5 s undo); checklists (check / uncheck, progress, reorder, hide / uncheck /
                    delete completed, convert); labels, search, filter, sort, multi-select bulk
                    actions, grid / list layout, drawer; reminders (quick picks, date, time, repeat),
                    Reminders tab, notification with Mark done / Snooze / Open, snooze presets.
                    Plain text only (D-09). Online-only with a clear offline state (D-07).
Out of Scope      : iOS release (REL-1.1); offline-first sync (L-01); rich-text formatting (L-02);
                    server push reminders (L-03); Cognito email / password accounts and account
                    linking (L-04); dark theme; tablet layout; sharing and collaborators; drawings,
                    images and voice notes; web client; location-based reminders; Play Store release
                    (deviation C-05).

Success Metrics   :
  - Notes + checklists created per week: 0 (new) → ≥ 5
  - Reminders firing within 1 min of the scheduled time: n/a (new) → ≥ 99 %
  - Crash-free users: n/a (new) → ≥ 99.5 %; Android ANR rate ≤ 0.47 %
  - API running cost: US$0 → ≤ US$1 per month (Device Farm excluded)

Benefit Measurement (operations 09-benefit-realisation.md §1):
  | Metric | Baseline (date, source) | Target | Data source | Owner | Checkpoints |
  |--------|-------------------------|--------|-------------|-------|-------------|
  | Notes + checklists created per week | 0 (2026-10-08, new product) | ≥ 5 | API metric `note_created` (count only — no content, no user identifiers) in CloudWatch | Product Owner (@abalas4) | 30 / 60 / 90 days after REL-1.0.0 |
  | Reminder on-time rate | to measure before release (UAT on personal phone) | ≥ 99 % within 1 min | Event `reminder_delivered` (delay in seconds only — no content); collection mechanism set in the HLD | Product Owner (@abalas4) | 30 / 60 / 90 days |
  | Crash-free users / ANR rate | to measure before release (UAT build) | ≥ 99.5 % / ≤ 0.47 % | Crash reporting (Crashlytics, no personal data) | Product Owner (@abalas4) | 30 / 60 / 90 days |
  | API running cost | US$0 (2026-10-08, AWS Billing) | ≤ US$1 / month | AWS Budgets alert + Cost Explorer, tag `service=jot-api` | Product Owner (@abalas4) | Monthly |
  | Leading: days with a note created in the first week | to measure at install | ≥ 5 of 7 | API metric `note_created` per day | Product Owner (@abalas4) | Day 7 |
  Pivot/Persevere decision : Pending

Compliance Regimes : None — personal, single-user app with no public distribution. Privacy & Data
                     Protection is still assessed as an NFR (row 15). Revisit trigger: before any
                     public distribution of the app.

WSJF Score        :
  User/Business Value   : 9
  Time Criticality      : 5
  Risk Reduction / OE   : 4
  Job Size              : 8
  WSJF                  : (9+5+4)/8 = 2.25   (proposed; Product Owner confirms at PI Planning)

Sizing            : M
PI Target         : PI-1
ART(s)            : Jot team (solo)
Linked Features   : (step 1.2)
                    Business:        THM01FTR01 Sign in with Google and account session
                                     THM01FTR02 Text notes
                                     THM01FTR03 Checklists
                                     THM01FTR04 Labels and navigation drawer
                                     THM01FTR10 Search, sort, filter and multi-select
                                                (split from "Organise and find" — two user journeys)
                                     THM01FTR05 Reminders and notifications
                    Implementation:  THM01FTR06 Jot API service foundation
                    Non-Functional:  THM01FTR11 Security baseline · THM01FTR12 Performance SLOs
                                     THM01FTR13 Availability and reliability · THM01FTR14 Observability and monitoring

Dependencies      : THM01EPC02 — CI pipeline, emulator / phone / Device Farm test runs and the dev
                    AWS environment must exist before the first Story can reach Done.
                    Google Cloud OAuth client (created by the owner) for sign-in.
Constraints       : React Native bare CLI + TypeScript (D-01); Appium Python + Espresso tests (D-02);
                    Python 3.13 FastAPI on Lambda arm64 + HTTP API (D-03); DynamoDB (D-04); Cognito
                    with Google federation (D-05); local notifications (D-06); online-only (D-07);
                    plain text (D-09); Snooze opens the W12 sheet (D-10); no Play Store — Story Done =
                    emulator matrix → personal phone + UAT → Device Farm (C-05); AWS always-free first;
                    stable versions only; public repository.
Risks             :
  - Risk 1: Local-notification library may not support the chosen React Native version (R-NOTIF)
    | L: M | I: H | Mitigation: dependency vetting before LLD approval; fallback library or a small
    native AlarmManager module (ADR)
  - Risk 2: Android 14+ denies exact alarms by default, so reminders fire late | L: H | I: H |
    Mitigation: in-context permission rationale; inexact fallback with a visible message; DFMEA row
  - Risk 3: Online-only MVP loses an edit when the network drops | L: M | I: H | Mitigation: writes
    fail visibly with Retry and the editor keeps unsaved text; optimistic concurrency (409 + reload)
  - Risk 4: Lambda container cold start makes the app feel slow | L: M | I: M | Mitigation: arm64,
    slim image, lazy imports; NFR p95 < 1 s cold / < 300 ms warm
  - Risk 5: Device Farm free minutes run out | L: L | I: M | Mitigation: emulator → phone gate before
    any Device Farm run; minutes guard; paid runs off by default

Requirement Coverage Assessment — THM01EPC01                         Product Stage: MVP
  | Type / Category | Status | Artefact ID(s) | Owner | Review / Trigger | Note (target, reason) |
  |---|---|---|---|---|---|
  | Functional | Defined | THM01FTR01–THM01FTR05, THM01FTR10 | Product Owner (@abalas4) | Step 1.2 | Scope = MVP Definition above; screens W1–W12 |
  | Technical / Enabler | Defined | THM01FTR06; THM01EPC02 | Architecture Lead (@abalas4) | Step 1.2 | API foundation here; delivery runway in THM01EPC02 |
  | Data | Evolving | — | Architecture Lead (@abalas4) | Step 1.7 (HLD) | Note, checklist, label, reminder entities with `version`, `updatedAt`, soft delete; retention TBD |
  | Interface & Integration | Evolving | THM01FTR06 | Architecture Lead (@abalas4) | Step 1.7 (LLD, OpenAPI 3.1) | REST API `jot-api`; Cognito + Google sign-in; OS notifications |
  | Transition & Migration | N/A | — | Architecture Lead (@abalas4) | — | New product, no existing data. Item-schema-version migration tests cover future changes (C-09) |
  | Constraints | Defined | Epic `Constraints` field | Product Owner (@abalas4) | — | See field |
  | 1 Performance | Evolving | THM01FTR12 | Architecture Lead (@abalas4) | HLD approval (1.7) | Initial: API p95 < 300 ms warm / < 1 s cold; app cold start ≤ 2 s on the low-end tier; screen transition ≤ 300 ms |
  | 2 Scalability | Deferred | — | Architecture Lead (@abalas4) | Before any public distribution | Single user; serverless scales on demand |
  | 3 Availability & Reliability | Evolving | THM01FTR13 | Architecture Lead (@abalas4) | HLD approval (1.7) | Initial: crash-free users ≥ 99.5 %; ANR ≤ 0.47 %; reminders on time ≥ 99 %; API availability target TBD |
  | 4 Security | Evolving | THM01FTR11 | Architecture Lead (@abalas4) | HLD approval (1.7) | Initial: OWASP MASVS L1; Cognito JWT on every API route; tokens in Keystore; TLS only; no secrets in the app or the repo; SCA + SAST + secrets scan on every build |
  | 5 Compliance & Regulatory | N/A | — | Product Owner (@abalas4) | Before any public distribution | Compliance Regimes: None (personal app) |
  | 6 Observability & Monitoring | Evolving | THM01FTR14 | Architecture Lead (@abalas4) | HLD approval (1.7) | Initial: structured JSON logs with traceId (CloudWatch), X-Ray traces, an alarm per SLO; crash reporting |
  | 7 Usability & Accessibility | Evolving | — | Product Owner (@abalas4) | Step 1.6a (style guide) | Initial: WCAG 2.1 AA applied to native (TalkBack labels, 48 dp targets, font scaling 200 %) |
  | 8 Maintainability | Evolving | — | Architecture Lead (@abalas4) | Step 1.2 | Initial: coverage ≥ 80 % new code; mutation ≥ 60 % business logic; no new Critical SAST findings |
  | 9 Portability & Interoperability | Evolving | — | Architecture Lead (@abalas4) | Step 1.7 (HLD platform scope) | Android minimum version TBD (target ≥ 95 % of devices); iOS-ready codebase; OpenAPI 3.1 |
  | 10 Disaster Recovery & BC | Evolving | — | Architecture Lead (@abalas4) | Step 1.7 (HLD) | Initial: DynamoDB point-in-time recovery in prod; RPO / RTO TBD |
  | 11 Data Quality & Integrity | Evolving | — | Architecture Lead (@abalas4) | Step 1.7 (LLD) | Idempotent writes; optimistic concurrency (version / If-Match → 409); validation at the API boundary |
  | 12 Capacity, Resource & Cost | Defined | Epic Success Metric | Product Owner (@abalas4) | Monthly | API cost ≤ US$1 / month; AWS Budgets alert; app download size budget TBD |
  | 13 AI / ML Fairness | N/A | — | — | — | No AI / ML in the product |
  | 14 Serviceability & Supportability | Evolving | — | Architecture Lead (@abalas4) | Step 6.1 (operations readiness) | Runbook per DFMEA failure mode with S ≥ 8; rollback = previous API image + hotfix APK |
  | 15 Privacy & Data Protection | Evolving | — | Product Owner (@abalas4) | Step 1.7 (HLD data inventory) | Data minimisation; no personal data in logs, metrics or notifications on the lock screen; delete-account path TBD |
  | 16 Localisation & i18n | N/A | — | Product Owner (@abalas4) | Before any public distribution | Single locale (English); strings still externalised |

ALM Status        : Portfolio Backlog
DoR Check         : ✅ Stored at 02-epics/THM01EPC01-<slug>.md
                    ✅ Parent Capability THM01CAP01 linked
                    ✅ Type Business
                    ✅ Lean Business Case complete (problem, solution, leading indicators, financial,
                       go / no-go threshold)
                    ✅ MVP definition written
                    ✅ Out of scope listed
                    ✅ Success metrics with baselines and targets
                    ✅ Benefit Measurement block (baselines "to measure before release" where new)
                    ✅ Compliance Regimes declared: None
                    ✅ Sized M
                    ✅ ≥ 3 Features identified (11 written at step 1.2)
                    ✅ Risks with likelihood / impact / mitigation
                    ✅ Product Stage MVP
                    ✅ Surfaces declared
                    ✅ Requirement Coverage Assessment present; Functional and the mandatory categories
                       (Security, Availability & Reliability, Observability, Performance) assessed
                    ✅ ART and PI target set
                    ✅ Epic Owner and Architecture Lead named
                    ✅ Portfolio Kanban approval — Product Owner approved and merged PR #1 (2026-10-08)
DoD Check         : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
