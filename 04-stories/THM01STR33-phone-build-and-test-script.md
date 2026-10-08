THM01STR33 — Phone build and test script

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR33 — Phone build and test script
Tags: [Functional] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR08
Component       : mobile/jot
Persona         : As the owner testing on my own Android phone
Goal            : I want one command, scripts/phone-test.sh, that builds the app, installs and runs the automated suites on my phone, records the result and the UAT note
Benefit         : So that the second Story Done gate (personal phone + UAT) is one command and leaves evidence

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)

Business Rules  :
  BR-01: Steps: check adb (wireless pairing, USB fallback) → check the dev environment is up → build APK + test APK (or use THM01STR68 `--from-ci <sha>`) → install → Espresso + Appium Python → HTML report
  BR-02: Result recorded as commit status `jot/phone-tests` (success / failure) on that commit via the gh CLI with the owner's login
  BR-03: Story Done runs use `--from-ci <sha>` so the phone tests the same binary as Device Farm
  BR-04: After the run it prompts for the UAT record (device model, Android version, build, pass / fail, notes) and writes it to 08-test-artefacts/ for the testing step
  BR-05: Options: --suite, --device <serial>, --skip-build; never prints tokens or account identifiers

Acceptance Criteria:
  AC-01: Given a paired phone and a running dev environment, When the owner runs scripts/phone-test.sh,
         Then the app is built, installed and tested and the HTML report path is printed
  AC-02: Given all tests pass, When the script ends, Then the commit has the jot/phone-tests success status
  AC-03: Given any test fails, When the script ends, Then the commit gets the jot/phone-tests failure
         status and the script exits non-zero with the report path printed
  AC-04: Given no device is connected or dev is down, When the script starts, Then it stops with a clear
         message before building
  AC-05: Given the tests have finished, When the script prompts, Then the owner's answers are written as a
         UAT record file under 08-test-artefacts/

Story Points    : 5
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Bash (Git Bash and Linux); adb; gh CLI; Appium; reuses the reference project's adb pairing scripts
Dependencies    : THM01STR30, THM01STR35 (dev environment)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
