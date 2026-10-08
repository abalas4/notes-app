THM01STR41 — Production deploy workflow

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR41 — Production deploy workflow
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner releasing to production
Goal            : I want a `deploy-prod` workflow that applies the reviewed prod plan from main with my approval
Benefit         : So that production changes only through reviewed code

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: main only, prod Environment with owner approval, jot-gh-deploy-prod
  BR-02: Applies the saved plan reviewed in the release change record (release skill); a changed plan needs a new approval

Acceptance Criteria:
  AC-01: Given a merged release commit, When the owner runs deploy-prod and approves it, Then the saved
         prod plan is applied and GET /api/v1/health on prod returns 200
  AC-02: Given a branch other than main or no owner approval, When deploy-prod is triggered, Then it does
         not assume jot-gh-deploy-prod and applies nothing
  AC-03: Given the plan changed after review, When deploy-prod runs, Then it stops and asks for a new
         approval

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : GitHub Actions; OpenTofu saved plans
Dependencies    : THM01STR38, THM01STR39, THM01STR69
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
