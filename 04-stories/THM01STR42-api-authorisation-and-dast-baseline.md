THM01STR42 — API authorisation and DAST baseline

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR42 — API authorisation and DAST baseline
Tags: [Non-Functional] [Security] [API]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR11
Component       : apis/jot-api
NFR Category    : Security
Persona         : As the owner protecting my notes
Goal            : I want automated tests that prove every route is authenticated and owner-scoped, plus a ZAP baseline scan of dev
Benefit         : So that nobody can read or change my data through the API

SLO/Threshold   :
  - 100 % of routes except health reject missing / invalid tokens with 401
  - 0 routes return or change another user's item (object-level authorisation test per route)
  - ZAP baseline against dev: 0 High alerts
Test Approach   : pytest security suite generated per route from the OpenAPI spec (two dev-pool users); OWASP ZAP baseline in Docker against dev

Acceptance Criteria:
  AC-01: Given two dev-pool users A and B, When A's token is used on every route with B's item IDs, Then
         every call returns 404 and B's data is unchanged
  AC-02: Given a new route added without auth, When the security suite runs in CI, Then it fails
  AC-03: Given dev is up, When the ZAP baseline runs, Then it reports 0 High alerts

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Tests in 07-source-code-tests/tests/apis/jot-api/security/; zap-rules.conf committed (folder standard §5)
Dependencies    : THM01STR04, THM01STR35
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
