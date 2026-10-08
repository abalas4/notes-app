THM01STR02 — DynamoDB repository layer with optimistic concurrency

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR02 — DynamoDB repository layer with optimistic concurrency
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR06
Component       : apis/jot-api
Persona         : As the jot-api service (enabler for the owner's data)
Goal            : I want a repository layer over one DynamoDB table — save, get, list, update, softDelete — that stores items per user with version, updatedAt, soft delete and an item schema version
Benefit         : So that every resource gets the same safe write rules and offline-first (L-01) can be added later without a breaking change

Endpoint Contract:
  Internal module (no public endpoint) — methods save, get, list, update(expectedVersion), softDelete, restore. Typed errors: NOT_FOUND, VERSION_CONFLICT, STORE_UNAVAILABLE (mapped to HTTP by THM01STR54).
  Shared checks : 401 for a missing / invalid token and 404 for another user's item are verified on every route by THM01STR42

Acceptance Criteria:
  AC-01: Given a new item, When save is called, Then it is stored under the caller's userId with version 1,
         createdAt, updatedAt and schemaVersion
  AC-02: Given an item at version 3, When update states expected version 3, Then it is stored as version 4
         with a new updatedAt
  AC-03: Given an item at version 4, When update states expected version 3, Then VERSION_CONFLICT is raised
         and the stored item (version, content, updatedAt) is unchanged
  AC-04: Given an item of user A, or no item for the key, When user B calls get or update, Then NOT_FOUND
         is raised; and soft-deleted items are excluded from list unless explicitly requested
  AC-05: Given the data store is unreachable, When any repository call is made, Then STORE_UNAVAILABLE is
         raised within 5 s and no partial write is made

Story Points    : 5
Sprint Target   : PI-1 iteration 03 (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : boto3 conditional expressions; single-table key design in the LLD; DynamoDB Local in integration tests; profile deviation ADR (C-09)
Dependencies    : THM01STR01
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
