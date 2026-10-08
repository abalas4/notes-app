THM01STR10 — Note editor with autosave, colour, pin and archive

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR10 — Note editor with autosave, colour, pin and archive
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want to write a note's title and body and have it saved without a Save button, and to set colour, pin and archive from the editor
Benefit         : So that capturing a thought takes seconds and nothing is lost

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR02/ux-spec.md — pending (step 1.6); source screens W4 Note editor (plain text — L-02)
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Top bar: back, pin, reminder, archive; title and body fields; bottom bar: colour, label, more; "Edited <time>"
  Key Elements  : Title field; body field (plain text); colour tray with 8 colours; pin toggle; archive
  States        : Default | Saving (subtle indicator) | Saved | Error (Retry, text kept) | Offline (banner, text kept) | Conflict (reloaded latest + message) | Background / resume
  Navigation    : From Home card or FAB; back saves and returns to Home
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Unsaved text survives app switch and process death (restored from saved instance state) until the API confirms
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a new note, When the owner types a title and body and taps back, Then the note is created
         through the API and shown first on Home
  AC-02: Given an open note, When the owner pauses typing for 1 s, Then the change is saved (PATCH with the
         note's version) and "Edited just now" is shown
  AC-03: Given the save fails or there is no network, When the owner keeps editing, Then the text stays, an
         offline / error message with Retry is shown, and Retry saves it
  AC-04: Given the API answers 409 VERSION_CONFLICT, When the save returns, Then the editor shows the
         latest server version and tells the owner their unsaved text was kept as a copy in the clipboard
  AC-05: Given the colour tray, When the owner picks a colour or taps pin or archive, Then the change is
         saved and reflected on Home

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Debounced PATCH; React Native TextInput (no rich text, D-09); colour tray bottom sheet
Dependencies    : THM01STR07, THM01STR08, THM01STR09
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
                  ⚠️ PO to confirm the conflict rule in AC-04 (keep own text in the clipboard) — or choose "keep mine / take theirs" at UX spec
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
