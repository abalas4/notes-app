THM01STR22 — Multi-select with bulk actions

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR22 — Multi-select with bulk actions
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR10
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want to long-press notes to select several and pin, label, recolour, archive or delete them together
Benefit         : So that tidying many notes takes one action instead of many

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR10/ux-spec.md — pending (step 1.6); source screens W3 Select and organize
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Selection app bar (✕, "N selected", pin, label, more); selected cards outlined with a check
  Key Elements  : Selection bar; bulk actions sheet: Pin / unpin, Add or change labels, Change colour, Archive, Delete
  States        : Default | Selecting | Applying | Partial failure | Offline
  Navigation    : Long-press a card enters selection; ✕ or back exits
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given Home, When the owner long-presses a note and taps two more, Then the bar shows "3 selected"
  AC-02: Given 3 selected notes, When the owner chooses Pin, Change colour (sage), Add label Work or
         Archive, Then that change shows on all 3 and selection ends
  AC-03: Given 3 selected notes, When the owner deletes them, Then a snackbar offers Undo for 5 s that
         restores all 3
  AC-04: Given one note fails with conflict in the batch, When the result returns, Then the bar shows "2 of
         3 updated · Retry" and Retry re-sends only that note (not_found results are not retried)
  AC-05: Given there is no network, When the owner chooses a bulk action, Then the offline message with
         Retry is shown and no note is shown as changed

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Selection state in Zustand; API THM01STR20
Dependencies    : THM01STR20, THM01STR09, THM01STR16, THM01STR11
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
