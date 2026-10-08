THM01STR39 — Lambda and HTTP API environments as code

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR39 — Lambda and HTTP API environments as code
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/envs/dev, envs/prod)
Persona         : As the owner deploying the API
Goal            : I want OpenTofu roots envs/dev and envs/prod built from shared modules: Lambda (container, arm64) and the HTTP API with the Cognito JWT authorizer and throttling
Benefit         : So that dev and prod differ only by variables and either can be rebuilt from code

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Modules in infra/modules/<module>/; dev and prod use the same modules; differences (sizes, prod-only protections, test users) come from variables or count, never from different resources definitions (IAC-12)
  BR-02: Authorizer reads the pool and client IDs from THM01STR40 outputs
  BR-03: HTTP API stage throttling: initial rate 10 rps, burst 20 (LLD may tune); access logs to CloudWatch
  BR-04: Lambda image referenced by digest (DS-01); execution role jot-<env>-lambda-exec

Acceptance Criteria:
  AC-01: Given envs/dev is applied with the API image, When GET /api/v1/health is called through the HTTP
         API, Then it returns 200
  AC-02: Given a dev-pool access token, When a protected route is called, Then the authorizer accepts it;
         with a token from another pool or none, Then 401
  AC-03: Given the dev stage, When its settings are read, Then throttling is rate 10 / burst 20 and access
         logging is on
  AC-04: Given envs/dev and envs/prod, When their configurations are compared, Then both use the same
         modules and differ only in variable values

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu modules: api, lambda
Dependencies    : THM01STR37, THM01STR38, THM01STR40, THM01STR01 (image with health route)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
