THM01STR34 — Device Farm workflow with gate and guard rails

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR34 — Device Farm workflow with gate and guard rails
Tags: [Functional] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR08
Component       : mobile/jot
Persona         : As the owner running the last Story Done gate
Goal            : I want a manual `device-farm` workflow that runs the suites on the pinned real-device pool only for a commit that already passed the emulator and phone gates
Benefit         : So that no Device Farm minutes are spent on a build that is known to be bad, and runs can never become paid by accident

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Inputs: commit SHA, suite, device pool; uses the CI-signed APK of that SHA
  BR-02: Gate: refuses unless the SHA has a green emulator-tests run and the jot/phone-tests success status
  BR-03: Guard rails: preflight check of the package, free-minutes check (GetAccountSettings), allow_paid = false by default, 10-minute job timeout, stop on first failure, cleanup always (even on cancel)
  BR-04: Runs in the protected `device-farm` Environment (owner approval) with the jot-gh-devicefarm role only
  BR-05: Results, videos and logs downloaded as artifacts; no account IDs or ARNs printed

Acceptance Criteria:
  AC-01: Given a SHA without a green emulator run or phone status, When device-farm is started, Then it
         stops before uploading anything
  AC-02: Given a SHA that passed both gates and enough free minutes, When the owner approves the run, Then
         the suite runs on the pool and the results are attached
  AC-03: Given the free minutes are below the run estimate and allow_paid is false, When the workflow
         checks, Then it stops with the remaining minutes shown
  AC-04: Given the run is cancelled mid-way, When the workflow ends, Then the cleanup step leaves no
         uploads or running jobs

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : AWS CLI devicefarm; scripts adapted from the reference project (preflight, run, cleanup)
Dependencies    : THM01STR32, THM01STR33, THM01STR37 (Device Farm project), THM01STR38 (role)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
