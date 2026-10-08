THM01STR56 — List notes with paging

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR56 — List notes with paging
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR02
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want to list my active or archived notes, most recently changed first, a page at a time
Benefit         : So that Home and Archive load quickly however many notes I have

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/notes?archived=false|true&cursor=<opaque>&limit=1..100 (default 50)
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : N/A
  Response 2xx  : 200 {items:[note], nextCursor?}
  Response 4xx  : 400 VALIDATION_ERROR (limit out of range, malformed cursor) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given 120 notes, When GET /api/v1/notes?limit=50 is called repeatedly with nextCursor, Then all
         120 come back exactly once across 3 pages, newest change first
  AC-02: Given archived and active notes, When GET with archived=true, Then only archived, non-deleted
         notes are returned; with archived=false only active ones
  AC-03: Given limit=0, limit=101 or a malformed cursor, When GET /api/v1/notes is called, Then 400
         VALIDATION_ERROR naming the parameter

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 2)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Opaque cursor from the DynamoDB LastEvaluatedKey (encoded and signed)
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
