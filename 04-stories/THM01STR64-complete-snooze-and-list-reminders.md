THM01STR64 — Complete, snooze and list reminders

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR64 — Complete, snooze and list reminders
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to mark a reminder done, snooze it, and list reminders as upcoming or done
Benefit         : So that the Reminders tab and the notification actions have one source of truth

Endpoint Contract:
  Method        : POST · POST · GET
  Path          : /api/v1/notes/{id}/reminder/done · /api/v1/notes/{id}/reminder/snooze · /api/v1/reminders?status=upcoming|done
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : snooze {until (ISO 8601, in the future)}
  Response 2xx  : done / snooze 200 note · GET 200 {items:[{noteId, title, dueAt, state, overdue}]} ordered by dueAt
  Response 4xx  : 400 VALIDATION_ERROR (until in the past) · 404 NOT_FOUND (no reminder) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a one-time reminder, When POST /reminder/done, Then it is listed under status=done and no
         longer under upcoming
  AC-02: Given a weekly reminder due Monday 09:00, When POST /reminder/done, Then that occurrence is listed
         as done and the reminder is upcoming for the next Monday 09:00
  AC-03: Given a weekly reminder due Monday 09:00, When POST /reminder/snooze until Monday 10:00, Then only
         this occurrence moves to 10:00 and the following Monday is still 09:00 (decision Q6)
  AC-04: Given reminders due yesterday, today and next week, When GET /reminders?status=upcoming, Then they
         come back in dueAt order and yesterday's is marked overdue
  AC-05: Given snooze until a past time, When POST /reminder/snooze, Then 400 VALIDATION_ERROR

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 5)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Occurrence handling for repeat rules in the service
Dependencies    : THM01STR23
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
