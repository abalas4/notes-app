THM01STR37 — Shared AWS prerequisites workflow

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR37 — Shared AWS prerequisites workflow
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner provisioning shared AWS resources
Goal            : I want a manual `aws-prereqs` workflow that plans and applies `infra/envs/shared`: image repository, SSM parameter paths, Device Farm project and pools, the Cognito dev pool (THM01STR40), budget alerts and log-retention defaults
Benefit         : So that no AWS console clicks are needed and every shared resource is reviewed as code

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Runs only in the aws-admin Environment with owner approval, using jot-gh-prereqs
  BR-02: Shows `tofu plan` in the job summary, saves it, and applies exactly that saved plan after approval
  BR-03: Image repository with a lifecycle policy (keep the last 5 images); SSM paths /jot/dev/* and /jot/prod/* created empty — secret values are put in by the owner (R-AWS-04)
  BR-04: Two AWS Budgets (free): monthly cost forecast > US$1 and actual > US$5, emailed to the owner
  BR-05: Default log retention 14 days for jot-* log groups; every resource tagged owner, service, environment, data-class (IAC-11)

Acceptance Criteria:
  AC-01: Given the bootstrap exists, When the owner runs aws-prereqs, Then the plan is shown in the job
         summary, and after approval exactly that plan is applied and every shared resource exists with the
         tags
  AC-02: Given nothing changed, When aws-prereqs runs again, Then the plan shows no changes
  AC-03: Given the applied budgets, When their settings are read, Then there are exactly two — forecast >
         US$1 and actual > US$5 — each notifying the owner's email
  AC-04: Given the jot-* log groups, When their settings are read, Then retention is 14 days

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu envs/shared; AWS provider (stable)
Dependencies    : THM01STR36
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
