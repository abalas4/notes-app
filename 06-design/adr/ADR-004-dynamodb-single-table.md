# ADR-004: DynamoDB single-table data store; a repository layer replaces the profile's SQLAlchemy + Alembic
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR06 LLD; THM01STR02; ADR-003, ADR-005, ADR-007, ADR-011

## Context
Notes, checklists, labels and reminders of one user at personal volume. No idle cost, no VPC or NAT.
The `lang-python-fastapi` profile assumes a relational database with SQLAlchemy and Alembic.

## Options considered
1. **DynamoDB, single-table design** — 25 GB of storage always free; no idle cost; DynamoDB Local for
   integration tests in Docker with no AWS account.
2. RDS PostgreSQL / Aurora Serverless v2 — idle hourly cost; the RDS free tier lasts 12 months only;
   needs a VPC.
3. Aurora DSQL — Postgres-like but limited (no foreign keys, limited Alembic support).

## Decision
DynamoDB, one table, every key scoped to `USER#<userId>` (ADR-005). The capacity mode (on-demand, or a
small provisioned table inside the always-free 25 RCU / WCU) is chosen in the THM01FTR06 LLD: the
always-free throughput applies only to provisioned mode, and on-demand requests cost cents.

**Profile deviation:** a repository layer on boto3 replaces SQLAlchemy. Schema changes are versioned
item attributes plus OpenTofu table definitions, so the profile's "Migration" test type becomes
item-schema-version tests. Every other part of the profile applies unchanged.

## Consequences
- Items carry `version`, `updatedAt`, soft-delete tombstones and `schemaVersion` (ADR-007).
- Optimistic concurrency on every write: a stale expected version → 409, item unchanged.
- `prod` table: point-in-time recovery on and `prevent_destroy`.
