THM01FTR04 — Labels and navigation drawer

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[BUSINESS FEATURE] THM01FTR04 — Labels and navigation drawer
Tags: [Business] [Functional] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic       : THM01EPC01
Surfaces          : API (apis/jot-api) · Mobile Android (mobile/jot) — iOS later (Epic Surfaces)
Feature Owner     : Product Owner (@abalas4)
Description       : The owner organises notes and checklists with labels: creates, renames and deletes
                    labels (W8), assigns and removes labels on a note through the label picker with
                    create-on-the-fly (W6), and moves between Notes, Reminders, Archive and each label
                    from the navigation drawer, which shows counts (W7). Deleting a label never deletes
                    notes — they only lose the label.

Benefit Hypothesis: If notes can be grouped by a few labels reachable from the drawer, then the owner
                    can find a note in ≤ 2 taps without searching, because most recall is "the work
                    one" or "the home one", not a keyword.
Success Metric    : Share of active notes with ≥ 1 label at 60 days | 0 % (new) | ≥ 50 %

Acceptance Criteria:
  AC-01: Given a note is open, When the owner opens the label picker, types a name that does not exist
         and taps "Create", Then the label is created, assigned to the note, and listed in the drawer
  AC-02: Given labels exist, When the owner ticks or unticks labels in the picker and taps Done, Then
         the note's labels are saved and shown as chips on the note card
  AC-03: Given the "Edit labels" screen, When the owner renames a label, Then every note with that
         label shows the new name; When they delete a label and confirm, Then the label is removed from
         all notes and no note is deleted
  AC-04: Given the drawer is open, When the owner taps a label, Then Home shows only notes with that
         label and the drawer count for the label equals the number of notes shown
  AC-05: Given a label name that already exists (case-insensitive) or is empty, When the owner tries to
         create or rename to it, Then the app refuses with an inline message and the API returns 409 /
         422 respectively

Sizing            : M
WSJF              : (6 + 4 + 2) / 4 = 3.0   (proposed)
PI Target         : PI-2+ (forecast after iteration 03 velocity)
Sprint Target     : PI-2+ — forecast after iteration 03 velocity (was: planned slice 4)
Release Roll-up   : REL-1.0.0 (all child Stories forecast; PI-1 Planning 2026-10-08)
Feature Type      : New
Original Feature  : N/A
Linked Stories    : THM01STR15 [API], THM01STR16 [Mobile] [Android], THM01STR17 [Mobile] [Android], THM01STR18 [Mobile] [Android], THM01STR62 [API] (step 1.3, after story review)
HLD Reference     : THM01FTR04-HLD
LLD Reference     : THM01FTR04-LLD

Dependencies      : THM01FTR02 (notes); THM01FTR06
Constraints       : Online-only (D-07); UX per screens W6, W7, W8.
Decision          : No Trash view in the MVP (story review Q3, 2026-10-08) — the W7 "Trash" entry is
                    hidden; deferred as L-05. Settings stays (sign-out, THM01STR55). Label counts are
                    active notes (not archived, not deleted).
Platform scope    : As THM01FTR01.
ALM Status        : Refined (PR #3, 2026-10-08)
DoR Check         : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ Feature Type
                    · ✅ Description · ✅ Benefit hypothesis · ✅ 5 ACs · ✅ Sized M · ✅ WSJF · ✅ PI Target
                    · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                    ✅ Sprint Target set at PI-1 Planning · ✅ Child Stories (step 1.3)
                    ⚠️ Style guide Approved with SG-15 — step 1.6a · ⚠️ Platform scope minimum OS — HLD (1.7)
DoD Check         : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
