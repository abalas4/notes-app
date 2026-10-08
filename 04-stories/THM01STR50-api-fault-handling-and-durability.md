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
Goal            : I want the API to fail safely when its data store fails and never acknowledge a write that was not stored
Benefit         : So that no note is ever lost silently

SLO/Threshold   :
  - Every 2xx write is durable (read-after-write returns it)
  - Store unavailable or throttling → 503 SERVICE_UNAVAILABLE in the standard body with Retry-After: 2 within 5 s; no partial writes; at most 3 store attempts
  - API monthly availability target 99.5 % (confirmed in the HLD)
Test Approach   : Fault-injection integration tests (DynamoDB Local stopped, throttling, timeouts); read-after-write checks

Acceptance Criteria:
  AC-01: Given DynamoDB is unavailable, When a note is created, Then 503 SERVICE_UNAVAILABLE with
         Retry-After is returned within 5 s and nothing is stored
  AC-02: Given the store throttles every request, When a note is created, Then 503 with Retry-After is
         returned within 5 s after at most 3 store attempts and nothing is stored
  AC-03: Given the store times out during an update or delete, When the call is made, Then 503 with
         Retry-After is returned and the note is unchanged when read again
  AC-04: Given a 201 or 200 for a write, When the note is read immediately, Then the same content is
         returned

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 2)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : botocore retry configuration; timeouts; resilience tests in tests/apis/jot-api/resilience/
Dependencies    : THM01STR02, THM01STR54, THM01STR07, THM01STR08
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
