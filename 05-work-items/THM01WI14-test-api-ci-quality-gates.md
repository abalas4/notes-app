THM01WI14 — Tests for the API CI quality gates

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[TEST] THM01WI14 — Tests for the API CI quality gates
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story    : THM01STR29
Owner           : QA Engineer (@abalas4)
Design Skill    : safe-alm-testing (Step 04)

Test Type       : Integration (pipeline behaviour on test PRs) | Security (fork PR, secrets) | Smoke
Objective       : Gates run and block as specified; skipped gates report success; local = CI outcome
AC Coverage     : AC-01, AC-02, AC-03, AC-04, AC-05
DFMEA Coverage  : THM01FTR07-DFMEA FM rows (false green, fork exposure, local / CI drift)
Framework       : Throwaway test PRs (failing test, High SAST finding, fake secret, low coverage, app-only
                  change); gate scripts run locally on the same commit

Test Cases       : designed with the safe-alm-testing skill (Step 04) at iteration start (shift-left);
                   each TC-## mapped to [AC-##] / [FM-##]
Test Data        : synthetic only — no production data, no personal data
Coverage Target  : ≥ 80% line coverage for new code; mutation score ≥ 60% for business logic
Test Checklist:
  [ ] All ACs covered by at least one test case (TC-## [AC-##] mapping complete)
  [ ] Happy path, partitions, boundaries, error paths covered
  [ ] In-scope DFMEA failure modes covered (TC-## [FM-##])
  [ ] Test data prepared — no production data
  [ ] Tests integrated into CI pipeline
  [ ] Test closure report completed (safe-alm-testing Step 04)

Effort Estimate : 4h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : THM01WI12 (PR merged), THM01WI13 (checks required)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
