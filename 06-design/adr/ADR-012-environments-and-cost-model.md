# ADR-012: Environments — local Docker API during development, `dev` on AWS only in test windows, `prod` from go-live; always-free cost model
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR08, THM01FTR09; ADR-002, ADR-003, ADR-008; THM01EPC01 metric "API cost ≤ US$1 / month"

## Context
Cost first: always-free AWS services, nothing billed hourly (no EC2, RDS, NAT Gateway, ALB, EKS,
Fargate, Secrets Manager). The AWS account is on the legacy free tier, and its 12-month offers are
treated as used up, so only always-free counts. No public API should exist until it is needed.

## Options considered
1. **Local Docker API for development; `dev` on AWS only during test windows; `prod` from go-live.**
2. A permanent `dev` stack — a public endpoint with nothing to test most of the time.
3. A private API reachable only over a VPN — AWS Client VPN costs about US$72+ per month.

## Decision

| Env | API | Database | Login | Reachable from the internet? | Exists |
|---|---|---|---|---|---|
| `local` | Docker Compose on the laptop | DynamoDB Local | Dev Cognito pool, or the dev token script for API-only tests | **No.** The emulator reaches it at `http://10.0.2.2:<port>`; cleartext allowed only in the debug build's network security config | Always |
| `cognito-dev` | — | — | Cognito user pool only | Only Cognito's hosted login | Always (free, no idle cost) |
| `dev` | Lambda + HTTP API (`envs/dev`) | DynamoDB dev table (disposable) | `cognito-dev` pool | Yes, with token auth | **Only during test windows** (phone UAT, Device Farm): `dev-up` before, `dev-down` after; state bucket, image repository and the Cognito dev pool stay |
| `prod` | Lambda + HTTP API (`envs/prod`, `prevent_destroy` on the table) | DynamoDB, point-in-time recovery on | Prod pool, Google only | Yes, with token auth | From REL-1.0.0 go-live |

- The release build always points to the HTTPS `dev` / `prod` URL; only the debug build may call
  `10.0.2.2`. The API base URL is chosen per build variant, never hard-coded in screens.
- Public endpoint protection (`dev`, `prod`): JWT authorizer on every route except a minimal `/health`,
  user-scoped data, throttling and a Lambda concurrency cap, TLS only, no secrets in the app.

## Consequences
**Cost model (personal use, per month):** development with only the local API and the Cognito dev pool
US$0; Lambda, Cognito (≤ 10,000 MAU), CloudWatch basics, X-Ray, SSM standard US$0 (always free);
DynamoDB US$0 to about US$0.05 (25 GB always free; on-demand requests billed — mode chosen in the LLD,
ADR-004); HTTP API US$0–0.10 (treated as paid); image repository about US$0.02 (lifecycle keeps 5
images); GitHub Actions US$0 (public repo, standard runners only); Device Farm US$0 inside the free
minutes, then US$0.17 per device-minute — the main cost risk (ADR-002 guard rails); Apple Developer
US$99 per year only when iOS starts. AWS Budgets alerts (the first two budgets are free) watch the
monthly cost.

Backlog (not in the MVP): app attestation (prove the caller is the genuine app) and a web application
firewall (about US$5+ per month).
