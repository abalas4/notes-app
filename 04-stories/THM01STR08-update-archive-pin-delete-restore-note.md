THM01STR08 — Update, archive, pin, delete and restore a note

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR08 — Update, archive, pin, delete and restore a note
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want to change a note's title, body, colour, pin or archive state, delete it softly and restore it within the undo window, with optimistic concurrency
Benefit         : So that edits are never silently overwritten and an accidental delete can be undone

Endpoint Contract:
  Method        : PATCH · DELETE · POST
  Path          : /api/v1/notes/{id} · /api/v1/notes/{id} · /api/v1/notes/{id}/restore
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : PATCH {version, title?, body?, color?, pinned?, archived?} (version required)
  Response 2xx  : PATCH 200 note (version+1) · DELETE 204 · restore 200 note
  Response 4xx  : 404 NOT_FOUND (also for another user's note) · 409 VERSION_CONFLICT {current version} · 400 VALIDATION_ERROR — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given a note at version 2, When PATCH with version 2 and a new colour, Then 200 with version 3 and
         the new colour
  AC-02: Given a note at version 3, When PATCH with version 2, Then 409 VERSION_CONFLICT with the current
         version and nothing changes
  AC-03: Given a note, When DELETE then POST /restore, Then the note is back unchanged; When only DELETE,
         Then it no longer appears in lists
  AC-04: Given a note owned by another user, When PATCH, DELETE or restore is called, Then 404 NOT_FOUND

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Conditional updates; soft delete (deletedAt) with a TTL purge window decided in the LLD
Dependencies    : THM01STR07
Analytics       : None — no Epic Success Metric is measured from this Story
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
