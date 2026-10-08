THM01FTR14 — Observability and monitoring

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL FEATURE] THM01FTR14 — Observability and monitoring
Tags: [Non-Functional] [Observability & Monitoring] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC01
Surfaces           : API (apis/jot-api) · Mobile Android (mobile/jot)
NFR Category       : Observability & Monitoring
Coverage Status    : Evolving — owner Architecture Lead (@abalas4); review point: HLD approval (step 1.7).
                     Matches THM01EPC01 coverage row 6.
Feature Owner      : Architecture Lead (@abalas4)
Description        : Problems are seen before the owner notices them, and the Epic's success metrics can
                     be measured — without collecting any note content or personal data.

SLO / Threshold    :
  - 100 % of API log lines are structured JSON with a trace ID; 0 log lines contain tokens, note text or
    email addresses
  - Every SLO in THM01FTR12 and THM01FTR13 has a CloudWatch alarm (within the 10 free alarms)
  - Metrics `note_created` and `reminder_delivered` (counts / delay only) available for the Epic benefit
    reports; crash reporting active in release builds
  - Log retention 14 days (cost)

Test Strategy      : Log-scan test in CI for forbidden fields; alarm tests by forcing each condition in
                     `dev`; trace propagation check app → API in E2E runs.

Acceptance Criteria:
  AC-01: Given an API request, When it is processed, Then one structured log line with the trace ID is
         written and an X-Ray trace exists for the same ID
  AC-02: Given the E2E suite has run, When all logs and metrics are scanned, Then no token, note text or email
         address appears
  AC-03: Given an SLO alarm condition is forced in `dev` (e.g. error rate > 5 % for 5 minutes), When the
         period ends, Then the alarm fires and notifies the owner's email

Sizing             : S
PI Target          : PI-1
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : TBD at step 1.3
HLD Reference      : THM01FTR14-HLD
LLD Reference      : THM01FTR14-LLD

ALM Status         : Refined (PR #3, 2026-10-08)
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ NFR category
                     · ⚠️ SLOs proposed — Product Owner confirms by approving this PR · ✅ Test strategy
                     · ✅ 3 ACs · ✅ Sized S · ✅ PI Target · ✅ HLD / LLD IDs · ✅ Owner
                     · ⚠️ Child Stories — step 1.3
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
