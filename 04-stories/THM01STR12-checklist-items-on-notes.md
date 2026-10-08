THM01STR12 — Checklist items on notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR12 — Checklist items on notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR03
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want list notes whose items I can add, edit, check, reorder and remove, with a saved "hide completed" setting
Benefit         : So that my checklists are stored with the same versioning and ownership rules as notes

Endpoint Contract:
  Method        : POST · PATCH
  Path          : /api/v1/notes (type "list") · /api/v1/notes/{id}
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : {version, items:[{id, text≤1000, checked, position}] (≤ 500 items), hideCompleted?}
  Response 2xx  : 201 / 200 note with items, hideCompleted and progress {done, total}
  Response 4xx  : 400 VALIDATION_ERROR · 409 VERSION_CONFLICT — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a list note with 3 items, When PATCH checks item 2, Then 200 with item 2 checked and
         progress {done:1, total:3}
  AC-02: Given a list note, When PATCH sends a new item order, Then positions are stored and returned in
         that order
  AC-03: Given a list note, When PATCH sets hideCompleted true, Then it is stored and returned on every
         later read (decision Q5)
  AC-04: Given 501 items or an item over 1,000 characters, When saved, Then 400 VALIDATION_ERROR naming the
         field and nothing changes
  AC-05: Given a stale version, When PATCH is sent, Then 409 VERSION_CONFLICT and the list is unchanged

Story Points    : 5
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 3)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Items stored inside the note item (size checked against the 400 KB DynamoDB item limit in the LLD)
Dependencies    : THM01STR07, THM01STR08
Analytics       : note_created with {type:"list"} is emitted by THM01STR07 for new lists — no extra event
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
