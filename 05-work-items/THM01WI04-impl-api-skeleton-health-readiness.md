THM01WI04 — jot-api skeleton with health and readiness, Dockerfile and Compose

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[IMPL] THM01WI04 — jot-api skeleton with health and readiness, Dockerfile and Compose
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story    : THM01STR01
Owner           : Developer (@abalas4)
Depends On LLD  : THM01WI03

Objective       : FastAPI app (Python 3.13) with GET /api/v1/health and GET /api/v1/ready (store check with a
                  2 s timeout), settings, multi-stage non-root Dockerfile with Lambda Web Adapter,
                  07-source-code-tests/docker-compose.yml with DynamoDB Local
Deliverable     : PR on feat/THM01STR01-api-skeleton (< 400 changed lines), verifier PASS

Implementation Checklist:
  [ ] LLD reviewed and understood
  [ ] Branch created from main / trunk
  [ ] Unit tests written (coverage ≥ 80% for new code)
  [ ] Integration tests updated
  [ ] No new SAST critical/blocker issues
  [ ] API contract matches OpenAPI spec
  [ ] Logging added per logging standard (structured JSON; traceId included)
  [ ] No secrets or credentials committed — use secrets manager / env vars only
  [ ] Dependency vulnerability scan passed
  [ ] OWASP Top 10 self-check completed for any new endpoints or input-handling code
  [ ] Feature flag applied (if applicable)
  [ ] IaC / config changes committed alongside code (no manual-only infra changes)
  [ ] Code reviewed using safe-alm-code-review skill (Step 03 in lifecycle)
  [ ] Pipeline green (build + test + SAST + SCA)

Effort Estimate : 8h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : THM01WI03 (LLD approved)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
