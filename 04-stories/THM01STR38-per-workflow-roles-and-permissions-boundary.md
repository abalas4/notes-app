THM01STR38 — Per-workflow roles and permissions boundary

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR38 — Per-workflow roles and permissions boundary
Tags: [Functional] [API] [Security] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner protecting the AWS account
Goal            : I want one least-privilege IAM role per workflow and environment, all under the jot-boundary permissions boundary
Benefit         : So that a leaked or misused workflow can only do its own small job

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Roles: jot-gh-plan (read-only), jot-gh-deploy-dev, jot-gh-deploy-prod, jot-gh-devicefarm, jot-gh-release (none — release signing needs no AWS), jot-dev-lambda-exec, jot-prod-lambda-exec (plan §8.2 R-AWS-03)
  BR-02: Trust: aud sts.amazonaws.com, repository abalas4/notes-app, the Environment, and the workflow file (custom OIDC sub with job_workflow_ref); maximum session 1 h
  BR-03: jot-gh-prereqs may create only jot-* roles that carry jot-boundary and may not change itself or the boundary
  BR-04: No `*` action or resource on any write permission; resources scoped by jot-<env>-* names and tags

Acceptance Criteria:
  AC-01: Given every role, When IAM Access Analyzer validates its policies and checkov scans them, Then
         there are no findings, no write permission uses `*`, and every trust policy has a maximum session
         of 1 h
  AC-02: Given jot-gh-prereqs, When it tries to create a role without jot-boundary or to edit its own
         policy, Then AWS returns AccessDenied
  AC-03: Given credentials from dev-up.yml (jot-gh-deploy-dev), When they call a write action on any
         jot-prod-* resource, Then AWS returns AccessDenied
  AC-04: Given jot-gh-deploy-dev, When a different workflow file, a different Environment or a fork asks
         for its credentials, Then STS refuses
  AC-05: Given jot-gh-devicefarm, When any workflow other than device-farm.yml asks for it, Then STS
         refuses

Story Points    : 5
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu IAM resources; GitHub OIDC sub-claim customisation for the repository
Dependencies    : THM01STR36, THM01STR37
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
