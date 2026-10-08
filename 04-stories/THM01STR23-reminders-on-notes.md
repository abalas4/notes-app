THM01STR23 — Reminders on notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR23 — Reminders on notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR05
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want to set, change, snooze, complete and remove a note's reminder and to list reminders as upcoming or done
Benefit         : So that reminders survive a reinstall and the Reminders tab has one source of truth

Endpoint Contract:
  Method        : PUT · DELETE · POST · GET
  Path          : /api/v1/notes/{id}/reminder · /api/v1/notes/{id}/reminder · /api/v1/notes/{id}/reminder/{done|snooze} · /api/v1/reminders?status=upcoming|done
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : PUT {version, dueAt (ISO 8601 with offset), timeZone (IANA), repeat: none|daily|weekly|monthly|yearly}; snooze {until}
  Response 2xx  : PUT 200 note with reminder {dueAt, timeZone, repeat, state, nextDueAt} · DELETE 204 · done / snooze 200 · GET 200 {items:[{noteId, title, dueAt, state}]}
  Response 4xx  : 400 VALIDATION_ERROR (dueAt in the past for a new reminder, unknown repeat / time zone) · 404 · 409 VERSION_CONFLICT — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given a note, When PUT a reminder for tomorrow 09:00 Asia/Kolkata with repeat none, Then 200 and
         GET /reminders?status=upcoming lists it
  AC-02: Given a weekly reminder, When POST /reminder/done, Then the occurrence is recorded as done and
         nextDueAt moves one week later
  AC-03: Given a reminder, When POST /reminder/snooze {until: +1 h}, Then dueAt becomes the snooze time and
         state stays upcoming
  AC-04: Given dueAt in the past or repeat "hourly", When PUT is called, Then 400 VALIDATION_ERROR naming
         the field

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Reminder stored on the note item; repeat rule expansion in the service; times stored in UTC with the IANA zone
Dependencies    : THM01STR07, THM01STR08
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
