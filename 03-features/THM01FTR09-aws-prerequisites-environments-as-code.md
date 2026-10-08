THM01FTR09 — AWS prerequisites and environments as code

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[IMPLEMENTATION FEATURE] THM01FTR09 — AWS prerequisites and environments as code
Tags: [Implementation] [API] [Infra] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC02
Surfaces           : API (apis/jot-api — infrastructure under 07-source-code-tests/infra/)
Feature Owner      : Architecture Lead (@abalas4)
Description        : Requirement R-AWS (plan §8.2). Every AWS resource the API needs is created by OpenTofu
                     through GitHub Actions: the `aws-prereqs` workflow (root `infra/envs/shared`) manages the
                     GitHub OIDC provider, per-workflow IAM roles and the permissions boundary, the state
                     bucket, the image repository, the `/jot/*` SSM parameter paths, the Device Farm project
                     and pools, and budget alerts; `dev-up` / `dev-down` / `deploy-prod` apply `envs/dev` and
                     `envs/prod` (Lambda, HTTP API, DynamoDB, Cognito, log groups, alarms); `drift-check` runs
                     weekly. Only the one-time `envs/bootstrap` apply and SSM secret values are done by the
                     owner with their own credentials.

Architectural Note : One role per workflow and environment — `jot-gh-prereqs`, `jot-gh-plan` (read-only),
                     `jot-gh-deploy-dev`, `jot-gh-deploy-prod`, `jot-gh-devicefarm`, plus `jot-<env>-lambda-exec`.
                     Trust pinned to `aud`, repository, Environment and workflow file (`job_workflow_ref`);
                     sessions ≤ 1 h; no long-lived keys. Every role created by `jot-gh-prereqs` must carry the
                     `jot-boundary` permissions boundary, and it cannot edit itself or the boundary. Resources
                     named `jot-<env>-*` and tagged `owner`, `service`, `environment`, `data-class` (IAC-11).
                     State encrypted (OpenTofu state encryption) with S3 native locking. Policies checked by
                     IAM Access Analyzer and checkov in CI. Production table has deletion protection and
                     point-in-time recovery (IAC-10, IAC-15).
Enablement Value   : Gives THM01FTR06 its environments and THM01FTR08 its AWS access; satisfies the
                     least-privilege requirement for the whole project.
ADR Reference      : TBD at step 1.7 — OpenTofu over Terraform / SAM (D-08); role model; SSM over Secrets Manager

Acceptance Criteria:
  AC-01: Given only the bootstrap has been applied, When the owner runs `aws-prereqs` and approves it, Then the
         plan is shown in the job summary, applied, and every R-AWS-01 resource exists with the required tags
  AC-02: Given any workflow role, When its policy is evaluated by IAM Access Analyzer, Then there are no findings
         for public or cross-account access and no `*` action or resource on a write permission
  AC-03: Given `jot-gh-prereqs`, When it tries to create a role without the `jot-boundary` boundary or to change
         its own policy, Then AWS denies the call
  AC-04: Given a role trusted for `dev-up.yml`, When a different workflow file or a fork asks for its token,
         Then AWS refuses to issue credentials
  AC-05: Given someone changes a `jot-*` resource in the console, When `drift-check` runs, Then it detects the
         drift and opens a GitHub issue

Sizing             : M
WSJF               : (5 + 10 + 10) / 5 = 5.0   (proposed; blocks every deployment)
PI Target          : PI-1
Sprint Target      : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : TBD at step 1.3 ([API] Stories with [Infra])
HLD Reference      : THM01FTR09-HLD
LLD Reference      : THM01FTR09-LLD

Dependencies       : AWS account (legacy free tier); owner runs the bootstrap; GitHub Environments
                     `aws-admin`, `dev`, `prod`, `device-farm` created by the owner
Constraints        : OpenTofu (D-08); IaC standard IAC-01…IAC-16; no Secrets Manager; no AWS identifiers in the
                     public repository; Claude never reads the owner's AWS credentials (plan §2 rule 5).
ALM Status         : Refined (PR #3, 2026-10-08)
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ Feature Type
                     · ✅ Description · ✅ Architectural note · ✅ 5 ACs · ✅ Sized M · ✅ WSJF · ✅ PI Target
                     · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                     ⚠️ Sprint Target — PI Planning (1.5) · ⚠️ Child Stories — step 1.3
                     N/A Style guide — no screens in this Feature
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
