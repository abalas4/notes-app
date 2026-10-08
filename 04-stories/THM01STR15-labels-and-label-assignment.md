THM01STR15 — Labels and label assignment

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR15 — Labels and label assignment
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR04
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want to create, list, rename and delete labels with note counts, and to set a note's labels
Benefit         : So that the label picker, the drawer and the Edit labels screen work from one consistent source

Endpoint Contract:
  Method        : GET · POST · PATCH · DELETE
  Path          : /api/v1/labels · /api/v1/labels/{id} (note labels set via PATCH /api/v1/notes/{id} {version, labelIds[]})
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : POST/PATCH {name: 1–50 chars, trimmed}
  Response 2xx  : GET 200 {items:[{id, name, noteCount}]} · POST 201 label · PATCH 200 label · DELETE 204
  Response 4xx  : 409 LABEL_EXISTS (case-insensitive) · 422 INVALID_NAME (empty) · 404 NOT_FOUND · 400 VALIDATION_ERROR (unknown labelId on a note) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given no label "Trip", When POST /api/v1/labels {name:"Trip"}, Then 201 and GET /labels lists it
         with noteCount 0
  AC-02: Given a label "Work", When POST {name:"work"} or PATCH another label to "WORK", Then 409
         LABEL_EXISTS
  AC-03: Given a label used by 3 notes, When DELETE /labels/{id}, Then 204, the 3 notes no longer list it,
         and no note is deleted
  AC-04: Given a note, When PATCH /notes/{id} sets labelIds to two existing labels, Then 200 and both
         labels' noteCount increase by 1
  AC-05: Given an empty or whitespace-only name, When POST or PATCH, Then 422 INVALID_NAME

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Label items in the single table; counts maintained transactionally or computed (LLD decides)
Dependencies    : THM01STR07, THM01STR08
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
