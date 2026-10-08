THM01STR72 — Reminder delivery telemetry endpoint

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR72 — Reminder delivery telemetry endpoint
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR14
Component       : apis/jot-api
Persona         : As the owner (through the Jot app)
Goal            : I want an endpoint that accepts the delay of a displayed reminder
Benefit         : So that the reminder on-time rate is measured from real use

Endpoint Contract:
  Method        : POST
  Path          : /api/v1/telemetry/reminder-delivered
  Auth          : Bearer JWT (Cognito access token)
  Request Body  : {delaySeconds: integer 0..86400, appVersion: string ≤ 20} — no other keys accepted
  Response 2xx  : 202 (no body)
  Response 4xx  : 400 VALIDATION_ERROR (missing / extra keys, out of range) — {error:{code,message,traceId}}
  Response 5xx  : 503 SERVICE_UNAVAILABLE / 500 INTERNAL — {error:{code,message,traceId}}
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a valid body {delaySeconds: 12, appVersion: "1.0.0"}, When it is posted, Then 202 and the
         reminder_delivered metric records 12
  AC-02: Given delaySeconds of -1 or 86401, a missing key or an extra key, When it is posted, Then 400
         VALIDATION_ERROR and nothing is recorded
  AC-03: Given a valid post, When it is logged, Then the log line has no note or user identifiers beyond
         the standard userId field

Story Points    : 2
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Small router publishing CloudWatch EMF
Dependencies    : THM01STR54, THM01STR04
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
