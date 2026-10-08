THM01STR15 — Create, rename and delete labels

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR15 — Create, rename and delete labels
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR04
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to create, list, rename and delete labels, each with a count of my active notes
Benefit         : So that the label picker, the drawer and the Edit labels screen work from one consistent source

Endpoint Contract:
  Method        : GET · POST · PATCH · DELETE
  Path          : /api/v1/labels · /api/v1/labels/{id}
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : POST / PATCH {name: 1–50 characters after trimming}
  Response 2xx  : GET 200 {items:[{id, name, noteCount}]} (noteCount = active notes: not archived, not deleted) · POST 201 · PATCH 200 · DELETE 204
  Response 4xx  : 409 LABEL_EXISTS (another label with the same name ignoring case) · 422 INVALID_NAME (empty or > 50) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given no label "Trip", When POST /api/v1/labels {name:"Trip"}, Then 201 and GET /labels lists it
         with noteCount 0
  AC-02: Given labels "Work" and "Home", When POST {name:"work"} or PATCH "Home" to "WORK", Then 409
         LABEL_EXISTS; When PATCH "Work" to "work" (same label, case only), Then 200 (decision Q10)
  AC-03: Given a label "Work", When PATCH {name:"Office"}, Then 200 and GET /labels returns "Office" with
         the same id and noteCount
  AC-04: Given an empty, whitespace-only or 51-character name, When POST or PATCH, Then 422 INVALID_NAME
  AC-05: Given a label used by 3 notes, When DELETE /labels/{id}, Then 204, the 3 notes no longer list it,
         and no note is deleted

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Label items in the single table; counts maintained or computed (LLD decides)
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
