# ADR-002: Mobile E2E with Appium (Python) + Espresso, run on emulator → personal phone → Device Farm
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR07, THM01FTR08; ADR-001, ADR-009, ADR-012

## Context
UI, E2E, accessibility and notification behaviour must be proven on Android now and on iOS later, at
near-zero cost. AWS Device Farm has 1,000 one-time free minutes (981.77 left on 2026-10-08), then
US$0.17 per device-minute. The plugin's MOB-01 rule needs every Story AC on each device tier (oldest and
latest supported OS, small and large phone, low-end Android).

## Options considered
1. **Appium 2 + Appium Python Client + pytest** as the cross-platform suite, **plus Espresso** as a fast
   Android smoke suite — the same language as the API tests; reused from the owner's proof of concept.
2. Appium + WebdriverIO (Node) — a second test language for the same coverage.
3. Detox / Maestro — no Device Farm test type; Detox also conflicts with app re-signing.

## Decision
- Suites: **Appium Python** (UiAutomator2 now, XCUITest later; the locator helper `by_test_id()` uses
  `AppiumBy.ID` on Android and `AppiumBy.ACCESSIBILITY_ID` on iOS; `accessibilityLabel` stays readable
  for TalkBack / VoiceOver) and **Espresso** for Android smoke. Notification flows use Appium
  (`openNotifications`) because Espresso cannot reach the notification shade.
- **One suite, three targets, in this order:** (1) Android emulator matrix — free, run as often as
  needed; (2) the owner's personal phone over wireless adb (USB fallback) with the same suites, plus
  manual UAT; (3) AWS Device Farm real devices, **last**. Only the runner configuration changes the
  target, never the test code.
- **Hard gate:** a Device Farm run never starts unless the same build passed the emulator matrix and the
  phone run (commit status `jot/phone-tests`). Steps 2 and 3 run once per slice, covering all its Stories.
- Emulator matrix (MOB-01 tiers): oldest supported OS on a small phone; latest OS on a large phone; a
  low-end profile (2 GB RAM, 2 cores). Google APIs images (Chrome is needed for the sign-in custom tab).
  Tablet: not supported in the MVP. The emulator calls the local Docker API (ADR-012).
- Unit / component: Jest + React Native Testing Library. Accessibility: RNTL queries + the Android
  Accessibility Test Framework.

## Consequences
- What the emulator cannot prove (OEM battery optimisation killing alarms, real notification shades,
  real start-up time and frame rate, real reboots) stays a DFMEA detection item until the Device Farm run.
- Device Farm budget: about 2 devices × 10 min per slice plus a full REL-1.0.0 regression ≈ 200 min,
  inside the free minutes. Guard rails: preflight check, Espresso first, 10-minute job timeout, stop at
  the first failure, paid minutes off unless the owner approves.
- Reminders on the emulator: tests schedule a minute ahead or use a debug-only hook; the exact-alarm
  permission is granted and revoked with `adb shell appops`. Offline: network toggled with adb.
- The test-run workflows and the phone script are delivered by THM01FTR08.
