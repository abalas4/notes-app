Iteration 01 plan — PI-1 — Jot team

```
ITERATION 01 — PI-1 — Jot team          Dates: 2026-10-08 → 2026-10-21
Status         : Confirmed
Iteration goal : Objectives 1, 2: the API skeleton runs in a container with health and readiness and the standard error body, and its PRs are gated by the API CI quality gates.
Capacity       : 8 pts (velocity — new team baseline, leave 0 days; estimates indicative — capacity.md)       Planned: 11
```

| Story | Points | Release Tag | DoR | Owner | Notes |
|-------|--------|-------------|-----|-------|-------|
| THM01STR01 API service skeleton, health and readiness | 3 | REL-1.0.0 (confirmed) | ✅ Ready (Work Items 05-work-items/) | Developer (@abalas4) | THM01WI01–06 |
| THM01STR54 Standard error body and request logging | 3 | REL-1.0.0 (confirmed) | ✅ Ready (Work Items 05-work-items/) | Developer (@abalas4) | THM01WI03 (shared LLD), WI07–08; needed by STR01 AC-03 |
| THM01STR29 API CI quality gates | 5 | REL-1.0.0 (confirmed) | ✅ Ready (Work Items 05-work-items/) | Developer (@abalas4) | THM01WI09–14; built with STR01 (D-01) |

Change 2026-10-08 (PO): THM01STR54 pulled into iteration 01 — THM01STR01 AC-03 needs the standard error body (red string found at iteration 01 planning). Load 11 pts > 8-pt baseline, accepted because estimates are indicative.

Review (at iteration end):
  Completed      : —      Not done: —
  Velocity       : —
  Demo           : —      (system-demo-01.md)
Retrospective    : —

Work order (gates): HLD WI01 / WI09 → DFMEA WI02 / WI10 → LLD WI03 / WI11 → design review (design-reviewer agent)
→ **owner approves the LLDs** → IMPL WI04 + WI12 (together, D-01) → WI05, WI07 → code review → TEST WI06, WI08, WI13, WI14.
