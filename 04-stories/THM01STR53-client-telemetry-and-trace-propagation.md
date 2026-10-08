THM01STR53 — Client telemetry and trace propagation

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR53 — Client telemetry and trace propagation
Tags: [Non-Functional] [Observability & Monitoring] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR14
Component       : mobile/jot
NFR Category    : Observability & Monitoring
Persona         : As the owner measuring reminder reliability
Goal            : I want the app to send the reminder_delivered delay to the API and to propagate a trace ID on every API call
Benefit         : So that reminder reliability is measured from real use and client problems can be traced to the server

SLO/Threshold   :
  - ≥ 95 % of displayed reminders report reminder_delivered within 24 h (sent when online)
  - 100 % of API calls carry a W3C traceparent header
  - Telemetry contains no identifiers or note text
Test Approach   : E2E check of the API request log for traceparent; unit tests of the telemetry payload; offline-then-online delivery test

Acceptance Criteria:
  AC-01: Given a reminder is displayed, When the app is next online, Then it posts {delaySeconds} to the
         telemetry endpoint and the metric increases
  AC-02: Given any API call from the app, When it is logged by the API, Then the traceId matches the app's
         traceparent
  AC-03: Given the telemetry payload, When it is inspected, Then it contains only delaySeconds and app
         version

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Small telemetry endpoint POST /api/v1/telemetry/reminder-delivered (contract in LLD); traceparent header in the generated API client
Dependencies    : THM01STR25, THM01STR52
Analytics       : reminder_delivered — when a reminder notification is displayed — {delaySeconds, appVersion} — owner's own app, no consent prompt (Epic metric: reminder on-time rate)
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
