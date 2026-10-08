THM01STR63 — Sort sheet and grid or list layout

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR63 — Sort sheet and grid or list layout
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR10
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want to choose how notes are sorted and whether they show as a grid or a list
Benefit         : So that Home looks the way I like it

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR10/ux-spec.md — pending (step 1.6); source screens W2 Sort and view
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : "Sorted by" control opening a sort sheet; grid / list toggle
  Key Elements  : Sort sheet: Date modified, Date created, Title (A to Z); Newest / Oldest first; Keep pinned notes on top; View as Grid / List
  States        : Default | Applying
  Navigation    : Home app bar
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: Sort, order, pinned-on-top and view choice in app preferences (not personal data); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given the sort sheet, When the owner picks Title with Keep pinned on top, Then pinned notes stay
         first, each section is A–Z, and the choice persists after restart
  AC-02: Given Keep pinned on top is off, When the list reloads, Then pinned notes are ordered like the
         others
  AC-03: Given the view is grid, When the owner taps the toggle, Then single-column cards show immediately;
         tapping again shows two-column cards immediately; the choice persists after restart
  AC-04: Given TalkBack is on, When the sort control is focused, Then it reads the current sort, e.g.
         "Sorted by date modified, newest first"

Story Points    : 2
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Preferences in AsyncStorage; FlashList layout switch
Dependencies    : THM01STR19, THM01STR09
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
