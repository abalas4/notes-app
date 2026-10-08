PI-1 ROAM board — Jot team

PI risks, each ROAMed at PI Planning and re-checked at every iteration review (one team: the ART Sync
is the iteration review). Project-wide risks stay in `00-planning/raid-log.md`; design risks in the DFMEAs.

| # | Risk | Raised by / date | Impact (objective / Feature) | ROAM | Owner | Action / mitigation | Due | Status |
|---|------|------------------|------------------------------|------|-------|---------------------|-----|--------|
| R-01 | The new-team baseline (8 pts / iteration) may be far from real velocity, so the REL-1.0.0 date cannot be forecast yet | Jot team / 2026-10-08 | REL-1.0.0 / all Features | Owned | Release Manager (@abalas4) | Measure velocity in iterations 01–03; re-forecast the roadmap at the iteration 03 review | 2026-11-18 | Open |
| R-02 | Iteration 01 carries the first HLD, DFMEA and LLD (THM01FTR06, THM01FTR07) as well as code, and may overrun | Jot team / 2026-10-08 | Objectives 1, 2 | Mitigated | Tech Lead (@abalas4) | Design only the Stories in the iteration (story slices of each Feature's design); buffer 15 %; carry-over is re-estimated, not assumed half done | 2026-10-21 | Open |
| R-03 | The 7-day cooling period may block the newest stable release of a scaffolding dependency | Jot team / 2026-10-08 | Objectives 1, 2, 5 | Accepted | Tech Lead (@abalas4) | Use the newest stable version older than 7 days (stable-versions rule) | — | Open |
| R-04 | The AWS bootstrap needs the owner's own credentials and a local run, which cannot be automated | Jot team / 2026-10-08 | Objective 3 | Owned | Product Owner (@abalas4) | Claude prepares the bootstrap code and steps; the owner runs it in their own terminal (credentials never shown to Claude) | 2026-11-04 | Open |
