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
Benefit         : So that no Device Farm minutes are spent on a build known to be bad, and runs never become paid by accident

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)

Business Rules  :
  BR-01: Inputs: commit SHA, suite, device pool; uses the CI build of that SHA (the signed APK only for the release-hardening run, decision Q12)
  BR-02: Gate: refuses unless the SHA has a green emulator-tests run and the jot/phone-tests success status
  BR-03: Run estimate = devices in the pool × suites × 10 minutes; the run stops if the remaining free minutes are below the estimate and allow_paid is false (default)
  BR-04: Guard rails: preflight package check, 10-minute job timeout, stop on first failure, cleanup always (also on cancel)
  BR-05: Runs in the protected `device-farm` Environment (owner approval) with the jot-gh-devicefarm role only; no account IDs or ARNs printed

Acceptance Criteria:
  AC-01: Given a SHA without a green emulator run or phone status, When device-farm is started, Then it
         stops before uploading anything and no device minutes are used
  AC-02: Given a SHA that passed both gates and enough free minutes, When the owner approves the run, Then
         the suite runs on the pool and results, videos and logs are attached
  AC-03: Given the remaining free minutes are below the run estimate and allow_paid is false, When the
         workflow checks, Then it stops before any upload and prints the remaining minutes
  AC-04: Given a device job fails, When the workflow evaluates it, Then no further jobs start and cleanup
         runs
  AC-05: Given a job reaches 10 minutes or the run is cancelled, When the workflow ends, Then the job is
         stopped and cleanup leaves no uploads or running jobs

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
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
