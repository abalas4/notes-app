THM01STR49 — Crash and ANR budget with crash reporting

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR49 — Crash and ANR budget with crash reporting
Tags: [Non-Functional] [Availability & Reliability] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR13
Component       : mobile/jot
NFR Category    : Availability & Reliability
Persona         : As the owner using the app every day
Goal            : I want crash reporting in release builds and test runs that fail on any crash or ANR
Benefit         : So that instability is caught before release and visible after it

SLO/Threshold   :
  - Crash-free users ≥ 99.5 % (30 days)
  - ANR rate ≤ 0.47 %
  - 0 crashes and 0 ANRs in the E2E suites on emulator, phone and Device Farm
Test Approach   : Crashlytics (no personal data) in release builds; E2E harness fails on crash dialogs / ANR traces

Acceptance Criteria:
  AC-01: Given a forced test crash in a release build, When the app restarts, Then the crash report arrives
         with no user identifiers or note text
  AC-02: Given an E2E run, When the app crashes or an ANR occurs, Then the run fails and the trace is
         attached

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : @react-native-firebase/crashlytics; logcat monitor in the test harness
Dependencies    : THM01STR30, THM01STR32
Analytics       : None — crash-free users is read from crash reporting, not an analytics event
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 2 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
