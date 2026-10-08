THM01STR49 — Crash and ANR budget with crash reporting

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR49 — Crash and ANR budget with crash reporting
Tags: [Non-Functional] [Availability & Reliability] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR13
Component       : mobile/jot
NFR Category    : Availability & Reliability
Persona         : As the maintainer of the app
Goal            : I want crash reporting in builds I use, test runs that fail on any crash or ANR, and a 30-day check of the crash and ANR budget
Benefit         : So that instability is caught before release and acted on after it

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
UX Spec         : N/A — no new screen

SLO/Threshold   :
  - Crash-free users ≥ 99.5 % and ANR rate ≤ 0.47 % over 30 days
  - 0 crashes and 0 ANRs in the E2E suites on emulator, phone and Device Farm
Test Approach   : Crashlytics (no personal data) in builds installed on the phone; E2E harness fails on crash dialogs or ANR traces; 30-day report review

Acceptance Criteria:
  AC-01: Given a forced test crash, When the app restarts, Then the crash report arrives with no user
         identifiers or note text
  AC-02: Given an E2E run, When the app crashes or an ANR occurs, Then the run fails and the trace is
         attached
  AC-03: Given the 30-day crash report after a release, When crash-free users are below 99.5 % or ANR above
         0.47 %, Then a defect is raised and the next release waits until it is fixed or the Product Owner
         accepts it

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
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
