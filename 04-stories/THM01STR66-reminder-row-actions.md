THM01STR66 — Reminder row actions

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR66 — Reminder row actions
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want a row menu on the Reminders tab to snooze, edit, mark done or remove a reminder
Benefit         : So that I can manage reminders without opening each note

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR05/ux-spec.md — pending (step 1.6); source screens W12 Snooze and edit reminder
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Row ⋮ menu: Snooze until (presets), Edit reminder, Mark done, Remove reminder
  Key Elements  : Row menu; snooze presets (as THM01STR65); confirmation for Remove
  States        : Default | Applying | Error (Retry) | Offline
  Navigation    : Reminders tab row ⋮; Edit → reminder sheet (THM01STR24)
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a row, When the owner snoozes it with a preset, Then the row moves to the group for its new
         time and the phone alarm is rescheduled
  AC-02: Given a row, When the owner chooses Edit reminder, Then the reminder sheet opens with the current
         values
  AC-03: Given a row, When the owner chooses Mark done, Then it moves to the Done chip
  AC-04: Given a row, When the owner chooses Remove reminder and confirms, Then the reminder and its
         scheduled notification are removed
  AC-05: Given the action fails or there is no network, When it is applied, Then the row is unchanged and
         an error / offline message with Retry is shown

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Shared snooze sheet; API THM01STR23, THM01STR64
Dependencies    : THM01STR27, THM01STR24, THM01STR65
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
