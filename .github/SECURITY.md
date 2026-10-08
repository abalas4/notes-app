# Security policy

## Reporting a vulnerability

Please do **not** open a public issue for security problems.

Report it privately through GitHub: **Security → Report a vulnerability** on this repository.
Include what you found, how to reproduce it, and the impact you expect.

You will get an acknowledgement within 7 days. Fixes are released as a Hotfix release and
credited in the release notes if you wish.

## Scope

- The Jot Android app (`07-source-code-tests/src/mobile/jot/`)
- The Jot API (`07-source-code-tests/src/apis/jot-api/`)
- The infrastructure code (`07-source-code-tests/infra/`) and the GitHub Actions workflows

## Never commit secrets

This repository is public. Secrets live only in AWS SSM Parameter Store and GitHub Environment
secrets. Every commit is scanned by gitleaks (pre-commit hook and CI).
