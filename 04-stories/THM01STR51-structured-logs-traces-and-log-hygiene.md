THM01STR51 — Structured logs, traces and log hygiene

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR51 — Structured logs, traces and log hygiene
Tags: [Non-Functional] [Observability & Monitoring] [API]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR14
Component       : apis/jot-api
NFR Category    : Observability & Monitoring
Persona         : As the owner diagnosing a problem
Goal            : I want every request log line structured with a trace ID, X-Ray traces, and an automated check that no personal data or token is ever logged
Benefit         : So that I can follow any request end to end without exposing my notes

SLO/Threshold   :
  - 100 % of request log lines are valid JSON with traceId, route, status and latencyMs (format from THM01STR54)
  - 0 log lines with tokens, note text, email addresses or names over the integration and E2E runs
  - Log retention 14 days
Test Approach   : Log-scan step in CI over integration and E2E logs (with a seeded negative control); X-Ray trace presence check

Acceptance Criteria:
  AC-01: Given any API request in dev, including failing (4xx / 5xx) ones, When it completes, Then exactly
         one valid JSON log line with traceId, route, status and latencyMs is written and an X-Ray trace
         with the same traceId exists
  AC-02: Given the integration and E2E suites have run, When the log scan runs over all captured logs, Then
         it finds 0 tokens, note text, email addresses or names
  AC-03: Given a log fixture seeded with a fake token and a fake email address, When the log scan runs,
         Then it fails and names both
  AC-04: Given the jot-* log groups, When their settings are read, Then retention is 14 days

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : structlog; OpenTelemetry → X-Ray (ADOT); log scanner script under scripts/
Dependencies    : THM01STR54, THM01STR32
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
