THM01FTR11 — Security baseline for app and API

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[NON-FUNCTIONAL FEATURE] THM01FTR11 — Security baseline for app and API
Tags: [Non-Functional] [Security] [API] [Mobile]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC01
Surfaces           : API (apis/jot-api) · Mobile Android (mobile/jot)
NFR Category       : Security
Coverage Status    : Evolving — owner Architecture Lead (@abalas4); review point: HLD approval (step 1.7),
                     then moves to Defined. Matches THM01EPC01 coverage row 4.
Feature Owner      : Architecture Lead (@abalas4)
Description        : The security floor for every Jot Story: authenticated and owner-scoped API access,
                     safe token storage on the phone, no secrets in the app or the public repository, and
                     automated supply-chain and code scanning on every build.

SLO / Threshold    :
  - 100 % of API routes except `/health` require a valid Cognito access token; 0 routes return another
    user's data (object-level authorisation test on every route)
  - App meets OWASP MASVS L1: tokens only in Android Keystore-backed storage; no secrets, keys or account
    IDs in the APK (MobSF static scan: 0 High findings); cleartext traffic disabled
  - Every build: SCA, SAST, secrets and container-image scans with 0 Critical / High unaccepted findings;
    SBOM generated at release
  - Critical vulnerabilities in running dependencies fixed within 7 days, High within 30 days

Test Strategy      : API security tests per OWASP API Top 10 (auth bypass, object-level authorisation,
                     mass assignment, rate limits); ZAP baseline against `dev`; MobSF static scan of the
                     APK in Docker; CI gates (SCA, Semgrep SAST, gitleaks, image scan); review agents.

Acceptance Criteria:
  AC-01: Given a valid token for user A, When it is used to read, change or delete an item owned by user B
         (dev pool test users), Then the API returns 404 and nothing changes
  AC-02: Given a release APK, When MobSF scans it, Then there are 0 High findings and no secret, key or
         AWS identifier in the binary
  AC-03: Given a pull request that adds a dependency with a known Critical CVE or a committed secret,
         When CI runs, Then the pipeline fails and the PR cannot be merged
  AC-04: Given the ZAP baseline scan against `dev`, When it completes, Then there are 0 High alerts

Sizing             : M
PI Target          : PI-1
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : THM01STR42 [API], THM01STR43 [Mobile] [Android], THM01STR44 [API] (step 1.3)
HLD Reference      : THM01FTR11-HLD
LLD Reference      : THM01FTR11-LLD

Dependencies       : THM01FTR06, THM01FTR01, THM01FTR07 (CI gates)
Constraints        : Public repository (plan §2 rule 7); no Secrets Manager (SSM SecureString)
ALM Status         : Refined (PR #3, 2026-10-08)
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ NFR category
                     · ⚠️ SLOs proposed from the plan and plugin defaults — Product Owner confirms by approving
                     this PR · ✅ Test strategy · ✅ 4 ACs · ✅ Sized M · ✅ PI Target · ✅ HLD / LLD IDs · ✅ Owner
                     ✅ Child Stories (step 1.3)
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
