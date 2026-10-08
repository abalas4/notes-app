THM01STR05 — Sign in with Google screen

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[MOBILE STORY] THM01STR05 — Sign in with Google screen
Tags: [Mobile] [Android] [Functional] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR01
Component       : mobile/jot (new)
Persona         : As the owner on Android
Goal            : I want a Sign-in screen with "Sign in with Google" that signs me in through Cognito in the system browser
Benefit         : So that I sign in with one tap and never type a password into the app

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
Device classes  : Small phone | Large phone; portrait
UX Spec         : 06-design/ux/THM01FTR01/ux-spec.md — pending (step 1.6); source screens Sign-in (no W-screen yet — design gap for UX spec)
Fidelity        : High-fidelity mockup (Jot design canvas) — confirmed against 08-ux-design.md §2 at step 1.6
Style Guide     : v1.1 incl. SG-15 — pending approval (step 1.6a)
Usability Check : Proposed "Not required — single-user app; the owner is the Product Owner" (PO decides at 1.6)

Screen / flow:
  Layout        : Full-screen welcome: app name, one-line purpose, primary button
  Key Elements  : "Sign in with Google" button; inline error with "Try again"
  States        : Default | Loading (browser open; button disabled) | Error (cancelled / sign-in failed) | Success → Home | Offline
  Navigation    : App start when no session; after sign-out; redirect URI com.jot.app:/oauth2redirect (validated)
Device behaviour:
  Offline       : Button disabled with "Connect to the internet to sign in"
  Permissions   : None
  Push          : None
  Lifecycle     : If the app process is killed while the browser is open, the next start shows the Sign-in screen in its Default state with nothing stored
  Data on device: Access, ID and refresh tokens only in Android Keystore-backed storage (react-native-keychain); nothing else
  Accessibility : TalkBack labels on every control; font scale 200 % reflows; touch targets ≥ 48 dp; reduced motion respected
  Privacy       : None — no data collection change; no store listing (C-05)

Acceptance Criteria:
  AC-01: Given no session, When the owner taps "Sign in with Google" and approves, Then no password field
         is shown in the app, the tokens are stored in Keystore-backed storage, GET /api/v1/me succeeds and
         Home opens
  AC-02: Given the browser sign-in is cancelled, When control returns to the app, Then the Sign-in screen
         shows "Sign-in cancelled" with Try again and nothing is stored
  AC-03: Given the browser returned but the token exchange fails (network error or error response), When
         the result arrives, Then nothing is stored and the Sign-in screen shows "Sign-in failed" with Try
         again
  AC-04: Given no network, When the Sign-in screen is shown, Then the button is disabled with the offline
         message
  AC-05: Given the owner tapped the button and the browser is open, When they tap it again, Then no second
         sign-in starts

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5) (Android app version / build set at release; min supported app version per HLD)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : React Native bare CLI + TypeScript; react-native-app-auth (Authorization Code + PKCE); react-native-keychain; React Navigation auth stack
Dependencies    : THM01STR04; THM01STR40 (Cognito + Google IdP in dev)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
