THM01STR09 — Home screen with pinned and other notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR09 — Home screen with pinned and other notes
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want a Home screen that shows my notes as colour cards with Pinned and Others sections
Benefit         : So that I see everything at a glance and start a new note in one tap

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR02/ux-spec.md — pending (step 1.6); source screens W1 Home
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : App bar with drawer button and search field; two-column masonry of note cards; Pinned / Others headers; new-note button
  Key Elements  : Note card (title, first lines or checklist preview, colour, label chips, reminder chip); new-note FAB
  States        : Default | Loading (skeleton cards) | Empty ("Notes you add appear here") | Error (Retry) | Offline (banner; cached list from this session) | Background / resume (refresh)
  Navigation    : Start screen after sign-in; card tap → editor; FAB → new note; drawer button
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given the owner has pinned and unpinned notes, When Home loads, Then pinned notes appear under
         "Pinned" and the rest under "Others", each card in its note colour
  AC-02: Given the owner has no notes, When Home loads, Then the empty state with the new-note button is
         shown
  AC-03: Given the API fails or the network is off, When Home loads, Then an error or offline message with
         Retry is shown and no cards are invented
  AC-04: Given TalkBack is on, When a card is focused, Then it reads the title, a short preview, pinned
         state and labels

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : FlashList v2 masonry; TanStack Query; generated API client; design tokens from the style guide
Dependencies    : THM01STR07; THM01STR05
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
