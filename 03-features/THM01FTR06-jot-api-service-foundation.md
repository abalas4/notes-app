THM01FTR06 — Jot API service foundation

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[IMPLEMENTATION FEATURE] THM01FTR06 — Jot API service foundation
Tags: [Implementation] [API] [Infra] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC01
Surfaces           : API (apis/jot-api)
Feature Owner      : Architecture Lead (@abalas4)
Description        : The skeleton every API Feature builds on: a FastAPI service packaged as a container
                     for AWS Lambda (arm64, Lambda Web Adapter) behind API Gateway HTTP API with a
                     Cognito JWT authorizer; `/health` and `/ready`; a DynamoDB single-table repository
                     layer with `version` / `updatedAt` and soft deletes; a standard error body;
                     structured JSON logging with trace IDs and OpenTelemetry → X-Ray; the OpenAPI 3.1
                     contract; and a local Docker Compose stack with DynamoDB Local for development.

Architectural Note : Python 3.13 + FastAPI per the `lang-python-fastapi` stack profile, except
                     persistence: DynamoDB replaces SQLAlchemy / Alembic, so migrations become
                     item-schema-version handling and tests (profile deviation, ADR — conformance C-09).
                     Optimistic concurrency on every write (version / If-Match → 409). Internal `userId`
                     mapped from the Cognito `sub` (D-05).
Enablement Value   : Unblocks the API side of THM01FTR01–05 and THM01FTR10; gives THM01FTR11–14 their
                     security, performance, reliability and observability hooks.
ADR Reference      : TBD at step 1.7 — stack (D-01…D-05), DynamoDB repository layer (C-09), Lambda
                     container + HTTP API

Acceptance Criteria:
  AC-01: Given the local Docker Compose stack is started, When `GET /health` and `GET /ready` are called,
         Then both return 200 and `/ready` reports the data store reachable
  AC-02: Given a deployed `dev` environment, When an API route is called without a valid Cognito access
         token, Then API Gateway or the service rejects it with 401 and the standard error body, and the
         log line carries the trace ID and no token or personal data
  AC-03: Given two writes to the same item with the same expected version, When the second one arrives,
         Then it is rejected with 409 and the stored item is unchanged
  AC-04: Given the service starts, When the OpenAPI document is generated, Then it matches the approved
         spec `06-design/api-specs/jot-api.openapi.yaml` (contract test in CI)
  AC-05: Given the data store is unavailable, When a route is called, Then the service returns 503 with
         a retry hint within the timeout and `/ready` reports not ready

Sizing             : M
WSJF               : (5 + 10 + 8) / 5 = 4.6   (proposed; takes its dependants' Time Criticality)
PI Target          : PI-1
Sprint Target      : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : THM01STR01 [API], THM01STR02 [API], THM01STR03 [API], THM01STR54 [API] (step 1.3, after story review)
HLD Reference      : THM01FTR06-HLD
LLD Reference      : THM01FTR06-LLD

Dependencies       : THM01FTR09 (AWS environments, roles and Cognito); THM01FTR07 (CI gates)
Constraints        : AWS always-free first; no Secrets Manager (SSM SecureString); stable versions,
                     exact pins, 7-day cooling period; Docker multi-stage, non-root; public repository.
Coverage notes     : AC-02 (401 + log hygiene) is delivered by THM01STR04 and THM01STR51; AC-05 (503 with Retry-After) by THM01STR54 and THM01STR50. Lambda / HTTP API / X-Ray come from THM01STR39 and THM01STR51.
ALM Status         : Refined (PR #3, 2026-10-08)
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces (API) · ✅ Feature
                     Type · ✅ Description · ✅ Architectural note · ✅ 5 ACs · ✅ Sized M · ✅ WSJF · ✅ PI Target
                     · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                     ⚠️ Sprint Target — PI Planning (1.5) · ✅ Child Stories (step 1.3)
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
