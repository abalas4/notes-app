THM01STR70 — Weekly drift check

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR70 — Weekly drift check
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner keeping AWS matching the code
Goal            : I want a weekly `drift-check` that finds any change made outside the code
Benefit         : So that a console change is found within a week (IAC-14)

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Weekly schedule; read-only jot-gh-plan; `tofu plan -detailed-exitcode` for shared, prod and dev (dev skipped when it is down)
  BR-02: Drift opens or updates one GitHub issue labelled drift listing changed jot-* resource names — never account IDs or ARNs

Acceptance Criteria:
  AC-01: Given a jot-* resource is changed in the console, When drift-check runs, Then an issue labelled
         drift is opened with the changed resource names
  AC-02: Given an open drift issue, When drift-check finds drift again, Then that issue is updated and no
         second issue is opened
  AC-03: Given no drift, When drift-check runs, Then no issue is opened
  AC-04: Given `tofu plan` errors, When drift-check runs, Then the run fails visibly and does not report
         "no drift"

Story Points    : 2
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : GitHub Actions schedule; OpenTofu; gh issue
Dependencies    : THM01STR38, THM01STR39, THM01STR69
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
