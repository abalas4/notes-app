THM01STR41 — Production deploy and weekly drift check

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR41 — Production deploy and weekly drift check
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner releasing and protecting production
Goal            : I want a `deploy-prod` workflow on main with my approval, and a weekly `drift-check` that finds manual changes
Benefit         : So that production changes only through reviewed code, and any console change is found within a week

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: deploy-prod: main only, prod Environment with owner approval, jot-gh-deploy-prod; applies the plan reviewed in the release change record (release skill)
  BR-02: drift-check: weekly schedule, read-only jot-gh-plan; `tofu plan -detailed-exitcode` for shared, prod and dev when it exists
  BR-03: Drift opens (or updates) one GitHub issue labelled drift with the plan summary, no IDs

Acceptance Criteria:
  AC-01: Given a merged release commit, When the owner runs deploy-prod and approves it, Then the prod plan
         is applied and the health route returns 200
  AC-02: Given a jot-* resource is changed in the console, When drift-check runs, Then an issue labelled
         drift is opened with the changed resource names
  AC-03: Given no drift, When drift-check runs, Then no issue is opened

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : GitHub Actions schedule; OpenTofu; gh issue
Dependencies    : THM01STR38, THM01STR39
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
