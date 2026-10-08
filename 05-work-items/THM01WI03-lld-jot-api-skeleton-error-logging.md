THM01WI03 — LLD for the jot-api skeleton, error model and request logging

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[LLD] THM01WI03 — LLD for the jot-api skeleton, error model and request logging
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story/Feature : THM01FTR06 (this revision: THM01STR01, THM01STR54; data model for THM01STR02 and the
                       OpenAPI contract for THM01STR03 are added as LLD revisions in iterations 02–03)
Owner                : Tech Lead (@abalas4)
LLD Reference ID     : THM01FTR06-LLD  (06-design/THM01FTR06-LLD.md)
Depends On HLD       : THM01WI01 (must be approved first)
Stack Profiles       : lang-python-fastapi (deviation: ADR-004)

Objective       : Implementation-ready design for the app factory, /api/v1/health and /api/v1/ready, the
                  error catalogue and standard body {error:{code,message,traceId}}, exception → status
                  mapping, request-log middleware, configuration catalogue, Docker / Compose layout

LLD Sections to Produce:
  [ ] Class / module diagram (UML or equivalent)
  [ ] Sequence diagrams for all primary flows
  [ ] Database schema (tables, columns, indexes, FK constraints, migrations; data class / retention)
  [ ] API contract (OpenAPI 3.x spec file; error shape with traceId; access / ownership rules;
      rate limit, idempotency, pagination, versioning; every status per endpoint)
  [ ] Error handling and exception catalogue
  [ ] Events & messaging — or N/A with reason
  [ ] Resilience & dependencies (timeout, retries, circuit breaker, fallback per dependency)
  [ ] State machine diagram (if stateful behaviour exists)
  [ ] Caching strategy (TTL, eviction, invalidation)
  [ ] Configuration and environment variables catalogue
  [ ] Logging, metrics, and alerting hooks defined
  [ ] Data migration & cut-over — or N/A
  [ ] UI design — N/A (no screens)
  [ ] Test strategy (frameworks from the stack profile, test doubles, key cases)
  [ ] Revision History

Deliverable     : 06-design/THM01FTR06-LLD.md (+ 06-design/api-specs/jot-api.openapi.yaml skeleton)
Review Gate     : Tech Lead + QA Lead sign-off (@abalas4) before implementation starts
Effort Estimate : 8h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : THM01WI01 (HLD), THM01WI02 (DFMEA: RPN ≥ 200 mitigated)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
