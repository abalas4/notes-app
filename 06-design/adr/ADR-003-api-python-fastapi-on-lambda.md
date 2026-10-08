# ADR-003: API in Python 3.13 + FastAPI, container on AWS Lambda (arm64) behind API Gateway HTTP API
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR06 HLD; ADR-004, ADR-005, ADR-012

## Context
Jot needs a private REST API on AWS at near-zero cost: always-free services first, nothing billed
while idle. The plugin automates its gates fully only for stacks with a profile; today only
`lang-python-fastapi` exists. The owner knows Python.

## Options considered
1. **Python 3.13 + FastAPI + Pydantic v2 on Lambda (arm64, container image, Lambda Web Adapter) behind
   API Gateway HTTP API with a Cognito JWT authorizer** — every plugin gate automated; Lambda is
   always free at this volume; the same Docker image runs in Compose, in the plugin's Docker test gates
   and in Lambda.
2. Node / TypeScript (Express / NestJS) on Lambda — one language with the app, but no plugin profile, so
   gates V1–V12 become manual evidence.
3. ECS Fargate / App Runner / EC2 — billed while idle.
4. Amplify / AppSync GraphQL — weaker fit with the plugin's REST, OpenAPI and Postman / Newman gates.
5. Firebase / Supabase — not hosted in AWS.
6. Lambda Function URL instead of HTTP API — US$0, but no per-route throttling and no authorizer before
   the code runs.

## Decision
Option 1, region us-west-2 (the same as Device Farm). Supporting choices: uvicorn; boto3 behind a
repository + service pattern (ADR-004); structlog JSON to CloudWatch Logs with 14-day retention;
OpenTelemetry to X-Ray; `/health` and `/ready`; SSM Parameter Store (standard) for configuration and
secrets — not Secrets Manager (US$0.40 per secret per month); ECR with a lifecycle policy that keeps 5
images. Quality and tests per the profile: mypy --strict, ruff, uv lockfile, pip-audit, gitleaks, pytest
with coverage ≥ 80 %, moto, DynamoDB Local, Schemathesis contract tests, Newman, mutmut, k6, OWASP ZAP;
a multi-stage non-root Dockerfile, hadolint, Trivy and a Syft SBOM.

## Consequences
- HTTP API costs US$1 per million requests outside the free tier — cents at personal volume.
- Cold starts with a container image: arm64, a slim image and lazy imports; NFR p95 < 1 s cold and
  < 300 ms warm (THM01FTR12).
- "Build once, promote by digest" from local to `dev` to `prod`.
