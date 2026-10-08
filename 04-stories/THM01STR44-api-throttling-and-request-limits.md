THM01STR44 — API throttling and request limits

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR44 — API throttling and request limits
Tags: [Non-Functional] [Security] [API]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR11
Component       : apis/jot-api
NFR Category    : Security
Persona         : As the owner paying the AWS bill
Goal            : I want rate limits on the HTTP API and size limits on every request
Benefit         : So that abuse of the public endpoint cannot run up cost or overload the service

SLO/Threshold   :
  - HTTP API stage throttle: 10 requests per second steady, burst 20 (LLD may tune) → 429
  - Request bodies > 64 KB rejected with 413 before reaching business logic
  - Every string field has a maximum length in the OpenAPI schema
Test Approach   : k6 burst test against dev; contract tests for limits

Acceptance Criteria:
  AC-01: Given dev, When 50 requests are sent within one second, Then requests above the limit get 429 and
         the service stays healthy
  AC-02: Given a 65 KB body, When it is POSTed, Then 413 PAYLOAD_TOO_LARGE is returned
  AC-03: Given the OpenAPI document, When it is linted, Then every string property has maxLength

Story Points    : 2
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : API Gateway HTTP API throttling (OpenTofu); FastAPI body-size middleware
Dependencies    : THM01STR39, THM01STR03
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
