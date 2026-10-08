Iteration 01 plan — PI-1 — Jot team

```
ITERATION 01 — PI-1 — Jot team          Dates: 2026-10-08 → 2026-10-21
Status         : Confirmed
Iteration goal : Objectives 1, 2: the API skeleton runs in a container with health and readiness and the standard error body, and its PRs are gated by the API CI quality gates.
Capacity       : 8 pts (velocity — new team baseline, leave 0 days; estimates indicative — capacity.md)       Planned: 11
```

| Story | Points | Release Tag | DoR | Owner | Notes |
|-------|--------|-------------|-----|-------|-------|
| THM01STR01 API service skeleton, health and readiness | 3 | REL-1.0.0 (forecast; confirmed when committed) | ✅ except Work Item files — created at iteration start | Developer (@abalas4) | WI types: HLD, DFMEA, LLD (THM01FTR06), IMPL, TEST |
| THM01STR54 Standard error body and request logging | 3 | REL-1.0.0 (forecast; confirmed when committed) | ✅ except Work Item files — created at iteration start | Developer (@abalas4) | WI types: LLD part (THM01FTR06), IMPL, TEST; needed by STR01 AC-03 |
| THM01STR29 API CI quality gates | 5 | REL-1.0.0 (forecast; confirmed when committed) | ✅ except Work Item files — created at iteration start | Developer (@abalas4) | WI types: HLD, DFMEA, LLD (THM01FTR07 — API pipeline part), IMPL, TASK (required checks), TEST; built with STR01 (D-01) |

Change 2026-10-08 (PO): THM01STR54 pulled into iteration 01 — THM01STR01 AC-03 needs the standard error body (red string found at iteration 01 planning). Load 11 pts > 8-pt baseline, accepted because estimates are indicative.

Review (at iteration end):
  Completed      : —      Not done: —
  Velocity       : —
  Demo           : —      (system-demo-01.md)
Retrospective    : —
