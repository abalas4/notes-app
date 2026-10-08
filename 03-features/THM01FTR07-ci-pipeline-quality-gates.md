THM01FTR07 — CI pipeline and quality gates

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[IMPLEMENTATION FEATURE] THM01FTR07 — CI pipeline and quality gates
Tags: [Implementation] [API] [Mobile] [Infra] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC02
Surfaces           : API (apis/jot-api) · Mobile Android (mobile/jot) — build and test pipelines only, no screens
Feature Owner      : Architecture Lead (@abalas4)
Description        : A GitHub Actions `ci` workflow that runs on every pull request and on `main`: API type
                     check, lint, unit and integration tests with coverage, Docker build and image scan, SCA,
                     SAST (Semgrep), secrets scan (gitleaks), IaC scan (checkov, trivy config, `tofu fmt` /
                     `validate`), licence check, OpenAPI contract check; app type check, lint, Jest unit tests,
                     Android release build signed in CI, and a MobSF static scan. Results become the required
                     status checks on `main`.

Architectural Note : One script per gate under `scripts/` (called by CI and runnable locally), so the plugin's
                     verifier gates and CI give the same answer. Actions pinned to commit SHAs; `GITHUB_TOKEN`
                     least-privilege `permissions:`; no `pull_request_target`; path filters so API-only changes
                     don't build the APK. The release APK is signed with the keystore held only in GitHub
                     Environment secrets — the same binary goes to the phone, Device Farm and the GitHub
                     Release (conformance C-08).
Enablement Value   : Makes the IMPL DoD and the plugin verifier gates (V-series) automatic for every Story of
                     THM01EPC01; produces the signed APK that THM01FTR08 tests.
ADR Reference      : TBD at step 1.7 — CI design; solo PR approval (D-11)

Acceptance Criteria:
  AC-01: Given a pull request that changes API code, When CI runs, Then every API gate runs and a failing gate
         blocks the merge through the required status checks on `main`
  AC-02: Given a pull request that changes app code, When CI runs, Then type check, lint, unit tests, the signed
         release build and the MobSF scan run and their reports are attached as artifacts
  AC-03: Given a pull request from a fork, When it is opened, Then no workflow gets secrets or an AWS role, and
         workflow runs wait for the owner's approval
  AC-04: Given the same gate script, When it is run locally and in CI on the same commit, Then both give the same
         result

Sizing             : M
WSJF               : (6 + 10 + 9) / 5 = 5.0   (proposed; every Story depends on it)
PI Target          : PI-1
Sprint Target      : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : TBD at step 1.3 (≥ 1 [API], ≥ 1 [Mobile] [Android])
HLD Reference      : THM01FTR07-HLD
LLD Reference      : THM01FTR07-LLD

Dependencies       : GitHub repository settings (owner); first app and API skeletons (THM01FTR06, app shell)
Constraints        : GitHub-hosted standard runners only (free for public repositories); stable tool
                     versions, exact pins; folder standard (`.github/workflows/`, `scripts/`).
ALM Status         : New
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ Feature Type
                     · ✅ Description · ✅ Architectural note · ✅ 4 ACs · ✅ Sized M · ✅ WSJF · ✅ PI Target
                     · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                     ⚠️ Sprint Target — PI Planning (1.5) · ⚠️ Child Stories — step 1.3
                     N/A Style guide — no screens in this Feature
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
