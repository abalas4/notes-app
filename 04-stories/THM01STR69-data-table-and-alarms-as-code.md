THM01STR69 — Data table and alarms as code

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR69 — Data table and alarms as code
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/modules/table, alarms)
Persona         : As the owner protecting my data
Goal            : I want the DynamoDB table and the CloudWatch alarms as modules used by envs/dev and envs/prod
Benefit         : So that my notes are protected against loss in prod and problems raise an alarm

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Capacity mode (on-demand or small provisioned) decided in the LLD (cost note, plan §7)
  BR-02: Prod table: point-in-time recovery on, deletion protection on, prevent_destroy (IAC-10, IAC-15)
  BR-03: Alarms defined by THM01STR52 are created here, notifying the owner's email through one SNS topic

Acceptance Criteria:
  AC-01: Given the prod table, When its settings are read, Then point-in-time recovery and deletion
         protection are on
  AC-02: Given the prod table, When a destroy is planned, Then OpenTofu refuses because of prevent_destroy
  AC-03: Given envs/dev is applied, When the alarms are listed, Then every alarm from THM01STR52 exists and
         notifies the owner's email

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu modules: table, alarms
Dependencies    : THM01STR37, THM01STR38
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
