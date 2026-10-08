THM01STR23 — Set, change and remove a reminder

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR23 — Set, change and remove a reminder
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to set, change and remove a note's reminder with a date, time, time zone and repeat rule
Benefit         : So that my reminders survive a reinstall

Endpoint Contract:
  Method        : PUT · DELETE
  Path          : /api/v1/notes/{id}/reminder
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : PUT {version, dueAt (ISO 8601 with offset), timeZone (IANA), repeat: none|daily|weekly|monthly|yearly}
  Response 2xx  : PUT 200 note with reminder {dueAt, timeZone, repeat, state:"upcoming"} · DELETE 204
  Response 4xx  : 400 VALIDATION_ERROR · 409 VERSION_CONFLICT — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a note with no reminder, When PUT a reminder for tomorrow 09:00 Asia/Kolkata with repeat
         none, Then 200 and the note carries the reminder in state upcoming
  AC-02: Given a note with a reminder, When PUT with a new time and repeat weekly, Then 200 and the
         reminder has the new time and rule
  AC-03: Given a note with a reminder, When DELETE /reminder, Then 204 and the note has no reminder
  AC-04: Given dueAt in the past, an unknown repeat value or an unknown time zone, When PUT is called, Then
         400 VALIDATION_ERROR naming the field
  AC-05: Given a stale version, When PUT is called, Then 409 VERSION_CONFLICT and the reminder is unchanged

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Reminder stored on the note item; times in UTC with the IANA zone
Dependencies    : THM01STR07, THM01STR08
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
