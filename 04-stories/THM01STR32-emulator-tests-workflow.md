THM01STR32 — Emulator tests workflow

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR32 — Emulator tests workflow
Tags: [Functional] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR08
Component       : mobile/jot
Persona         : As the owner testing a commit
Goal            : I want an `emulator-tests` workflow I can start with Run workflow (and that also runs on every PR) which runs Espresso and Appium Python on Android emulators against the API in Docker
Benefit         : So that the first Story Done gate (emulator matrix) runs automatically and for free

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)

Business Rules  :
  BR-01: Inputs: suite (espresso | appium-python | all), API levels (default: the emulator matrix — oldest supported and latest stable, set in the HLD)
  BR-02: The API runs from docker-compose in the same job with DynamoDB Local and test users; no AWS access
  BR-03: One automatic rerun of a failed test is allowed and reported as flaky; a test that fails twice fails the run
  BR-04: Reports (HTML + JUnit, screenshots on failure) uploaded as artifacts; the run result is what the Device Farm gate reads
  BR-05: Test code lives only in 07-source-code-tests/tests/mobile/jot/ (ui/ for Espresso, e2e/ for Appium); the workflow only calls scripts/

Acceptance Criteria:
  AC-01: Given a commit, When the owner runs emulator-tests with suite all, Then the APK and test APK are
         built, GET /api/v1/health on the Docker API returns 200, the emulator boots on each matrix API
         level, both suites run and HTML and JUnit reports are attached
  AC-02: Given a test that fails twice, When the run ends, Then the workflow is red and the failing test's
         screenshot is in the artifacts; a test that passes on the rerun is listed as flaky
  AC-03: Given a PR, When it is opened or updated, Then emulator-tests runs automatically and its result is
         reported on the PR
  AC-04: Given the same commit and suite, When the owner runs it locally through scripts/, Then each test
         case has the same pass / fail outcome as the CI run (flaky reruns excepted)

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : GitHub ubuntu runner with KVM; android-emulator-runner action pinned by SHA (or sdk tools directly); Appium 2 + UiAutomator2; pytest
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
