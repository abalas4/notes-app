THM01STR04 — Authenticate requests and resolve the current user

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR04 — Authenticate requests and resolve the current user
Tags: [API] [Functional] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR01
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want every API request authenticated with a Cognito access token and mapped from the token subject to an internal userId, plus GET /api/v1/me
Benefit         : So that all my data is owner-scoped and email / password accounts (L-04) can be added later without moving data

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/me
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : N/A
  Response 2xx  : 200 {userId, createdAt} (display name comes from the ID token in the app, not from the API)
  Response 4xx  : 401 UNAUTHENTICATED {error:{code,message,traceId}} (missing / expired / invalid token or another user pool)
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a valid access token for a first-time Google user, When GET /api/v1/me is called, Then 200
         with a new internal userId and the subject-to-userId mapping is stored
  AC-02: Given the same user calls again, When GET /api/v1/me is called, Then the same userId is returned
  AC-03: Given two first-time calls for the same subject arrive at the same time, When both complete, Then
         exactly one userId is created and both responses return it
  AC-04: Given no Authorization header, an expired token or a token from another user pool, When any route
         except health / ready is called, Then 401 UNAUTHENTICATED in the standard error body and no data
  AC-05: Given a valid token, When the mapping cannot be read or written because the store is unavailable,
         Then 503 SERVICE_UNAVAILABLE in the standard error body and no userId is created

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : API Gateway HTTP API JWT authorizer (Cognito, THM01STR39) + in-service claim check; conditional put for the mapping item; log hygiene owned by THM01STR51
Dependencies    : THM01STR02, THM01STR54; THM01STR40 (Cognito pools)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
