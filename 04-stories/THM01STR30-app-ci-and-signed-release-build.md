THM01STR30 — App CI and signed release build

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR30 — App CI and signed release build
Tags: [Functional] [Mobile] [Android] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR07
Component       : mobile/jot
Persona         : As the owner merging an app pull request
Goal            : I want CI that type-checks, lints and unit-tests the app, builds the release APK signed in CI, and scans it with MobSF
Benefit         : So that the one signed binary used on the phone, Device Farm and the GitHub Release is built and checked the same way every time

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Gates: tsc --noEmit, ESLint, Prettier check, Jest with coverage ≥ 80 % on new code, npm audit, licence check, Android release build, MobSF static scan (0 High)
  BR-02: The keystore and its passwords live only in the GitHub Environment secret store; never in the repo or logs
  BR-03: Release build only on main and on manual runs; PRs build a debug APK to save time
  BR-04: The signed APK and its SHA-256 are kept as a workflow artifact for THM01STR33 (--from-ci) and THM01STR34

Acceptance Criteria:
  AC-01: Given a PR that changes app code, When CI runs, Then type check, lint, unit tests and a debug
         build run and failures block the merge
  AC-02: Given a push to main, When CI runs, Then a release APK signed with the CI keystore and its SHA-256
         are attached as an artifact
  AC-03: Given the release APK, When MobSF scans it, Then there are 0 High findings or the check fails
  AC-04: Given the workflow logs, When they are searched, Then no keystore password or key material appears

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Node LTS (stable), Gradle with caching, JDK (stable LTS); MobSF in Docker
Dependencies    : App skeleton (first [Mobile] Story THM01STR05)
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
