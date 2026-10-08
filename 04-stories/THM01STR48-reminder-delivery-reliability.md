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
Goal            : I want reminders to fire on time even when the phone is idle, in Doze or has just restarted
Benefit         : So that I can trust Jot with things I must not forget

SLO/Threshold   :
  - ≥ 99 % of reminders fire within 1 minute of dueAt (exact alarms allowed)
  - 0 missed reminders after reboot
  - With exact alarms denied: fire within 15 minutes and the reminder is marked "may be late"
Test Approach   : Emulator tests with forced Doze / idle (adb deviceidle) and reboot; 20-reminder run over 2 hours on the phone during UAT; Device Farm run

Acceptance Criteria:
  AC-01: Given 20 reminders over 2 hours and the device in Doze, When their times arrive, Then at least 19
         fire within 1 minute and none is missed
  AC-02: Given scheduled reminders, When the device reboots, Then each fires at its time without the app
         being opened
  AC-03: Given exact alarms are denied, When a reminder is due, Then it fires within 15 minutes

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Local notification library with AlarmManager exact alarms; boot receiver
Dependencies    : THM01STR25, THM01STR28
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
