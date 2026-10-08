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
Goal            : I want structured JSON logs with trace IDs, X-Ray traces, and an automated check that no personal data or token is logged
Benefit         : So that I can follow any request end to end without exposing my notes

SLO/Threshold   :
  - 100 % of request log lines are JSON with traceId, route, status, latency
  - 0 log lines with tokens, note text, emails or names (scan over the full test run)
  - Log retention 14 days
Test Approach   : Log-scan step in CI over integration and E2E logs; X-Ray trace presence check

Acceptance Criteria:
  AC-01: Given an API request in dev, When it completes, Then one JSON log line and one X-Ray trace share
         the same traceId
  AC-02: Given the integration suite has run, When the log scan runs, Then it finds no tokens, note text or
         email addresses
  AC-03: Given the log group, When its settings are read, Then retention is 14 days

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : structlog; OpenTelemetry → X-Ray (ADOT); log scanner script under scripts/
Dependencies    : THM01STR01
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
