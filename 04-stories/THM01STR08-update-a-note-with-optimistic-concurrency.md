THM01STR08 — Update a note with optimistic concurrency

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR08 — Update a note with optimistic concurrency
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to change a note's title, body, colour, pin or archive state, rejecting changes based on an old version
Benefit         : So that an edit is never silently overwritten

Endpoint Contract:
  Method        : PATCH
  Path          : /api/v1/notes/{id}
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : {version (required), title?, body?, color?, pinned?, archived?}
  Response 2xx  : 200 note (version + 1)
  Response 4xx  : 400 VALIDATION_ERROR · 409 VERSION_CONFLICT {currentVersion} — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a note at version 2, When PATCH with version 2 and a new colour, Then 200 with version 3 and
         the new colour
  AC-02: Given a note at version 3, When PATCH with version 2, Then 409 VERSION_CONFLICT with
         currentVersion 3 and nothing changes
  AC-03: Given a PATCH with an unknown colour, a body over 20,000 characters or no version, When it is
         sent, Then 400 VALIDATION_ERROR naming the field and nothing changes

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 2)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Conditional update on version (THM01STR02)
Dependencies    : THM01STR07
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
