THM01WI06 — Tests for the jot-api skeleton, health and readiness

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[TEST] THM01WI06 — Tests for the jot-api skeleton, health and readiness
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story    : THM01STR01
Owner           : QA Engineer (@abalas4)
Design Skill    : safe-alm-testing (Step 04)

Test Type       : Unit | Integration (DynamoDB Local up / stopped) | Smoke (Newman)
Objective       : Verify health, readiness and the store-unavailable path
AC Coverage     : AC-01, AC-02, AC-03
DFMEA Coverage  : THM01FTR06-DFMEA FM rows for readiness / store timeout (numbers set when the DFMEA is written)
Framework       : pytest + pytest-cov; Docker Compose; Newman

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
Blocked By      : THM01WI04 (PR merged — code review APPROVED)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
