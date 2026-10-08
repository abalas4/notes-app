THM01STR68 — Install the CI build for a commit

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR68 — Install the CI build for a commit
Tags: [Functional] [Mobile] [Android]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR08
Component       : mobile/jot
Persona         : As the owner testing exactly what CI built
Goal            : I want `scripts/phone-test.sh --from-ci <sha>` to download and verify the CI APK for that commit before installing it
Benefit         : So that the phone and Device Farm test the identical binary, and a corrupted or swapped file is never installed

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Platform        : Android <minimum API set in the HLD, step 1.7>+
Counterpart     : none — iOS is Later (Epic Surfaces; REL-1.1)

Business Rules  :
  BR-01: Downloads the APK, test APK and SHA-256 file from the CI run for that commit (debug build during slices; the signed release-hardening build when the sha is a release-hardening run, decision Q12)
  BR-02: Installs only when the computed SHA-256 matches the CI record

Acceptance Criteria:
  AC-01: Given a commit with a green CI build, When the owner runs phone-test.sh --from-ci <sha>, Then the
         APK for that commit is downloaded, its SHA-256 matches, and it is installed and tested
  AC-02: Given the downloaded APK's SHA-256 does not match the CI record, When the script checks it, Then
         it stops before installing and sets no success status
  AC-03: Given a commit with no CI build artifact, When the owner runs --from-ci, Then the script stops and
         names the missing artifact

Story Points    : 2
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : gh run download; sha256sum
Dependencies    : THM01STR33, THM01STR30
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 2 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
