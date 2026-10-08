THM01STR52 — Metrics and SLO alarms

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR52 — Metrics and SLO alarms
Tags: [Non-Functional] [Observability & Monitoring] [API]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR14
Component       : apis/jot-api
NFR Category    : Observability & Monitoring
Persona         : As the owner running the service
Goal            : I want the note_created and reminder_delivered metrics and a CloudWatch alarm for every API SLO
Benefit         : So that I hear about problems first and the Epic benefit reports have data

SLO/Threshold   :
  - Alarms: 5xx rate > 5 % for 5 min; warm p95 latency > 300 ms for 15 min; throttles > 0 for 5 min; Lambda errors > 0 for 5 min — every API SLO in THM01FTR12 / THM01FTR13 covered, ≤ 10 alarms (free tier)
  - Alarm notification by email to the owner
  - Metrics note_created (count by type: text, list) and reminder_delivered (delaySeconds) with no user or note identifiers
Test Approach   : Force each alarm condition in dev and confirm the email; metric checks after the E2E run

Acceptance Criteria:
  AC-01: Given each condition (5xx > 5 %, p95 > 300 ms, throttles, Lambda errors) is forced in dev for its
         period, When the period ends, Then the matching alarm fires and the owner gets the email
  AC-02: Given the alarm definitions, When they are listed, Then every API SLO in THM01FTR12 and THM01FTR13
         has an alarm and there are at most 10
  AC-03: Given 3 text and 2 list notes are created in the E2E run, When CloudWatch is queried, Then
         note_created shows 3 for text and 2 for list
  AC-04: Given a reminder_delivered post with delaySeconds 12 (THM01STR72), When CloudWatch is queried,
         Then the metric records 12
  AC-05: Given the metric definitions, When they are inspected, Then no dimension contains a user or note
         identifier

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : CloudWatch EMF from the service; alarms deployed by THM01STR69; SNS email subscription
Dependencies    : THM01STR07, THM01STR69, THM01STR72
Analytics       : note_created and reminder_delivered are published here for the Epic Benefit Measurement (no identifiers)
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
