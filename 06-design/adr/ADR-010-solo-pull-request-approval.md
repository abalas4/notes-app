# ADR-010: Pull-request approval for a solo developer — recorded approval comment, then the owner merges
Status        : Accepted (deviation from plugin rules — approved by the Product Owner)
Date          : 2026-10-08
Deciders      : Product Owner, Tech Lead (@abalas4)
Related       : CONTRIBUTING.md; code review skill (step 03)

## Context
The way of working (§6.4) requires branch protection on `main`, required status checks and one approval
per PR. The repository is public on GitHub Free, so branch protection and required checks are enforced
for free. But the owner is the only person, and GitHub does not let a PR author approve their own PR.

## Options considered
1. **Approval comment by the owner after the code-review report, then the owner merges.** Branch
   protection keeps "PR required", required status checks, conversation resolution, no bypass, no
   force-push or deletion; the "required approvals" setting stays off.
2. A second GitHub account to approve — a fake reviewer adds no assurance.
3. No PR at all — loses the required checks and the review record.

## Decision
Option 1. A PR merges only after the `/safe-alm-code-review` report has verdict APPROVE (or every
blocker resolved), and the owner has posted an approval comment on the PR that names the review report.
The owner merges; nobody pushes to `main` directly.

## Consequences
- The review evidence is the code-review report plus the approval comment; the release traceability
  matrix links both.
- Revisit when a second contributor joins: then turn on "required approvals: 1" and supersede this ADR.
