THM01STR17 — Edit labels screen

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR17 — Edit labels screen
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR04
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want a screen to create, rename and delete labels
Benefit         : So that I can tidy my labels in one place, knowing deleting a label never deletes notes

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR04/ux-spec.md — pending (step 1.6); source screens W8 Manage labels
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : List of labels with note counts and Edit; inline rename; Delete label with confirmation; explanatory note
  Key Elements  : Create new label row; label row (name, count, Edit); rename field; Delete label; "Deleting a label never deletes notes" text
  States        : Default | Editing | Empty | Saving | Error (inline name exists / empty) | Offline
  Navigation    : Drawer → Edit labels; back to drawer
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a label, When the owner renames it, Then every note card shows the new name
  AC-02: Given a label used by notes, When the owner deletes it and confirms, Then it disappears from the
         drawer and the notes, and all notes remain
  AC-03: Given the owner renames a label to an existing name or to empty, When they confirm, Then an inline
         message explains why and nothing changes

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : API THM01STR15
Dependencies    : THM01STR15, THM01STR18
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
