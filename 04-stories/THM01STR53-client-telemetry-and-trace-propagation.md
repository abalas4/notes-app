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
Goal            : I want the app to report each displayed reminder's delay and to send a trace ID with every API call
Benefit         : So that reminder reliability is measured from real use and app problems can be traced to the server

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
UX Spec         : N/A — no new screen
Offline         : When offline, reminder_delivered events are queued on the device and sent once when the connection returns
Data on device  : Queue of {delaySeconds, appVersion} entries only (no personal data) in app storage; cleared on sign-out

SLO/Threshold   :
  - ≥ 95 % of displayed reminders reported within 24 h (monitored in the benefit report, not a test gate)
  - 100 % of API calls carry a W3C traceparent header
  - Telemetry body has exactly delaySeconds and appVersion
Test Approach   : E2E check of API logs for the traceparent; unit tests of the payload; offline-then-online delivery test

Acceptance Criteria:
  AC-01: Given a reminder is displayed while online, When the app reports it, Then exactly one POST
         /api/v1/telemetry/reminder-delivered is sent whose body has exactly the keys delaySeconds
         (integer) and appVersion (string)
  AC-02: Given a reminder is displayed while offline, When the connection returns, Then the queued event is
         sent once and removed from the queue
  AC-03: Given the telemetry post fails (5xx or timeout), When the app retries, Then it retries up to 3
         times with backoff, shows the owner no error, and keeps the event queued if all fail
  AC-04: Given any API call from the app, When the API logs it, Then the logged traceId matches the app's
         traceparent

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 5
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : traceparent header in the generated API client; small persisted queue
Dependencies    : THM01STR25, THM01STR72, THM01STR51
Analytics       : reminder_delivered — when a reminder notification is displayed — {delaySeconds, appVersion} — owner's own app, no consent prompt; no privacy regime (Epic metric: reminder on-time rate)
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
