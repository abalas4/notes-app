THM01WI11 — LLD for the API CI pipeline

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[LLD] THM01WI11 — LLD for the API CI pipeline
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story/Feature : THM01FTR07 (this revision: THM01STR29 — API pipeline; app, infra and release-hardening
                       parts added as LLD revisions with THM01STR30, STR31, STR67)
Owner                : Tech Lead (@abalas4)
LLD Reference ID     : THM01FTR07-LLD  (06-design/THM01FTR07-LLD.md)
Depends On HLD       : THM01WI09 (must be approved first)
Stack Profiles       : lang-python-fastapi

Objective       : Workflow `ci` jobs and triggers, one script per gate under scripts/ (BR-01, BR-02), job-level
                  path filters (BR-04), SHA-pinned actions and least-privilege permissions (BR-03), artifact
                  layout (BR-05), required status-check names for branch protection

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

Deliverable     : 06-design/THM01FTR07-LLD.md
Review Gate     : Tech Lead + QA Lead sign-off (@abalas4) before implementation starts
Effort Estimate : 8h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : THM01WI09 (HLD), THM01WI10 (DFMEA: RPN ≥ 200 mitigated)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
