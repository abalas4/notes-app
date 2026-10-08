THM01STR55 — Sign out from Settings

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR55 — Sign out from Settings
Tags: [Mobile] [Android] [Functional] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR01
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want a Settings screen with my account and a Sign out action that removes everything of mine from the phone
Benefit         : So that when I sign out, nothing of mine is left on the phone or usable elsewhere

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR01/ux-spec.md — pending (step 1.6); source screens Settings (design gap — UX spec); W7 drawer entry
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Settings screen: account row, Sign out with confirmation
  Key Elements  : Account row (display name from the ID token); "Sign out"; confirmation dialog
  States        : Default | Signing out | Error (revoke failed — local sign-out still completes) | Offline
  Navigation    : Drawer → Settings; after sign-out the Sign-in screen with the back stack cleared
Device behaviour:
  Offline       : Sign-out works offline: local tokens and reminders are removed; the refresh-token revoke is skipped and the token simply expires
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: On sign-out: all tokens deleted, scheduled reminder notifications cancelled (decision Q1), in-memory notes cleared
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given the owner is signed in, When they choose Sign out and confirm, Then the refresh token is
         revoked at Cognito, all stored tokens are deleted, all scheduled reminder notifications are
         cancelled and the Sign-in screen opens
  AC-02: Given the owner has just signed out, When they press Android Back on the Sign-in screen, Then the
         app closes without showing Home or any note
  AC-03: Given the sign-out confirmation, When the owner cancels, Then nothing changes
  AC-04: Given there is no network, When the owner signs out, Then the local sign-out completes the same
         way and the app does not wait for the revoke

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Cognito revoke endpoint; react-native-keychain; local-notification cancelAll; navigation reset
Dependencies    : THM01STR05, THM01STR18 (drawer), THM01STR25 (scheduled reminders)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
                  ⚠️ Design gap: Settings screen not in W1–W12 — added at UX spec (1.6)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
