THM01STR32 — Emulator tests workflow

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR32 — Emulator tests workflow
Tags: [Functional] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR08
Component       : mobile/jot
Persona         : As the owner testing a commit
Goal            : I want an `emulator-tests` workflow I can start with Run workflow (and that also runs on every PR) which runs Espresso and Appium Python on an Android emulator against the API in Docker
Benefit         : So that the first Story Done gate (emulator matrix) runs automatically and for free

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Inputs: suite (espresso | appium-python | all), API level (from the emulator matrix); defaults run the full matrix on main
  BR-02: The API runs from docker-compose in the same job with DynamoDB Local and dev-pool-style test users; no AWS access
  BR-03: Reports (HTML + JUnit, screenshots on failure) uploaded as artifacts; the run result is the commit status used by the Device Farm gate
  BR-04: Test code lives only in 07-source-code-tests/tests/mobile/jot/ (ui/ for Espresso, e2e/ for Appium); the workflow only calls scripts/

Acceptance Criteria:
  AC-01: Given a commit, When the owner runs emulator-tests with suite all, Then the APK and test APK are
         built, the emulator boots with KVM, both suites run and reports are attached
  AC-02: Given a failing test, When the run ends, Then the workflow is red and the failing test's
         screenshot is in the artifacts
  AC-03: Given a PR, When it is opened or updated, Then emulator-tests runs automatically and its result is
         reported on the PR
  AC-04: Given the same commit, When the owner runs the same suite locally through scripts/, Then it gives
         the same result

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : GitHub ubuntu runner with KVM; reactivecircus/android-emulator-runner pinned by SHA (or sdk tools directly); Appium 2 + UiAutomator2; pytest
Dependencies    : THM01STR30 (APK build), THM01STR01 (Compose API)
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
