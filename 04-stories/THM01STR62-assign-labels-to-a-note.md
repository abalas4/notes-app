THM01STR62 — Assign labels to a note

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR62 — Assign labels to a note
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR04
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to set the labels on a note
Benefit         : So that my notes can be grouped and the label counts stay right

Endpoint Contract:
  Method        : PATCH
  Path          : /api/v1/notes/{id} {version, labelIds[]}
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : N/A
  Response 2xx  : 200 note with labelIds
  Response 4xx  : 400 VALIDATION_ERROR (unknown labelId) · 409 VERSION_CONFLICT — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a note and two of my labels, When PATCH sets labelIds to both, Then 200 and both labels'
         noteCount increase by 1
  AC-02: Given a note with label Work, When PATCH sets labelIds to [], Then 200 and Work's noteCount
         decreases by 1
  AC-03: Given a labelId that does not exist or is not mine, When PATCH sets it, Then 400 VALIDATION_ERROR
         naming labelIds and the note's labels are unchanged

Story Points    : 2
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Same note update path (THM01STR08)
Dependencies    : THM01STR15, THM01STR08
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
