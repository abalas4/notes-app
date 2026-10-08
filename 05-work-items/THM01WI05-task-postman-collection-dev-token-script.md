THM01WI05 — Postman collection, environment and dev token script for jot-api

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[TASK] THM01WI05 — Postman collection, environment and dev token script for jot-api
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story    : THM01STR01
Owner           : Developer (@abalas4)
Task Type       : Config

Objective       : The plugin's API test assets from the first endpoint on
Deliverable     : postman/JotApi.postman_collection.json (Smoke folder: health, ready),
                  postman/JotApi-Local-Dev.postman_environment.json, scripts/generate-dev-token.* (local key,
                  trusted only when ENV=local — ADR-005); Newman run green against Compose

Steps           :
  1. Generate the collection and environment per the implementation skill's Postman standard
  2. Add the dev token script (no secrets committed)
  3. Run Newman against the local Compose stack

Effort Estimate : 2h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : THM01WI04
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
