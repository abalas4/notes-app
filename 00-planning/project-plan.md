# Jot — Project Plan (notes, checklists, reminders)

> Status: **Stack confirmed by the user 2026-10-08 (§11 D-01…D-11, Q1–Q6).**
> No SAFe ALM skill is run until the stack is confirmed.
> Created: 2026-10-08 · Owner: @abalas4 · Tracker: §13 (update after every completed step)
> Location: `00-planning/project-plan.md`. The plugin's structure standard §9 allows no plan file at the repo root.
> This file describes how the work is planned, so it lives in `00-planning/` with no THM ID (standard §2a).

A simple, colour-coded mobile app for capturing **notes**, **checklists (task lists)** and **reminders**,
backed by a private REST API hosted on AWS. Android first; iPhone later, using the same codebase.
The UI follows the **Jot Design System v1** (`design.md`, `wireframe.html`, `jot-canvas/project/*.dc.html`
screens W1–W12). It is currently in `design_style_guide/` and moves to `06-design/ux/` at Phase 0 (§0, C-02).

Way of working: **SAFe ALM Way of Working v1.1**, carried out with the
`safe-alm-skills-with-sub-agents` plugin (v1.1.0, 6 skills, 23 sub-agents). All artefacts are
committed to a **public GitHub repository** (`abalas4/notes-app`) using the plugin's mandatory folder structure (§9).

---

## 0. Way-of-working conformance (mandatory — user instruction 2026-10-08)

**Rule:** all work strictly follows the SAFe ALM Way of Working and the plugin's skills, gates,
templates and folder standard. In particular:
- Every lifecycle step runs **through its skill**, in order: `/safe-alm-requirements` → `/safe-alm-implementation` →
  `/safe-alm-code-review` → `/safe-alm-testing` → `/safe-alm-release` → `/safe-alm-operations`.
  Release planning runs at PI Planning, as the way of working allows. Artefacts are never hand-written outside a skill.
- A step starts only when the previous step's exit gate is met: LLD Approved → verifier PASS → review APPROVE and
  PR merged → Story Done → GO recorded. Claude never skips a gate. When a skill stops at a gate, Claude reports what is
  missing and waits.
- Human decisions stay with the user: LLD sign-off, PR merge, Story acceptance (UAT), release GO, on-call ownership.
- One Story per conversation (`/clear` between Stories); artefact IDs are always quoted.
- Folder and naming rules follow `project-structure-standard.md` (violations are 🔴 at V34 / T-07).
- Branches `feat|fix|refactor|test|chore|docs|perf/<STORY-ID>-<slug>`; Conventional Commits with the Story ID;
  PR < 400 changed lines per IMPL WI; the IMPL WI ID goes in the PR description; tags `REL-x.y.z`.
- Every deviation from a plugin rule needs an **ADR** (`06-design/adr/`) and the user's explicit approval. Nothing is waived silently.

### Conformance register (plan checked against the plugin on 2026-10-08)

| ID | Plugin rule | Finding in the earlier draft | Resolution | Status |
|---|---|---|---|---|
| C-01 | Structure §9: only listed files at the repo root | `PROJECT-PLAN.md` and `CLAUDE.md` at the root | Plan moved to `00-planning/project-plan.md`. `CLAUDE.md` is kept local and gitignored, so it never enters the repo; it only points to this plan | ✅ fixed (plan); CLAUDE.md at Phase 0 — **Update 2026-10-08 (user: "folder structure across the board"):** `project-plan.md` is not a §2a file either, so at Step 01 it is **migrated and deleted**: decisions → ADRs (`06-design/adr/`), risks → `00-planning/raid-log.md`, plan + tracker → `00-planning/PI-1/` (objectives, iteration plans), roadmap → `10-release/PI-1-release-roadmap.md`. `CLAUDE.md` lives in the local workspace folder, outside the repo (§9a) |
| C-02 | Structure §3: style guide record at `06-design/ux/style-guide.md`; UX artefacts under `06-design/ux/<ID>/` | `design_style_guide/` at the root (unknown top-level folder 🔴) | Phase 0: move the source files to `06-design/ux/` (wireframes and canvas referenced from `style-guide.md` as the design-tool library). Step 01 produces the `style-guide.md` record | Phase 0 — **Update 2026-10-08 (user):** raw design sources are **not committed**. Phase 0 moves `design_style_guide/` to the workspace folder `jot-design-source/`, beside (not inside) the repo (§9a). At Step 01 `design.md` becomes `06-design/ux/style-guide.md`, and each wireframe screen becomes approved snapshots `06-design/ux/<Feature ID>/<screen>-<state>.png` referenced by that Feature's `ux-spec.md`. `style-guide.md` links the claude.ai design system as the design-tool library. No ADR needed |
| C-03 | Requirements `08-ux-design.md` §1: style guide **Approved** with SG-01…SG-15 before any UX DESIGN WI | `design.md` has no SG-07 empty / error / loading / offline patterns, SG-09 content, SG-11 motion, SG-12 i18n, or full SG-15 mobile (dark mode, app icon, splash, permission rationale) | Step 01: the requirements skill drafts the missing sections; **you approve** the style guide v1.1 | Step 01 |
| C-04 | Structure §6: IaC in `07-source-code-tests/infra/`; Compose files at `07-source-code-tests/` | SAM `template.yaml` placed inside `src/apis/jot-api/` (superseded: D-08 = OpenTofu) | §9 corrected: `07-source-code-tests/infra/{modules,envs/dev,envs/prod}` — fits OpenTofu's module/env layout directly | ✅ fixed |
| C-05 | Testing §16 UAT: `[Mobile]` UAT on a **real device** with a **store-track build** (Play internal testing), not a simulator, before Story Done | Story Done planned on the emulator only; distribution by sideload / Firebase App Distribution | **Approved deviation (user, 2026-10-08)**: no Play Store, because this is not a real product. Story Done = (1) automated suites green on the emulator matrix, (2) UAT on your **personal Android phone** with the **CI-signed release APK** installed over adb (the same binary later sent to Device Farm), against the `dev` stack, **and** (3) the same suites green on **AWS Device Farm** real devices. Recorded as an ADR at Step 01 | ✅ deviation approved (ADR at Step 01) |
| C-06 | Testing §19 MOB-01: every Story AC on each device tier (oldest and latest supported OS, small and large phone, low-end Android); emulators allowed; at least one real device before release | Emulator plan had 2 AVDs, no oldest-OS or low-end tier | Emulator matrix extended (§5.3). Real devices: your phone (UAT) + Device Farm hardening before release | ✅ fixed |
| C-07 | Way of working §6.4: branch protection on `main`, required checks, one approval per PR | **GitHub Free does not offer branch protection or rulesets on private repos**, and GitHub does not let a PR author approve their own PR (you are the only person) | Either **GitHub Pro (US$4/month)**, which enables protection and required checks, **or** an ADR accepting process-only protection. Either way, "approval" = your recorded approval comment on the PR after the code-review report, then you merge → **Q5, D-11** | ✅ resolved 2026-10-08: **public repo** (Q5) → branch protection + required checks are free and enforced. Only the self-approval part remains (D-11 ADR) |
| C-08 | Implementation MA-18: release builds signed by CI only; the same signed binary is promoted internal → beta → production. Testing MOB-10: store pre-launch report and Data safety | No store tracks (C-05 deviation) | CI signs the release APK (keystore in GitHub secrets, never in the repo). That **one binary** goes to your phone, to Device Farm, and to the GitHub Release asset for REL-x.y.z. Store promotion and MOB-10 are **N/A by the same ADR** as C-05. MobSF and the privacy/permission review still run (V45, MOB-09) | ✅ planned (deviation via C-05 ADR) — **Update 2026-10-08 (Q12):** signing happens only in the manual release-hardening workflow; that one signed APK goes to phone UAT, the Device Farm regression and the GitHub Release. Slice testing uses the CI debug build (bundled JS) |
| C-09 | Stack profile `lang-python-fastapi` assumes SQLAlchemy + Alembic; no profile exists for React Native | DynamoDB and React Native are outside the profiles | ADRs at Step 01: DynamoDB repository layer + item-schema-version migration tests; RN mobile gates via `mobile-01-apps.md` with JS commands supplied as PARENT evidence | Step 01 (ADRs) |

---

## 1. Scope

### 1.1 MVP (release REL-1.0.0, Android)

| Area | Capability | Design reference |
|---|---|---|
| Notes | Create / edit / delete text notes; title + body; 8 note colours; pin / unpin; archive / unarchive; delete with Undo snackbar (5 s) | W1 Home, W4 Note, Editor, Components |
| Checklists | List notes with items; check / uncheck (strike-through, moves to "Completed"); progress "N of M done"; reorder (drag handle); hide completed, uncheck all, delete completed, convert to note | W5 List, W10 List states, Tasks |
| Organise | Labels (create, rename, delete, assign through a label picker); search; filter chips; sort; multi-select with bulk actions; two-column masonry / single-column toggle; side drawer | W2 Sort, W3 Select, W6 Label picker, W7 Drawer, W8 Labels |
| Reminders | Date/time reminder on a note or list (quick picks, calendar, time, repeat); Reminders tab (Overdue / Today / Tomorrow, Upcoming / Done); local notification with **Mark done / Snooze / Open**; snooze presets; edit / remove reminder | W9 Reminder, W11 Notification, W12 Snooze |
| Account | **Sign in with Google** (through Cognito) / sign out; data synced to the API so it survives reinstall and a phone change | — |
| Offline | **Online-only MVP (D-07).** No network → clear offline state (banner + disabled/failed writes with Retry); nothing is lost silently. Offline-first sync is deferred (§1.3 L-01) | — |

### 1.2 Out of scope for MVP (backlog)
iOS release (planned for REL-1.1, see §3.3), **Cognito native accounts (email + password, MFA) and
Google ↔ native account linking — Phase B in §4.2**, dark theme, tablet layout, sharing and collaborators,
drawings and images, voice notes, web client, location-based reminders, and the items in §1.3. `design.md` also marks the
dark theme, tablet layout, empty and error states, and sharing as not yet designed. Empty and error
states are still needed for the MVP, so they go to UX as a design gap at Step 01.

