THM01STR01 — API service skeleton with health and readiness

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR01 — API service skeleton with health and readiness
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR06
Component       : apis/jot-api (new)
Persona         : As the owner (through the Jot app)
Goal            : I want a running jot-api service with /api/v1/health and /api/v1/ready, runnable locally with Docker Compose and DynamoDB Local
Benefit         : So that every later API Story builds on one tested skeleton and I can check the service is up

Endpoint Contract:
  Method        : GET
  Path          : /api/v1/health · /api/v1/ready
  Auth          : None (health and readiness only)
  Request Body  : N/A
  Response 2xx  : 200 {status:"ok", version} · /ready 200 {status:"ready", checks:{store:"ok"}}
  Response 4xx  : /ready 503 SERVICE_UNAVAILABLE {error:{code,message,traceId}} with checks.store "unavailable"
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given the local Compose stack is up, When GET /api/v1/health is called, Then 200 with status "ok"
         and the build version
  AC-02: Given DynamoDB Local is reachable, When GET /api/v1/ready is called, Then 200 with checks.store
         "ok"
  AC-03: Given DynamoDB Local is stopped, When GET /api/v1/ready is called, Then 503 SERVICE_UNAVAILABLE in
         the standard error body with checks.store "unavailable" within 2 s

Story Points    : 3
Sprint Target   : PI-1 iteration 01 (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Python 3.13, FastAPI, Pydantic v2; container for Lambda arm64 + Lambda Web Adapter; docker-compose.yml at 07-source-code-tests/ (folder standard §6)
Dependencies    : THM01STR29 (API CI gates) runs on its PR; THM01STR54 (error body)
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
