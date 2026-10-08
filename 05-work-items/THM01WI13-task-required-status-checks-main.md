THM01WI13 — Required status checks on main and fork-PR approval

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[TASK] THM01WI13 — Required status checks on main and fork-PR approval
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Story    : THM01STR29
Owner           : Product Owner (@abalas4) — GitHub settings need the owner's account
Task Type       : Config

Objective       : Make the new CI checks blocking (AC-01, AC-02) and keep fork PRs waiting for approval (AC-03)
Deliverable     : Branch protection on main lists the CI check names from THM01WI11 as required; Actions
                  setting "require approval for fork PR workflows" confirmed; README checklist ticked

Steps           :
  1. Claude lists the exact check names after the first green run
  2. The owner adds them as required status checks in the repository settings
  3. Claude verifies with a test PR (THM01WI14)

Effort Estimate : 1h
Sprint Target   : PI-1 iteration 01
Release Tag     : REL-1.0.0 (inherited from the parent Story)
Blocked By      : THM01WI12 (first green CI run)
ALM Status      : New
DoD Check       : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
