# ADR-008: Infrastructure as code with OpenTofu, deployed by GitHub Actions through OIDC with one role per workflow
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR09 HLD / LLD; THM01FTR07; THM01STR36–41, THM01STR69, THM01STR70; ADR-012

## Context
Every AWS resource must be created and changed from code, never by hand in the console; no long-lived
AWS keys; least privilege per workflow. The owner knows Terraform / HCL.

## Options considered
1. **OpenTofu** — open-source (MPL-2.0) fork of Terraform; the same HCL and AWS provider.
2. Terraform — rejected: the BUSL licence is not open source.
3. AWS SAM / CloudFormation — the owner knows HCL; weaker multi-environment module layout.

## Decision
- **OpenTofu** under `07-source-code-tests/infra/`: `modules/<module>/` and one root per environment
  `envs/{bootstrap,shared,dev,prod}`. State in a private, versioned, encrypted S3 bucket with S3-native
  locking (`use_lockfile`) and OpenTofu client-side state encryption (secrets such as the Google client
  secret can land in state). `tofu fmt` / `validate` / `plan` in CI, the plan reviewed on the PR,
  scanned by checkov and trivy config, reviewed by `review-iac`; apply only the reviewed plan.
- **One-time bootstrap (the only manual AWS step):** the owner runs `envs/bootstrap` once, locally, with
  their own credentials. It creates the state bucket, the GitHub OIDC provider and the `jot-gh-prereqs`
  role; its state then moves into the bucket and the `aws-prereqs` workflow owns everything.
- **`aws-prereqs` workflow** (manual, Environment `aws-admin`, the plan shown before apply) manages the
  account-level root `envs/shared`: OIDC provider, the roles and policies below, the permissions
  boundary, state bucket, ECR repository + lifecycle policy, SSM path `/jot/*`, Device Farm project and
  pools, AWS Budgets alerts (≤ 2, free), CloudWatch log-retention defaults.
- **One role per workflow and environment** (no shared deploy role, no `*:*`, no long-lived keys):

| Role | Assumable only by | May do |
|---|---|---|
| `jot-gh-prereqs` | `aws-prereqs.yml`, Environment `aws-admin` | The `envs/shared` resources only; IAM limited to `jot-*`; every role it creates carries the `jot-boundary` permissions boundary; cannot change its own role or the boundary |
| `jot-gh-plan` | PR workflows from this repository's branches (not forks) | Read-only `tofu plan` |
| `jot-gh-deploy-dev` | `dev-up.yml` / `dev-down.yml`, Environment `dev` | Create / destroy only `jot-dev-*` resources; push to the API image repository; read `/jot/dev/*`; state key `dev/*`; pass only `jot-dev-lambda-exec` |
| `jot-gh-deploy-prod` | `deploy-prod.yml` on `main`, Environment `prod` | As dev for `jot-prod-*`; no delete on the table |
| `jot-gh-devicefarm` | `device-farm.yml`, Environment `device-farm` | Device Farm actions on the `jot` project only, plus the free-minutes check |
| `jot-dev-lambda-exec` / `jot-prod-lambda-exec` | Lambda | CRUD on its own table, its own log group, X-Ray |

- Trust policies pin `aud = sts.amazonaws.com`, this repository, the Environment and the workflow file
  (custom OIDC `sub` with `job_workflow_ref`); sessions ≤ 1 h. Resources are named `jot-<env>-*` and
  tagged `owner`, `service`, `environment`, `data-class` (IAC-11); policies use names and tags as
  conditions. IAM Access Analyzer policy validation and checkov fail the PR on a finding.
- **Drift detection (IAC-14):** a weekly `drift-check` workflow runs `tofu plan` with `jot-gh-plan`; any
  drift opens an issue.

## Consequences
- Secret values (the Google client secret) never pass through the repository or logs: the owner puts
  them into SSM once with their own credentials; OpenTofu references only the parameter name.
- Outside AWS and not automatable: the Google OAuth client and GitHub settings that need the owner's
  account (Environment reviewers, branch protection, secret scanning) — a README checklist.
- Emulator tests need no AWS role (local Docker API, ADR-012).
