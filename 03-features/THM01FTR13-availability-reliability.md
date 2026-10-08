THM01FTR13 — Availability and reliability

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL FEATURE] THM01FTR13 — Availability and reliability
Tags: [Non-Functional] [Availability & Reliability] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC01
Surfaces           : API (apis/jot-api) · Mobile Android (mobile/jot)
NFR Category       : Availability & Reliability
Coverage Status    : Defined for the app metrics (Epic Success Metrics confirmed by the Product Owner);
                     Evolving for API availability — owner Architecture Lead (@abalas4), review point HLD
                     approval (step 1.7). Matches THM01EPC01 coverage row 3.
Feature Owner      : Architecture Lead (@abalas4)
Description        : The owner must be able to trust Jot: it does not crash, does not freeze, never loses a
                     note, and reminders fire on time.

SLO / Threshold    :
  - Crash-free users ≥ 99.5 % and Android ANR rate ≤ 0.47 % (30-day window)
  - ≥ 99 % of reminders fire within 1 minute of the scheduled time (30-day window)
  - 0 lost notes: every acknowledged write is durable; failed writes are visible with Retry (D-07)
  - API monthly availability: initial target 99.5 % (TBD, confirmed in the HLD)

Test Strategy      : Device-matrix runs (emulator → phone → Device Farm) with crash and ANR checks;
                     reminder timing tests including Doze / idle and reboot; fault injection on the API
                     (store unavailable, timeouts) and network loss mid-edit; DFMEA rows for each failure
                     mode with S ≥ 8.

Acceptance Criteria:
  AC-01: Given the full E2E suite on the emulator matrix and the phone, When it runs, Then there are 0 crashes
         and 0 ANRs
  AC-02: Given 20 reminders scheduled over 2 hours with the phone idle (Doze), When their times arrive, Then
         at least 19 fire within 1 minute and none is missed
  AC-03: Given the network drops in the middle of saving a note, When the save fails, Then the text is kept,
         Retry succeeds once the network returns, and the stored note equals what was typed
  AC-04: Given the phone restarts, When it boots, Then all future reminders are rescheduled

Sizing             : M
PI Target          : PI-1
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : THM01STR48 [Mobile] [Android], THM01STR49 [Mobile] [Android], THM01STR50 [API] (step 1.3)
HLD Reference      : THM01FTR13-HLD
LLD Reference      : THM01FTR13-LLD

ALM Status         : Refined (PR #3, 2026-10-08)
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ NFR category
                     · ✅ App SLOs measurable (Epic metrics) · ⚠️ API availability target TBD — HLD (1.7)
                     · ✅ Test strategy · ✅ 4 ACs · ✅ Sized M · ✅ PI Target · ✅ HLD / LLD IDs · ✅ Owner
                     · ✅ Child Stories (step 1.3)
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
