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
  - p95 < 300 ms (warm) at 5 requests per second for 10 minutes
  - Error rate < 1 % during the test
Test Approach   : k6 scenario (list, create, update notes) against dev; baseline JSON committed in tests/apis/jot-api/load/

Acceptance Criteria:
  AC-01: Given dev at 5 rps for 10 minutes, When the k6 test runs, Then p95 < 300 ms and errors < 1 %
  AC-02: Given a new baseline, When a later run is 20 % slower at p95, Then the performance check fails

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : k6 in Docker; load/<scenario>_test.js and load/<scenario>-baseline.json (folder standard §5)
Dependencies    : THM01STR07, THM01STR35
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 2 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
