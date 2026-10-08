THM01STR21 — Search bar, label chips, sort sheet and layout toggle

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR21 — Search bar, label chips, sort sheet and layout toggle
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR10
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want to search notes, filter with label chips, choose a sort order and switch between grid and list
Benefit         : So that I find any note in a few seconds

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR10/ux-spec.md — pending (step 1.6); source screens W1 Home, W2 Sort and view
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Search field in the app bar; label chip row (All, labels, + Label); "Sorted by" control opening a sort sheet; grid / list toggle
  Key Elements  : Search field with clear; chips; sort sheet (Date modified, Date created, Title A–Z; Newest / Oldest; Keep pinned on top); view toggle
  States        : Default | Searching | No results ("No notes match") | Error (Retry) | Offline
  Navigation    : Home; chip "+ Label" opens the label picker for filtering
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: Sort, order and view choice stored in app preferences (not personal data); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given notes, When the owner types "lemon", Then matching notes are shown within 1 s of the last
         keystroke and clearing the field restores the full list
  AC-02: Given label chips, When the owner taps Work, Then only Work notes are shown and All clears the
         filter
  AC-03: Given the sort sheet, When the owner picks Title A–Z with Keep pinned on top, Then the list is
         ordered that way and the choice persists after restart
  AC-04: Given the view toggle, When the owner switches to list, Then single-column cards are shown and the
         choice persists after restart

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Debounced query (300 ms) against THM01STR19; preferences in AsyncStorage
Dependencies    : THM01STR19, THM01STR09, THM01STR15
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
