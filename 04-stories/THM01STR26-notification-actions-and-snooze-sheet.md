THM01STR26 — Notification actions and snooze sheet

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR26 — Notification actions and snooze sheet
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want Mark done, Snooze and Open on the reminder notification, with Snooze opening the snooze sheet
Benefit         : So that I can deal with a reminder straight from the notification

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR05/ux-spec.md — pending (step 1.6); source screens W11 Reminder notification, W12 Snooze and edit
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Android notification: title, body or "N of M done · next: <item>", label; three actions. Snooze sheet: In 10 minutes, In 1 hour, Tonight 8:00 PM, Tomorrow 9:00 AM, Pick date and time
  Key Elements  : Actions Mark done / Snooze / Open; snooze presets
  States        : Default | Applying | Error (Retry in app) | Offline (action shown as failed with Retry — online-only, D-07)
  Navigation    : Open → note editor; Snooze → app opens on the snooze sheet (D-10); deep link jot://note/{id} validated against the signed-in user's notes
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : POST_NOTIFICATIONS (Android 13+) and SCHEDULE_EXACT_ALARM / USE_EXACT_ALARM (Android 14+) — to alert at the set time — asked when the first reminder is saved, with rationale "Jot needs permission to alert you at the time you choose" — if denied: reminder saved and marked "won't alert" / "may be late" (THM01STR28)
  Push          : As THM01STR25; checklist reminders show progress and the next unchecked item
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a reminder notification, When the owner taps Mark done, Then the notification is dismissed
         and the reminder is marked done through the API
  AC-02: Given a reminder notification, When the owner taps Snooze and picks "In 1 hour", Then the reminder
         is rescheduled for one hour later on the phone and the API
  AC-03: Given a reminder notification, When the owner taps Open, Then the app opens on that note
  AC-04: Given Mark done is tapped with no network, When the app cannot reach the API, Then the reminder
         stays upcoming and the app shows a message with Retry the next time it opens

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Notification action handlers (background task); deep-link handling with validation
Dependencies    : THM01STR25, THM01STR23
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
