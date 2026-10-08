THM01STR24 — Add or edit a reminder

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR24 — Add or edit a reminder
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want a reminder sheet with Later today, Tomorrow and Pick date, a time and a repeat option, for new and existing reminders
Benefit         : So that setting a reminder takes two taps for the common cases

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR05/ux-spec.md — pending (step 1.6); source screens W9 Reminder date picker
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Bottom sheet over the editor: quick picks; month calendar; time; repeat; Cancel / Save
  Key Elements  : Later today (next full hour + 3 h, not after 21:00); Tomorrow (09:00); calendar; time; repeat (Does not repeat, Daily, Weekly, Monthly, Yearly)
  States        : Default | Saving | Error (Retry) | Offline (Save disabled with message) | Permission needed (THM01STR28)
  Navigation    : Editor top-bar reminder button on notes and checklists; reminder chip on a card; Reminders tab row → Edit
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : POST_NOTIFICATIONS (Android 13+) and SCHEDULE_EXACT_ALARM (Android 14+) — to alert at the set time — asked when the first reminder is saved, with rationale "Jot needs permission to alert you at the time you choose" — if denied: reminder saved and marked "won't alert" / "may be late" (THM01STR28)
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given an open note or checklist, When the owner taps Tomorrow and Save, Then the reminder is saved
         for tomorrow 09:00 local time and the card shows the reminder chip
  AC-02: Given the sheet, When the owner picks a date, a time and one of the repeat options, Then the saved
         reminder uses exactly that time and rule; a time earlier than now today is refused with "Pick a
         time in the future"
  AC-03: Given the time is after 21:00, When the sheet opens, Then "Later today" is not shown (decision
         Q14)
  AC-04: Given a note with a reminder, When the owner opens it from the chip, changes the time and saves,
         Then the sheet showed the current values and the new time is saved
  AC-05: Given the API fails or there is no network, When the owner taps Save, Then an error / offline
         message with Retry is shown and no chip appears

Story Points    : 5
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 5)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : @react-native-community/datetimepicker; bottom sheet; API THM01STR23
Dependencies    : THM01STR23, THM01STR10, THM01STR13
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
