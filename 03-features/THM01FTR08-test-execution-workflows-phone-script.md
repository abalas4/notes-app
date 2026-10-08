THM01FTR08 — Test-execution workflows and phone script

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[IMPLEMENTATION FEATURE] THM01FTR08 — Test-execution workflows and phone script
Tags: [Implementation] [API] [Mobile] [Infra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Parent Epic        : THM01EPC02
Surfaces           : API (apis/jot-api — dev environment for tests) · Mobile Android (mobile/jot — test runs)
Feature Owner      : Architecture Lead (@abalas4)
Description        : Requirement R-TX (plan §8.1). Manual GitHub Actions workflows started with "Run workflow"
                     or `gh workflow run`: `emulator-tests` (also on every PR), `device-farm`, `dev-up` and
                     `dev-down`; and one local script, `scripts/phone-test.sh`, that builds (or downloads the
                     CI-signed APK with `--from-ci <sha>`), installs and runs Espresso + Appium Python on the
                     owner's phone over adb, then records a `jot/phone-tests` commit status and prompts for the
                     UAT record.

Architectural Note : One suite, three targets: the same Espresso and Appium Python tests run on the emulator,
                     the phone and Device Farm; only runner configuration changes. The Device Farm workflow
                     enforces the hard gate — it refuses a commit without a green emulator run and a green
                     `jot/phone-tests` status. Device Farm guard rails from the reference project: preflight,
                     free-minutes check, `allow_paid = false` default, 10-minute job timeout, stop on first
                     failure, cleanup always. Protected Environments `dev` and `device-farm` with the owner as
                     required reviewer. No self-hosted runner (public repository).
Enablement Value   : Produces Story Done evidence for every [Mobile] Story of THM01EPC01 (emulator matrix →
                     phone + UAT → Device Farm, deviation C-05).
ADR Reference      : TBD at step 1.7 — test-execution design; C-05 deviation

Acceptance Criteria:
  AC-01: Given a commit, When the owner runs `emulator-tests`, Then the APK and test APK are built, an emulator
         and the local Docker API start in the job, Espresso + Appium Python run, and HTML / JUnit reports are
         attached
  AC-02: Given a connected phone and a running `dev` environment, When the owner runs `scripts/phone-test.sh`,
         Then the app is built, installed and tested on the phone, an HTML report is written, and on success the
         commit gets the `jot/phone-tests` success status
  AC-03: Given a commit without a green emulator run or phone status, When `device-farm` is started for it, Then
         the workflow stops before uploading anything and no device minutes are used
  AC-04: Given `dev-up` was run, When `dev-down` runs, Then every `jot-dev-*` resource is destroyed except the
         state bucket and the image repository, and the job summary says so

Sizing             : M
WSJF               : (5 + 8 + 7) / 5 = 4.0   (proposed)
PI Target          : PI-1
Sprint Target      : TBD at PI Planning (step 1.5) — emulator, dev and phone parts in slice 1; Device Farm by slice 2
Release Tag        : None — forecast at PI Planning (step 1.5)
Feature Type       : New
Original Feature   : N/A
Linked Stories     : TBD at step 1.3 (≥ 1 [API], ≥ 1 [Mobile] [Android])
HLD Reference      : THM01FTR08-HLD
LLD Reference      : THM01FTR08-LLD

Dependencies       : THM01FTR07 (signed APK, CI); THM01FTR09 (roles for `dev` and Device Farm, dev environment)
Constraints        : Device Farm free minutes are one-time (981.77 left); test code only under `tests/`,
                     helpers under `scripts/` (folder standard); stable versions.
ALM Status         : New
DoR Check          : ✅ Stored at standard path · ✅ Parent Epic · ✅ Tags · ✅ Surfaces · ✅ Feature Type
                     · ✅ Description · ✅ Architectural note · ✅ 4 ACs · ✅ Sized M · ✅ WSJF · ✅ PI Target
                     · ✅ HLD / LLD IDs · ✅ Dependencies and constraints · ✅ Owner
                     ⚠️ Sprint Target — PI Planning (1.5) · ⚠️ Child Stories — step 1.3
                     N/A Style guide — no screens in this Feature
DoD Check          : ⚠️ Not started
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
