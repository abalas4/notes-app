THM01STR13 — Checklist editor with progress

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR13 — Checklist editor with progress
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR03
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want to add, edit, check, uncheck and delete items and see completed items move to a Completed group with "N of M done"
Benefit         : So that I can tick off shopping and task lists quickly

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR03/ux-spec.md — pending (step 1.6); source screens W5 List, W10 List states
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Title; unchecked items with drag handles; "+ List item"; collapsible "Completed · N" group; progress text
  Key Elements  : Checkbox per item; item text field; delete item ✕; progress "N of M done"
  States        : Default | Empty list | Saving | Error (Retry) | Offline | Conflict (latest version reloaded) | Background / resume
  Navigation    : FAB menu "New list"; card tap on a list note
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a list note, When the owner adds three items and checks one, Then it moves to Completed with
         strike-through and the header reads "1 of 3 done"
  AC-02: Given a checked item, When it is unchecked, Then it returns to its earlier position among
         unchecked items
  AC-03: Given an item, When the owner edits its text or taps ✕, Then the change is saved and the progress
         updates
  AC-04: Given a new list with no items, When the editor opens, Then only "+ List item" is shown and no
         progress text
  AC-05: Given the API returns an error, 409 or there is no network, When the owner checks an item, Then
         the app shows the error / offline message with Retry, the item is not shown as saved, and for 409
         Retry reloads the latest list first

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 3
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Shared editor shell with THM01STR10; UI shows saved state only after the API confirms (D-07)
Dependencies    : THM01STR12, THM01STR10
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
