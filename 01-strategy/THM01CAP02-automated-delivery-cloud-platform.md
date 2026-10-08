THM01CAP02 — Automated delivery and cloud platform

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[CAPABILITY] THM01CAP02 — Automated delivery and cloud platform
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Theme     : THM01
Type             : Enabler
Description      : The architectural runway every Jot change travels on: a CI pipeline with the
                   way-of-working quality and security gates; one-click test runs on an emulator,
                   the owner's phone and AWS Device Farm; and every AWS resource the API needs
                   created from code by GitHub Actions with narrowly scoped, keyless access.
Benefit Hypothesis: If building, testing and provisioning are automated end to end, then every
                   Story can be verified on emulator → phone → Device Farm and released with no
                   manual AWS console steps, because manual set-up is slow, error-prone and leaves
                   undocumented, over-privileged access behind.
Success Metrics  :
  - Manual AWS console changes after the one-time bootstrap: 0 (drift check finds none)
  - Test runs started from GitHub Actions or one local script: 100 % of emulator, Device Farm and
    dev-environment runs
  - Long-lived AWS access keys stored anywhere: 0
WSJF Priority    : Value 6 | Time Criticality 9 | Risk Reduction 9 | Job Size 5 → WSJF 4.8
                   (proposed; Product Owner confirms at PI Planning)
Sizing           : S
Affected ARTs    : Jot team (solo)
PI Target        : PI-1
Linked Epics     : THM01EPC02
Business Owner   : Product Owner (@abalas4)
Arch Owner       : Architecture Lead (@abalas4)
Dependencies     : AWS account (legacy free tier); GitHub repository settings (branch protection,
                   Environments with required reviewers) applied by the owner.
Constraints      : OpenTofu, not Terraform (licence) — D-08; GitHub Actions with OIDC only;
                   one IAM role per workflow with a permissions boundary; Device Farm free minutes
                   are one-time; public repository; stable tool versions only.
ALM Status       : Analysing
DoR Check        : ✅ Stored at 01-strategy/THM01CAP02-<slug>.md
                   ✅ Parent Theme THM01 linked
                   ✅ Type Enabler
                   ✅ Description clear to non-technical readers
                   ✅ Benefit hypothesis (If / then / because)
                   ✅ Success metrics with baselines and targets
                   ✅ Sized S
                   ✅ ART identified
                   ✅ Business Owner and Architecture Owner named
                   ✅ Dependencies and constraints documented
                   ⚠️ LBC approval — Product Owner approves THM01EPC02 in its pull request
DoD Check        : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
