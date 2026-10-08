THM01STR67 — Release-hardening signed build workflow

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR67 — Release-hardening signed build workflow
Tags: [Functional] [Mobile] [Android] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR07
Component       : mobile/jot
Persona         : As the owner preparing REL-1.0.0
Goal            : I want a manual `release-hardening` workflow that builds the one signed release APK used for final phone UAT, the Device Farm regression and the GitHub Release
Benefit         : So that signing keys are used only once per release and the same signed binary is tested and shipped (C-08)

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)

Business Rules  :
  BR-01: Manual trigger from main only, in a protected `release` Environment with owner approval
  BR-02: The keystore and its passwords exist only as `release` Environment secrets; no other workflow can read them
  BR-03: Output: signed release APK, its SHA-256 and SBOM, kept as artifacts and attached to the GitHub Release by the release step
  BR-04: Logs are scanned for key material before the job ends

Acceptance Criteria:
  AC-01: Given a commit on main, When the owner runs release-hardening and approves it, Then a signed
         release APK, its SHA-256 and its SBOM are attached as artifacts
  AC-02: Given a branch other than main, When release-hardening is started, Then it stops before reading
         any secret
  AC-03: Given the job logs, When gitleaks and a check for the literal keystore password run over them,
         Then nothing is found
  AC-04: Given the signed APK, When apksigner verifies it, Then the signature is valid and matches the
         release certificate fingerprint recorded in the release plan

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 6)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : Gradle release signing; apksigner; syft (CycloneDX)
Dependencies    : THM01STR30
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
                  ⚠️ Planned for the release-hardening phase before REL-1.0.0 (slice after Story work)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
