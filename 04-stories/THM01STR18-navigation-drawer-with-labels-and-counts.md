THM01STR18 — Navigation drawer with labels and counts

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR18 — Navigation drawer with labels and counts
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR04
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want a navigation drawer with Notes, Reminders, my labels with counts, Archive and Settings
Benefit         : So that I can reach any group of notes in two taps

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR04/ux-spec.md — pending (step 1.6); source screens W7 Navigation drawer (Trash entry removed — decision Q3, L-05)
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : App name; Notes (count); Reminders (count); Labels section with counts; Create new label; Edit labels; Archive; Settings
  Key Elements  : Drawer items with counts; active item highlight
  States        : Default | Loading counts | Error (counts hidden, items still usable, Retry) | Offline
  Navigation    : Hamburger on Home; system back closes the drawer; destinations below
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given labels exist, When the owner opens the drawer, Then each label shows its count of active
         notes and Notes / Reminders show their counts
  AC-02: Given the drawer, When the owner taps a label with N active notes, Then Home shows exactly those N
         notes and the label is highlighted
  AC-03: Given the drawer, When the owner taps Notes, Reminders, Archive, Settings, Create new label or
         Edit labels, Then that screen or flow opens and the drawer closes
  AC-04: Given the counts request fails, When the drawer opens, Then counts are hidden, every item is still
         tappable and Retry reloads the counts
  AC-05: Given TalkBack is on, When the drawer opens, Then focus moves into it and each item reads its
         name, count and whether it is selected

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 4)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : React Navigation drawer; Reminders tab THM01STR27, Archive THM01STR58 and Settings THM01STR55 are stubs until those Stories ship
Dependencies    : THM01STR15, THM01STR09
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
