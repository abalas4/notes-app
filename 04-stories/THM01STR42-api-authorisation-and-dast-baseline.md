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
  - 100 % of routes except health / ready reject missing, expired or malformed tokens with 401
  - 0 routes return or change another user's item (object-level authorisation test per route)
  - ZAP baseline against dev: 0 High alerts
Test Approach   : pytest security suite generated per route from the OpenAPI spec using the two dev-pool test users; OWASP ZAP baseline in Docker against dev

Acceptance Criteria:
  AC-01: Given users A and B and every route in the OpenAPI spec that takes an item ID, When A's token is
         used with B's item ID to read, change or delete, Then the response is 404 and B's item is
         unchanged
  AC-02: Given the list and create routes, When A calls them, Then only A's items are returned or created
  AC-03: Given every route except health and ready, When called with no token, an expired token or a
         malformed token, Then the response is 401 in the standard error body
  AC-04: Given a new route is added without an auth requirement, When the security suite runs in CI, Then
         it fails and names the route
  AC-05: Given dev is up, When the ZAP baseline runs, Then it reports 0 High alerts

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Tests in 07-source-code-tests/tests/apis/jot-api/security/; zap-rules.conf committed (folder standard §5)
Dependencies    : THM01STR04, THM01STR35, THM01STR40 (test users)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
