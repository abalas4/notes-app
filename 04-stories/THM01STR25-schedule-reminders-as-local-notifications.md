THM01STR25 — Schedule reminders as local notifications

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR25 — Schedule reminders as local notifications
Tags: [Mobile] [Android] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want every upcoming reminder scheduled on the phone as a local notification, and rescheduled after sign-in, reboot or a change
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
  Permissions   : POST_NOTIFICATIONS (Android 13+) and SCHEDULE_EXACT_ALARM / USE_EXACT_ALARM (Android 14+) — to alert at the set time — asked when the first reminder is saved, with rationale "Jot needs permission to alert you at the time you choose" — if denied: reminder saved and marked "won't alert" / "may be late" (THM01STR28)
  Push          : Local notification at dueAt — title only on the lock screen (body hidden unless the owner allows it in Android settings) — tap opens the note
  Lifecycle     : Reschedule on BOOT_COMPLETED, app update, sign-in and when the reminder list changes
  Data on device: Scheduled alarms hold only noteId and title in the notification payload; removed when a reminder is removed
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given an upcoming reminder saved through the API, When the save succeeds, Then exactly one local
         notification is scheduled for dueAt with the noteId
  AC-02: Given the phone is offline, When dueAt arrives, Then the notification is shown within 1 minute
  AC-03: Given the phone restarts, When it finishes booting, Then all future reminders are scheduled again
         without opening the app
  AC-04: Given a reminder is removed or the note deleted, When the change is saved, Then the scheduled
         notification is cancelled
  AC-05: Given a fresh install, When the owner signs in, Then all upcoming reminders from GET /reminders
         are scheduled

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Local notification library (Notifee provisional — vetting before LLD approval, plan risk R-NOTIF); AlarmManager exact alarms where permitted
Dependencies    : THM01STR23, THM01STR24, THM01STR28
Analytics       : reminder_delivered — when a notification is displayed — {delaySeconds} only (no IDs, no content) — owner's own app, no consent prompt (Epic metric: reminder on-time rate; sent via THM01STR53)
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
                  ⚠️ Library choice depends on R-NOTIF vetting (step 1.7)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
