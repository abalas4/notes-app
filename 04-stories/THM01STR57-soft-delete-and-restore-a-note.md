THM01STR57 — Soft delete and restore a note

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR57 — Soft delete and restore a note
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to delete a note and restore it within a short window
Benefit         : So that the app's 5-second Undo always works, even on a slow network

Endpoint Contract:
  Method        : DELETE · POST
  Path          : /api/v1/notes/{id} · /api/v1/notes/{id}/restore
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : N/A
  Response 2xx  : DELETE 204 · restore 200 note (same content, version + 1)
  Response 4xx  : 404 NOT_FOUND (also when the restore window has passed) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a note, When DELETE is called, Then 204 and the note no longer appears in any list
  AC-02: Given a note deleted less than 30 seconds ago, When POST /restore is called, Then 200 with the
         same content and it appears in lists again
  AC-03: Given a note deleted more than 30 seconds ago, When POST /restore is called, Then 404 NOT_FOUND
         and the note stays deleted

Story Points    : 2
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 2)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : deletedAt + TTL purge (window 30 s server-side for the 5 s client Undo, decision Q4)
Dependencies    : THM01STR07
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
