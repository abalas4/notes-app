THM01STR31 — Infrastructure and supply-chain gates

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR31 — Infrastructure and supply-chain gates
Tags: [Functional] [API] [Security] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR07
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner merging an infrastructure pull request
Goal            : I want CI gates for OpenTofu code and IAM policies, and an SBOM for every release build
Benefit         : So that infrastructure changes are reviewed with their plan and cannot widen access unnoticed

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: tofu fmt -check, tofu validate, checkov and trivy config with 0 High / Critical (suppressions need a reason and rule ID)
  BR-02: IAM policies validated with IAM Access Analyzer validate-policy and the no-new-access checks
  BR-03: `tofu plan` for each affected environment posted to the PR using the read-only jot-gh-plan role (not for fork PRs)
  BR-04: SBOM (CycloneDX) generated for the API image and the APK on main

Acceptance Criteria:
  AC-01: Given a PR that changes infra code, When CI runs, Then fmt, validate, checkov, trivy config and
         Access Analyzer run and the plan is posted to the PR
  AC-02: Given a policy with Action "*" on a write permission, When CI runs, Then the IaC gate fails
  AC-03: Given a push to main, When CI runs, Then SBOM files for the API image and the APK are attached as
         artifacts

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu (stable), checkov, trivy, aws accessanalyzer, syft
Dependencies    : THM01STR36 (bootstrap) for the plan role
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
