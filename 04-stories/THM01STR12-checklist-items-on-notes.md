THM01STR12 — Checklist items on notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR12 — Checklist items on notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR03
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want list notes whose items can be added, edited, checked, reordered and removed, and conversion between text and list
Benefit         : So that checklists use the same note endpoints, versioning and ownership rules

Endpoint Contract:
  Method        : POST · PATCH · POST
  Path          : /api/v1/notes (type "list") · /api/v1/notes/{id} · /api/v1/notes/{id}/convert
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : items:[{id, text≤1000, checked, position}] (≤ 500 items); convert {version, to:"text"|"list"}
  Response 2xx  : 201 / 200 note with items and progress {done, total}
  Response 4xx  : 400 VALIDATION_ERROR · 404 NOT_FOUND · 409 VERSION_CONFLICT — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given a list note with 3 items, When PATCH checks item 2, Then 200 with item 2 checked and
         progress {done:1, total:3}
  AC-02: Given a list note, When PATCH sends a new item order, Then positions are stored and returned in
         that order
  AC-03: Given a list note, When POST /convert to "text", Then each item becomes one body line and items
         are removed; converting a text note to "list" makes one item per non-empty line
  AC-04: Given 501 items or an item over 1,000 characters, When saved, Then 400 VALIDATION_ERROR

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 3
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Items stored inside the note item (size checked against the 400 KB DynamoDB limit in the LLD)
Dependencies    : THM01STR07, THM01STR08
Analytics       : note_created with {type:"list"} is emitted by THM01STR07 for new lists — no extra event
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
