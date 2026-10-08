THM01STR35 — Dev environment up and down workflows

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR35 — Dev environment up and down workflows
Tags: [Functional] [API] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR08
Component       : apis/jot-api (infrastructure under 07-source-code-tests/infra/envs/dev)
Persona         : As the owner starting a test window
Goal            : I want manual `dev-up` and `dev-down` workflows that create and destroy the dev AWS environment
Benefit         : So that the API is reachable only during phone and Device Farm windows and costs nothing otherwise

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: dev-up: build and push the API image, `tofu apply` envs/dev, wait for GET /api/v1/health = 200 (up to 5 minutes), print the API base URL in the job summary
  BR-02: dev-down: `tofu destroy` of envs/dev except the Cognito dev pool and its test users; the state bucket and image repository live in shared and are untouched (decision Q11)
  BR-03: Both run in the protected `dev` Environment with the jot-gh-deploy-dev role only; no account IDs or ARNs in logs

Acceptance Criteria:
  AC-01: Given dev is down, When the owner runs dev-up and approves it, Then GET <base URL>/api/v1/health
         returns 200 and the URL is in the job summary
  AC-02: Given dev is up, When the owner runs dev-down, Then every jot-dev-* resource is destroyed except
         the Cognito dev pool and its users, and the summary lists what was kept
  AC-03: Given `tofu apply` fails or health is not 200 within 5 minutes, When dev-up ends, Then the
         workflow is red, no URL is published as ready, and the summary names the failing step
  AC-04: Given dev is already down, When the owner runs dev-down, Then it succeeds with "nothing to
         destroy"
  AC-05: Given dev is up, When dev-up runs again, Then nothing changes

Story Points    : 3
Sprint Target   : PI-2+ — forecast after iteration 03 velocity (slice 1)
Release Tag     : REL-1.0.0 (forecast at PI-1 Planning 2026-10-08; confirmed at Sprint Planning)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : OpenTofu envs/dev; Docker Buildx to the image repository
Dependencies    : THM01STR39, THM01STR69 (dev environment code), THM01STR38 (roles)
Analytics       : None — no Epic Success Metric is measured from this Story
ALM Status      : New
DoR Check       : ✅ Stored at 04-stories/<ID>-<slug>.md · ✅ Parent Feature linked
                  ✅ One primary surface tag + Component · ✅ Story Type New / Original N/A
                  ✅ As a / I want / So that · ✅ 5 ACs in Gherkin · ✅ Sized 3 pts · ✅ Analytics line set
                  ✅ Dependencies noted
                  ✅ Release Tag REL-1.0.0 forecast (PI-1 Planning); confirmed at Sprint Planning
                  ⚠️ Work Items — identified at step 1.7 (DESIGN / HLD / DFMEA / LLD / IMPL / TEST)
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
