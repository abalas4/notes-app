THM01STR28 — Notification and exact-alarm permission flow

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR28 — Notification and exact-alarm permission flow
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want the app to ask for notification and exact-alarm permission in context, explain why, and handle a refusal clearly
Benefit         : So that I understand why the permission matters and still know when a reminder will not alert

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR05/ux-spec.md — pending (step 1.6); source screens Permission rationale (design gap — UX spec)
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Rationale dialog before the system prompt; banner on the Reminders tab when denied
  Key Elements  : Rationale text; Allow / Not now; "Enable in settings" link
  States        : Not asked | Rationale | Granted | Denied | Denied permanently (settings link)
  Navigation    : Triggered by a reminder Save; banner → Android app settings
Device behaviour:
  Offline       : Online-only (D-07): offline banner; actions that need the API are disabled or fail visibly with Retry; nothing is shown as saved until the API confirms
  Permissions   : POST_NOTIFICATIONS (Android 13+) and SCHEDULE_EXACT_ALARM (Android 14+) — to alert at the set time — asked when the first reminder is saved, with rationale "Jot needs permission to alert you at the time you choose" — if denied: reminder saved and marked "won't alert" / "may be late" (THM01STR28)
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: No note data at rest beyond the in-memory cache; nothing persisted (op-sqlite deferred with L-01); cleared on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given notification permission was never asked, When the owner saves the first reminder, Then the
         rationale is shown, then the system prompt
  AC-02: Given the rationale, When the owner taps "Not now", Then no system prompt appears, the reminder is
         saved as "won't alert", and the rationale is shown again on the next reminder save
  AC-03: Given the owner denies notifications, When the reminder is saved, Then the card shows "won't
         alert" and the Reminders tab shows "Enable notifications" with a link that opens Android
         notification settings
  AC-04: Given exact alarms are not allowed (Android 14+), When the owner saves a reminder, Then the app
         offers a link to allow them; if still not allowed, an inexact alarm is used and the reminder shows
         "may be late" (fires within 15 minutes, THM01STR48)

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 5)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : PermissionsAndroid; AlarmManager.canScheduleExactAlarms; settings intents
Dependencies    : THM01STR24, THM01STR27
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
                  ⚠️ Design gap: rationale dialog and denied banner not in W1–W12 — added at UX spec (1.6)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
