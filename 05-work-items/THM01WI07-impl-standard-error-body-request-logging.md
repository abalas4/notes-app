THM01WI07 — Standard error body, exception mapping and request logging

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[IMPL] THM01WI07 — Standard error body, exception mapping and request logging
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story    : THM01STR54
Owner           : Developer (@abalas4)
Depends On LLD  : THM01WI03

Objective       : Error catalogue and handlers producing {error:{code,message,traceId}} (404 for unknown
                  routes, 500 INTERNAL with no stack trace, 409 / 503 + Retry-After from typed repository
                  errors); traceId middleware; exactly one JSON log line per request (traceId, route, method,
                  status, latencyMs, userId when known — no headers, query, body or token)
Deliverable     : PR on feat/THM01STR54-error-body-logging (< 400 changed lines), verifier PASS

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
Blocked By      : THM01WI03 (LLD approved); THM01WI04 (app factory)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
