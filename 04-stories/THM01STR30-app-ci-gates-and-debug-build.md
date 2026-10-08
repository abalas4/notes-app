THM01STR30 — App CI gates and debug build

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR30 — App CI gates and debug build
Tags: [Functional] [Mobile] [Android] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR07
Component       : mobile/jot
Persona         : As the owner merging an app pull request
Goal            : I want CI that type-checks, lints and unit-tests the app and builds the debug APK and test APK with bundled JavaScript on every PR and on main
Benefit         : So that every commit produces a tested build that runs on the emulator, my phone and Device Farm without a dev server

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)

Business Rules  :
  BR-01: Gates: tsc --noEmit, ESLint, Prettier check, Jest with coverage ≥ 80 % on new code, npm audit (no High / Critical), licence check, debug build, MobSF static scan on main
  BR-02: Builds are debug builds with the JS bundle embedded; no signing keystore is used here (signed builds only for release hardening, decision Q12 — THM01STR67)
  BR-03: The APK, test APK and their SHA-256 are kept as workflow artifacts for THM01STR32–34 and THM01STR68
  BR-04: Each gate is one script under scripts/, runnable locally

Acceptance Criteria:
  AC-01: Given a PR that changes app code, When CI runs, Then type check, lint, unit tests and the debug
         build run and their results are required status checks
  AC-02: Given a PR whose new code has coverage below 80 %, or a High npm audit finding, When CI runs, Then
         the matching check is red and the merge is blocked
  AC-03: Given a push to main, When CI runs, Then the debug APK and test APK with their SHA-256 are
         attached as artifacts and run without a Metro server
  AC-04: Given the debug APK on main, When MobSF scans it, Then the report is attached as an artifact and
         the check is red if any High finding exists
  AC-05: Given the same commit, When a gate script runs locally and in CI, Then each check has the same
         pass / fail outcome

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Node LTS (stable), Gradle with caching, JDK LTS (stable); MobSF in Docker
Dependencies    : App skeleton (first [Mobile] Story THM01STR05)
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
