THM01STR43 — App MASVS L1 controls

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL STORY] THM01STR43 — App MASVS L1 controls
Tags: [Non-Functional] [Security] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR11
Component       : mobile/jot
NFR Category    : Security
Persona         : As the owner protecting my phone data
Goal            : I want the app to meet OWASP MASVS L1: secure token storage, no cleartext traffic, validated deep links and no secrets in the APK
Benefit         : So that a lost phone or a malicious link cannot expose my notes or my session

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)
UX Spec         : N/A — no new screen; the "Note not found" message reuses the Home error state (THM01STR65)
Offline         : N/A
Data on device  : Tokens only in Keystore-backed storage; excluded from Android backup; cleared on sign-out

SLO/Threshold   :
  - Tokens only in Android Keystore-backed storage; 0 tokens in AsyncStorage, logcat or backups
  - Cleartext traffic disabled; TLS only
  - MobSF static scan: 0 High findings; 0 secrets, keys or AWS identifiers in the APK
  - Deep links accept only jot://note/{id} and only for the signed-in user's notes
Test Approach   : MobSF static scan in CI (THM01STR30); gitleaks over the unpacked APK; emulator test inspecting storage, backup and logcat; unit tests for deep-link parsing

Acceptance Criteria:
  AC-01: Given a build APK, When MobSF scans it and gitleaks scans the unpacked APK, Then there are 0 High
         findings and 0 secrets, keys or AWS account IDs
  AC-02: Given the app is signed in and used, When app storage, Android backup data and logcat are
         inspected on the emulator, Then no token appears outside the Keystore-backed store
  AC-03: Given the build, When the app attempts an http:// request, Then it is blocked
  AC-04: Given a malformed deep link, When it is opened, Then Home shows "Note not found" and no network
         request is made
  AC-05: Given a deep link to a note ID that is not the user's, When it is opened, Then Home shows "Note
         not found" after the API returns 404

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 2)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : react-native-keychain; network_security_config (cleartextTrafficPermitted=false); backup rules
Dependencies    : THM01STR05, THM01STR65, THM01STR30
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ UX Spec Approved for Android — step 1.6 (needs style guide Approved, step 1.6a)
                  ⚠️ Platform minimum Android version — HLD (step 1.7)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
