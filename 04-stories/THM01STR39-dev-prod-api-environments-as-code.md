THM01STR39 — Dev and prod API environments as code

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR39 — Dev and prod API environments as code
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/envs/dev, envs/prod)
Persona         : As the owner deploying the API
Goal            : I want OpenTofu roots envs/dev and envs/prod built from shared modules: Lambda (container, arm64), HTTP API with the Cognito JWT authorizer and throttling, DynamoDB table, log groups and alarms
Benefit         : So that dev and prod differ only by variables and either can be rebuilt from code

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Modules in infra/modules/<module>/; environments differ only by variables (IAC-12)
  BR-02: DynamoDB on-demand vs small provisioned capacity decided in the LLD (cost note, plan §7); prod: point-in-time recovery on, deletion protection and prevent_destroy (IAC-10, IAC-15)
  BR-03: HTTP API stage throttling set (rate and burst in the LLD); access logs to CloudWatch with 14-day retention
  BR-04: Lambda image referenced by digest (DS-01); execution role jot-<env>-lambda-exec

Acceptance Criteria:
  AC-01: Given envs/dev is applied, When the API health route is called, Then it returns 200 through the
         HTTP API
  AC-02: Given the prod table, When a destroy is planned, Then OpenTofu refuses because of prevent_destroy
         and AWS deletion protection is on
  AC-03: Given envs/dev and envs/prod, When their plans are compared, Then only variable values differ, not
         resources

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu modules: api, table, cognito, alarms
Dependencies    : THM01STR37, THM01STR38
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 5 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
