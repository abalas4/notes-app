THM01WI09 — CI pipeline and quality gates architecture

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[HLD] THM01WI09 — CI pipeline and quality gates architecture
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story/Feature : THM01FTR07 (serves THM01STR29 now; THM01STR30, STR31, STR67 later)
Owner                : Solution Architect (@abalas4)
HLD Reference ID     : THM01FTR07-HLD  (06-design/THM01FTR07-HLD.md)

Objective       : Architecture of the GitHub Actions pipelines: workflows, gate scripts shared with local runs,
                  required status checks, path filters, fork-PR isolation, artifacts, OIDC boundary (ADR-008,
                  ADR-010, ADR-011, CONTRIBUTING.md)

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

Deliverable     : 06-design/THM01FTR07-HLD.md
Review Gate     : Architecture Review Board sign-off (Architecture Lead @abalas4) before LLD begins;
                  safe-alm-req-design-reviewer run first
Effort Estimate : 4h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : None
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
