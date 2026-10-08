THM01STR25 — Schedule reminders as local notifications

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR25 — Schedule reminders as local notifications
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want every upcoming reminder scheduled on the phone as a local notification and kept in step with every change
Benefit         : So that reminders fire on time even with no network

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR05/ux-spec.md — pending (step 1.6); source screens — (background behaviour; no screen)
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : No screen
  Key Elements  : —
  States        : Background | Reboot | Sign-in | Permission denied
  Navigation    : —
Device behaviour:
  Offline       : Scheduling works offline; the notification fires from the phone's alarm, not the network
  Permissions   : POST_NOTIFICATIONS (Android 13+) and SCHEDULE_EXACT_ALARM (Android 14+) — to alert at the set time — asked when the first reminder is saved, with rationale "Jot needs permission to alert you at the time you choose" — if denied: reminder saved and marked "won't alert" / "may be late" (THM01STR28)
  Push          : Local notification at dueAt (content and actions in THM01STR26)
  Lifecycle     : Reschedule on boot, app update, sign-in and every reminder change; cancel all on sign-out (THM01STR55)
  Data on device: Scheduled alarms hold only noteId and title; removed when the reminder is removed
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given an upcoming reminder saved through the API, When dueAt arrives with the phone offline and
         the app closed, Then the notification appears within 1 minute
  AC-02: Given the phone restarts before a reminder's time, When that time arrives, Then the notification
         appears without the app being opened; and a reminder whose time passed while the phone was off is
         shown right after boot, marked overdue (decision Q8)
  AC-03: Given a reminder is changed, snoozed, marked done (repeating: next occurrence) or removed, When
         the change is saved, Then exactly one notification is scheduled for the new time, or none if
         removed
  AC-04: Given a fresh install, When the owner signs in, Then every upcoming reminder from the API is
         scheduled
  AC-05: Given notification permission is denied, When dueAt arrives, Then no notification is shown and the
         reminder shows "won't alert"

Story Points    : 5
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 5)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Local notification library (Notifee provisional — vetting before LLD approval, RAID-015 R-NOTIF); AlarmManager exact alarms where permitted; boot receiver
Dependencies    : THM01STR23, THM01STR64, THM01STR24, THM01STR28
Analytics       : reminder_delivered — when a notification is displayed — {delaySeconds, appVersion} only — owner's own app, no consent prompt (Epic metric: reminder on-time rate; sent by THM01STR53)
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
                  ⚠️ Library choice depends on R-NOTIF vetting (step 1.7)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
