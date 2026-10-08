THM01EPC02 — Build, test and AWS delivery automation

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[EPIC] THM01EPC02 — Build, test and AWS delivery automation
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Capability : THM01CAP02
Type              : Enabler
Product Stage     : MVP
Surfaces          : API / backend: Yes (pipelines and infrastructure for apis/jot-api)
                    Web UI: No
                    Mobile app: Yes (Android build, signing and test pipelines for mobile/jot; no screens)
                                iOS: Later (with THM01EPC01)
Epic Owner        : Architecture Lead (@abalas4)
Architecture Lead : Architecture Lead (@abalas4)
Description       : Build the runway every Jot change travels on. A CI pipeline runs the way-of-working
                    gates on every pull request. Manual GitHub Actions workflows run the test suites
                    on an Android emulator and on AWS Device Farm and bring the dev AWS environment up
                    and down; one local script builds and tests on the owner's phone. A manual
                    workflow creates every AWS prerequisite of the API from OpenTofu code, using one
                    narrowly scoped OIDC role per workflow and no stored AWS keys.

Lean Business Case
  Problem Statement  : Without automation, every Story needs manual builds, manual AWS console set-up
                       and hand-run tests on three targets — slow, error-prone, and it leaves
                       undocumented and over-privileged access behind in a public project.
  Solution Overview  : GitHub Actions (free and unmetered for this public repository) with OIDC to
                       AWS; OpenTofu roots `infra/envs/{bootstrap,shared,dev,prod}`; workflows
                       `ci`, `emulator-tests`, `device-farm`, `dev-up`, `dev-down`, `aws-prereqs`,
                       `deploy-prod`, `drift-check`; script `scripts/phone-test.sh` (plan §8.1, §8.2).
  Leading Indicators : The first app Story is tested on emulator and phone using only the workflows and
                       the script; the dev environment is created and destroyed by workflow with no
                       console step.
  Non-Financial      : Least-privilege, auditable access; repeatable environments; Story Done evidence
                       produced automatically.
  Financial          : US$0 — GitHub Actions free for public repositories; OpenTofu state in S3 at a
                       fraction of a cent; Device Farm only from the one-time free minutes.
  Go/No-Go Threshold : By the end of slice 2: emulator, dev-environment and phone runs fully automated;
                       Device Farm workflow enforcing the emulator → phone gate; 0 long-lived AWS keys.
  Pivot/Persevere    : If emulator runs on GitHub-hosted runners are too slow or flaky (> 20 % reruns),
                       pivot to running the emulator suite locally through the same scripts and keep CI
                       for build, unit and scan gates.

MVP Definition    : CI gates on every PR; emulator-tests, device-farm, dev-up / dev-down and aws-prereqs
                    workflows; phone-test script; fine-grained OIDC roles with a permissions boundary;
                    weekly drift check; prod deploy workflow with approval.
Out of Scope      : Self-hosted runners (unsafe on a public repository); iOS build pipeline (REL-1.1);
                    store publishing pipelines (no Play Store, deviation C-05); multi-account AWS
                    organisation.

Success Metrics   :
  - Manual AWS console changes after the one-time bootstrap: n/a (new) → 0 (drift check clean)
  - Emulator, Device Farm and dev-environment runs started from a workflow: n/a → 100 %
  - Long-lived AWS access keys stored anywhere: 0 → 0
  - Device Farm runs started without a green emulator + phone run for the same commit: 0

Benefit Measurement (operations 09-benefit-realisation.md §1):
  | Metric | Baseline (date, source) | Target | Data source | Owner | Checkpoints |
  |--------|-------------------------|--------|-------------|-------|-------------|
  | Manual AWS changes (drift) | n/a (2026-10-08, new) | 0 | `drift-check` workflow results / opened issues | Architecture Lead (@abalas4) | Weekly; 30 / 60 / 90 days |
  | Automated test-run share | n/a (new) | 100 % | GitHub Actions run history + `jot/phone-tests` commit statuses | Architecture Lead (@abalas4) | End of each slice |
  | Long-lived AWS keys | 0 (2026-10-08, IAM) | 0 | IAM credential report | Architecture Lead (@abalas4) | Monthly |
  | Gate bypasses on Device Farm | n/a (new) | 0 | `device-farm` workflow gate log | Architecture Lead (@abalas4) | Per Device Farm run |
  Pivot/Persevere decision : Pending

Compliance Regimes : None — internal delivery tooling for a personal app. Revisit trigger: with THM01EPC01.

WSJF Score        :
  User/Business Value   : 6
  Time Criticality      : 9
  Risk Reduction / OE   : 9
  Job Size              : 5
  WSJF                  : (6+9+9)/5 = 4.8   (proposed; Product Owner confirms at PI Planning)

Sizing            : S
PI Target         : PI-1 (slice 1, Device Farm workflow by slice 2)
ART(s)            : Jot team (solo)
Linked Features   : (step 1.2)
                    THM01FTR07 CI pipeline and quality gates
                    THM01FTR08 Test-execution workflows and phone script (R-TX)
                    THM01FTR09 AWS prerequisites and environments as code (R-AWS)

Dependencies      : One-time local `infra/envs/bootstrap` apply and SSM secret values (owner, own
                    credentials); GitHub Environments `aws-admin`, `dev`, `prod`, `device-farm` with the
                    owner as required reviewer; Device Farm free minutes.
Constraints       : OpenTofu (D-08); GitHub Actions + OIDC only, no stored keys; one IAM role per
                    workflow and environment with the `jot-boundary` permissions boundary; trust policies
                    pinned to repository, environment and workflow file; actions pinned to commit SHAs;
                    no `pull_request_target`; no self-hosted runners; folder standard for every file;
                    stable versions only.
