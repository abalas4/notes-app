THM01STR19 — Search, filter and sort notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR19 — Search, filter and sort notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR10
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want query parameters on the notes list for text search, label filter and sort order
Benefit         : So that Home can show exactly the notes I am looking for

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/notes?q=<text>&labelId=<id>&sort=updated|created|title&order=asc|desc&archived=false
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : N/A
  Response 2xx  : 200 {items:[note], nextCursor?} — pinned first when pinnedFirst=true (default)
  Response 4xx  : 400 VALIDATION_ERROR (unknown sort / order, q > 100 chars) · 401 — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given notes containing "lemon" in a title, a body and a checklist item, When GET /notes?q=LEMON,
         Then exactly those three notes are returned
  AC-02: Given notes with label Work, When GET /notes?labelId=<Work>, Then only those notes are returned
  AC-03: Given sort=title&order=asc, When GET /notes, Then pinned notes come first, each group sorted A–Z
  AC-04: Given sort=size, When GET /notes, Then 400 VALIDATION_ERROR naming sort

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Single user, so filtering and search can run in the service over the user's partition (≤ a few thousand notes); revisit with an index if needed (LLD)
Dependencies    : THM01STR07, THM01STR15
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
