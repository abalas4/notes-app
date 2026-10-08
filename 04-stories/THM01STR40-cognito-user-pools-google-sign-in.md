THM01STR40 — Cognito user pools with Google sign-in

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR40 — Cognito user pools with Google sign-in
Tags: [Functional] [API] [Security] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR09
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/)
Persona         : As the owner setting up sign-in
Goal            : I want the Cognito module: a dev pool (Google + native test users) in envs/shared and a prod pool (Google only) in envs/prod, each with the app client for PKCE
Benefit         : So that sign-in works in both environments without console set-up, and tests can sign in without a real Google account

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Lite tier; app client: public client, Authorization Code + PKCE only, no client secret, callback com.jot.app:/oauth2redirect, access token 1 h, refresh token 30 days, token revocation enabled
  BR-02: Google client ID and secret read from SSM SecureString /jot/<env>/google-* put in by the owner; never in the repo, plan output or logs
  BR-03: Dev pool: two native test users with generated passwords stored in SSM; prod pool: native sign-up disabled (L-04 later)
  BR-04: The dev pool lives in envs/shared so dev-down never destroys it (decision Q11); outputs (pool and client IDs) are read by THM01STR39

Acceptance Criteria:
  AC-01: Given the dev pool, When an automated test signs in as a native test user, Then Cognito issues
         access, ID and refresh tokens
  AC-02: Given the prod pool, When native sign-up is attempted, Then Cognito refuses it
  AC-03: Given the app client in each pool, When its configuration is read, Then it is public with no
         secret, PKCE code flow only, the callback above, access 1 h, refresh 30 days and revocation
         enabled
  AC-04: Given the CI logs and job summaries of plan and apply, When gitleaks and a check for the Google
         client secret value run over them, Then nothing is found

Story Points    : 3
Sprint Target   : PI-1 stretch, iteration 04 if velocity allows (slice 1); else PI-2+
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu aws_cognito_* resources; Google identity provider
Dependencies    : THM01STR37 (SSM paths); Google OAuth client created by the owner
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 4 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
