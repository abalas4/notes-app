PI-1 capacity — Jot team

```
CAPACITY — PI-1 — Jot team                         Iterations: 01–04 (+ IP iteration)
PI dates : 2026-10-08 → 2026-12-16   · iteration length 2 weeks · one team, one developer, full-time
Source   : requirements 10-pi-planning.md §1 (new-team rule: 8 pts per full-time developer per
           2-week iteration until 3 iterations of velocity exist)
```

| Iteration | Dates | Team members × days available | Holidays / leave / training | Normalised capacity (pts) | Historic velocity (last 3) | Planned load (pts) |
|-----------|-------|-------------------------------|-----------------------------|---------------------------|----------------------------|--------------------|
| 01 | 2026-10-08 → 2026-10-21 | 1 × 10 | none known | 8 | — (new team) | 8 |
| 02 | 2026-10-22 → 2026-11-04 | 1 × 10 | none known | 8 | — | 6 |
| 03 | 2026-11-05 → 2026-11-18 | 1 × 10 | none known | 8 | — | 5 |
| 04 | 2026-11-19 → 2026-12-02 | 1 × 10 | none known | 8 | — | 3 committed (+ 5 stretch) |
| IP | 2026-12-03 → 2026-12-16 | 1 × 10 | — | no committed Feature work | — | — |
| **PI** | | | | **32** | | **22 committed** |

Leave not yet known: each day of leave reduces that iteration by 1 pt; the iteration plan records it.

## Capacity allocation (share of PI capacity, 32 pts)

| Allocation | Agreed share | Points | Committed in PI-1 |
|---|---|---|---|
| Business Features (THM01EPC01, incl. its Implementation and NFR Features) | 55 % | 17.6 | 14 pts — THM01FTR06 (all four Stories) |
| Enablers (THM01EPC02 — CI, test workflows, AWS as code) | 25 % | 8 | 8 pts — THM01STR29, THM01STR36 |
| Tech debt / upgrades / reliability | 5 % | 1.6 | Reserved hours, no Story: dependency upgrades and cooling-period checks (stable-versions rule) |
| Defects / support | 0 % | 0 | Nothing is live yet |
| Buffer (unplanned) | 15 % | 4.8 | Unplanned work; stretch objectives use it only if not needed |

- **Committed load 22 pts ≤ capacity minus buffer (27.2 pts).** Business is below its 55 % share
  because every other Business Story needs authentication and the AWS prerequisites first
  (dependency board); the stretch objectives (`objectives.md` #4, #5) take up the difference.
- The debt share below the operations default (15–20 %) is agreed in `objectives.md` (greenfield
  codebase); it returns to 15 % from PI-2.
- **Velocity switch:** after iteration 03 the plan uses the median velocity of iterations 01–03 and
  the PI release roadmap is re-forecast (`10-release/PI-1-release-roadmap.md`).
