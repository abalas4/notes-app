THM01FTR01 — Sign in with Google and account session

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[BUSINESS FEATURE] THM01FTR01 — Sign in with Google and account session
Tags: [Business] [Functional] [API] [Mobile] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic       : THM01EPC01
Surfaces          : API (apis/jot-api) · Mobile Android (mobile/jot) — iOS later (Epic Surfaces)
Feature Owner     : Product Owner (@abalas4)
Description       : The owner signs in with their Google account through Cognito (Authorization Code +
                    PKCE in the system browser), stays signed in across app restarts, and can sign out.
                    The API accepts only requests with a valid Cognito access token and maps the
                    token's subject to an internal user ID from day one (Cognito native accounts come
                    later, L-04).

Benefit Hypothesis: If signing in takes one tap on a Google account and the session survives
                    restarts, then the owner will open Jot as often as their old notes app, because
                    repeated logins are the main friction for a capture tool.
Success Metric    : Sign-ins needed per week after the first | n/a (new) | ≤ 1 (only after sign-out
                    or token expiry beyond the refresh window)

Acceptance Criteria:
  AC-01: Given the app is installed and nobody is signed in, When the owner taps "Sign in with Google"
         and completes the Google consent, Then the Home screen opens with the owner's notes and no
         password is entered in the app
  AC-02: Given the owner is signed in, When the app is closed and reopened (including after a phone
         restart), Then Home opens without a sign-in prompt while the refresh token is valid
  AC-03: Given the owner is signed in, When they choose "Sign out" and confirm, Then the refresh
         token is revoked at Cognito, all tokens are removed from the Keystore-backed storage, all
         scheduled reminder notifications are cancelled, and the Sign-in screen is shown (decisions
         Q1, Q13)
  AC-04: Given a request to any API route except health, When it has no access token or an expired /
         invalid one, Then the API returns 401 with the standard error body and no data
  AC-05: Given the sign-in page is open, When the owner cancels it or the network fails, Then the app
         returns to the Sign-in screen with a clear message and a "Try again" action

Sizing            : M
WSJF              : (8 + 10 + 8) / 5 = 5.2   (proposed; every other Feature needs a signed-in user)
PI Target         : PI-1
Sprint Target     : TBD at PI Planning (step 1.5) — planned slice 1
Release Roll-up   : None yet — derived from child Stories (forecast at PI Planning)
Feature Type      : New
Original Feature  : N/A
Linked Stories    : THM01STR04 [API], THM01STR05 [Mobile] [Android], THM01STR06 [Mobile] [Android] (step 1.3)
HLD Reference     : THM01FTR01-HLD
LLD Reference     : THM01FTR01-LLD

Dependencies      : THM01FTR06 (API foundation); THM01FTR09 (Cognito user pools and the Google client
                    secret in SSM); Google Cloud OAuth client created by the owner.
Constraints       : Cognito Lite tier; Google federation only in production (D-05); dev pool has native
                    test users for automated tests; no client secret in the app; tokens only in
                    Keystore-backed storage (MASVS L1).
Platform scope    : Android, phones, portrait; minimum OS version TBD in the HLD (target ≥ 95 % of
                    active devices); React Native bare CLI (D-01); device matrix plan §5.3; distribution
                    by CI-signed APK, no store (C-05).
ALM Status        : Refined (PR #3, 2026-10-08)
DoR Check         : ✅ Stored at 03-features/THM01FTR01-<slug>.md · ✅ Parent Epic linked · ✅ Type tags
                    · ✅ Surfaces filled (API, Mobile Android) · ✅ Feature Type New / Original N/A
                    · ✅ Description · ✅ Benefit hypothesis · ✅ 5 ACs in Gherkin · ✅ Sized M · ✅ WSJF
                    · ✅ PI Target · ✅ HLD / LLD IDs assigned · ✅ Dependencies and constraints · ✅ Owner
                    ⚠️ Sprint Target — PI Planning (1.5)
                    ✅ Child Stories (step 1.3)
                    ⚠️ Style guide Approved with SG-15 — step 1.6a
                    ⚠️ Platform scope: minimum OS version and technology ADR — HLD (1.7)
DoD Check         : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
