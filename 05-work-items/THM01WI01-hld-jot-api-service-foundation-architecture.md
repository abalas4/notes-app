THM01WI01 — Jot API service foundation architecture

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[HLD] THM01WI01 — Jot API service foundation architecture
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story/Feature : THM01FTR06 (serves THM01STR01, THM01STR54; THM01STR02, THM01STR03 later in PI-1)
Owner                : Solution Architect (@abalas4)
HLD Reference ID     : THM01FTR06-HLD  (06-design/THM01FTR06-HLD.md)

Objective       : Produce the high-level architecture of the jot-api service: container on Lambda behind
                  HTTP API, data store, auth boundary, observability, environments (ADR-003, 004, 005, 007, 012)

HLD Sections to Produce:
  [ ] System context diagram (C4 Level 1)
  [ ] Component/container diagram (C4 Level 2)
  [ ] Technology choices with rationale (cite the Accepted ADRs)
  [ ] Integration points and external dependencies
  [ ] Data flow overview
  [ ] Key architectural decisions (ADR files in 06-design/adr/, listed with status)
  [ ] Security and compliance considerations; STRIDE threat table
  [ ] Data inventory & lifecycle (classification, stores, retention, erasure); §8.3 DPIA screening
  [ ] Scalability and HA strategy overview; NFR traceability table
  [ ] Deployment & release (environments, rollout, feature flags, rollback)
  [ ] Open questions / assumptions; Revision History

Deliverable     : 06-design/THM01FTR06-HLD.md
Review Gate     : Architecture Review Board sign-off (Architecture Lead @abalas4) before LLD begins;
                  safe-alm-req-design-reviewer run first
Effort Estimate : 8h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : None
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
