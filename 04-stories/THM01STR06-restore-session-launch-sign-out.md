THM01STR06 — Restore session on launch and sign out

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR06 — Restore session on launch and sign out
Tags: [Mobile] [Android] [Functional] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR01
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want the app to reopen signed in while my refresh token is valid, and a Sign out action in Settings
Benefit         : So that I don't sign in every day, and I can end the session when I want

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR01/ux-spec.md — pending (step 1.6); source screens W7 drawer (Settings entry) — Settings screen is a design gap for UX spec
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Splash while restoring; Settings screen with account row and Sign out
  Key Elements  : Account row (display name), "Sign out" with confirmation
  States        : Default | Loading (token refresh) | Error (refresh failed → Sign-in) | Success | Offline | Background / resume
  Navigation    : Drawer → Settings; sign-out returns to Sign-in with the back stack cleared
Device behaviour:
  Offline       : Valid access token: app opens and shows the offline banner; expired token and no network: Sign-in screen with offline message
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: Tokens in Keystore-backed storage; all tokens and in-memory data removed on sign-out
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a stored refresh token that is still valid, When the app is cold-started, Then Home opens
         without the Sign-in screen
  AC-02: Given the refresh token is expired or revoked, When the app starts, Then the Sign-in screen is
         shown and the stored tokens are deleted
  AC-03: Given the owner is signed in, When they choose Sign out and confirm, Then all tokens are deleted,
         scheduled reminder notifications are kept (they belong to the phone), and the Sign-in screen opens
         with no way back
  AC-04: Given the phone has no network and the access token is still valid, When the app starts, Then Home
         opens with the offline banner

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : react-native-app-auth refresh; react-native-keychain; navigation reset
Dependencies    : THM01STR05
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
                  ⚠️ Design gap: Settings screen not in W1–W12 — added at UX spec (1.6)
                  ⚠️ PO to confirm: should sign-out also cancel scheduled reminders? (AC-03 assumes kept)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
