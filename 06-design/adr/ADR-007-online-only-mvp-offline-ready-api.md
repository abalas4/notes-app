# ADR-007: Online-only MVP; the API is built so offline-first can be added without a breaking change
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR02, THM01FTR06 LLDs; ADR-004; RAID log (L-01)

## Context
Offline-first sync (local database, outbox, conflict handling) roughly adds a slice of work and a new
class of data-loss risks. The MVP serves one person who is usually online.

## Options considered
1. **Online-only MVP** with a clear offline state; offline-first later.
2. Offline-first from the start (outbox, `changes?since=` pull, encrypted local database).

## Decision
- The MVP is online-only. With no network the app shows an offline banner and writes fail visibly with
  Retry; nothing is lost silently; the editor keeps unsaved text until it is saved.
- The MVP keeps no notes at rest on the phone (confirmed in the HLD); only tokens are stored (Keystore).
- So offline-first (L-01) can be added later without breaking the API, every entity carries `version`
  and `updatedAt`, writes use optimistic concurrency (expected version / `If-Match` → 409), and deletes
  are soft (tombstones). The later model: the client pushes an outbox and pulls
  `changes?since=<cursor>`, last-writer-wins per field group, confirmed in the LLD at that time.

## Consequences
- Lost-edit and concurrent-edit risks are handled by visible failures and 409 + reload (RAID log; DFMEA
  rows in THM01FTR02).
- The encrypted local database (SQLCipher, MA-05) is deferred with L-01.
