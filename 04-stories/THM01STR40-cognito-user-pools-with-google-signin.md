THM01STR40 — Cognito user pools with Google sign-in

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR40 — Cognito user pools with Google sign-in
Tags: [Functional] [API] [Security] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner setting up sign-in
Goal            : I want Cognito user pools as code: prod with Google federation only, dev with Google plus native test users for automated tests, and the app client for PKCE
Benefit         : So that sign-in works in both environments without any console set-up and tests can sign in without a real Google account

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Lite tier; app client: public client, Authorization Code + PKCE, no client secret, callback com.jot.app:/oauth2redirect
  BR-02: Google client ID and secret read from SSM SecureString (/jot/<env>/google-*) put in by the owner; never in the repo or logs
  BR-03: Dev pool: 2 native test users whose passwords are generated into SSM; prod pool: no native sign-up (Phase B later, L-04)
  BR-04: Token lifetimes: access 1 h, refresh 30 days (LLD may tune)

Acceptance Criteria:
  AC-01: Given the dev pool, When an automated test signs in as a native test user, Then it receives tokens
         the API accepts
  AC-02: Given the prod pool, When native sign-up is attempted, Then Cognito refuses it
  AC-03: Given the plan output and workflow logs, When they are searched, Then the Google client secret
         does not appear

Story Points    : 3
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu aws_cognito_* resources; Google identity provider
Dependencies    : THM01STR37 (SSM paths); Google OAuth client created by the owner
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 3 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ⚠️ Release Tag — forecast at PI Planning (1.5), confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
