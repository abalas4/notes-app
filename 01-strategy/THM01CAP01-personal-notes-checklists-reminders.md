THM01CAP01 — Personal notes, checklists and reminders

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[CAPABILITY] THM01CAP01 — Personal notes, checklists and reminders
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Theme     : THM01
Type             : Business
Description      : A mobile app in which one signed-in person writes colour-coded notes and
                   checklists, organises them with labels, search and pinning, and sets
                   date / time reminders that arrive as phone notifications with Mark done,
                   Snooze and Open actions. Data is kept in the cloud, so it survives a
                   reinstall or a new phone.
Benefit Hypothesis: If notes, checklists and reminders live in one fast, calm app whose
                   reminders always fire, then the owner will stop using other notes and
                   reminder apps, because scattered tools and missed reminders are the reasons
                   things get forgotten today.
Success Metrics  :
  - Notes + checklists created per week: 0 → ≥ 5 (30 / 60 / 90 days after REL-1.0.0)
  - Reminders firing within 1 min of schedule: n/a → ≥ 99 %
  - Crash-free users: n/a → ≥ 99.5 %; Android ANR rate ≤ 0.47 %
WSJF Priority    : Value 9 | Time Criticality 5 | Risk Reduction 4 | Job Size 8 → WSJF 2.25
                   (proposed; Product Owner confirms at PI Planning)
Sizing           : M
Affected ARTs    : Jot team (solo)
PI Target        : PI-1
Linked Epics     : THM01EPC01
Business Owner   : Product Owner (@abalas4)
Arch Owner       : Architecture Lead (@abalas4)
Dependencies     : THM01CAP02 (build, test and cloud delivery runway) must deliver CI and the dev
                   environment before the first app Story can be tested on a device.
Constraints      : Android first, iOS later from the same codebase; no Play Store distribution
                   (approved deviation C-05); online-only MVP (D-07); AWS always-free services
                   wherever possible; public repository.
ALM Status       : Analysing
DoR Check        : ✅ Stored at 01-strategy/THM01CAP01-<slug>.md
                   ✅ Parent Theme THM01 linked
                   ✅ Type Business
                   ✅ Description clear to non-technical readers
                   ✅ Benefit hypothesis (If / then / because)
                   ✅ Success metrics with baselines and targets
                   ✅ Sized M
                   ✅ ART identified
                   ✅ Business Owner and Architecture Owner named
                   ✅ Dependencies and constraints documented
                   ⚠️ LBC approval — Product Owner approves THM01EPC01 in its pull request
DoD Check        : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
