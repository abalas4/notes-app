THM01STR04 — Authenticate requests and resolve the current user

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR04 — Authenticate requests and resolve the current user
Tags: [API] [Functional] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR01
Component       : apis/jot-api
Persona         : As the Jot app
Goal            : I want every API request authenticated with a Cognito access token and mapped from the token subject to an internal userId, plus GET /api/v1/me
Benefit         : So that all data is owner-scoped and native Cognito accounts (L-04) can be added later without moving data

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/me
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : N/A
  Response 2xx  : 200 {userId, displayName, createdAt}
  Response 4xx  : 401 UNAUTHENTICATED {error:{code,message,traceId}} (missing / expired / invalid token)
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given a valid access token for a first-time Google user, When GET /api/v1/me is called, Then 200
         with a new internal userId, and the subject-to-userId mapping is stored
  AC-02: Given the same user calls again, When GET /api/v1/me is called, Then the same userId is returned
  AC-03: Given no Authorization header, or an expired token, or a token from another user pool, When any
         route except health is called, Then 401 UNAUTHENTICATED and no data
  AC-04: Given any request, When it is logged, Then the log line has the userId but never the token, email
         or name

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : API Gateway HTTP API JWT authorizer (Cognito) + in-service claim check; mapping item in the single table
Dependencies    : THM01STR02; THM01STR40 (Cognito pools)
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
