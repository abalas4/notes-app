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

SLO/Threshold   :
  - Tokens only in Android Keystore-backed storage; 0 tokens in AsyncStorage, logs or backups
  - Cleartext traffic disabled; TLS only
  - MobSF static scan: 0 High findings; 0 secrets / AWS identifiers in the APK
  - Deep links accept only jot://note/{id} for the signed-in user's notes
Test Approach   : MobSF static scan in CI (THM01STR30); unit tests for deep-link validation; device test inspecting app storage and backup exclusion

Acceptance Criteria:
  AC-01: Given a release APK, When MobSF scans it, Then there are 0 High findings and no secret strings
  AC-02: Given the app is signed in, When app storage and Android backup data are inspected on the
         emulator, Then no token appears outside the Keystore-backed store
  AC-03: Given a deep link to a note ID that does not belong to the user or a malformed link, When it is
         opened, Then the app shows Home with "Note not found" and makes no other request

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 2
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : react-native-keychain; network_security_config; android:allowBackup rules
Dependencies    : THM01STR05, THM01STR26, THM01STR30
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ SLO + test approach defined
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
