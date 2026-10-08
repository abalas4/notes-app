# Contributing to Jot

Jot is built by one owner (@abalas4) with an AI coding assistant. These rules apply to every change,
whoever makes it.

## Way of working

The project follows the **SAFe ALM way of working** with its lifecycle skills and gates:
requirements → implementation → code review → testing → release → operations.

- Every lifecycle step runs through its skill, in order. Artefacts are produced by the skill, not
  hand-written outside it.
- A step starts only when the previous step's exit gate is met: LLD Approved → verifier PASS → review
  APPROVE and PR merged → Story Done → release GO recorded. No gate is skipped; when a gate is not met,
  the missing items are reported and work waits.
- Human decisions stay with the owner: LLD sign-off, PR merge, Story acceptance (UAT), release GO,
  on-call ownership.
- **Any deviation from a way-of-working rule needs an ADR in `06-design/adr/` and the owner's explicit
  approval.** Nothing is waived silently. Current deviations: ADR-004 (data layer), ADR-009 (no app
  store), ADR-010 (solo PR approval), ADR-011 (no React Native stack profile).
- Planning lives in `00-planning/` (PI plans, iteration plans, RAID log) and `10-release/` (PI release
  roadmap, release plans).

## Repository layout

Every file goes where the plugin's project structure standard puts it (gate V34, review T-07). The
README lists the folders. Nothing at the root outside the allowed files. If something has no defined
home, raise it (ADR) instead of inventing a folder.

## Branches, commits and pull requests

- Trunk-based on `main`, protected: pull request required, required status checks, conversations
  resolved, no force-push or deletion. Approval per ADR-010.
- Branches: `feat|fix|refactor|test|chore|docs|perf/<STORY-ID>-<slug>` (planning work: `docs/<ID>-<slug>`).
- Conventional Commits with the Story ID, e.g. `feat(jot-api): add health route [THM01STR01]`.
- One IMPL Work Item per PR, under 400 changed lines; the IMPL Work Item ID in the PR description.
- Release tags `REL-x.y.z` on the deployed commit.

## Engineering rules

1. **Cost first.** Always-free AWS services where possible; serverless, pay-per-request. Nothing billed
   while idle (no EC2, RDS, NAT Gateway, ALB, EKS, Fargate, Secrets Manager). Model: ADR-012.
2. **Share code with iOS.** One React Native codebase; platform-specific code only where the OS requires
   it; libraries must support both platforms (ADR-001).
3. **Stable versions only.** Every language, runtime, framework, library, tool, base image, GitHub Action
   and AWS runtime uses its latest **stable** release — no alpha, beta, RC, preview, nightly, canary or
   `next` tags. On top: the 7-day cooling period, the language-version stability policy and exact
   version pins. A feature that exists only in a pre-release needs an ADR and the owner's approval.
4. **Credentials stay with the owner.** The AI assistant never reads local cloud-credential files and
   never prints credentials, account IDs or resource ARNs. The owner runs every admin step (the one-time
   bootstrap, SSM secret values) in their own terminal (ADR-008).

## Public repository hygiene

The repository is public; everything committed is world-readable.

- **No secrets, ever.** gitleaks runs as a pre-commit hook and as a required CI check; GitHub secret
  scanning and push protection are on.
- **No identifiers:** no AWS account IDs, ARNs, Cognito pool / client IDs, API URLs or Device Farm ARNs in
  committed files. They come from GitHub Environment variables / secrets, SSM, or git-ignored `*.tfvars`.
  OpenTofu state stays in the private state bucket.
- The Android signing keystore and its passwords live only in GitHub Environment secrets.
- **CI safety:** deploy jobs run only on `main` or protected Environments; OIDC trust is pinned to this
  repository, `main` and the Environments; no `pull_request_target`; runs from fork PRs need approval;
  Actions pinned to commit SHAs; `GITHUB_TOKEN` gets least-privilege `permissions:`.
- **No local-only names:** no local folder names, local file paths, personal names or unrelated
  third-party product names in committed files. The project is "Jot" / `notes-app`; the owner is
  `@abalas4`.
- Test data is synthetic. Screenshots and logs in the repository contain no tokens or email addresses.
- Check the staged files before every commit.

## Licence

No open-source licence: all rights reserved (see the README). Security reports:
[`.github/SECURITY.md`](.github/SECURITY.md).