### 1.3 Deferred to later releases — do not lose (backlog register)
Each item becomes a backlog Feature at Step 01 (`/safe-alm-requirements`) with Feature Type = New and a
target release tag set at PI planning (1.5).

| ID | Deferred capability | Decided | MVP behaviour meanwhile | Notes for later |
|---|---|---|---|---|
| L-01 | **Offline-first** with outbox sync | D-07, 2026-10-08 | Online-only; offline banner + Retry | Outbox + `changes?since=` pull, LWW per field group, tombstones, op-sqlite (SQLCipher) local DB; DFMEA rows for conflicts / data loss. Design the API (`version`, `updatedAt`, soft deletes) so it can be added without a breaking change |
| L-02 | **Rich-text "Aa" formatting** in the W4 editor | D-09, 2026-10-08 | Plain text; "Aa" button hidden | Candidates `react-native-enriched` (native) or `10tap-editor` (WebView); needs a stored format + migration of plain-text bodies |
| L-03 | **Server push reminders** (FCM/APNs + EventBridge Scheduler) | D-06, 2026-10-08 | Local notifications on the device | Needed for reminders across multiple devices |
| L-04 | **Cognito native accounts** + Google ↔ native linking | D-05, 2026-10-08 | Google federation only | Phase B in §4.2 |
| L-05 | **Trash view** (restore / delete forever, e.g. 7 days) | Story review Q3, 2026-10-08 | Delete = 5 s Undo, then gone | Drawer entry hidden until then; server soft-delete already exists |

---

## 2. Guiding constraints

1. **Cost first:** use AWS **always-free** services where possible. Use serverless pay-per-request
   services (no idle cost). Avoid anything billed hourly: no EC2, RDS, NAT Gateway, ALB, EKS or
   Fargate services, and no Secrets Manager.
2. **Reuse what is proven:** the React Native + Appium + Espresso + AWS Device Farm setup in
   rnlab_aws reference project (kept locally, outside this repo) already runs on real devices (Espresso 2/2,
   Appium Node 4/4, Appium Python 4/4).
3. **Maximise code shared with iOS:** one codebase, with platform-specific code only where the OS requires it.
4. **Plugin fit:** the plugin can only fully run its gates (commands, patterns, test runners) on a
   stack that has a **stack profile**. Today only `lang-python-fastapi` exists.
5. **Security hard rules carried over from rnlab_aws:** Claude never reads `~/.aws`, never echoes
   credentials, account IDs or ARNs, and the user runs every admin step (IAM, credential refresh)
   in their own terminal.
6. **Stable versions only (user rule, 2026-10-08):** every language, runtime, framework, library, tool,
   base image, GitHub Action and AWS runtime uses its **latest stable release** — no alpha, beta, RC,
   preview, nightly, canary or `next` tags. On top of that, the plugin's 7-day cooling period and
   language-version stability policy apply, and versions are pinned exactly. If a needed feature exists
   only in a pre-release, that needs an ADR + user approval.
