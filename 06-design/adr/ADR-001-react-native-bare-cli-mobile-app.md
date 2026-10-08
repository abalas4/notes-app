# ADR-001: Mobile app built with React Native (bare CLI, TypeScript), iOS-ready
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01EPC01; THM01FTR01–05, THM01FTR10 HLDs; ADR-002, ADR-006, ADR-011

## Context
Jot ships on Android first and must reach iPhone later from the same code (THM01EPC01 Surfaces:
Mobile app = Yes, Android; iOS later). The owner already ran a React Native proof of concept (kept
outside this repo) end to end on AWS Device Farm with Espresso and Appium. The 12 approved screens
(W1–W12) use only flex / grid layout, rounded corners, soft shadows, one inset ring and one dashed
ring — no gradients, blur, images or custom drawing.

## Options considered
1. **React Native, bare CLI, TypeScript** — about 90–95 % of the code shared with iOS; proven on Device
   Farm with the owner's tooling; the same `testID`s serve Appium on Android and iOS; named in the
   plugin's mobile rules (`mobile-01-apps.md`); free (MIT).
2. Flutter — similar sharing, but a new learning curve and Dart E2E tests; not proven with the owner's
   tooling.
3. Native Kotlin + Swift — two apps, almost nothing shared.
4. React Native with Expo (managed) — Expo prebuild regenerates the native folders and breaks the
   checked-in Espresso project (`android/app/src/androidTest`).

## Decision
React Native **bare CLI** with **TypeScript** and the New Architecture, in one cross-platform component
`07-source-code-tests/src/mobile/jot/` (`android/` now, `ios/` later). Version: the latest stable
release that has cleared the 7-day cooling period (`CONTRIBUTING.md`, stable versions only).

## Consequences
- Every library must support Android **and** iOS. Candidate set, each vetted at its LLD (licence,
  maintenance, New Architecture support, cooling period): React Navigation (stack, tabs, drawer),
  TanStack Query (server state), Zustand (UI state), react-native-keychain (tokens), openapi-typescript
  + openapi-fetch (client generated from the OpenAPI spec), react-native-app-auth (PKCE, system
  browser), FlashList (masonry), react-native-draggable-flatlist with Reanimated and Gesture Handler, a
  bottom-sheet library, a native menu, the community date-time picker, react-native-svg, and crash
  reporting with no personal data. Notifications: ADR-006.
- All 12 screens are feasible. Two caveats became product decisions: W4 rich-text "Aa" → plain text in
  the MVP (RAID log, L-02); the W11 notification is drawn by the OS, and its Snooze action opens the W12
  sheet (ADR-006).
- Design tokens come from `06-design/ux/style-guide.md` through `src/shared/design-tokens/`; fonts are
  bundled as static files.
- The same `testID` on every element, so the Appium suite runs on iOS with a capability change only.
- iOS later needs an Apple Developer membership and macOS builds (GitHub-hosted macOS runners are free
  for public repos). iOS Stories are raised as `[iOS]` counterparts in a later PI.
- No plugin stack profile exists for React Native: ADR-011.
