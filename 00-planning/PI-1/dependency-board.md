PI-1 dependency board — Jot team

One team, so there are no cross-team dependencies; Story-to-Story dependencies stay in each Story's
`Dependencies` field. This board holds the external dependencies and the order of the committed work.

| # | Needed by (team / Feature / Story) | Provided by (team / external) | What | Needed in iteration | Committed in iteration | Status | Link |
|---|------------------------------------|-------------------------------|------|---------------------|------------------------|--------|------|
| D-01 | Jot / THM01FTR06 / THM01STR01 | Jot / THM01STR29 | API CI gates run on the skeleton's PR (built together) | 01 | 01 | Committed | THM01STR01, THM01STR29 Dependencies |
| D-02 | Jot / THM01FTR06 / THM01STR02, THM01STR03 | Jot / THM01STR01, THM01STR54 | Running service and error body | 03 | 01, 02 | Committed | THM01STR02, THM01STR03 Dependencies |
| D-03 | Jot / THM01FTR09 / THM01STR36 | Owner (external to the team) | AWS admin credentials on the owner's machine; GitHub Environment `aws-admin` | 02 | — (owner action) | Owned — ROAM R-04 | THM01STR36 Dependencies |
| D-04 | Jot / THM01FTR09 / THM01STR40 (stretch) | Owner (external) | Google OAuth client created in the owner's Google account | 04 | — (owner action) | Open — needed only if objective 4 is pulled in | THM01STR40 Dependencies |
| D-05 | Jot / THM01FTR01 / THM01STR04 (stretch) | Jot / THM01STR40 ← THM01STR37 ← THM01STR36 | Cognito dev pool for token checks | 04 | stretch | Uncommitted | THM01STR04 Dependencies |

No red strings: no dependency is needed earlier than the iteration it is committed in.

## Milestones

| Milestone | Date | Features |
|---|---|---|
| API skeleton with CI gates on `main` | 2026-10-21 (iteration 01 end) | THM01FTR06, THM01FTR07 |
| AWS account bootstrapped as code | 2026-11-04 (iteration 02 end) | THM01FTR09 |
| Velocity measured; REL-1.0.0 re-forecast | 2026-11-18 (iteration 03 end) | all |
| PI-1 System Demo | 2026-12-02 (iteration 04 end) | THM01FTR06, FTR07, FTR09 |
| Inspect & Adapt + PI-2 Planning (IP iteration) | 2026-12-03 → 2026-12-16 | — |

Release dates come from `10-release/PI-1-release-roadmap.md`.
