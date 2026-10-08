THM01STR03 — OpenAPI 3.1 contract and contract test

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR03 — OpenAPI 3.1 contract and contract test
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR06
Component       : apis/jot-api
Persona         : As the Jot app developer
Goal            : I want the API's OpenAPI 3.1 document committed as 06-design/api-specs/jot-api.openapi.yaml and checked against the running service in CI
Benefit         : So that the app's typed client is generated from a contract that cannot drift from the code

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/openapi.json
  Auth          : None in local / dev; disabled in prod
  Request Body  : N/A
  Response 2xx  : 200 OpenAPI 3.1 document
  Response 4xx  : 404 in prod
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}

Acceptance Criteria:
  AC-01: Given the service is running, When the generated OpenAPI document is compared with
         06-design/api-specs/jot-api.openapi.yaml, Then there is no difference
  AC-02: Given a change to a route without a spec update, When CI runs the contract test, Then the PR check
         fails
  AC-03: Given the prod environment, When /api/v1/openapi.json is requested, Then it returns 404

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : FastAPI OpenAPI generation; Schemathesis contract tests; openapi-typescript for the app client
Dependencies    : THM01STR01
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
