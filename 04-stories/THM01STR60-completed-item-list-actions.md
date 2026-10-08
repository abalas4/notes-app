THM01STR60 — Completed-item list actions

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR60 — Completed-item list actions
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR03
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want Hide completed, Uncheck all and Delete completed on a checklist
Benefit         : So that long lists stay tidy

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR03/ux-spec.md — pending (step 1.6); source screens W5 List, W10 List states
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : List "more" menu
  Key Elements  : Hide completed (toggle); Uncheck all; Delete completed (with confirmation)
  States        : Default | Applying | Error (Retry) | Offline
  Navigation    : List editor "more" menu
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a list with 2 checked items, When the owner turns on Hide completed, Then the Completed
         group is hidden and stays hidden after reopening the list (saved with the note, decision Q5)
  AC-02: Given 2 checked and 3 unchecked items, When the owner chooses Uncheck all, Then all 5 are
         unchecked, the header reads "0 of 5 done", and it stays so after reopening
  AC-03: Given 2 checked items, When the owner chooses Delete completed and confirms, Then the 2 checked
         items are removed and the others are unchanged; When they cancel, nothing changes
  AC-04: Given the action fails or there is no network, When it is applied, Then the list is not shown as
         changed and an error / offline message with Retry is shown

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 3)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : PATCH items / hideCompleted (THM01STR12)
Dependencies    : THM01STR12, THM01STR13
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
