THM01STR20 — Batch update and delete notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR20 — Batch update and delete notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR10
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want one call that applies pin, unpin, labels, colour, archive, unarchive, delete or restore to several notes
Benefit         : So that bulk actions are fast and each note's outcome is reported

Endpoint Contract:
  Method        : POST
  Path          : /api/v1/notes/batch
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : {items:[{id, version}] (1–100), action: pin|unpin|archive|unarchive|delete|restore|color|setLabels, value?}
  Response 2xx  : 200 {results:[{id, status:"ok"|"not_found"|"conflict", note?}]}
  Response 4xx  : 400 VALIDATION_ERROR (unknown action, 0 or > 100 items, invalid colour or unknown label in value) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given three of my notes, When POST /notes/batch {action:"archive"}, Then 200 and all three report
         ok and are archived
  AC-02: Given three of my notes, When the batch runs with pin, then color "sage", then setLabels [Work],
         Then after each call all three report ok and show that change
  AC-03: Given one id is another user's and one has a stale version, When the batch runs, Then those report
         not_found and conflict and the rest are applied
  AC-04: Given an unknown action, 101 items or an unknown colour, When POST /notes/batch, Then 400
         VALIDATION_ERROR and nothing changes
  AC-05: Given a batch delete less than 30 seconds ago, When POST /notes/batch {action:"restore"} with the
         same ids, Then all report ok and are restored

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 4)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Per-item conditional writes; bounded batch size
Dependencies    : THM01STR08, THM01STR57, THM01STR62
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
