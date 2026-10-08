THM01STR71 — Scroll, search and transition performance

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR71 — Scroll, search and transition performance
Tags: [Non-Functional] [Performance] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR12
Component       : mobile/jot
NFR Category    : Performance
Persona         : As the owner browsing my notes
Goal            : I want smooth scrolling, quick search and quick screen changes with many notes
Benefit         : So that the app feels fluid however many notes I have

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
UX Spec         : N/A — no new screen

SLO/Threshold   :
  - Scrolling 500 notes: ≤ 5 % of frames over 16 ms during a 10 s fling
  - Search results within 1 s of the last keystroke at p95 over 20 runs with 500 notes
  - Home ↔ editor transition ≤ 300 ms
Test Approach   : Macrobenchmark frame timing and Perfetto on the low-end emulator; Appium timing for search

Acceptance Criteria:
  AC-01: Given the low-end emulator with 500 notes, When the owner flings through the list for 10 s, Then
         at most 5 % of frames take longer than 16 ms
  AC-02: Given 500 notes, When a search word is typed and typing stops, over 20 runs, Then results show
         within 1 s of the last keystroke at p95
  AC-03: Given the low-end emulator, When the owner opens a note from Home and goes back, Then each
         transition completes within 300 ms

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 4)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : FlashList; Perfetto traces; Appium timing helpers
Dependencies    : THM01STR09, THM01STR21, THM01STR10
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
