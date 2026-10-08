THM01STR36 — One-time bootstrap root

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR36 — One-time bootstrap root
Tags: [Functional] [API] [Security] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner setting up AWS once
Goal            : I want an `infra/envs/bootstrap` OpenTofu root that I apply once with my own credentials to create the state bucket, the GitHub OIDC provider and the jot-gh-prereqs role
Benefit         : So that GitHub Actions can take over everything else without any stored AWS keys

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Creates only: versioned, encrypted, public-access-blocked state bucket; GitHub OIDC identity provider; jot-gh-prereqs role trusted only for aws-prereqs.yml in the aws-admin Environment
  BR-02: Runs locally with the owner's credentials; Claude never reads them (plan §2 rule 5); a README section gives the exact commands
  BR-03: After apply, its state is migrated into the state bucket so the aws-prereqs workflow owns these resources from then on
  BR-04: No account ID, ARN or bucket name committed; values come from git-ignored *.tfvars (an *.tfvars.example is committed)

Acceptance Criteria:
  AC-01: Given an AWS account with no Jot resources, When the owner applies envs/bootstrap, Then the
         bucket, OIDC provider and jot-gh-prereqs role exist with the required tags
  AC-02: Given the bucket, When its settings are read, Then versioning and default encryption are on and
         all public access is blocked
  AC-03: Given the bootstrap has been applied, When its state migration step runs, Then `tofu plan` from
         the aws-prereqs workflow shows no changes for those three resources

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu (stable) with S3 backend and native locking; OpenTofu state encryption
Dependencies    : Owner's AWS credentials (local); GitHub Environment aws-admin
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
