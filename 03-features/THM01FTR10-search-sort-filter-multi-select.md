THM01FTR10 — Search, sort, filter and multi-select

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[BUSINESS FEATURE] THM01FTR10 — Search, sort, filter and multi-select
Tags: [Business] [Functional] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic       : THM01EPC01
Surfaces          : API (apis/jot-api) · Mobile Android (mobile/jot) — iOS later (Epic Surfaces)
Feature Owner     : Product Owner (@abalas4)
Description       : On Home the owner searches notes by text, filters with label chips, sorts (date
                    modified, date created, title A–Z; newest or oldest first; pinned kept on top),
                    switches between grid (two-column masonry) and list view (W1, W2), and long-presses
                    to select several notes and pin / unpin, label, recolour, archive or delete them in
                    one action (W3). Split from the earlier "Organise and find" Feature because finding
                    and bulk-editing are a different journey from labelling (THM01FTR04).

Benefit Hypothesis: If any note can be found by typing a word or picking a chip, and tidied in bulk,
                    then the owner keeps using Jot as notes accumulate, because finding things again is
                    what makes a notes app worth keeping.
Success Metric    : Time to find a known note among 100 | n/a (new) | ≤ 5 s (measured in UAT)

Acceptance Criteria:
  AC-01: Given notes exist, When the owner types a word in "Search notes", Then only notes whose title,
         body or checklist items contain it (case-insensitive) are shown, within 1 s of the last keystroke
  AC-02: Given the sort sheet, When the owner picks a sort field and direction with "Keep pinned notes on
         top" on, Then Pinned notes stay first and each section is ordered as chosen; the choice persists
         after restart
  AC-03: Given label chips above the list, When the owner taps a chip, Then only notes with that label
         are shown and "All" clears the filter
  AC-04: Given the owner long-presses a note and selects two more, When they choose a bulk action (pin /
         unpin, labels, colour, archive, delete), Then the action is applied to exactly the selected notes
         and delete offers 5 s Undo for all of them
  AC-05: Given the view toggle, When the owner switches grid ↔ list, Then the layout changes immediately
         and the choice persists after restart

Sizing            : M
WSJF              : (6 + 3 + 2) / 4 = 2.75   (proposed)
PI Target         : PI-2+ (forecast after iteration 03 velocity)
Sprint Target     : PI-2+ — forecast after iteration 03 velocity (was: planned slice 4)
Release Roll-up   : REL-1.0.0 (all child Stories forecast; PI-1 Planning 2026-10-08)
Feature Type      : New
Original Feature  : N/A
Linked Stories    : THM01STR19 [API], THM01STR20 [API], THM01STR21 [Mobile] [Android], THM01STR22 [Mobile] [Android], THM01STR63 [Mobile] [Android] (step 1.3, after story review)
HLD Reference     : THM01FTR10-HLD
LLD Reference     : THM01FTR10-LLD

Dependencies      : THM01FTR02, THM01FTR03 (content to search); THM01FTR04 (label chips); THM01FTR06
Constraints       : Online-only (D-07) — search runs against the API or the loaded list (decided in the
                    HLD); single user, so no search service is needed at this scale; UX per W1, W2, W3.
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