7. **Public repository hygiene (Q5, 2026-10-08):** the repo is public, so everything committed is world-readable.
   - No secrets, ever: gitleaks as a pre-commit hook **and** a required CI check; GitHub secret scanning + push protection on.
   - No AWS account IDs, ARNs, Cognito pool/client IDs, API URLs or Device Farm ARNs in committed files:
     they come from GitHub Environment variables/secrets, SSM, or git-ignored `*.tfvars`.
     The OpenTofu state stays in the private S3 bucket, never in git.
   - The Android signing keystore and its passwords live only in GitHub Environment secrets.
   - CI safety: deploy jobs run only on `main` / protected Environments. The OIDC role trust policy is pinned to
     `repo:<owner>/<repo>:ref:refs/heads/main` and environment subjects. No `pull_request_target`.
     Workflow runs from fork PRs need approval. Actions are pinned to commit SHAs, and `GITHUB_TOKEN` gets least-privilege `permissions:`.
   - Branch protection on `main`: PR required, required status checks, no force-push or deletion, conversations resolved.
   - **No local-only names:** the local folder name, local file paths, personal names and third-party product names never appear in committed files; the project is "Jot" / `notes-app`, the owner `@abalas4`.
   - Test data is synthetic (no personal data), and screenshots and logs in the repo contain no tokens or emails.
   - **No open-source licence (Q6):** all rights reserved. No `LICENSE` file; README states "Copyright © 2026 <owner>. All rights reserved. Source visible for reference only." (GitHub's terms still let people view and fork on GitHub.) Add `.github/SECURITY.md` (GitHub reads it there; a root `SECURITY.md` is not allowed by the structure standard §9).

---

## 3. Frontend: evaluation of the rnlab_aws stack

### 3.1 What rnlab_aws uses

| Item | rnlab_aws | Outcome |
|---|---|---|
| Framework | React Native **0.85.3** bare CLI (no Expo), React 19.2.3, TypeScript 5.8, New Architecture | ✅ works end to end, including Device Farm |
| Unit tests | Jest 29 + react-test-renderer | ✅ |
| E2E (Android) | Appium + WebdriverIO (Node), Appium Python, Espresso | ✅ all three pass on Device Farm (us-west-2) |
| Skipped | Detox (no Device Farm test type; conflicts with app re-signing), Maestro (no Device Farm test type) | — |
| Build | Docker toolchain image (Node 22, JDK 17, Android SDK) | ✅ |
| Device Farm scripts | `aws/` run.sh, preflight, rehearse, cleanup, redact, scan-logs, package allowlist | ✅ reusable almost unchanged |

### 3.2 Verdict: **reuse React Native (bare CLI, TypeScript)**

| Criterion | React Native (recommended) | Flutter | Native Kotlin + Swift |
|---|---|---|---|
| Code shared with iOS | ~90–95 % (UI, state, sync, API client; only notification and auth config differ by platform) | ~90–95 % | ~0 % (two apps) |
| Proven on Device Farm with your tooling | **Yes** (rnlab_aws) | No — new learning curve | Espresso only |
| Appium tests shared with iOS | Yes — same `testID`s map to accessibility ids (UiAutomator2 / XCUITest) | Needs the Flutter driver | Separate |
| Plugin support | `mobile-01-apps.md` names React Native; cross-platform layout = one component `mobile/<app>` | Named too | Named |
| E2E test language | **Python** (Appium Python Client + pytest), the same language as the API tests | Dart | Kotlin / Swift |
| Cost | Free | Free | Free |

**Why not Expo (managed):** Espresso needs a checked-in `android/app/src/androidTest` project.
Bare CLI keeps that working exactly as in rnlab_aws. Expo prebuild would regenerate native folders
and break that setup.

### 3.3 iPhone readiness: build it in from day one
- One component `07-source-code-tests/src/mobile/jot/` containing `android/` and `ios/` folders (the plugin's cross-platform layout).
- Choose only libraries that support **both** platforms (all libraries in §5.2 do).
- Use the same `testID` on every element, so the Appium Python tests run on iOS with only a capability change (XCUITest driver).
- **Espresso is Android-only.** Keep Espresso for a small, fast Android smoke suite. Put the
  cross-platform E2E suite in **Appium + Python (Appium Python Client + pytest)** (user decision D-02). Drop WebdriverIO here, so we
  don't maintain the same suite twice.
- iOS needs: an Apple Developer Program membership (US$99/yr; Device Farm needs a signed `.ipa`) and a
  macOS build. You have no Mac, so the build runs on GitHub Actions macOS runners. The repo is public (Q5), so standard
  GitHub-hosted runners, macOS included, are free with no minute limit.
  This is the plan already drafted in rnlab_aws `AWS-DEVICE-FARM-PLAN.md` §15.
- The plugin requires one Story per platform for each behaviour. iOS Stories will be raised as
  counterparts (`[iOS]`) in a later PI. The code is shared, but each platform has its own ACs and tests.

### 3.4 Can React Native build the mockups? — **Yes, all 12 (two with caveats)**

Checked against `wireframe.html` (W1–W12) and the hi-fi screens in `jot-canvas/project/`.
The designs use only flex and grid layouts, rounded corners, soft shadows, one inset ring, one dashed
ring and font weights 300–800. They use **no** gradients, blur, animation, images or custom drawing.
React Native ≥ 0.76 supports CSS-like `boxShadow` (including inset) and `borderStyle: 'dashed'` on both platforms.

| Wireframe | RN implementation (Android and iOS) | Feasible |
|---|---|---|
| W1 Home — search pill, label chips, sort row, Pinned/Others **two-column masonry**, FAB, floating bottom nav | FlashList v2 `masonry`; horizontal ScrollView chips; custom tab bar on React Navigation bottom tabs; `boxShadow` elevation | ✅ |
| W2 Sort and view sheet | @gorhom/bottom-sheet; radio and switch rows; grid ↔ list toggles the FlashList `numColumns` | ✅ |
| W3 Long-press multi-select + bulk action sheet | `Pressable onLongPress`, selection mode in Zustand, contextual top bar, 2 px ink ring for selected | ✅ |
| W4 Text note editor — top bar (pin, reminder, archive), bottom toolbar (**Aa** format, colour, label, more) | TextInput for title and body, colour tray sheet, label sheet | ✅ ⚠️ **Rich-text "Aa" formatting** is not built into RN's TextInput. Options: `react-native-enriched` (native, new architecture), `10tap-editor` (TipTap in a WebView), or plain text in the MVP with formatting later → **D-09: plain text in MVP, rich text later (L-02)** |
| W5 List editor — drag handles, add item, Done group | react-native-draggable-flatlist (Reanimated + Gesture Handler); collapsible section | ✅ |
| W6 Label picker — search/create inline, multi-tick, counts | Bottom sheet + TextInput filter + checkbox rows | ✅ |
| W7 Navigation drawer — labels with counts, archive, trash, settings | React Navigation drawer with custom content | ✅ |
| W8 Manage labels — create, rename inline, delete | FlatList of editable rows + confirm dialog | ✅ |
| W9 Reminder sheet — quick picks, **month calendar** (dashed today ring, filled selected date), time, repeat | Calendar as a custom 7-column grid (or react-native-calendars), dashed border; @react-native-community/datetimepicker for the time; repeat options in a sheet | ✅ |
| W10 List completion — strike-through, dim, move to Completed, progress bar, overflow menu | `textDecorationLine: 'line-through'`, ink-soft colour, layout animation; progress bar as a View; @react-native-menu/menu (native popup menu) | ✅ |
| W11 **Reminder notification** — title, body, label, list progress + next item, Mark done / Snooze / Open | Notifee: title, body, BigText style, teal accent, small icon, up to 3 action buttons; tapping opens the note via a validated deep link | ✅ ⚠️ The **OS draws the notification**, so it follows the system style rather than the exact mockup card. An action button cannot open a menu inside the notification. "Snooze" will either apply a default (e.g. 10 min) or open the app's W12 snooze sheet (decided at UX spec) |
| W12 Reminders tab — Upcoming/Done chips, Overdue/Today groups, row menu with snooze presets, edit, mark done, remove | SectionList + bottom-sheet menu; snooze reschedules the Notifee trigger and syncs to the API | ✅ |

Design-system items: tokens from `design.md` are copied verbatim into `theme/tokens.ts`. We bundle
static font files for Bricolage Grotesque (600/700/800) and Figtree (300–800), because static files
render more consistently on Android than variable fonts. Touch targets are ≥ 44 pt / 48 dp (`hitSlop`).
The snackbar and FAB are custom components. A one-screen spike (W1 Home + W5 List) in Phase 2,
slice 2 confirms masonry and drag performance on a low-end device.

---

## 4. Backend recommendation

**Language choice:** you said the stack can change if I recommend a different language. I still
recommend **Python**, for three reasons: (a) you are familiar with it; (b) it is the plugin's only
full stack profile, so every gate is automated; (c) Python Lambdas are always-free and cold-start acceptably.
Node/TypeScript would let the app and the API share one language. The plugin has no profile for it,
and you know Python better, so the extra effort isn't worth it.

### 4.1 Recommended: **Python 3.13 + FastAPI on AWS Lambda (container image) + DynamoDB**

| Decision | Choice | Why |
|---|---|---|
| Language / framework | **Python 3.13, FastAPI, Pydantic v2** | It is the only stack with a plugin profile (`lang-python-fastapi`): verifier gates V1–V12, test runner commands, review patterns and the Docker/Postman templates all work out of the box. With any other language, those gates become manual "PARENT" evidence. |
| Compute | **AWS Lambda (arm64)**, container image, with **AWS Lambda Web Adapter** | Always free: 1M requests + 400k GB-s per month. Arm64 costs ~20 % less. Lambda Web Adapter runs the unchanged uvicorn app, so **the same Docker image** runs locally in Compose, in the plugin's Docker test gates, and in Lambda ("build once, promote by digest"). |
| API front door | **API Gateway HTTP API** + Cognito **JWT authorizer** | Throttling (OWASP API4) and auth before the code runs. Costs $1.00 per million requests after the free tier, so effectively $0 at personal volume. *Fallback:* Lambda Function URL ($0) with in-app JWT validation. |
| Database | **DynamoDB on-demand**, single-table design | Always free: 25 GB storage. No idle cost, no VPC/NAT. RDS/Aurora have idle hourly cost; Aurora DSQL is Postgres-like but limited (no FKs, limited Alembic support). |
| Local DB for tests | **DynamoDB Local** container (`amazon/dynamodb-local`) | Integration tests run in Docker as the plugin requires, with no AWS account needed. |
| Auth | **Amazon Cognito user pool** (Lite tier), managed login, OAuth2 **Authorization Code + PKCE** | Always free up to 10,000 MAU. Meets mobile rule MA-04 (system browser login, no embedded webview). |
| Reminders delivery | **Local notifications on the device** (Notifee), scheduled from synced reminder data | $0. Works offline and on both platforms. Server push (FCM/APNs + EventBridge Scheduler, both free-tier) is deferred to multi-device sync (backlog). |
| Config / secrets | **SSM Parameter Store (standard)** | Free. Secrets Manager costs $0.40 per secret per month. |
| Observability | structlog JSON → **CloudWatch Logs**; OpenTelemetry → **AWS X-Ray**; CloudWatch alarms | Always free: 5 GB logs, 10 metrics, 10 alarms, 100k traces per month. Log retention set to 14 days to keep storage at $0. |
| IaC | **OpenTofu** (D-08; MPL-2.0 open-source fork of Terraform, same HCL and `hashicorp/aws` provider) | State in a private, versioned S3 bucket with S3-native locking (`use_lockfile`) and OpenTofu client-side **state encryption** (secrets such as the Google client secret can land in state). Cost ≈ $0. Bucket created once by a small `infra/envs/bootstrap` config. `tofu fmt`/`validate`/`plan` in CI; plan reviewed on the PR; scanned by checkov + trivy config; reviewed by `review-iac`. |
| Image registry | **Amazon ECR** private repository with a lifecycle policy (keep the last 5 images) | ~150 MB image ≈ $0.02 per month after the free tier. |

**Profile deviation (to record as an ADR at Step 01):** the profile assumes SQLAlchemy + Alembic
(relational). DynamoDB replaces them with a repository layer on `boto3`. Schema changes become
versioned item attributes plus OpenTofu table definitions, so the "Migration" test type becomes
item-schema-version tests. Everything else in the profile applies unchanged.

### 4.2 Authentication and authorization

**Phase A — MVP: Google sign-in through Cognito (user decision 2026-10-08)**

```
App ──(Auth Code + PKCE, system browser, identity_provider=Google)──▶ Cognito managed login
     ◀── redirects to Google ──▶ user signs in with Google account ──▶ Cognito /oauth2/idpresponse
     ◀── code ── app exchanges code + PKCE verifier ──▶ Cognito tokens (access / ID / refresh)
App ── Bearer <Cognito access JWT> ──▶ API Gateway JWT authorizer ──▶ Lambda (FastAPI) ──▶ DynamoDB
```
- **Google side (free):** a Google Cloud project, an OAuth consent screen (External; scopes `openid email profile`
  only, which are non-sensitive, so Google needs no app verification) and an OAuth client of type
  **Web application**. The client is Cognito, not the phone app. Its redirect URI is
  `https://<prefix>.auth.us-west-2.amazoncognito.com/oauth2/idpresponse`. The Google client secret is
  stored only in Cognito (read by OpenTofu from an SSM SecureString parameter; state is encrypted), never in the app or the repo.
- **Cognito side:** user pool (Lite tier, which includes social sign-in in the 10,000 MAU always-free allowance),
  Google as an identity provider, attribute mapping (email, email_verified, name), a free Cognito
  domain prefix, and an app client (public, no secret, PKCE, callback `com.jot.app://auth/callback`).
  The app passes `identity_provider=Google`, so the user goes straight to Google's page.
- **The app and the API do not know Google exists.** They only see Cognito tokens. This is what makes
  Phase B a configuration change.
- **Native sign-up is disabled in prod for Phase A.** The only way in is Google.

**Phase B — backlog (user decision 2026-10-08): Cognito native accounts (email + password, MFA)**
- Enable native sign-in on the same user pool and add it to managed login. The app and the API stay unchanged.
- **Identity design decided now so Phase B loses no data:** a Google-federated user and a later
  native user are different Cognito users with **different `sub` values**. So the API **does not key
  data by `sub`**. On first sign-in it creates an internal `userId` (ULID) and an identity map item
  `IDENTITY#<sub> → userId`. All notes are keyed `USER#<userId>`. In Phase B, a pre-sign-up Lambda
  trigger links an existing Google user and a new native user that share a verified email
  (`AdminLinkProviderForUser`). Both identities then resolve to the same `userId`. The `sub → userId`
  lookup is cached in Lambda memory, so it adds ~1 DynamoDB read per cold container.

**Authorization (both phases):** the user id comes only from the verified token, never from the request.
Every DynamoDB key is scoped to `USER#<userId>`, which blocks OWASP API1 (BOLA). Another user's note
returns 404. The MVP has a single "owner" role. Tokens live in Keystore/Keychain. Logout revokes the
refresh token, wipes the local DB and cancels scheduled reminder notifications.

**Testing without Google (important):** Google blocks automated sign-ins (bot detection, CAPTCHA,
2-step verification), so Appium and Espresso **must not** drive the Google login page. Instead:
- `local` (Docker): the dev token script signs JWTs with a local key, and the API trusts that key only when `ENV=local`.
- `dev`/test pool (emulator and Device Farm): native sign-in is **enabled only in the dev pool** for
  admin-created test users (no self sign-up). E2E tests sign in as those users. The password is kept in
  SSM or GitHub secrets and passed to test runs, never committed.
- Manual check of the Google flow on the emulator (Google APIs image with Chrome) and once on Device Farm with a throwaway Google account.
- `prod`: Google only.

### 4.3 Alternatives considered (not recommended)

| Option | Rejected because |
|---|---|
| Node/TypeScript (Express/NestJS) on Lambda | One language with the app, but no plugin profile, so gates V1–V12 would all be manual |
| RDS PostgreSQL / Aurora Serverless v2 | Idle hourly cost; RDS free tier is 12 months (or credits) only; needs a VPC |
| ECS Fargate / App Runner / EC2 | Billed while idle |
| AWS Amplify / AppSync GraphQL | Weaker fit with the plugin (REST, OpenAPI, Postman/Newman gates); more lock-in |
| Firebase / Supabase | Not hosted in AWS (your requirement) |

---

## 5. Full technology list

### 5.1 Backend API — `07-source-code-tests/src/apis/jot-api/`

| Layer | Technology | Cost |
|---|---|---|
| Runtime | Python 3.13 (Lambda-supported until 2029), uvicorn | Free |
| Framework | FastAPI, Pydantic v2, pydantic-settings | Free |
| Data access | boto3 (DynamoDB), repository + service pattern | Free |
| Auth | Cognito JWT via API Gateway authorizer; PyJWT/JWKS check in the app as defence in depth; dev token script for local runs | Free |
| Quality | mypy --strict, ruff, uv (lockfile), pip-audit, gitleaks | Free |
| Tests | pytest + pytest-cov (≥ 80 %), moto for unit fakes, DynamoDB Local for integration, Schemathesis (contract vs OpenAPI 3.1), Newman (Postman), mutmut, k6 (performance), OWASP ZAP (DAST) | Free |
| Observability | structlog, OpenTelemetry SDK → X-Ray, correlation ID middleware, `/health` + `/ready` | Free tier |
| Container | Multi-stage Dockerfile, non-root, Lambda Web Adapter; hadolint, Trivy, Syft SBOM | Free |
| Hosting | Lambda arm64 + API Gateway HTTP API + DynamoDB + Cognito + SSM + CloudWatch + X-Ray + ECR, region **us-west-2** (same as Device Farm) | ~$0 (see §7) |

### 5.2 Mobile app — `07-source-code-tests/src/mobile/jot/` (Android now, iOS-ready)

| Concern | Library (all support Android + iOS) | Licence |
|---|---|---|
| Framework | React Native (bare CLI, New Architecture), React 19, TypeScript — **latest stable that has cleared the 7-day cooling period**; baseline is rnlab_aws RN 0.85.x | MIT |
| Navigation | React Navigation 7 (native stack, bottom tabs, drawer) | MIT |
| Server state | TanStack Query v5 (online-only MVP, D-07; outbox sync deferred → L-01) | MIT |
| UI state | Zustand | MIT |
| Local storage | react-native-keychain for tokens. op-sqlite with SQLCipher (MA-05) is **deferred with offline-first (L-01)** — MVP keeps no notes at rest on the device (to be confirmed in the HLD) | MIT |
| API client | openapi-typescript + openapi-fetch, generated from the API's OpenAPI spec (MA-03) | MIT |
| Auth | react-native-app-auth (Cognito, PKCE, system browser) | MIT |
| Notifications | Notifee (trigger notifications, action buttons Mark done / Snooze / Open) — ⚠️ **provisional, pending dependency vetting (R-NOTIF)**; fallback `expo-notifications` or a small native AlarmManager module | Apache-2.0 |
| Lists | FlashList v2 (masonry), react-native-draggable-flatlist (reorder), Reanimated + Gesture Handler | MIT |
| Sheets, menus, pickers | @gorhom/bottom-sheet, @react-native-menu/menu, @react-native-community/datetimepicker | MIT |
| Rich text | **Not in MVP (D-09)** → L-02: react-native-enriched, or 10tap-editor | MIT |
| Design | Tokens from `design.md` → `src/theme/tokens.ts`; fonts Bricolage Grotesque + Figtree (OFL, bundled); icons react-native-svg + lucide-react-native | MIT / OFL / ISC |
| Crash reporting | Firebase Crashlytics via @react-native-firebase (free, no personal data, MA-15) | Apache-2.0 |
| Quality | ESLint, Prettier, `tsc --noEmit`, npm audit, MobSF (static scan in Docker, V45) | Free |

### 5.3 Mobile testing

| Test type | Tool | Where it runs | Cost |
|---|---|---|---|
| Unit / component | Jest + React Native Testing Library | Docker (rnlab toolchain image) | Free |
| Accessibility | RNTL a11y queries + Android Accessibility Test Framework (via Espresso) | Docker / emulator | Free |
| Contract (consumer) | Generated typed client + Schemathesis against the API spec (Pact only if needed later) | Docker | Free |
| UI / E2E — Android smoke | **Espresso** (fastest; fewest device minutes) | **Android emulator** during development; Device Farm in the hardening phase | Free / Device Farm minutes |
| UI / E2E — cross-platform | **Appium 2 + Appium Python Client + pytest**, UiAutomator2 now, XCUITest later. Locator helper `by_test_id()` uses `AppiumBy.ID` (Android resource-id) or `AppiumBy.ACCESSIBILITY_ID` (iOS accessibilityIdentifier), depending on the platform; `accessibilityLabel` stays human-readable for TalkBack/VoiceOver (MA-14). Linted with ruff + mypy like the API code | **Android emulator** during development; Device Farm in the hardening phase | Free / Device Farm minutes |
| Notification flows | Appium (`openNotifications`), because Espresso cannot reach the notification shade | Emulator first, then Device Farm (real OEM notification and battery behaviour) | — |
| Device matrix | AWS Device Farm, pinned pool of 2 Android devices (e.g. Android 14 + 15/16) | us-west-2, **after the emulator suite is green** | see §7 |

**Emulator-first approach (user decision 2026-10-08).** All UI, E2E, accessibility and notification
tests are developed and run on an Android emulator, at no cost. Device Farm comes later, only to
confirm that the emulator-green suite also passes on real devices.

| Emulator setup | Choice |
|---|---|
| Where it runs | Android Studio AVD on Windows (hardware acceleration via WHPX/Hyper-V). Appium and the tests run in WSL/Docker and reach the emulator over the rnlab_aws adb bridge (`scripts/adb-connect.sh`) |
| API it talks to | The **local Docker API** (`local` env, §5.4) at `10.0.2.2`, not reachable from the internet. No AWS API is deployed for emulator testing |
| System images | **Google APIs** x86_64 images (they include Chrome, which the Cognito login in Custom Tabs needs) |
| AVD matrix (MOB-01 tiers, C-06) | (1) **oldest supported OS** (min SDK set by the NFR at Step 01, e.g. API 29), small phone 720×1280; (2) **latest OS** (API 36), large phone 1080×2400; (3) **low-end Android** profile (2 GB RAM, 2 cores) for MOB-08 performance. Tablet: N/A (not supported in MVP) |
| Reminders on the emulator | Tests schedule reminders a minute ahead, or use a debug-only test hook to fire a trigger now. Exact-alarm permission is granted and revoked with `adb shell appops` to test the denied path |
| Offline tests | `adb shell svc wifi/data disable` or emulator network toggles |
| Optional CI | Nightly emulator run on GitHub Actions Linux (KVM) with `reactivecircus/android-emulator-runner`, if minutes allow. Not on every PR |
| iOS later | The iOS **Simulator** needs macOS, so it runs on a GitHub Actions macOS runner (10× minutes) when iOS starts |

What the emulator **cannot** prove, so Device Farm checks it later: OEM battery optimisation that
delays or kills alarms (Samsung, Xiaomi), real notification shade variations, real-world performance
(start-up time, frame rate on a low-end device), and behaviour after a real reboot. These stay as
DFMEA detection items until the Device Farm phase.

### 5.4 Delivery

| Concern | Choice | Cost |
|---|---|---|
| Source control | **Public** GitHub repo (Q5), trunk-based, branch protection + required checks on `main` (C-07). Public-repo hygiene in §2 rule 7 | Free |
| CI | GitHub Actions (standard runners free and unmetered on public repos): API gates, app unit tests, Android release build, SAST (Semgrep), IaC scan (checkov), secrets (gitleaks), licence check | Free |
| CD | GitHub OIDC → least-privilege IAM deploy role (no long-lived keys) → build + push image to ECR → `tofu plan` (artifact on the PR) → `tofu apply` of the reviewed plan | Free |
| Android distribution | **No Play Store** (C-05 deviation). During slices the CI debug APK (bundled JS) is installed; for release hardening the CI-signed release APK (Q12) is installed on your phone with `adb install`, uploaded to Device Farm, and attached to the GitHub Release for each REL tag | Free |
| Environments | See the environment table below | ~$0 |

**Environments (user decision 2026-10-08: no public API until it is needed)**

| Env | API | Database | Login | Reachable from internet? | When it exists |
|---|---|---|---|---|---|
| `local` | Docker Compose on the laptop | DynamoDB Local | Dev **Cognito pool** (Google + admin-created native test users), or the dev token script for API-only tests | **No.** The emulator reaches the API at `http://10.0.2.2:<port>` (cleartext allowed **only** in the debug build's network security config) | Always, during slices 1–6 |
| `cognito-dev` | — | — | Cognito user pool only (managed login; no API) | Cognito's hosted login only; there is no API of ours | Always (free, no idle cost) |
| `dev` | Lambda + HTTP API (OpenTofu `envs/dev`) | DynamoDB (dev table) | `cognito-dev` pool | Yes, with token auth | **Only during test windows** (Story UAT on your phone, Device Farm): `tofu apply` before, `tofu destroy` after (state bucket and ECR repo stay). Table data is disposable |
| `prod` | Lambda + HTTP API (OpenTofu `envs/prod`, `prevent_destroy` on the table) | DynamoDB (point-in-time recovery on) | Prod pool: Google only | Yes, with token auth | From REL-1.0.0 go-live |

The release build always points at the HTTPS `dev`/`prod` URL; only the debug build can call `10.0.2.2`.
The API base URL is chosen per build variant, never hard-coded in screens.

**Public endpoint protection (`dev` and `prod`):** JWT authorizer on every route except a minimal
`/health`, user-scoped data, throttling + Lambda concurrency cap, TLS only, no secrets in the app.
Backlog: Play Integrity / Firebase App Check (prove the caller is the genuine app) and AWS WAF (~$5+/month).
A private API is not possible for phones without a VPN (AWS Client VPN ≈ $72+/month), so it is rejected.

---

## 6. Architecture (overview; the HLD at Step 01 is authoritative)

```
 Android app (React Native)                               AWS us-west-2
 ┌──────────────────────────┐   HTTPS + JWT    ┌───────────────────────────┐
 │ UI (Jot tokens) ─ Zustand │ ───────────────▶ │ API Gateway HTTP API      │
 │ TanStack Query (online)   │                  │  └ Cognito JWT authorizer │
 │ keychain (tokens)         │                  └────────────┬──────────────┘
 │ Notifee local reminders   │                               ▼
 │ app-auth (PKCE) ──────────┼──▶ Cognito managed login   Lambda arm64 (container:
 └──────────────────────────┘                             FastAPI + Web Adapter)
                                                               │
                                     DynamoDB (single table) ◀─┘─▶ CloudWatch / X-Ray
```
MVP is online-only (D-07). To keep offline-first (L-01) a non-breaking addition later, each entity
still carries `version` and `updatedAt`, writes use optimistic concurrency (`If-Match`/version), and
deletes are soft (tombstones). The later sync model: the client pushes an outbox and pulls
`changes?since=<cursor>`, last-writer-wins per field group (confirmed in the LLD at that time).

---

## 7. Cost estimate (personal / test usage)

| Item | Monthly | Notes |
|---|---|---|
| Slices 1–6 (local Docker API + `cognito-dev` pool only) | **$0** | Nothing of ours is publicly reachable |
| Lambda, Cognito (≤10k MAU), CloudWatch basics, X-Ray, SSM standard | **$0** | Always-free tiers |
| DynamoDB | $0 – ~$0.05 | 25 GB storage always free. **Correction (2026-10-08):** the always-free 25 RCU/WCU applies only to *provisioned* mode; on-demand requests are billed (cents at personal volume). Choose on-demand vs small provisioned (free) in the LLD |
| API Gateway HTTP API | $0 – $0.10 | 1M/month free only in an account's first 12 months; afterwards $1/M. Treat as paid (Q1) |
| ECR | ~$0.02 | 500 MB free only in the first 12 months; lifecycle policy keeps 5 images |
| GitHub Actions | $0 | Public repo: standard runners unmetered. Don't use larger (paid) runners. Cache Gradle/npm for speed |
| **AWS Device Farm** | **$0 until the one-time 1,000 free minutes are used, then $0.17/device-minute** | **The main cost risk.** Rules carried over from rnlab_aws: preflight first, Espresso first, 10-min job timeout, stop at first failure, never `--allow-paid` without asking. Budget: ~2 devices × ~10 min per release ≈ 20 min per release. |
| Apple Developer (only when iOS starts) | US$99/yr | Not needed for MVP |

**Note:** AWS accounts created after 15 Jul 2025 use the credit-based Free plan (6 months)
instead of the 12-month free tier. Always-free offers apply either way. We confirm the exact
figures against AWS pricing pages at Step 01 (NFR: Cost) and add an **AWS Budgets** alert.
The first two budgets are free.

---

## 8. Testing and quality strategy (summary)

- **API:** unit + integration (DynamoDB Local) in Docker with ≥ 80 % coverage and HTML reports;
  Schemathesis contract tests; Newman with the `safe-alm-test-newman-fixer` loop until 0 failures;
  k6 smoke performance (p95 < 300 ms warm); ZAP baseline; mutmut.
- **App:** Jest unit tests ≥ 80 % on new code; Espresso smoke; Appium Python E2E covering every UX Spec
  state (W1–W12, offline, permission denied, notification actions); accessibility (TalkBack labels, 48 dp targets).
- **Story Done (Step 04, C-05 deviation)** needs all three, in this order:
  1. **Emulator matrix:** automated suites green (§5.3, MOB-01…MOB-09). Free, and run as often as needed.
  2. **Personal phone:** with the CI-built APK for the commit (debug build during slices; the signed APK in release hardening, Q12) and the `dev` stack (deployed for the window):
     a. the **same automated Espresso + Appium suites** run on your phone over adb (wireless pairing or USB,
        reusing rnlab_aws `scripts/adb-pair-connect.sh` and the Docker test runner). Free. **Wireless adb to your
        phone is already proven in rnlab_aws** (user, 2026-10-08), so wireless is the default and USB the fallback.
     b. your **manual UAT**, recorded as `UAT-<Story ID>` (device model, Android version, build).
  3. **Device Farm (last step):** the same suites pass on the pinned real-device pool.
  **One test suite, three targets:** the tests are written once. Only the target changes (emulator AVD, your
  phone's adb serial, Device Farm pool), set through the runner configuration, never in the test code.
  **Hard gate (user, 2026-10-08):** a Device Farm run is never started unless the same build has passed the
  emulator matrix **and** the automated suites + UAT on your phone. A failure at the emulator or phone stage is fixed there first, so no
  device minutes are spent on a known-bad build. The rnlab_aws `preflight.sh` check also runs before every upload.
  To save device minutes and deploy windows, steps 2 and 3 run **once per slice**, covering all of that slice's
  Stories. Stories wait in testing until their slice passes. A failure is logged as a defect and fixed through the
  normal flow; only the failing suite is re-run.
- **Device Farm minute budget:** ~2 devices × ~10 min × 6 slices ≈ 120 min, plus re-runs and a final
  REL-1.0.0 regression run ≈ 200 min in total. That is within the one-time 1,000 free minutes, if enough remain (Q2).
- **Gates:** the plugin's verifier gates V1–V47 (mobile V44–V45), parallel code review agents, and release go / no-go.

### 8.1 Test-execution tooling (user requirement R-TX, 2026-10-08)
Delivered as an Enabler Feature at Step 01 ("CI/CD and test-execution workflows"). All workflows call the
same `scripts/…` you can run locally, so a suite behaves the same on your laptop and in CI.

| ID | What | How it is started | Contents |
|---|---|---|---|
| R-TX-01 | **Emulator tests** workflow | **Run workflow** button / `gh workflow run emulator-tests.yml`; also runs automatically on every PR | Build APK + test APK → Android emulator on a GitHub Linux runner (KVM) → local Docker API in the job → Espresso + Appium Python → HTML/JUnit reports as artifacts. Inputs: suite, API level |
| R-TX-02 | **Device Farm** workflow | Manual only (Run workflow / `gh`) | Inputs: commit SHA (build), suite (espresso / appium-python / all), device pool. Uses the CI-built APK for that SHA. rnlab_aws guard rails: preflight, free-minutes check, `allow_paid` = false by default, 10-min job timeout, stop on first failure, cleanup always. **Enforces the §8 hard gate:** refuses to run unless that SHA has a green emulator run **and** a green phone run (commit status `jot/phone-tests`) |
| R-TX-03 | **dev AWS stack** workflows | Manual: `dev-up` (`tofu apply`) and `dev-down` (`tofu destroy`) | Builds/pushes the API image, applies `envs/dev`, prints the API base URL to the job summary (masked IDs). `dev-down` keeps the state bucket and ECR repo |
| R-TX-04 | **Phone script** (local, one command) | `scripts/phone-test.sh` on your PC | Checks adb (wireless pairing, USB fallback) → checks the `dev` stack is up → **builds** the APK + test APK (`--from-ci <sha>` instead downloads the CI-signed APK, used for Story Done so the phone and Device Farm test the identical binary) → installs → runs Espresso + Appium Python against the phone → HTML report → on success sets commit status `jot/phone-tests` on the SHA → prompts for the manual UAT record. Options: `--suite`, `--device <serial>`, `--skip-build` |

Rules:
- Manual workflows run in a protected GitHub **Environment** (`dev` / `device-farm`) that only `@abalas4` can approve; AWS access via OIDC scoped to those environments. No self-hosted runner (public repo).
- The phone cannot be reached from GitHub-hosted runners, so R-TX-04 is local by design.
- Slice 1 delivers R-TX-01, R-TX-03 and R-TX-04; R-TX-02 is delivered before the first Device Farm window (by slice 2).

### 8.2 AWS prerequisites as code, with fine-grained access (user requirement R-AWS, 2026-10-08)
Every AWS prerequisite of the API is created and changed by OpenTofu through a **manual GitHub Actions
workflow** (`aws-prereqs`), never by hand in the console. Part of the same Enabler Feature as §8.1.

**R-AWS-01 · What the `aws-prereqs` workflow manages** (`infra/envs/shared` — the account-level root, manual Run workflow, `aws-admin` Environment with your approval, `tofu plan` shown in the job summary before `apply`):
GitHub OIDC identity provider; the per-workflow IAM roles and policies below; the permissions boundary;
OpenTofu state bucket (versioned, encrypted, public access blocked); ECR repository + lifecycle policy;
SSM parameter path `/jot/*` (the Google client secret value is entered by you, see R-AWS-04);
Device Farm project + device pools; AWS Budgets alerts (≤ 2, free); CloudWatch log-retention defaults.

**R-AWS-02 · One-time bootstrap (the only manual AWS step).** GitHub cannot reach AWS until an OIDC
provider and a role exist, so you run `infra/envs/bootstrap` **once, locally, with your own credentials** (§2 rule 5).
It creates only: the state bucket, the OIDC provider and the `jot-gh-prereqs` role. Its state is then moved
into the S3 bucket and from that point the `aws-prereqs` workflow owns everything, including those three.

**R-AWS-03 · Fine-grained roles — one per workflow and environment** (no shared "deploy" role, no `*:*`, no long-lived keys):

| Role | Assumable only by (OIDC `sub` + `job_workflow_ref`) | May do |
|---|---|---|
| `jot-gh-prereqs` | `aws-prereqs.yml`, Environment `aws-admin` | Manage the R-AWS-01 resources only. IAM limited to `jot-*` roles/policies, **every role it creates must carry the `jot-boundary` permissions boundary**, and it cannot change its own role or the boundary (blocks privilege escalation) |
| `jot-gh-plan` | PR workflows from this repo's branches (not forks) | Read-only: `tofu plan` (describe/list/get on `jot-*` resources, read state). No writes |
| `jot-gh-deploy-dev` | `dev-up.yml` / `dev-down.yml`, Environment `dev` | Create/destroy only `jot-dev-*` Lambda, HTTP API, DynamoDB table, Cognito dev pool, log groups; push to the `jot-api` ECR repo; read `/jot/dev/*` SSM; state key `dev/*` only; `iam:PassRole` only for `jot-dev-lambda-exec` |
| `jot-gh-deploy-prod` | `deploy-prod.yml` on `main`, Environment `prod` (your approval) | As dev, for `jot-prod-*`; **no delete** on the table (also `prevent_destroy`) |
| `jot-gh-devicefarm` | `device-farm.yml`, Environment `device-farm` | Device Farm actions on the `jot` project ARN only, plus `GetAccountSettings` (free-minutes guard) |
| `jot-dev-lambda-exec` / `jot-prod-lambda-exec` | Lambda service | Runtime: CRUD on its own table only, write its own log group, X-Ray put |

Emulator tests need no AWS role (local Docker API).

**R-AWS-04 · Rules**
- Trust policies pin `aud = sts.amazonaws.com`, the repo `abalas4/notes-app`, the Environment, and the workflow file (custom OIDC `sub` claim including `job_workflow_ref`). Session duration ≤ 1 h.
- Resources are named `jot-<env>-*` and tagged per IAC-11: `owner=abalas4`, `service=<jot-api|…>`, `environment=<env>`, `data-class=<class>`; policies use those names/tags as conditions.
- **Drift detection (IAC-14):** a scheduled weekly `drift-check` workflow runs `tofu plan` for `shared`, `dev` (when up) and `prod` with the read-only `jot-gh-plan` role; any drift opens a GitHub issue.
- Policies are validated in CI with IAM Access Analyzer (`validate-policy`, plus "no new public / cross-account access" checks) and checkov; a finding fails the PR.
- Secret **values** (Google client secret) never pass through the repo or workflow logs: you put them into SSM once with your own credentials (`aws ssm put-parameter --type SecureString`); OpenTofu only references the parameter name.
- Not automatable (outside AWS): creating the Google OAuth client in Google Cloud Console, GitHub repo settings that need your account (Environments' required reviewers, branch protection, secret scanning) — documented as a checklist in the README.

---

## 9. Repository structure (plugin `project-structure-standard.md`)

```
notes-app/                               (public GitHub repo root)
├── README.md  CHANGELOG.md  CODEOWNERS  .gitignore  .gitattributes  .editorconfig  .pre-commit-config.yaml
├── .github/                             workflows/ (CI, emulator-tests, device-farm, dev-up/down, aws-prereqs, deploy-prod, drift-check), SECURITY.md
├── 00-planning/                         raid-log.md, PI-1/ (capacity, objectives, ROAM, dependency board, iteration plans, system demos); this plan until Step 01 (C-01)
├── 01-strategy/  02-epics/  03-features/  04-stories/  05-work-items/
├── 06-design/                           HLD, DFMEA, LLD, adr/, api-specs/jot-api.openapi.yaml
│   └── ux/                              style-guide.md, <Feature ID>/ux-spec.md + <screen>-<state>.png snapshots (raw sources stay outside the repo, C-02)
├── 07-source-code-tests/
│   ├── docker-compose.yml  docker-compose.test.yml   (API + DynamoDB Local)
│   ├── infra/                           OpenTofu: modules/<module>/, envs/{bootstrap,shared,dev,prod}/ — one root per environment (iac-01 §1, C-04, §8.2)
│   ├── src/apis/jot-api/                FastAPI service, Dockerfile (+ Dockerfile.dockerignore)
│   ├── src/mobile/jot/                  React Native app (android/ now, ios/ later)
│   ├── tests/apis/jot-api/              unit/ integration/ contract/ e2e/ security/ load/ mutation/ resilience/ migration/ privacy/ (those that apply)
│   └── tests/mobile/jot/                unit/ ui/ e2e/ accessibility/ device/
├── 08-test-artefacts/                   test plans, results, defects, closure reports
├── 09-documentation/                    user guide, API consumer docs
├── 10-release/                          roadmap, REL-x.y.z packs
├── 11-operations/                       SLOs, alarms, runbooks
├── postman/                             JotApi.postman_collection.json, JotApi-Local-Dev.postman_environment.json (§9 naming)
└── scripts/                             generate-dev-token, run.sh/run.bat, phone-test.sh, Device Farm helpers (adapted from rnlab_aws). Test code itself lives only in tests/, never in scripts/
```
Git ignores: `.claude/` (local Claude tooling, C-01), `htmlcov/`, `reports/`, `.alm-runs/`,
`node_modules`, build outputs, `.env*`, `*.keystore`, `aws/.aws-creds.env`,
`google-services.json` (it holds only public values, but we keep it out of the repo by choice), and coverage HTML.
### 9a. Local workspace (user, 2026-10-08)
The git repo is the folder `notes-app/`, so **all git content stays inside it**. The surrounding local folder is a
workspace that is never committed:
```
<local workspace>/                       (not a git repo; Claude Code is launched here, so session memory keeps working)
├── CLAUDE.md                            local Claude instructions → points to notes-app/00-planning/project-plan.md
├── jot-design-source/                   raw design files (design.md, wireframe.html, jot-canvas/) — input to Step 01, never committed
└── notes-app/                           git repo → github.com/abalas4/notes-app (structure above)
```
All git commands run inside `notes-app/`. Repo paths in this plan are relative to `notes-app/`; the design sources are
at `../jot-design-source/` from the repo.

**Folder rule (user, 2026-10-08):** every file Claude creates — scripts, workflows, IaC, tests, docs, artefacts —
goes to the path the plugin's `project-structure-standard.md` defines (gate V34, review T-07). Nothing at the root outside §9.
If something has no defined home, raise it with the user (ADR) instead of inventing a folder.
Conventions: branches `feat/<STORY-ID>-<slug>`, Conventional Commits `feat(jot-api): … [THM01STR03]`,
PRs < 400 lines, tags `REL-x.y.z`.

---

## 10. SDLC execution plan (step by step, after the stack is approved)

Each step ends at a **human gate**. Claude prepares the evidence, and you approve before the next step starts.

| Phase | Skill / agents | Output | Human gate |
|---|---|---|---|
| 0. Setup (repo hygiene only, no ALM artefacts) | — | `git init`, `.gitignore`, `.gitattributes`, `.editorconfig`, `.pre-commit-config.yaml` (gitleaks), README, `.github/SECURITY.md`, `CODEOWNERS`, workspace `CLAUDE.md` (outside the repo, §9a); move `design_style_guide/` to the workspace folder `jot-design-source/` (outside the repo, §9a); create `notes-app/` and move `00-planning/` into it (C-02); push to the public repo (by you) | Repo created |
| 1. Requirements | `/safe-alm-requirements` (+ story-reviewer, coverage-auditor) | Theme, Epic (Surfaces: Mobile app = Yes, Android, cross-platform), Features, Stories (`[API]`, `[Mobile][Android]`), NFRs, PI plan, RAID | Stories reviewed |
| 1a. Style guide | `/safe-alm-requirements` (`08-ux-design.md` §1) | `06-design/ux/style-guide.md` v1.1 with SG-01…SG-15 (C-03) | **Style guide Approved** |
| 1b. Release plan | `/safe-alm-release` (PI roadmap) | Draft REL-1.0.0 plan; Story release tags | Roadmap agreed |
| 1c. Design | design-doc-gen + design-reviewer (one per Feature, parallel) | UX Spec per Feature (from W1–W12), HLD, DFMEA, LLD, ADRs (stack, DynamoDB, sync, reminders, auth, C-07/C-09 deviations), OpenAPI 3.1 | **UX Spec + LLD Approved** |
| 2. Implementation | `/safe-alm-implementation` per IMPL WI (wi-triage, impl-verifier) | API first (foundation → notes → lists → labels → reminders → sync), then app screens; Docker, Postman, OpenTofu | Verifier PASS, PR open |
| 3. Code review | `/safe-alm-code-review` (up to 11 agents in parallel) | Review report per PR | You comment your approval + merge |
| 4. Testing | `/safe-alm-testing` (test-design-reviewer, test-runner, newman-fixer) | TEST WIs, emulator-matrix results, phone UAT record, Device Farm results, defects, closure report | **You accept UAT** + Device Farm green → Story Done |
| 5. Release | `/safe-alm-release` (release-readiness, traceability-auditor, ops-readiness-auditor) | Release notes, change record, go / no-go evidence | **You record GO** |
| 6. Operations | `/safe-alm-operations` | SLOs, alarms, runbooks, budget alert | On-call owner confirmed |

Order of delivery inside Phase 2–4 (vertical slices, each a Story set through review and test):
1. API foundation + auth + health
2. Notes CRUD (API + Home/Editor)
3. Checklists
4. Labels, search, sort, select
5. Reminders + notifications + snooze
(Offline sync removed from the MVP by D-07 → L-01.)

Each slice: build and test on the emulator against the local Docker API → deploy `dev` (OpenTofu) for the window →
phone UAT + Device Farm run → delete `dev`. The first slice also brings up the state bucket (bootstrap), the OpenTofu `dev` environment and the
Device Farm scripts (adapted from rnlab_aws).
6. REL-1.0.0: full regression on Device Farm, then `prod` deploy of the API; the signed APK is attached to the GitHub Release

**AWS steps you run yourself:** only the one-time `infra/envs/bootstrap` apply (R-AWS-02) and putting secret values into SSM
(R-AWS-04), both with your own credentials. Everything else in AWS is created by the `aws-prereqs` workflow (§8.2).

---

## 11. Decisions for you to confirm

| ID | Decision | Recommendation |
|---|---|---|
| D-01 | Frontend framework | ✅ **React Native bare CLI + TypeScript** (reuse rnlab_aws), iOS-ready — confirmed by user 2026-10-08 |
| D-02 | Mobile E2E frameworks | ✅ **Appium + Python** (Appium Python Client + pytest, reusing rnlab_aws `tests/appium-python` and its Device Farm test spec) as the cross-platform suite + **Espresso** Android smoke; WebdriverIO dropped — confirmed by user 2026-10-08 |
| D-03 | Backend | ✅ confirmed 2026-10-08: **Python 3.13 + FastAPI** in a container on **Lambda arm64** (Lambda Web Adapter), behind **API Gateway HTTP API** (alternative: Lambda Function URL, $0 but no per-route throttling) |
| D-04 | Database | ✅ confirmed 2026-10-08: **DynamoDB** on-demand (ADR for the SQLAlchemy/Alembic profile deviation) |
| D-05 | Auth | ✅ confirmed 2026-10-08: **Cognito** (Lite) + PKCE. **Phase A: Google federation only** (prod); Phase B: Cognito native accounts. Internal `userId` with `sub` mapping from day one; dev pool has native test users for automated tests (§4.2) |
| D-06 | Reminders | ✅ confirmed 2026-10-08: **Local notifications** in MVP, **subject to the library supporting our React Native version** (R-NOTIF); server push later (L-03). Library is **Notifee, provisional** until it passes dependency vetting at the LLD stage (risk R-NOTIF, §12) |
| D-07 | Offline | ✅ confirmed 2026-10-08: **Online-only MVP**; offline-first deferred (L-01) |
| D-08 | IaC / CI | ✅ confirmed 2026-10-08: **OpenTofu** (not Terraform — BUSL licence; not SAM — user knows Terraform/HCL) + **GitHub Actions** with OIDC |
| D-09 | W4 "Aa" text formatting | ✅ confirmed 2026-10-08: **Plain text in MVP**; rich text later (L-02) |
| D-10 | W11 notification "Snooze" action | ✅ confirmed 2026-10-08: **Opens the app's W12 snooze sheet** (matches the wireframe's "Snooze opens quick options") |
| D-11 | PR approval as a solo developer (C-07) | ✅ confirmed 2026-10-08: Your approval comment on the PR after the `/safe-alm-code-review` report, then you merge. Recorded in an ADR, because GitHub does not allow self-approval |

Open questions:
- ~~Q1. Legacy free tier or new Free plan?~~ Answered 2026-10-08: **legacy free tier** (Free Tier page shows only the usage table, no plan/credits panel). No forced account closure. Assume the 12-month offers are used up or expiring, so only always-free applies — costed in §7.
- ~~Q2. Device Farm free minutes used?~~ Answered 2026-10-08: **981.77 of 1,000 remaining** (confirmed live by the user) — enough for the ~200 needed.
- ~~Q3. Project/app name?~~ Answered 2026-10-08: **"Jot"**, package id `com.jot.app`.
- ~~Q4. GitHub repository?~~ Answered 2026-10-08: **https://github.com/abalas4/notes-app** (public, created by the user). OIDC trust subject: `repo:abalas4/notes-app:ref:refs/heads/main`.
- ~~Q6. Licence for the public repo?~~ Answered 2026-10-08: **none — all rights reserved** (notice in README).
- ~~Q5. GitHub Pro or Free?~~ Answered 2026-10-08: **public repo** on GitHub Free. Branch protection and Actions are free (C-07 resolved).
- ~~Q6. Google Play Console?~~ Answered 2026-10-08: no Play Store. Recorded as the C-05 deviation (personal phone + Device Farm).

---

## 12. Risks

| Risk | Mitigation |
|---|---|
| Device Farm minutes become paid | Local-first testing; Device Farm only at release candidates; rnlab_aws guard rails; Budgets alert |
| **R-NOTIF** — Notifee maintenance status and compatibility with our React Native version not yet verified (as of 2026-10-08) | **Before LLD approval (1.7/1.9):** run the plugin's dependency vetting on Notifee: 7-day cooling period, recent releases / open-issue activity, RN version + New Architecture support, Android 14+/iOS support, licence. If it fails → `expo-notifications` (works in bare RN) or a small native AlarmManager module; record the choice in an ADR. D-06 is "local reminders", independent of the library |
| Android 14+ exact alarms (`SCHEDULE_EXACT_ALARM` is denied by default) | Notifee alarm-manager triggers with in-context permission rationale and a denied-path fallback (inexact alarm + message) — DFMEA row |
| Lambda cold starts with a container image | arm64, slim image, lazy imports; NFR set to p95 < 1 s cold / < 300 ms warm |
| No plugin profile for React Native | Mobile gates use the generic `mobile-01-apps.md` rules; JS commands supplied as PARENT evidence (noted in the ADR) |
| Public repo exposes something sensitive (secrets, account IDs, endpoints) or a fork PR abuses CI | §2 rule 7: gitleaks pre-commit + CI, no IDs in committed tfvars, OIDC trust pinned to `main`/environments, no `pull_request_target`, fork-PR approval required; API throttling + JWT + AWS Budgets alert |
| Lost edits when the network drops (online-only MVP) | Writes fail visibly with Retry and the editor keeps unsaved text until saved; DFMEA row. Sync-conflict risk returns with L-01 |
| Concurrent edits from two devices overwrite each other | Optimistic concurrency (version / `If-Match` → 409 + reload) |

---

## 13. Progress tracker

> **Resume rule:** at the start of every session, read this section first, continue from
> "Next step", and update the checklist + session log after **every** completed step.

**Current phase:** Step 01 (requirements) · **Next step:** 1.3 User Stories on branch `docs/THM01-stories`. Story ID map (fixed): FTR06 STR01–03 · FTR01 STR04–06 · FTR02 STR07–11 · FTR03 STR12–14 · FTR04 STR15–18 · FTR10 STR19–22 · FTR05 STR23–28 · FTR07 STR29–31 · FTR08 STR32–35 · FTR09 STR36–41 · FTR11 STR42–44 · FTR12 STR45–47 · FTR13 STR48–50 · FTR14 STR51–53. Sub-progress: ✅ STR01–53 written · review fixes: ✅ FTR06, 01, 02, 03, 04, 10, 05, 07, 08, 09, 11, 12 (new STR54–71) · ⏳ FTR13, FTR14 (+STR72) · then Feature/Epic text + Linked Stories · then story-reviewer per Feature. Open: Trash view (FTR04); sign-out keeps reminders? (STR06).

### Pending queries for the user (ask these on resume, in this order)
| # | Query | Recommendation |
|---|---|---|

When all of these are answered: mark P-03 done, then Phase 0 (setup), then `/safe-alm-requirements`. Run one step at a time.

### Checklist
- [x] P-01 Read the way-of-working artifact, the design style guide and the rnlab_aws reference
- [x] P-02 Draft technology plan (this file)
- [x] P-02a Conformance check against the plugin (§0, C-01…C-09); plan moved to `00-planning/`
- [x] P-03 **User confirms the technology stack** (D-01…D-11, Q1–Q6) — 2026-10-08
- [x] 0.1 git init, `.gitignore`, `.gitattributes`, `.editorconfig`, `.pre-commit-config.yaml`, README, `.github/SECURITY.md`, `CODEOWNERS`, workspace `CLAUDE.md` (outside the repo); create `notes-app/` (repo) in the workspace, move `00-planning/` into it, move `design_style_guide/` → workspace `jot-design-source/` (C-02); structure check: nothing at the root outside §9 — done 2026-10-08 (commit `eda4450`; repo-local author = GitHub noreply email)
- [x] 0.2 First push to https://github.com/abalas4/notes-app (public; repo created by user 2026-10-08) — done 2026-10-08: pushed; branch protection on `main` (PR required, approvals unticked per D-11, conversation resolution, no bypass, no force-push/deletion; status checks added when CI exists); pre-commit 4.6.2 + gitleaks hook installed and passing
- [x] 1.1 Strategic Theme + Epic (`/safe-alm-requirements`) — include the R-TX Enabler Feature (§8.1) — **done 2026-10-08 — approved and merged in PR #1 (`d7176c4`)**: THM01, THM01CAP01 (Business), THM01CAP02 (Enabler), THM01EPC01 (Business, Android MVP), THM01EPC02 (Enabler, R-TX/R-AWS). Feature IDs reserved: FTR01–06 (EPC01), FTR07–09 (EPC02)
- [x] 1.2 Features + NFR Features — **done 2026-10-08 — approved and merged in PR #3 (`a5d0496`); proposed SLOs and WSJF confirmed**: EPC01 → FTR01–06, FTR10 (split), NFR FTR11–14; EPC02 → FTR07–09
- [ ] 1.3 User Stories + ACs (story-reviewer findings resolved)
- [ ] 1.4 Coverage audit (coverage-auditor)
- [ ] 1.5 PI plan, RAID log, PI release roadmap (`/safe-alm-release`) — then **migrate this plan into the standard artefacts and delete `project-plan.md`** (C-01); the tracker continues in `00-planning/PI-1/`
- [ ] 1.6a Style guide record `06-design/ux/style-guide.md` SG-01…SG-15 built from `../jot-design-source/design.md` — **user approves** (C-03)
- [ ] 1.6 UX spec per Feature mapped to W1–W12 (+ empty / error states)
- [ ] 1.7 HLD, DFMEA, LLD per Feature + ADRs + OpenAPI 3.1 — **includes R-NOTIF: vet Notifee (or pick fallback) before LLD approval**
- [ ] 1.8 Design review (design-reviewer) — gaps closed
- [ ] 1.9 **User approves LLDs**
- [ ] 2.x Implementation slices 1–6 (one row each, added at Sprint Planning)
- [ ] 3.x Code review per PR
- [ ] 4.x Testing per slice: same automated suites on emulator → personal phone (+ manual UAT) → Device Farm (last) — **user accepts UAT**
- [ ] 4.y REL-1.0.0 full regression on Device Farm
- [ ] 5.1 REL-1.0.0 go / no-go — **user records GO**
- [ ] 6.1 SLOs, alarms, runbooks, budget alert; ops readiness

### Decisions log
| Date | ID | Decision | By |
|---|---|---|---|
| 2026-10-08 | — | Plan drafted; iOS reuse added as a requirement (user, mid-session) | Claude |
| 2026-10-08 | — | **All work strictly follows the plugin's way of working, skills and gates; deviations only through ADR + user approval** | User |
| 2026-10-08 | — | Plan moved to `00-planning/project-plan.md`; conformance register C-01…C-09 added | Claude |
| 2026-10-08 | C-05 | **Deviation approved:** no Play Store. Story Done = emulator matrix + UAT on personal Android phone (CI-signed APK) + Device Farm pass. MOB-10 and store promotion N/A. ADR at Step 01 | User |
| 2026-10-08 | D-01 | React Native bare CLI + TypeScript confirmed | User |
| 2026-10-08 | D-02 | Appium **Python** (not WebdriverIO) + Espresso; platform-aware `by_test_id()` so the same tests run on iOS | User |
| 2026-10-08 | D-03/04/05 | Confirmed: FastAPI on Lambda behind HTTP API; DynamoDB; Cognito + Google federation | User |
| 2026-10-08 | C-05 | Automated suites run on all three targets in order: emulator → personal phone (+ manual UAT) → Device Farm last | User |
| 2026-10-08 | — | User: stack may change if another language is better; user knows Python → Python kept for API | User |
| 2026-10-08 | — | No public API during development: emulator → local Docker API; `dev` AWS stack only for Device Farm / real-phone windows; `prod` from go-live | User |
| 2026-10-08 | — | Rationale for HTTP API, Lambda, DynamoDB explained; HTTP API kept over Function URL (pending user confirmation in D-03) | Claude |
| 2026-10-08 | — | Login: Google federation through Cognito first; Cognito native identity later | User |
| 2026-10-08 | — | Testing is emulator-first; Device Farm only in a later hardening phase before REL-1.0.0 | User |
| 2026-10-08 | R-NOTIF | Notifee caveat recorded: maintenance/compatibility unverified; vet before LLD approval, fallback expo-notifications / native module (user asked to track it) | User |
| 2026-10-08 | D-06 | Local notifications in MVP, subject to library support for our RN version (R-NOTIF); server push → L-03 | User |
| 2026-10-08 | D-07 | **Online-only MVP**; offline-first → L-01. Slice 6 removed; op-sqlite deferred; API keeps version/updatedAt/tombstones | User |
| 2026-10-08 | D-09 | Plain text in MVP; rich text → L-02 (user: "mention for later so we don't miss it") | User |
| 2026-10-08 | D-08 | **OpenTofu** + GitHub Actions OIDC. Terraform rejected for its BUSL (non-open-source) licence; user knows Terraform. S3 state + native locking + state encryption (≈ $0). Record in an ADR at Step 01 | User |
| 2026-10-08 | D-10 | Notification "Snooze" opens the app's W12 snooze sheet | User |
| 2026-10-08 | D-11 | Solo PR approval: approval comment on the PR after the `/safe-alm-code-review` report, then user merges (ADR) | User |
| 2026-10-08 | Q3 | App name "Jot", package id `com.jot.app` | User |
| 2026-10-08 | — | **Stable versions only** for all software (§2 rule 6) | User |
| 2026-10-08 | Q5 | **Public GitHub repo** (Free): branch protection + Actions free; C-07 resolved except self-approval (D-11). Public-repo hygiene added as §2 rule 7; licence → Q6 | User |
| 2026-10-08 | Q6 | No open-source licence: all rights reserved, notice in README, no LICENSE file | User |
| 2026-10-08 | Q2 | Device Farm: 981.77 of 1,000 free minutes remaining (user confirmed live) | User |
| 2026-10-08 | Q1 | AWS account on the **legacy free tier**; plan costs on always-free only. DynamoDB on-demand cost note corrected in §7 | User |
| 2026-10-08 | Q4 | Public repo https://github.com/abalas4/notes-app (created by user) | User |
| 2026-10-08 | P-03 | **Technology stack confirmed** — all D-01…D-11 and Q1–Q6 answered | User |
| 2026-10-08 | — | Public-repo naming: never use the local folder name, local paths or third-party product names in repo content (§2 rule 7) | User |
| 2026-10-08 | R-TX | Manual GitHub Actions workflows for emulator tests, Device Farm and dev stack up/down; one local script to build + test on the personal phone (§8.1) | User |
| 2026-10-08 | R-AWS | All AWS prerequisites automated via a manual `aws-prereqs` GitHub Actions workflow (OpenTofu), one fine-grained OIDC role per workflow/environment with a permissions boundary; only a one-time local bootstrap + SSM secret values stay manual (§8.2) | User |
| 2026-10-08 | — | **All created files follow the plugin folder standard.** Plan re-checked: IaC roots moved to `infra/envs/{bootstrap,shared}`, `SECURITY.md` → `.github/`, test folder `load/` (not `performance/`), Postman names, IAC-11 tags, IAC-14 drift workflow | User |
| 2026-10-08 | C-01/C-02 | **Folder standard across the board.** `project-plan.md` migrated into standard artefacts at Step 01 then deleted; design sources kept outside the repo and converted to `style-guide.md` + per-Feature UX snapshots; `CLAUDE.md` → `.claude/` | User |
| 2026-10-08 | §9a | Repo lives in `notes-app/` inside the local workspace; `CLAUDE.md` and `jot-design-source/` sit in the workspace, outside git | User |
| 2026-10-08 | 1.1 | Hierarchy: THM01 → CAP01 Business → EPC01 app MVP; CAP02 Enabler → EPC02 delivery automation (R-TX/R-AWS). Metrics: adoption ≥ 5 notes/week, reminders on time ≥ 99 %, crash-free ≥ 99.5 % / ANR ≤ 0.47 %, API cost ≤ US$1/month. Compliance Regimes: None. Roles shown as `Role (@abalas4)` | User |
| 2026-10-08 | 1.1 | **Approved:** THM01 Approved; CAP01/CAP02 and EPC01/EPC02 → Portfolio Backlog (PR #1 merged) | User |
| 2026-10-08 | 1.2 | 'Organise and find' split into FTR04 Labels + FTR10 Search/sort/filter/select (skill rule: two user journeys); NFR Features FTR11–14 with proposed SLOs | Claude (PO confirms in PR) |
| 2026-10-08 | 1.2 | **Approved:** FTR01–14 → Refined; FTR04/FTR10 split, proposed SLOs and WSJF confirmed (PR #3 merged) | User |
| 2026-10-08 | 1.3-Q | Story-review business rules (all as recommended except Q12): Q1 sign-out cancels phone reminders · Q2 edit conflict → latest version + own text to clipboard · Q3 no Trash in MVP (→ L-05) · Q4 restore only within Undo (server accepts 30 s) · Q5 "Hide completed" saved with the note · Q6 snooze moves only this occurrence · Q7 offline Mark done → notification stays "Couldn't save — tap to retry" · Q8 reminder due while phone off → fire after boot, marked overdue · Q9 Open on deleted note → Home + "Note not found" · Q10 case-only label rename allowed · Q11 dev-down keeps Cognito dev pool, state bucket, image repo · Q13 sign-out revokes refresh token at Cognito · Q14 "Later today" hidden after 21:00 | User |
| 2026-10-08 | 1.3-Q12 | **Signed APK only for release hardening.** All other builds (PRs, main, emulator, phone, Device Farm during slices) use the CI debug build with bundled JS; a manual release-hardening workflow signs the APK that goes to phone UAT, Device Farm regression and the GitHub Release (C-08 still met) | User |
| 2026-10-08 | 1.3 | Settled by Claude (PO did not object): numeric limits → defaults in LLD; Epic 95 % = pivot floor vs 99 % target (note added); Feature metrics sign-ins/week, find ≤ 5 s, labels in use → UAT observation only | Claude |
| 2026-10-08 | — | §1.3 deferred-capabilities register (L-01…L-04) added | Claude |
| 2026-10-08 | — | Mockups (wireframe.html W1–W12 + hi-fi canvas) validated as buildable in React Native; caveats → D-09, D-10 | Claude |

### Session log
| Date | Session summary |
|---|---|
| 2026-10-08 | Read the way of working (6 skills, 23 agents, folder standard, trunk-based branching), Jot design system (W1–W12), and rnlab_aws (RN 0.85.3, Appium/Espresso on Device Farm). Found that the plugin has only the `lang-python-fastapi` stack profile. Drafted this plan. Waiting on the user. |
| 2026-10-08 (cont.) | Clarifications: auth flow, Google federation (native Cognito → backlog), Lambda/DynamoDB/HTTP API rationale, no public API in dev, strict plugin conformance (§0, C-01…C-09), no Play Store deviation (C-05), tests on emulator → phone → Device Farm, Appium Python. D-01…D-05 confirmed. User restarting; resume at D-06. |
| 2026-10-08 (session 3) | Answered all pending queries: D-06 local reminders (R-NOTIF caveat), D-07 online-only, D-08 OpenTofu, D-09 plain text, D-10, D-11, Q1 legacy free tier, Q2 981.77 min, Q3 Jot/com.jot.app, Q4 abalas4/notes-app, Q5 public repo, Q6 no licence. Added §1.3 deferred register (L-01…L-04), §2 rules 6 (stable versions) and 7 (public-repo hygiene), DynamoDB cost correction. P-03 done; next Phase 0.1. |
| 2026-10-08 (session 3, cont.) | Phase 0.1 done: workspace split into `notes-app/` (repo) + `jot-design-source/` + local `CLAUDE.md`; repo files created; `git init` with origin; first commit with the noreply author email. Next: 0.2 push by user. |
| 2026-10-08 (session 3, cont.) | 0.2 done (push, branch protection, pre-commit 4.6.2). Step 01 started: 1.1 artefacts written on branch `docs/THM01-strategy-and-epic`; awaiting PR approval. |
| 2026-10-08 (session 3, cont.) | 1.2 written (FTR01–14). Recovery: feature commits had landed on local `main` after an external branch switch, so PR #2 merged only eb5d290; commits rebased onto `origin/main` as branch `docs/THM01-features-content`, tracker rows lost in the rebase restored. Claude now checks the current branch before every commit. |
