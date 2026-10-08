THM01STR20 — Batch update and delete notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR20 — Batch update and delete notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR10
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want one call that applies pin / unpin, labels, colour, archive or delete to several notes
Benefit         : So that bulk actions are fast and either fully applied or clearly reported per note

Endpoint Contract:
  Method        : POST
  Path          : /api/v1/notes/batch
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : {noteIds[1..100], action: pin|unpin|archive|unarchive|delete|restore|color|setLabels, value?}
  Response 2xx  : 200 {results:[{id, status:"ok"|"not_found"|"conflict", note?}]}
  Response 4xx  : 400 VALIDATION_ERROR (unknown action, > 100 ids) · 401 — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given three of my notes, When POST /notes/batch {action:"archive"}, Then 200 and all three report
         ok and are archived
  AC-02: Given one id belongs to another user, When the batch runs, Then that id reports not_found and the
         others are applied
  AC-03: Given 101 ids, When POST /notes/batch, Then 400 VALIDATION_ERROR
  AC-04: Given a batch delete, When POST /notes/batch {action:"restore"} with the same ids within the undo
         window, Then all are restored

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 4
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Per-item conditional writes; bounded batch size
Dependencies    : THM01STR08
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
