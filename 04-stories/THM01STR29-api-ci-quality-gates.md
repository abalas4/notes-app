THM01STR29 — API CI quality gates

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[FUNCTIONAL STORY] THM01STR29 — API CI quality gates
Tags: [Functional] [API] [Security]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Feature  : THM01FTR07
Component       : apis/jot-api
Persona         : As the owner merging an API pull request
Goal            : I want a `ci` workflow that runs every API gate on each pull request and on main and reports them as required status checks
Benefit         : So that no API change reaches main without passing the way-of-working gates

Endpoint Contract: N/A — pipeline / infrastructure Story, no HTTP endpoint
UX Spec         : N/A — no screens (Feature has no UI; style guide not required)

Business Rules  :
  BR-01: Gates: type check (mypy), lint (ruff), unit + integration tests in Docker with coverage ≥ 80 % on new code, Docker build, image scan, SCA, SAST (Semgrep), secrets (gitleaks), licence check, OpenAPI contract check
  BR-02: Each gate is one script under scripts/ that CI calls and the owner can run locally
  BR-03: Actions pinned to commit SHAs; `permissions:` least privilege; no pull_request_target; no AWS role for PR runs
  BR-04: Reports (coverage HTML, scan results) attached as artifacts; never committed (folder standard §11)

Acceptance Criteria:
  AC-01: Given a PR that changes API code, When CI runs, Then every gate in BR-01 runs and its result
         appears as a status check
  AC-02: Given a PR with a failing unit test or a High SAST finding, When CI finishes, Then the required
         check is red and GitHub blocks the merge
  AC-03: Given the same commit, When a gate script runs locally and in CI, Then both report the same pass /
         fail
  AC-04: Given a PR that changes only app code, When CI runs, Then API gates are skipped by path filters
         and reported as skipped, not failed

Story Points    : 5
Sprint Target   : TBD at PI Planning (step 1.5) — planned slice 1
Release Tag     : None — forecast at PI Planning (step 1.5)
Story Type      : New
Original Story  : N/A
Linked WI       : TBD at step 1.7
Tech Notes      : GitHub Actions ubuntu runners; Docker Buildx; Semgrep; gitleaks; Trivy / Grype; pip-audit; pip-licenses
Dependencies    : THM01STR01 (code to build)
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
