# ADR-011: Mobile gates run without a React Native stack profile — generic mobile rules plus PARENT evidence
Status        : Accepted (deviation from plugin rules — approved by the Product Owner)
Date          : 2026-10-08
Deciders      : Product Owner, Tech Lead (@abalas4)
Related       : ADR-001, ADR-004; THM01FTR07 (THM01STR30); all `[Mobile]` Stories

## Context
The plugin runs its language-specific gates (commands, review patterns, test-runner commands) from a
stack profile. Only `lang-python-fastapi` exists; there is no profile for React Native / TypeScript.
The API's DynamoDB deviation from the Python profile is covered by ADR-004.

## Options considered
1. **Use the plugin's generic mobile rules (`mobile-01-apps.md`, V44–V45, MOB-01…MOB-09) and supply the
   JavaScript / TypeScript commands as PARENT evidence** in the verifier and review reports.
2. Write a React Native stack profile first — useful, but outside this project's scope.
3. Skip the language-specific mobile gates — not acceptable.

## Decision
Option 1. Each mobile LLD sets `Stack Profiles: none — TypeScript / React Native` and lists the commands
that stand in for the profile gates: `tsc --noEmit` (types), ESLint + Prettier (lint / format), Jest +
React Native Testing Library with coverage ≥ 80 % on new code (unit), `npm audit` (dependencies), MobSF
in Docker (static scan, V45), the licence check, the debug build. The verifier and code-review reports
quote their output as PARENT evidence.

## Consequences
- The mobile gates are automated in CI (THM01STR30) but not driven by a plugin profile, so their
  completeness is checked by the code review, not by the profile.
- Revisit if the plugin ships a React Native profile: supersede this ADR and adopt it.
