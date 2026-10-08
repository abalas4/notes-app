THM01STR19 — Search, filter and sort notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR19 — Search, filter and sort notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR10
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want query parameters on the notes list for text search, label filter and sort order
Benefit         : So that Home can show exactly the notes I am looking for

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/notes?q=<text ≤100>&labelId=<id>&sort=updated|created|title&order=asc|desc&pinnedFirst=true|false&archived=false|true
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : N/A
  Response 2xx  : 200 {items:[note], nextCursor?} — defaults sort=updated, order=desc, pinnedFirst=true, archived=false (archived notes are searched only with archived=true)
  Response 4xx  : 400 VALIDATION_ERROR (unknown sort / order, q > 100 characters) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given notes containing "lemon" in a title, a body and a checklist item, When GET /notes?q=LEMON,
         Then exactly those three notes are returned
  AC-02: Given notes labelled Work, some containing "lemon", When GET /notes?q=lemon&labelId=<Work>, Then
         only Work notes containing "lemon" are returned
  AC-03: Given one pinned note and others with different dates, When GET with sort=updated&order=desc (and
         with created, title, asc), Then the pinned note is first and the rest follow the chosen order;
         with pinnedFirst=false the pinned note is ordered like the others
  AC-04: Given sort=size, order=up or a 101-character q, When GET /notes, Then 400 VALIDATION_ERROR naming
         the parameter

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Single user, so filtering and search run in the service over the user's partition (a few thousand notes at most); index revisited in the LLD if needed
Dependencies    : THM01STR56, THM01STR12, THM01STR15
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
