Release plan — REL-1.0.0

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RELEASE PLAN — REL-1.0.0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Status             : Draft   (05-release-types-and-cadence.md §6)
Release Train / PI : Jot / PI-1 (forecast; delivery spans later PIs) — roadmap: 10-release/PI-1-release-roadmap.md
Release Manager    : Release Manager (@abalas4)
Target date / window: TBD — re-forecast at the iteration 03 review (2026-11-18) from measured velocity
Type               : Planned
Cadence            : PI train
Branches           : release line none (trunk-based; tag on main)
Git tag            : REL-1.0.0 on the deployed commit (created by the release stage)
Merge-back         : N/A (Planned)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

The MVP release of Jot for Android (THM01EPC01 MVP Definition) with the delivery automation of
THM01EPC02. Every Story of THM01 is forecast to it; Stories slip to a later release only with a reason
recorded in the roadmap.

## Scope (forecast — 72 Stories)

| Story | Feature | Type (New/Mod/Hotfix) | Status | Components |
|-------|---------|-----------------------|--------|------------|
| THM01STR04 Authenticate requests and resolve the current user | THM01FTR01 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR05 Sign in with Google screen | THM01FTR01 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR06 Restore session on launch | THM01FTR01 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR55 Sign out from Settings | THM01FTR01 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR07 Create a note | THM01FTR02 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR08 Update a note with optimistic concurrency | THM01FTR02 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR09 Home screen with pinned and other notes | THM01FTR02 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR10 Note editor with autosave, colour, pin and archive | THM01FTR02 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR11 Delete a note with five-second undo | THM01FTR02 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR56 List notes with paging | THM01FTR02 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR57 Soft delete and restore a note | THM01FTR02 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR58 Archive view | THM01FTR02 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR12 Checklist items on notes | THM01FTR03 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR13 Checklist editor with progress | THM01FTR03 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR14 Reorder checklist items | THM01FTR03 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR59 Convert between text and list notes | THM01FTR03 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR60 Completed-item list actions | THM01FTR03 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR61 Convert between list and text in the app | THM01FTR03 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR15 Create, rename and delete labels | THM01FTR04 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR16 Label picker with inline create | THM01FTR04 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR17 Edit labels screen | THM01FTR04 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR18 Navigation drawer with labels and counts | THM01FTR04 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR62 Assign labels to a note | THM01FTR04 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR23 Set, change and remove a reminder | THM01FTR05 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR24 Add or edit a reminder | THM01FTR05 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR25 Schedule reminders as local notifications | THM01FTR05 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR26 Reminder notification content and Mark done | THM01FTR05 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR27 Reminders tab | THM01FTR05 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR28 Notification and exact-alarm permission flow | THM01FTR05 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR64 Complete, snooze and list reminders | THM01FTR05 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR65 Snooze and open from a notification | THM01FTR05 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR66 Reminder row actions | THM01FTR05 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR01 API service skeleton with health and readiness | THM01FTR06 | New | Planned in PI-1 | apis/jot-api |
| THM01STR02 DynamoDB repository layer with optimistic concurrency | THM01FTR06 | New | Planned in PI-1 | apis/jot-api |
| THM01STR03 OpenAPI 3.1 contract and contract test | THM01FTR06 | New | Planned in PI-1 | apis/jot-api |
| THM01STR54 Standard error body and request logging | THM01FTR06 | New | Planned in PI-1 | apis/jot-api |
| THM01STR29 API CI quality gates | THM01FTR07 | New | Planned in PI-1 | apis/jot-api |
| THM01STR30 App CI gates and debug build | THM01FTR07 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR31 Infrastructure and supply-chain gates | THM01FTR07 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR67 Release-hardening signed build workflow | THM01FTR07 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR32 Emulator tests workflow | THM01FTR08 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR33 Phone build and test script | THM01FTR08 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR34 Device Farm workflow with gate and guard rails | THM01FTR08 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR35 Dev environment up and down workflows | THM01FTR08 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR68 Install the CI build for a commit | THM01FTR08 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR36 One-time bootstrap root | THM01FTR09 | New | Planned in PI-1 | apis/jot-api |
| THM01STR37 Shared AWS prerequisites workflow | THM01FTR09 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR38 Per-workflow roles and permissions boundary | THM01FTR09 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR39 Lambda and HTTP API environments as code | THM01FTR09 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR40 Cognito user pools with Google sign-in | THM01FTR09 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR41 Production deploy workflow | THM01FTR09 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR69 Data table and alarms as code | THM01FTR09 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR70 Weekly drift check | THM01FTR09 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR19 Search, filter and sort notes | THM01FTR10 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR20 Batch update and delete notes | THM01FTR10 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR21 Search notes and filter by label chips | THM01FTR10 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR22 Multi-select with bulk actions | THM01FTR10 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR63 Sort sheet and grid or list layout | THM01FTR10 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR42 API authorisation and DAST baseline | THM01FTR11 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR43 App MASVS L1 controls | THM01FTR11 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR44 API throttling and request limits | THM01FTR11 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR45 API latency under load | THM01FTR12 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR46 Lambda cold start budget | THM01FTR12 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR47 App cold start and main-thread hygiene | THM01FTR12 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR71 Scroll, search and transition performance | THM01FTR12 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR48 Reminder delivery reliability | THM01FTR13 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR49 Crash and ANR budget with crash reporting | THM01FTR13 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR50 API fault handling and durability | THM01FTR13 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR51 Structured logs, traces and log hygiene | THM01FTR14 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR52 Metrics and SLO alarms | THM01FTR14 | New | Forecast (PI-2+) | apis/jot-api |
| THM01STR53 Client telemetry and trace propagation | THM01FTR14 | New | Forecast (PI-2+) | mobile/jot |
| THM01STR72 Reminder delivery telemetry endpoint | THM01FTR14 | New | Forecast (PI-2+) | apis/jot-api |

Excluded (moved to REL-x): none

## Components and versions

| Component | From | To | Change class | Migration? | Flags | Infra change? |
|-----------|------|----|--------------|------------|-------|---------------|
| apis/jot-api | — (new) | 1.0.0 | major (first release) | No (new table) | TBD in HLD | Yes — Lambda, HTTP API, data table, Cognito (`prod`) |
| mobile/jot | — (new) | 1.0.0 | major (first release) | No | TBD in HLD | No |
| infra (`07-source-code-tests/infra/`) | — (new) | 1.0.0 | major | — | — | Yes — bootstrap, shared, `dev`, `prod` |

## Mobile builds

| Platform | Component | App version | Build | Store / track | Phased rollout | Min supported version | Stories |
|----------|-----------|-------------|-------|---------------|----------------|-----------------------|---------|
| Android | mobile/jot | 1.0.0 | Release-hardening signed APK (1.3-Q12) | None — no app store (deviation C-05, ADR at design); APK attached to the GitHub Release and installed on the owner's phone | N/A (single user) | 1.0.0 | all `[Mobile]` Stories |

Dependencies / ordering: infra `prod` stack before the API; API before the app build that points to it; Cognito
`prod` pool and Google client before sign-in.
Rollout strategy      : from the HLD Deployment & Release sections (step 1.7) | Feature flags: TBD in HLD
Rollback plan         : from the HLDs — API: previous Lambda version / image; app: reinstall the previous signed
                        APK; infra: previous OpenTofu state version
