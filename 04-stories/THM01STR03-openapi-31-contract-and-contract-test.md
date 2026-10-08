THM01STR03 — OpenAPI 3.1 contract and contract test

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR03 — OpenAPI 3.1 contract and contract test
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR06
Component       : apis/jot-api
Persona         : As the owner (as the app developer)
Goal            : I want the API's OpenAPI 3.1 document committed as 06-design/api-specs/jot-api.openapi.yaml and checked against the running service in CI
Benefit         : So that the app's typed client is generated from a contract that cannot drift from the code

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/openapi.json
  Auth          : None in local / dev; route disabled in prod
  Request Body  : N/A
  Response 2xx  : 200 OpenAPI 3.1 document (local / dev)
  Response 4xx  : 404 NOT_FOUND {error:{code,message,traceId}} (prod)
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given the service is built from a PR, When its generated OpenAPI document is compared (normalised,
         key order ignored) with 06-design/api-specs/jot-api.openapi.yaml, Then paths, schemas and
         operation IDs are identical
  AC-02: Given a route is changed and the spec file is not, When the CI contract test runs, Then the job
         fails and names the differing path
  AC-03: Given the local or dev environment, When GET /api/v1/openapi.json is called without a token, Then
         200 with a valid OpenAPI 3.1 document
  AC-04: Given the prod environment, When GET /api/v1/openapi.json is called, Then 404 NOT_FOUND in the
         standard error body
  AC-05: Given the running service, When Schemathesis runs against the spec, Then no response is 5xx and
         every response matches its schema

Story Points    : 3
Sprint Target   : PI-1 iteration 03 (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : FastAPI OpenAPI generation; Schemathesis; openapi-typescript for the app client
Dependencies    : THM01STR01, THM01STR54
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