Risks             :
  - Risk 1: A misconfigured OIDC trust lets another repository or workflow assume a role | L: L | I: H |
    Mitigation: `sub` + `job_workflow_ref` pinning; IAM Access Analyzer + checkov in CI
  - Risk 2: The prerequisites role escalates its own privileges | L: L | I: H | Mitigation: permissions
    boundary required on every created role; the role cannot edit itself or the boundary
  - Risk 3: A secret or identifier leaks through the public repository or workflow logs | L: M | I: H |
    Mitigation: gitleaks pre-commit + CI, push protection, values only in SSM / Environment secrets,
    masked outputs
  - Risk 4: Emulator runs on hosted runners are slow or flaky | L: M | I: M | Mitigation: KVM
    acceleration, caching, retry-once policy; pivot rule above
  - Risk 5: Device Farm free minutes exhausted by failed runs | L: L | I: M | Mitigation: enforced
    emulator → phone gate, minutes guard, paid runs off by default

Requirement Coverage Assessment — THM01EPC02                         Product Stage: MVP
  | Type / Category | Status | Artefact ID(s) | Owner | Review / Trigger | Note (target, reason) |
  |---|---|---|---|---|---|
  | Functional | Defined | THM01FTR07–THM01FTR09 | Architecture Lead (@abalas4) | Step 1.3 | Plan §8.1 (R-TX), §8.2 (R-AWS) |
  | Technical / Enabler | Defined | THM01FTR07–THM01FTR09 | Architecture Lead (@abalas4) | Step 1.3 | This whole Epic is enabler work |
  | Data | N/A | — | — | — | No product data; state files and test reports only |
  | Interface & Integration | Evolving | THM01FTR08, THM01FTR09 | Architecture Lead (@abalas4) | Step 1.7 (HLD) | GitHub OIDC ↔ AWS STS; Device Farm API; Actions artifacts and commit statuses |
  | Transition & Migration | N/A | — | — | — | Greenfield |
  | Constraints | Defined | Epic `Constraints` field | Architecture Lead (@abalas4) | — | See field |
  | 1 Performance | Evolving | — | Architecture Lead (@abalas4) | Step 1.2 | Initial: PR CI ≤ 15 min; emulator suite ≤ 30 min (not customer-facing) |
  | 2 Scalability | N/A | — | — | — | One developer |
  | 3 Availability & Reliability | Evolving | — | Architecture Lead (@abalas4) | Step 1.2 | Initial: flaky-test rerun rate ≤ 5 %; `dev-down` always cleans up |
  | 4 Security | Evolving | THM01FTR07, THM01FTR09 | Architecture Lead (@abalas4) | Step 1.2 | Least privilege per workflow; permissions boundary; no long-lived keys; Access Analyzer + checkov clean; SHA-pinned actions |
  | 5 Compliance & Regulatory | N/A | — | — | — | No regime |
  | 6 Observability & Monitoring | Evolving | — | Architecture Lead (@abalas4) | Step 1.2 | Job summaries, artifacts and reports per run; drift issues; budget alerts |
  | 7 Usability & Accessibility | N/A | — | — | — | No end-user screens |
  | 8 Maintainability | Evolving | — | Architecture Lead (@abalas4) | Step 1.2 | One script per task shared by CI and local runs; IaC modules reused across environments |
  | 9 Portability & Interoperability | Evolving | — | Architecture Lead (@abalas4) | Step 1.7 | Scripts run in Git Bash / Linux runners; OpenTofu provider pins |
  | 10 Disaster Recovery & BC | Evolving | — | Architecture Lead (@abalas4) | Step 1.7 | State bucket versioned; environments rebuildable from code |
  | 11 Data Quality & Integrity | N/A | — | — | — | No product data |
  | 12 Capacity, Resource & Cost | Defined | Epic Success Metrics | Product Owner (@abalas4) | Per Device Farm run | GitHub Actions US$0; Device Farm within free minutes; paid runs off by default |
  | 13 AI / ML Fairness | N/A | — | — | — | No AI / ML |
  | 14 Serviceability & Supportability | Evolving | — | Architecture Lead (@abalas4) | Step 6.1 | README setup checklist; workflow runbooks |
  | 15 Privacy & Data Protection | Evolving | — | Architecture Lead (@abalas4) | Step 1.2 | No personal data, account IDs or secrets in logs, artifacts or the repository |
  | 16 Localisation & i18n | N/A | — | — | — | Internal tooling |

ALM Status        : Portfolio Backlog
DoR Check         : ✅ Stored at 02-epics/THM01EPC02-<slug>.md
                    ✅ Parent Capability THM01CAP02 linked
                    ✅ Type Enabler
                    ✅ Lean Business Case complete
                    ✅ MVP definition written
                    ✅ Out of scope listed
                    ✅ Success metrics with baselines and targets
                    ✅ Benefit Measurement block
                    ✅ Compliance Regimes declared: None
                    ✅ Sized S
                    ✅ ≥ 3 Features identified (3 written at step 1.2)
                    ✅ Risks with likelihood / impact / mitigation
                    ✅ Product Stage MVP
                    ✅ Surfaces declared
                    ✅ Requirement Coverage Assessment present; mandatory categories assessed
                       (Performance not customer-facing)
                    ✅ ART and PI target set
                    ✅ Epic Owner and Architecture Lead named
                    ✅ Portfolio Kanban approval — Product Owner approved and merged PR #1 (2026-10-08)
DoD Check         : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
