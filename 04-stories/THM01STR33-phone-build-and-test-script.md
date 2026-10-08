THM01STR33 — Phone build and test script

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR33 — Phone build and test script
Tags: [Functional] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR08
Component       : mobile/jot
Persona         : As the owner testing on my own Android phone
Goal            : I want one command, scripts/phone-test.sh, that builds (or downloads the CI-signed APK), installs and runs the automated suites on my phone and records the result
Benefit         : So that the second Story Done gate (personal phone + UAT) is one command and leaves evidence

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Steps: check adb (wireless pairing, USB fallback) → check the dev environment is up → build APK + test APK, or `--from-ci <sha>` downloads the CI-signed APK for that commit → install → Espresso + Appium Python → HTML report
  BR-02: On success it sets the commit status `jot/phone-tests` = success on that commit (via the gh CLI with the owner's login); on failure = failure
  BR-03: Story Done runs must use `--from-ci <sha>` so the phone tests the same binary as Device Farm
  BR-04: After the run it prompts for the manual UAT record (device model, Android version, build) written to 08-test-artefacts/ by the testing step
  BR-05: Options: --suite, --device <serial>, --skip-build; never prints tokens or account identifiers

Acceptance Criteria:
  AC-01: Given a paired phone and a running dev environment, When the owner runs scripts/phone-test.sh,
         Then the app is built, installed and tested and an HTML report path is printed
  AC-02: Given --from-ci <sha>, When the script runs, Then it installs the CI-signed APK for that commit
         and verifies its SHA-256 before testing
  AC-03: Given all tests pass, When the script ends, Then the commit has the jot/phone-tests success status
  AC-04: Given no device is connected or dev is down, When the script starts, Then it stops with a clear
         message before building

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Bash (runs in Git Bash and Linux); adb; gh CLI; Appium; reuses the reference project's adb pairing scripts
Dependencies    : THM01STR30, THM01STR35 (dev environment)
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
