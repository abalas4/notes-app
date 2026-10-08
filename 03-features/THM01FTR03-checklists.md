THM01FTR03 — Checklists

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[BUSINESS FEATURE] THM01FTR03 — Checklists
Tags: [Business] [Functional] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic       : THM01EPC01
Surfaces          : API (apis/jot-api) · Mobile Android (mobile/jot) — iOS later (Epic Surfaces)
Feature Owner     : Product Owner (@abalas4)
Description       : The owner creates list notes made of items, checks and unchecks items (checked
                    items move to a "Completed" group with strike-through), sees "N of M done"
                    progress, reorders items by dragging, and can hide completed items, uncheck all,
                    delete completed items, or convert a list to a text note and back. Screens W5 List
                    and W10 List states. Checklists share colours, pin, archive and delete with text
                    notes (THM01FTR02).

Benefit Hypothesis: If to-do lists live next to notes and show progress at a glance, then the owner
                    will keep shopping and task lists in Jot instead of a separate to-do app, because
                    one place for both removes the switch between apps.
Success Metric    : Share of new items created as checklists | n/a (new) | ≥ 1 checklist per week in
                    use at 30 days (counts toward the Epic adoption metric)

Acceptance Criteria:
  AC-01: Given the owner creates a list note, When they add items and check one, Then the item moves to
         "Completed" with strike-through and the progress shows "1 of N done"
  AC-02: Given a list with several items, When the owner drags an item by its handle to a new position,
         Then the new order is saved and is the same after reopening the app
  AC-03: Given a list with completed items, When the owner chooses "Hide completed", "Uncheck all"
         or "Delete completed", Then exactly that action is applied and saved with the note, so
         "Hide completed" stays on after reopening (decision Q5)
  AC-04: Given a list note, When the owner converts it to a text note, Then each item becomes one line
         of the body (checked state dropped after a confirmation), and converting a text note to a
         list turns each non-empty line into an item
  AC-05: Given the network is unavailable, When the owner checks an item, Then the app shows the
         offline state with "Retry" and does not show the item as saved until the API confirms it

Sizing            : M
WSJF              : (8 + 6 + 3) / 5 = 3.4   (proposed)
PI Target         : PI-2+ (forecast after iteration 03 velocity)
Sprint Target     : PI-2+ — forecast after iteration 03 velocity (was: planned slice 3)
Release Roll-up   : REL-1.0.0 (all child Stories forecast; PI-1 Planning 2026-10-08)
Feature Type      : New
Original Feature  : N/A
Linked Stories    : THM01STR12 [API], THM01STR13 [Mobile] [Android], THM01STR14 [Mobile] [Android], THM01STR59 [API], THM01STR60 [Mobile] [Android], THM01STR61 [Mobile] [Android] (step 1.3, after story review)
HLD Reference     : THM01FTR03-HLD
LLD Reference     : THM01FTR03-LLD

Dependencies      : THM01FTR02 (note entity, colours, pin, archive, delete); THM01FTR06
Constraints       : Online-only (D-07); item order and checked state stored on the server with the
                    note's version (optimistic concurrency); UX per screens W5, W10.
Platform scope    : As THM01FTR01.
ALM Status        : Refined (PR #3, 2026-10-08)
DoR Check         : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ Feature Type
                    · ✅ Description · ✅ Benefit hypothesis · ✅ 5 ACs · ✅ Sized M · ✅ WSJF · ✅ PI Target
                    · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                    ✅ Sprint Target set at PI-1 Planning
                    ✅ Child Stories (step 1.3)
                    ⚠️ Style guide Approved with SG-15 — step 1.6a
                    ⚠️ Platform scope minimum OS version — HLD (1.7)
DoD Check         : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
