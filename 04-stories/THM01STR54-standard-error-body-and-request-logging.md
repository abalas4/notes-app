THM01STR54 — Standard error body and request logging

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR54 — Standard error body and request logging
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR06
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want every error returned in one standard body with a traceId, every typed service error mapped to its HTTP status, and one structured log line per request
Benefit         : So that the app can handle every failure the same way and any request can be traced without exposing my data

Endpoint Contract:
  Method        : —
  Path          : All routes
  Auth          : As the route
  Request Body  : N/A
  Response 2xx  : —
  Response 4xx  : {error:{code,message,traceId}}; VALIDATION_ERROR→400, UNAUTHENTICATED→401, NOT_FOUND→404, VERSION_CONFLICT→409, PAYLOAD_TOO_LARGE→413, STORE_UNAVAILABLE→503 + Retry-After
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a request for a route that does not exist, When it is handled, Then 404 NOT_FOUND in the
         standard error body with a traceId
  AC-02: Given a handler raises an unexpected exception, When the request is handled, Then 500 INTERNAL in
         the standard body with a traceId and no stack trace or exception text
  AC-03: Given the repository raises VERSION_CONFLICT or STORE_UNAVAILABLE, When the response is built,
         Then it is 409 CONFLICT, or 503 SERVICE_UNAVAILABLE with a Retry-After header, in the standard
         body
  AC-04: Given any request, When it is handled, Then exactly one JSON log line is written with exactly
         traceId, route, method, status, latencyMs (integer) and userId (when known), and no headers, query
         string, body or token

Story Points    : 3
Sprint Target   : PI-1 iteration 01 (slice 1)
Release Tag     : REL-1.0.0 (confirmed at iteration 01 planning 2026-10-08)
Story Type      : New
Original Story  : N/A
Linked WI       : THM01WI03 [LLD] (THM01FTR06, shared with STR01); THM01WI07 [IMPL], THM01WI08 [TEST]
Tech Notes      : FastAPI exception handlers; structlog; trace ID from the incoming traceparent or generated (W3C); OTel/X-Ray export is THM01STR51
Dependencies    : THM01STR01
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : Ready
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 confirmed (iteration 01 planning)
                  ✅ Work Items identified (05-work-items/, iteration 01 planning 2026-10-08)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
