THM01STR47 — App start, scroll and search performance

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR47 — App start, scroll and search performance
Tags: [Non-Functional] [Performance] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR12
Component       : mobile/jot
NFR Category    : Performance
Persona         : As the owner capturing a thought
Goal            : I want the app to start fast, scroll smoothly and search quickly on a low-end phone
Benefit         : So that capture is never slowed down by the app

SLO/Threshold   :
  - Cold start to interactive Home ≤ 2 s on the low-end emulator tier
  - Scrolling 500 notes at 60 fps (no frames > 16 ms in steady scroll)
  - Search results within 1 s of the last keystroke with 500 notes
  - No network or disk I/O on the main thread (StrictMode clean)
Test Approach   : Android macrobenchmark / Perfetto on the low-end emulator; Appium timing check for search; StrictMode in debug builds

Acceptance Criteria:
  AC-01: Given the low-end emulator with 500 notes, When the app is cold-started 10 times, Then median time
         to interactive Home ≤ 2 s
  AC-02: Given 500 notes, When the owner flings through the list, Then the frame-timing report shows 60 fps
         steady scroll
  AC-03: Given 500 notes, When the owner types a search word, Then results appear within 1 s of the last
         keystroke

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : FlashList; Hermes; macrobenchmark module in tests/mobile/jot/device/
Dependencies    : THM01STR09, THM01STR21
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
