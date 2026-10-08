THM01STR59 — Convert between text and list notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR59 — Convert between text and list notes
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR03
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to convert a list note to a text note and a text note to a list note
Benefit         : So that I can change a note's form without retyping it

Endpoint Contract:
  Method        : POST
  Path          : /api/v1/notes/{id}/convert
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : {version, to:"text"|"list"}
  Response 2xx  : 200 note in the new type
  Response 4xx  : 400 VALIDATION_ERROR · 409 VERSION_CONFLICT — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a list note with items A, B (checked), C, When POST /convert to "text", Then the body is the
         three lines "A", "B", "C" in order, items and checked state are removed, and type is "text"
  AC-02: Given a text note with 3 non-empty lines and 1 blank line, When POST /convert to "list", Then it
         has 3 unchecked items in the original order and an empty body
  AC-03: Given a stale version, When POST /convert is sent, Then 409 VERSION_CONFLICT and the note is
         unchanged

Story Points    : 2
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 3)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Same note item; conversion in the service
Dependencies    : THM01STR12
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
