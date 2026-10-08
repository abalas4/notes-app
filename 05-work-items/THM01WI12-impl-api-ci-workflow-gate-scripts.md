THM01WI12 — API CI workflow and gate scripts

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[IMPL] THM01WI12 — API CI workflow and gate scripts
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story    : THM01STR29
Owner           : Developer (@abalas4)
Depends On LLD  : THM01WI11

Objective       : .github/workflows/ci.yml and scripts/ gate scripts for the BR-01 gates, runnable locally with
                  the same result; reports as artifacts
Deliverable     : PR on feat/THM01STR29-api-ci-gates (< 400 changed lines; split per gate group if larger),
                  verifier PASS

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
Blocked By      : THM01WI11 (LLD approved); built together with THM01WI04 (D-01)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
