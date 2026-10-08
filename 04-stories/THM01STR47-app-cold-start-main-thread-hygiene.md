THM01STR47 — App cold start and main-thread hygiene

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR47 — App cold start and main-thread hygiene
Tags: [Non-Functional] [Performance] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR12
Component       : mobile/jot
NFR Category    : Performance
Persona         : As the owner capturing a thought
Goal            : I want the app to start fast on a low-end phone and never do network or disk work on the main thread
Benefit         : So that capture is never slowed down by the app

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
UX Spec         : N/A — no new screen

SLO/Threshold   :
  - Cold start to interactive Home: median ≤ 2 s and slowest ≤ 3 s over 10 starts on the low-end emulator tier with 500 notes
  - 0 StrictMode main-thread network or disk violations
Test Approach   : Android macrobenchmark on the low-end emulator; StrictMode penaltyDeath in debug builds during the E2E run

Acceptance Criteria:
  AC-01: Given the low-end emulator with 500 notes, When the app is cold-started 10 times, Then the median
         time to interactive Home is at most 2 s and the slowest at most 3 s
  AC-02: Given a debug build with StrictMode set to fail on violations, When the owner launches the app,
         opens Home, scrolls, searches and opens a note, Then no main-thread network or disk violation
         occurs

Story Points    : 2
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 4)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Hermes; macrobenchmark module in tests/mobile/jot/device/
Dependencies    : THM01STR09
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 2 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
