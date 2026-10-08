THM01STR02 — DynamoDB repository layer with optimistic concurrency

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[API STORY] THM01STR02 — DynamoDB repository layer with optimistic concurrency
Tags: [API] [Functional]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR06
Component       : apis/jot-api
Persona         : As the jot-api service
Goal            : I want a repository layer over one DynamoDB table that stores items per user with version, updatedAt, soft delete and an item schema version
Benefit         : So that every resource gets the same safe write rules and offline-first (L-01) can be added later without a breaking change

Endpoint Contract:
  Internal module — no public endpoint. Conditional writes on `version`; reads exclude soft-deleted items unless asked.

Acceptance Criteria:
  AC-01: Given a new item, When it is saved, Then it is stored under the caller's userId with version 1,
         createdAt, updatedAt and schemaVersion
  AC-02: Given an item at version 3, When an update says expected version 3, Then it is saved as version 4;
         When another update also says 3, Then it is rejected with VERSION_CONFLICT and the item is
         unchanged
  AC-03: Given an item of user A, When user B's repository call asks for it, Then nothing is returned
         (partition key is the userId)
  AC-04: Given a soft-deleted item, When items are listed, Then it is excluded, and it is returned only
         when deleted items are requested explicitly

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : boto3 with conditional expressions; single-table key design set in the LLD; DynamoDB Local in integration tests; profile deviation ADR (C-09)
Dependencies    : THM01STR01
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted · ✅ Endpoint contract sketched (final in LLD / OpenAPI)
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
