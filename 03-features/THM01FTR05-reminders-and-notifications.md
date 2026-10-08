THM01FTR05 — Reminders and notifications

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[BUSINESS FEATURE] THM01FTR05 — Reminders and notifications
Tags: [Business] [Functional] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic       : THM01EPC01
Surfaces          : API (apis/jot-api) · Mobile Android (mobile/jot) — iOS later (Epic Surfaces)
Feature Owner     : Product Owner (@abalas4)
Description       : The owner adds a reminder to a note or checklist (Later today, Tomorrow, or a date,
                    time and repeat — W9); sees reminders on the Reminders tab grouped Overdue / Today /
                    later with Upcoming / Done chips (W12); and receives a phone notification at the set
                    time showing the title, body or "N of M done" with the next item, and the actions
                    Mark done, Snooze and Open (W11). Snooze opens the app's snooze sheet with presets
                    (10 min, 1 h, tonight 8 PM, tomorrow 9 AM, pick date and time) — D-10. Reminders are
                    local notifications scheduled on the phone (D-06), so they fire without a network;
                    the reminder data is stored by the API so it survives a reinstall.

Benefit Hypothesis: If reminders fire on time even offline and can be snoozed or completed from the
                    notification, then the owner stops using a separate reminder app, because a missed
                    or awkward reminder is the reason reminders get ignored.
Success Metric    : Reminders firing within 1 min of the scheduled time | n/a (new) | ≥ 99 % (Epic metric)

Acceptance Criteria:
  AC-01: Given a note is open, When the owner sets a reminder for a date and time with "Does not repeat"
         and saves, Then the reminder is stored by the API, scheduled on the phone, and the note card
         shows the reminder chip
  AC-02: Given a scheduled reminder and the phone has no network, When the scheduled time arrives, Then
         the notification is shown within 1 minute with Mark done, Snooze and Open, and the lock screen
         shows no note text unless the owner allowed it in Android settings
  AC-03: Given a reminder notification, When the owner taps "Snooze", Then the app opens the snooze
         sheet and a chosen preset reschedules the reminder and updates the API; When they tap
         "Mark done", Then the notification is dismissed, the reminder moves to Done, and a repeating
         reminder schedules its next occurrence
  AC-04: Given Android has not granted notification or exact-alarm permission, When the owner sets the
         first reminder, Then the app explains why in context and asks; if denied, the reminder is saved,
         marked "may be late / will not alert", and the Reminders tab shows how to enable it
  AC-05: Given the app is reinstalled or the phone restarted, When the owner signs in or the phone boots,
         Then every future reminder from the API is scheduled again on the phone

Sizing            : L
WSJF              : (9 + 6 + 7) / 6 = 3.67   (proposed; reliability risk reduced early)
PI Target         : PI-1
Sprint Target     : TBD at PI Planning (step 1.5) — planned slice 5
Release Roll-up   : None yet — derived from child Stories
Feature Type      : New
Original Feature  : N/A
Linked Stories    : TBD at step 1.3 (≥ 1 [API], ≥ 1 [Mobile] [Android]; expected ≥ 4 because of the size)
HLD Reference     : THM01FTR05-HLD
LLD Reference     : THM01FTR05-LLD

Dependencies      : THM01FTR02, THM01FTR03 (notes and lists to remind about); THM01FTR06
Constraints       : Local notifications (D-06); notification library provisional until dependency
                    vetting before LLD approval (plan risk R-NOTIF); Android 13+ notification permission
                    and Android 14+ exact-alarm rules; server push is L-03; UX per W9, W11, W12.
Platform scope    : As THM01FTR01.
ALM Status        : Refined (PR #3, 2026-10-08)
DoR Check         : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ Feature Type
                    · ✅ Description · ✅ Benefit hypothesis · ✅ 5 ACs · ✅ Sized L · ✅ WSJF · ✅ PI Target
                    · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                    ⚠️ Sprint Target — PI Planning (1.5) · ⚠️ Child Stories — step 1.3
                    ⚠️ Style guide Approved with SG-15 — step 1.6a · ⚠️ Platform scope minimum OS — HLD (1.7)
DoD Check         : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
