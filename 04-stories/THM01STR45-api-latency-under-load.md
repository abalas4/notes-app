THM01STR45 — API latency under load

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR45 — API latency under load
Tags: [Non-Functional] [Performance] [API]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR12
Component       : apis/jot-api
NFR Category    : Performance
Persona         : As the owner using the app
Goal            : I want the API to respond fast at ten times my normal load
Benefit         : So that the app never waits on the server

SLO/Threshold   :
  - Warm p95 < 300 ms at 5 requests per second for 10 minutes over a dataset of 500 notes (cold starts excluded and reported separately)
  - Error rate < 1 % during the test
Test Approach   : k6 scenario (list, create, update notes) against pre-warmed dev; baseline JSON committed in tests/apis/jot-api/load/

Acceptance Criteria:
  AC-01: Given dev is pre-warmed and holds 500 notes, When the k6 scenario (list, create, update) runs at 5
         rps for 10 minutes, Then warm p95 is below 300 ms and errors below 1 %, with cold-start requests
         reported separately
  AC-02: Given the committed baseline JSON, When a later run's p95 is more than 20 % above it, Then the CI
         performance check fails

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 2)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : k6 in Docker; load/<scenario>_test.js and load/<scenario>-baseline.json (folder standard §5)
Dependencies    : THM01STR07, THM01STR08, THM01STR56, THM01STR35
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 2 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
