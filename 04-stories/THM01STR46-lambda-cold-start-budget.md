THM01STR46 — Lambda cold start budget

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR46 — Lambda cold start budget
Tags: [Non-Functional] [Performance] [API]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR12
Component       : apis/jot-api
NFR Category    : Performance
Persona         : As the owner opening the app after a while
Goal            : I want the first API call after the function was idle to finish in under a second
Benefit         : So that the app feels instant even when it has not been used for hours

SLO/Threshold   :
  - Cold start request < 1 s end to end (p95 over 20 cold starts)
  - Image size ≤ 200 MB (slim, arm64)
Test Approach   : Script forcing cold starts (config change) and reading X-Ray init + duration; image size check in CI

Acceptance Criteria:
  AC-01: Given 20 forced cold starts in dev, When their durations are read from X-Ray, Then p95 < 1 s
  AC-02: Given the API image, When it is built in CI, Then its size is ≤ 200 MB

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Lambda arm64, Lambda Web Adapter, lazy imports, slim base image
Dependencies    : THM01STR39
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
