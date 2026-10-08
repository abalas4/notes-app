THM01STR07 — Create and list notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR07 — Create and list notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want to create a text note and to list my notes (active or archived), newest change first
Benefit         : So that the app can show Home and Archive from the API

Endpoint Contract:
  Method        : POST · GET
  Path          : /api/v1/notes · /api/v1/notes?archived=false|true&cursor=<opaque>&limit=50
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : POST {type:"text", title≤200, body≤20000, color∈8 tokens, pinned?}
  Response 2xx  : POST 201 {id, type:"text"|"list", title, body, items[], color, pinned, archived, labelIds[], reminder?, version, createdAt, updatedAt} + Location · GET 200 {items:[note], nextCursor?}
  Response 4xx  : 400 VALIDATION_ERROR (field details) · 401 UNAUTHENTICATED · 413 PAYLOAD_TOO_LARGE — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given a signed-in user, When POST /api/v1/notes with a title, body and colour, Then 201 with the
         note at version 1 and it appears first in GET /api/v1/notes
  AC-02: Given a body over 20,000 characters or an unknown colour, When POST is called, Then 400
         VALIDATION_ERROR naming the field and nothing is stored
  AC-03: Given 120 notes, When GET /api/v1/notes?limit=50 is called repeatedly with nextCursor, Then all
         120 come back exactly once across 3 pages
  AC-04: Given archived and active notes, When GET with archived=true, Then only archived, non-deleted
         notes are returned

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : FastAPI router notes; repository layer (THM01STR02); opaque cursor from the DynamoDB LastEvaluatedKey
Dependencies    : THM01STR02, THM01STR04
Analytics       : note_created — on 201 from POST /notes (text or list) — {type} only, no IDs or content — owner's own app, no consent prompt needed (Epic metric: notes + checklists per week)
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
