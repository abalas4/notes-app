THM01FTR12 — Performance SLOs for app and API

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL FEATURE] THM01FTR12 — Performance SLOs for app and API
Tags: [Non-Functional] [Performance] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC01
Surfaces           : API (apis/jot-api) · Mobile Android (mobile/jot)
NFR Category       : Performance
Coverage Status    : Evolving — owner Architecture Lead (@abalas4); review point: HLD approval (step 1.7).
                     Matches THM01EPC01 coverage row 1.
Feature Owner      : Architecture Lead (@abalas4)
Description        : Jot must feel instant for capture: the app starts quickly, screens switch without
                     lag, and API calls return fast even when the Lambda function starts cold.

SLO / Threshold    :
  - API latency p95 < 300 ms warm and < 1 s on a cold start, at 5 requests per second for 10 minutes
    (personal-use load × 10)
  - App cold start to an interactive Home ≤ 2 s on the low-end emulator tier
  - Screen transitions ≤ 300 ms; list scrolling at 60 fps with 500 notes; no network or disk I/O on the
    main thread
  - Search results shown within 1 s of the last keystroke with 500 notes

Test Strategy      : k6 smoke-load test against the local stack and `dev`; cold-start measurement from
                     X-Ray; Android macro-benchmarks / Perfetto traces on the low-end emulator; Appium timing
                     checks for search.

Acceptance Criteria:
  AC-01: Given `dev` at 5 requests per second for 10 minutes, When the k6 test runs, Then API p95 latency is
         below 300 ms and the error rate is below 1 %
  AC-02: Given the function has been idle long enough to start cold, When the first request arrives, Then it
         completes in under 1 s
  AC-03: Given the low-end emulator tier with 500 notes, When the app is cold-started, Then Home is
         interactive within 2 s and scrolling stays at 60 fps

Sizing             : S
PI Target          : PI-1
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : TBD at step 1.3
HLD Reference      : THM01FTR12-HLD
LLD Reference      : THM01FTR12-LLD

ALM Status         : Refined (PR #3, 2026-10-08)
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ NFR category
                     · ⚠️ SLOs proposed (plan §12 and plugin mobile defaults) — Product Owner confirms by
                     approving this PR · ✅ Test strategy · ✅ 3 ACs · ✅ Sized S · ✅ PI Target · ✅ HLD / LLD IDs
                     · ✅ Owner · ⚠️ Child Stories — step 1.3
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
