THM01STR48 — Reminder delivery reliability

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR48 — Reminder delivery reliability
Tags: [Non-Functional] [Availability & Reliability] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR13
Component       : mobile/jot
NFR Category    : Availability & Reliability
Persona         : As the owner relying on reminders
Goal            : I want reminders to fire on time when the phone is idle, in Doze, has restarted or was off at the due time
Benefit         : So that I can trust Jot with things I must not forget

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
UX Spec         : N/A — no new screen

SLO/Threshold   :
  - ≥ 99 % of reminders fire within 1 minute of dueAt when exact alarms are allowed
  - 0 missed reminders after a reboot
  - Exact alarms denied: fire no later than dueAt + 15 minutes and the reminder is shown as "may be late"
  - Due while the phone was off: shown right after boot, marked overdue (decision Q8)
Test Approach   : Emulator tests with forced Doze / idle (adb deviceidle), reboot and power-off; 20-reminder run over 2 hours on the phone during UAT; Device Farm run

Acceptance Criteria:
  AC-01: Given 20 reminders over 2 hours and the device in Doze, When their times arrive, Then at least 19
         fire within 1 minute of dueAt and none is missed
  AC-02: Given 20 scheduled reminders, When the device reboots before they are due, Then each fires within
         1 minute of its dueAt without the app being opened
  AC-03: Given exact-alarm permission is denied, When a reminder reaches its dueAt, Then the notification
         fires no later than dueAt + 15 minutes and the reminder is shown as "may be late"
  AC-04: Given a reminder's dueAt passed while the device was powered off, When the device boots, Then the
         notification is shown within 1 minute of boot and the reminder is marked overdue

Story Points    : 5
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 5)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Local notification library with AlarmManager exact alarms; boot receiver
Dependencies    : THM01STR24, THM01STR25, THM01STR28
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
