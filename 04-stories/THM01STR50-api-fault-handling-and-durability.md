THM01STR50 — API fault handling and durability

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR50 — API fault handling and durability
Tags: [Non-Functional] [Availability & Reliability] [API]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR13
Component       : apis/jot-api
NFR Category    : Availability & Reliability
Persona         : As the owner saving notes
Goal            : I want the API to fail safely when its data store or a dependency fails, and never acknowledge a write that was not stored
Benefit         : So that no note is ever lost silently

SLO/Threshold   :
  - Every 2xx write is durable (read-after-write returns it)
  - Store unavailable → 503 with retry hint within 5 s; no partial writes
  - API monthly availability target 99.5 % (to be confirmed in the HLD)
Test Approach   : Fault-injection integration tests (DynamoDB Local stopped, throttling, timeouts); read-after-write checks

Acceptance Criteria:
  AC-01: Given DynamoDB is unavailable, When a note is created, Then 503 SERVICE_UNAVAILABLE is returned
         within 5 s and nothing is stored
  AC-02: Given a 201 for a new note, When it is read immediately, Then the same content is returned
  AC-03: Given throttling from the store, When a request is retried by the service, Then it uses bounded
         exponential backoff (≤ 3 tries) and then returns 503

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : botocore retry config; timeouts; resilience tests in tests/apis/jot-api/resilience/
Dependencies    : THM01STR02, THM01STR07
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
