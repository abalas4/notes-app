THM01STR07 — Create a note

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR07 — Create a note
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to create a text note with a title, body, colour and pin state
Benefit         : So that what I write is stored safely in the cloud

Endpoint Contract:
  Method        : POST
  Path          : /api/v1/notes
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : {type:"text", title≤200, body≤20000, color ∈ the 8 palette tokens, pinned?}
  Response 2xx  : 201 {id, type:"text"|"list", title, body, items[], hideCompleted, color, pinned, archived, labelIds[], reminder?, version, createdAt, updatedAt} + Location header
  Response 4xx  : 400 VALIDATION_ERROR (field named) · 413 PAYLOAD_TOO_LARGE — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a signed-in user, When POST /api/v1/notes with a title, body and colour, Then 201 with the
         note at version 1 and a Location header
  AC-02: Given a body over 20,000 characters, a title over 200 or an unknown colour, When POST is called,
         Then 400 VALIDATION_ERROR naming the field and nothing is stored
  AC-03: Given a request body over 64 KB, When POST is called, Then 413 PAYLOAD_TOO_LARGE and nothing is
         stored

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 2)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : FastAPI router notes; repository layer (THM01STR02)
Dependencies    : THM01STR02, THM01STR04, THM01STR54
Analytics       : note_created — on 201 from POST /notes (text or list) — {type} only, no IDs or content — owner's own app, no consent prompt (Epic metric: notes + checklists per week)
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
