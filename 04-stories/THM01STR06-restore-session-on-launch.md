THM01STR06 — Restore session on launch

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR06 — Restore session on launch
Tags: [Mobile] [Android] [Functional] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR01
Component       : mobile/jot
Persona         : As the owner on Android
Goal            : I want the app to reopen signed in while my session is valid, and to handle expiry and offline starts sensibly
Benefit         : So that I don't sign in every day, and a bad connection never signs me out

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR01/ux-spec.md — pending (step 1.6); source screens Splash / Home
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Splash while restoring, then Home or Sign-in
  Key Elements  : —
  States        : Loading (restoring) | Success → Home | Expired → Sign-in | Offline | Background / resume
  Navigation    : App start; resume after a long background period
Device behaviour:
  Offline       : Valid access token: Home with offline banner. Expired access token and no network: Sign-in with offline message, refresh token kept
  Permissions   : None
  Push          : None
  Lifecycle     : Process death or app switch restores the current screen and any unsaved text
  Data on device: Tokens in Keystore-backed storage; deleted only when the server rejects the refresh token
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given a stored refresh token that is still valid, When the app is cold-started, Then Home opens
         without the Sign-in screen
  AC-02: Given the server rejects the refresh token (expired or revoked), When the app starts, Then the
         stored tokens are deleted and the Sign-in screen opens
  AC-03: Given the access token is still valid and there is no network, When the app starts, Then Home
         opens with the offline banner
  AC-04: Given the access token has expired and there is no network, When the app starts, Then the Sign-in
         screen shows "Connect to the internet to sign in" and the stored refresh token is not deleted

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : react-native-app-auth refresh; react-native-keychain
Dependencies    : THM01STR05; THM01STR09 (Home)
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
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
