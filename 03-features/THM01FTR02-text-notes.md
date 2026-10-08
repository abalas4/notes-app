THM01FTR02 — Text notes

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[BUSINESS FEATURE] THM01FTR02 — Text notes
Tags: [Business] [Functional] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic       : THM01EPC01
Surfaces          : API (apis/jot-api) · Mobile Android (mobile/jot) — iOS later (Epic Surfaces)
Feature Owner     : Product Owner (@abalas4)
Description       : The owner creates, reads, edits and deletes plain-text notes with a title and a
                    body, chooses one of 8 note colours, pins notes to the top, archives and
                    unarchives them, and can undo a delete for 5 seconds. Screens W1 Home and W4 Note
                    editor (plain text — rich text is L-02). Every change is saved to the API;
                    with no network the app shows an offline state instead of losing the edit (D-07).

Benefit Hypothesis: If a new note can be started in one tap and is saved without a "Save" step, then
                    the owner will capture ≥ 5 notes or checklists a week, because capture speed
                    decides whether a thought is written down at all.
Success Metric    : Notes + checklists created per week | 0 (new) | ≥ 5 (Epic metric)

Acceptance Criteria:
  AC-01: Given the owner is on Home, When they tap the new-note button, type a title and body and go
         back, Then the note is saved without a separate save action and appears at the top of the
         unpinned notes
  AC-02: Given a note is open, When the owner picks one of the 8 colours or toggles pin or archive,
         Then the change is saved and Home shows the note in the right colour, section (Pinned /
         Others) or the Archive view
  AC-03: Given a note on Home, When the owner deletes it, Then it disappears, a snackbar offers
         "Undo" for 5 seconds, and Undo restores it unchanged; after 5 seconds the delete is final
         for the owner (soft-deleted on the server)
  AC-04: Given the owner is editing a note, When the network is unavailable or the save fails, Then
         the text stays in the editor, an offline / error message with "Retry" is shown, and no edit is
         lost silently
  AC-05: Given the same note was changed elsewhere since it was opened, When the owner saves, Then the
         API rejects the stale version (409) and the app reloads the latest version and tells the owner

Sizing            : M
WSJF              : (10 + 8 + 5) / 5 = 4.6   (proposed)
PI Target         : PI-1
Sprint Target     : TBD at PI Planning (step 1.5) — planned slice 2
Release Roll-up   : None yet — derived from child Stories
Feature Type      : New
Original Feature  : N/A
Linked Stories    : TBD at step 1.3 (≥ 1 [API], ≥ 1 [Mobile] [Android])
HLD Reference     : THM01FTR02-HLD
LLD Reference     : THM01FTR02-LLD

Dependencies      : THM01FTR01 (signed-in user); THM01FTR06 (API foundation, data store, versioning)
Constraints       : Plain text only in the MVP (D-09); online-only (D-07); every entity carries
                    `version` and `updatedAt` and deletes are soft, so offline-first (L-01) can be added
                    later without a breaking change; UX per the Jot design system screens W1, W4.
Platform scope    : As THM01FTR01 (Android phones; minimum OS version TBD in the HLD).
ALM Status        : Refined (PR #3, 2026-10-08)
DoR Check         : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ Feature Type
                    · ✅ Description · ✅ Benefit hypothesis · ✅ 5 ACs · ✅ Sized M · ✅ WSJF · ✅ PI Target
                    · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                    ⚠️ Sprint Target — PI Planning (1.5)
                    ⚠️ Child Stories — step 1.3
                    ⚠️ Style guide Approved with SG-15 — step 1.6a
                    ⚠️ Platform scope minimum OS version — HLD (1.7)
DoD Check         : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
