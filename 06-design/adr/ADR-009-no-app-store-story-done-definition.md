# ADR-009: No app store — Story Done on emulator + personal-phone UAT + Device Farm; CI-signed APK only for release hardening
Status        : Accepted (deviation from plugin rules — approved by the Product Owner)
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR07 (THM01STR67), THM01FTR08; REL-1.0.0 release plan; ADR-002

## Context
Plugin rules: testing §16 UAT needs `[Mobile]` UAT on a real device with a **store-track build** (e.g.
Play internal testing) before Story Done; implementation MA-18 promotes one CI-signed binary through
store tracks; testing MOB-10 needs the store pre-launch report and Data safety form. Jot is a personal
app with no Play Store listing.

## Options considered
1. **No app store.** Story Done on the emulator matrix, the owner's phone and Device Farm; a CI-signed
   APK for release hardening only.
2. Publish to Play internal testing — a developer account and store compliance work for a single user.

## Decision
- **Story Done (testing step), in this order:** (1) automated suites green on the emulator matrix;
  (2) the same suites green on the owner's personal phone **and** the owner's manual UAT recorded as
  `UAT-<Story ID>` (device model, Android version, build), against the `dev` stack; (3) the same suites
  green on Device Farm. Steps 2 and 3 run once per slice (ADR-002).
- **Builds:** during slices every target (PRs, `main`, emulator, phone, Device Farm) uses the CI debug
  build with bundled JS. A **manual release-hardening workflow** signs the release APK (keystore and
  passwords only in GitHub Environment secrets); that **one signed binary** goes to the phone UAT, the
  Device Farm regression and the GitHub Release for `REL-x.y.z` (Story decision 1.3-Q12, THM01STR67).
- **N/A by this ADR:** store tracks and promotion (MA-18 promotion part), MOB-10 store pre-launch report
  and Data safety form. MobSF and the privacy / permission review still run (V45, MOB-09).

## Consequences
- Distribution of REL-1.0.0 is the signed APK attached to the GitHub Release and installed with adb.
- Revisit if Jot is ever distributed to other people (then a store track and MOB-10 apply).
