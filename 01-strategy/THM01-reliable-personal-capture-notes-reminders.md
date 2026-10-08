THM01 — Reliable personal capture of notes, tasks and reminders

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[THEME] THM01 — Reliable personal capture of notes, tasks and reminders
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Vision Statement : Let one person capture a thought, a to-do list or a reminder in two taps or fewer,
                   find it again instantly, and trust that it is never lost and reminders always fire.
Business Outcome : Jot becomes the owner's only notes / checklist / reminder app within 90 days of
                   REL-1.0.0, at a running cost of ≤ US$1 per month.
OKR Reference    : O1: A notes app I trust every day
                     → KR1: ≥ 5 notes or checklists created per week (30 / 60 / 90 days after REL-1.0.0)
                     → KR2: ≥ 99 % of reminders fire within 1 minute of their scheduled time
                     → KR3: crash-free users ≥ 99.5 %; Android ANR rate ≤ 0.47 %
                     → KR4: API running cost ≤ US$1 per month (Device Farm excluded)
Time Horizon     : Short-term (6–12 mo) — Android MVP (REL-1.0.0), then iOS (REL-1.1)
Innovation Type  : Core
Value Stream(s)  : Personal productivity (capture → organise → recall → remind)
Business Sponsor : Product Owner (@abalas4)
Priority         : High
Linked Capabilities: THM01CAP01 (Business), THM01CAP02 (Enabler)
Strategic Metrics:
  - Adoption: notes + checklists created per week — baseline 0 (new product) → target ≥ 5
  - Reminder reliability: share of reminders firing within 1 min of schedule — baseline n/a (new) → ≥ 99 %
  - Stability: crash-free users — baseline n/a (new) → ≥ 99.5 %; ANR rate ≤ 0.47 %
  - Running cost: AWS bill for the API — baseline US$0 → ≤ US$1 per month
Risk / Dependencies: Android 14+ exact-alarm restrictions (reminder reliability); local-notification
                   library support for the chosen React Native version (RAID-015, R-NOTIF);
                   online-only MVP may lose edits when the network drops (offline-first deferred, L-01);
                   AWS Device Farm free minutes are one-time (981.77 remaining).
ALM Status       : Approved (PR #1, 2026-10-08)
DoR Check        : ✅ Sponsor sign-off — Product Owner approved and merged PR #1 (2026-10-08)
                   ✅ Stored at 01-strategy/THM01-<slug>.md
                   ✅ Title and vision statement written
                   ✅ Four measurable KPIs / OKRs defined
                   ✅ Business Sponsor identified and committed (PR #1)
                   ✅ Time horizon and priority assigned
                   ✅ Value Stream owner confirmed: Product Owner (@abalas4)
                   ✅ No duplication — first Theme in this portfolio
DoD Check        : N/A at intake
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
