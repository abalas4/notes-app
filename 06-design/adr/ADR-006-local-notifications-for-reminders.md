# ADR-006: Reminders delivered as local notifications on the phone; library chosen after vetting
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR05 HLD / LLD / DFMEA; ADR-001; RAID log (R-NOTIF, L-03)

## Context
Reminders must fire on time (Epic metric: ≥ 99 % within 1 minute) with Mark done / Snooze / Open
actions (W11). The MVP serves one person on one phone. Android 14+ denies exact alarms by default.

## Options considered
1. **Local notifications scheduled on the phone** from the synced reminder data — US$0, work without a
   network, available on Android and iOS.
2. Server push (FCM / APNs + EventBridge Scheduler) — needed only for multiple devices; more moving parts.

## Decision
- Local notifications in the MVP; server push is deferred (RAID log, L-03).
- Library: **Notifee is provisional.** Before the THM01FTR05 LLD is approved it passes dependency
  vetting: 7-day cooling period, release and issue activity, support for our React Native version and
  the New Architecture, Android 14+ (and iOS), licence. If it fails: `expo-notifications` (works in bare
  React Native) or a small native AlarmManager module, recorded in a new ADR that supersedes this
  library line. The decision "local reminders" does not depend on the library (RAID log, R-NOTIF).
- The W11 notification is drawn by the OS, so it follows the system style, not the mockup card exactly.
  Its **Snooze** action opens the app's W12 snooze sheet (an action button cannot open a menu inside the
  notification). Tapping the body opens the note through a validated deep link.

## Consequences
- Exact alarms: in-context permission rationale (style guide SG-15) and a denied path with inexact
  alarms and a message — a DFMEA row in THM01FTR05.
- Sign-out cancels all scheduled reminders; a reminder due while the phone was off fires after boot,
  marked overdue (Story decisions Q1, Q8).
- OEM battery optimisation can delay alarms; proven only on real devices (ADR-002).
