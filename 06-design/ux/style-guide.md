Design Style Guide: Jot

```
Design Style Guide: Jot                  Version: 1.0   Status: Approved
Owner                : UX Lead (@abalas4)
Design system        : none — this guide is the source
Design-tool library  : Jot design source v1 (design notes, wireframes W1–W12, high-fidelity canvas) — kept
                       outside the repository; approved frames are exported as snapshots to
                       06-design/ux/<Feature or Story ID>/ when each UX Spec is approved (08-ux-design.md §5)
Token export         : 07-source-code-tests/src/shared/design-tokens/ (project-structure-standard.md §4) —
                       created in the first implementation slice; the mobile app imports its theme from there
Sections             : SG-01 … SG-15 — see the table below
Accessibility check  : contrast table (SG-02) computed 2026-10-08 by Claude from the token hex values
                       (WCAG 2.1 relative luminance); to be re-verified by the token unit tests
Parent               : THM01EPC01 (Surfaces: Mobile app = Yes, Android; Web UI = No)
```

| Section | Status | Link |
|---|---|---|
| SG-01 Principles | Complete | [SG-01](#sg-01-principles) |
| SG-02 Brand and colour | Complete — 3 fixes accepted (P-01…P-03) | [SG-02](#sg-02-brand-and-colour) |
| SG-03 Typography | Complete | [SG-03](#sg-03-typography) |
| SG-04 Design tokens | Complete | [SG-04](#sg-04-design-tokens) |
| SG-05 Layout | Complete — orientation (P-04) (P-04) | [SG-05](#sg-05-layout) |
| SG-06 Components | Complete | [SG-06](#sg-06-components) |
| SG-07 Patterns | Complete — state patterns (P-05) (P-05) | [SG-07](#sg-07-patterns) |
| SG-08 Iconography and imagery | Complete | [SG-08](#sg-08-iconography-and-imagery) |
| SG-09 Content and voice | Complete | [SG-09](#sg-09-content-and-voice) |
| SG-10 Accessibility | Complete | [SG-10](#sg-10-accessibility) |
| SG-11 Motion | Complete — values (P-06) (P-06) | [SG-11](#sg-11-motion) |
| SG-12 Internationalisation | Complete — single locale (English) | [SG-12](#sg-12-internationalisation) |
| SG-13 Data visualisation | N/A — Jot shows no charts (the checklist progress bar is a component, SG-06) | — |
| SG-14 AI / chat surfaces | N/A — no `[GenAI]` Stories in THM01 | — |
| SG-15 Mobile platforms | Complete — app icon / launch screen (P-07) (P-07) | [SG-15](#sg-15-mobile-platforms) |

Items marked **P-nn** were not in the design source; they close gaps the plugin's section minimums
require. All seven (P-01…P-07) were accepted by the Product Owner on 2026-10-08 and are part of v1.0.

---

## SG-01 Principles

Jot is a calm, colour-coded app for capturing notes, checklists and reminders in two taps or fewer.

1. **Capture first.** Writing never waits on organising. The FAB is the single capture entry point.
2. **Colour is meaning.** Tint groups notes; text stays ink. Colour is never the only signal.
3. **Glanceable.** Cards reveal content, not chrome.
4. **Calm by default.** One primary action per screen; destructive actions offer Undo rather than
   interrupt.

**Target user:** one person keeping personal notes, lists and reminders on their own phone.
**Target devices:** Android phones, portrait (SG-05, SG-15). Tablet layout and iOS are deferred
(Epic out-of-scope list); the codebase stays iOS-ready.

## SG-02 Brand and colour

Light theme only in MVP. Dark theme is deferred (THM01EPC01 out of scope); tokens are named by role
so a dark set can be added as a minor version.

### Core palette

| Token | Name | Hex | Role |
|---|---|---|---|
| `color.bg` | Paper | `#FBFAF7` | App background |
| `color.surface` | Surface | `#FFFFFF` | Search pill, sheets, trays, nav bar |
| `color.ink` | Ink | `#1F1D1A` | Primary text, icons, selection ring |
| `color.ink-soft` | Ink soft | `#5C5850` | Secondary text, completed list items |
| `color.meta` | Meta | `#4A463F` | Timestamps and counts on Paper |
| `color.accent` | Teal | `#0F766E` | Primary actions, focus, FAB, checkbox fill |
| `color.accent-tonal` | Teal tonal fill | `#D6EEEA` | Selected chips, active nav pill, tonal buttons |
| `color.on-accent-tonal` | Teal on tonal | `#0B4F4A` | Text on teal tonal fill |
| `color.on-accent` | White | `#FFFFFF` | Text / icons on Teal |
| `color.danger` | Danger | `#B42318` | Destructive actions, error text |
| `color.danger-tonal` | Danger tonal fill | `#FADBD8` | Overdue tag, error banners |
| `color.outline` | Outline | `rgba(31,29,26,.12)` | Decorative dividers and card edges only |
| `color.outline-strong` | Outline strong | `#857F76` | **Accepted (P-01)** — boundaries that identify a control |
| `color.inverse` | Snackbar | `#1F1D1A` (= Ink) | Snackbar fill; text `#FFFFFF`, action `#D6EEEA` |

**Semantic palette:** success = Teal (confirmations use text, e.g. "Saved"), error = Danger,
warning = Danger tonal + text ("Overdue"), info = Ink on Surface. Jot needs no separate
success / warning hues.

### Note colours

| Token | Name | Hex |
|---|---|---|
| `color.note.plain` | Plain | `#FFFFFF` |
| `color.note.butter` | Butter | `#FFF1B8` |
| `color.note.coral` | Coral | `#FFD9CF` |
| `color.note.sage` | Sage | `#D5EBD3` |
| `color.note.sky` | Sky | `#D2E6F7` |
| `color.note.lilac` | Lilac | `#E4DBF5` |
| `color.note.rose` | Rose | `#F8D6E4` |
| `color.note.sand` | Sand | `#EFE3D2` |

The selected colour swatch shows a 2 dp Ink ring, never hue alone.

### Contrast table (WCAG 2.1 AA: text ≥ 4.5:1, large text and UI components ≥ 3:1)

| Foreground | Background | Ratio | Use | Result |
|---|---|---|---|---|
| Ink | Paper / Surface | 16.11 / 16.81 | Body, titles | ✅ |
| Ink | each note colour | 12.60 – 16.81 | Card and editor text | ✅ |
| Ink | 8 % Ink tag over each note colour | 10.82 – 14.36 | Label / reminder tags | ✅ |
| Ink soft | Paper / Surface | 6.78 / 7.08 | Secondary text | ✅ |
| Ink soft | each note colour | 5.30 – 7.08 | Completed items, card meta | ✅ |
| Meta | Paper | 8.99 | Timestamps, counts | ✅ |
| Teal | Paper / Surface | 5.24 / 5.47 | Text buttons, links | ✅ |
| Teal | note colours | 4.10 – 4.83 (Plain 5.47) | — | ❌ for text → **P-02** |
| White | Teal | 5.47 | Filled button, FAB icon | ✅ |
| Teal on tonal | Teal tonal | 7.74 | Selected chip / tonal button text | ✅ |
| Ink | Teal tonal | 13.83 | Active nav label | ✅ |
| Danger | Paper / Surface | 6.30 / 6.57 | Destructive text buttons, errors | ✅ |
| Danger | Danger tonal | 5.07 | "Overdue" tag text | ✅ |
| White / Teal tonal | Ink (snackbar) | 16.81 / 13.83 | Snackbar text / "Undo" | ✅ |
| Teal | Paper / Surface | 5.24 / 5.47 | FAB, focus border, checkbox (UI) | ✅ |
| Teal | note colours | 4.10 – 4.83 | Checkbox fill, progress bar (UI) | ✅ (≥ 3:1) |
| Ink ring | Paper / Surface | 16.11 / 16.81 | Selection ring (UI) | ✅ |
| Outline 12 % | Paper / Surface | 1.27 | Card edges, dividers (decorative) | ✅ decorative only |
| Outline 12 % | Surface | 1.27 | Text field, outlined button, chip, Plain swatch boundary | ❌ → **P-01** |
| Outline strong | Paper / Surface / Butter | 3.80 / 3.97 / 3.50 | Control boundaries | ✅ |
| Ink soft | each note colour | ≥ 5.30 | Unchecked checkbox border on tinted rows | ✅ → **P-03** |
| Teal tonal pill | Surface | 1.22 | Active nav indicator | ✅ — not the only signal: active label is bold (SG-06) |

**Accepted fixes (P-01…P-03, not in the design source):**
- **P-01** — add `color.outline-strong` `#857F76` for any boundary that identifies a control: text
  field (unfocused), outlined button, unselected filter chip, the Plain swatch in the colour tray.
  The 12 % outline stays for decorative card edges and dividers only.
- **P-02** — Teal is never used for **text** on a note colour; on tinted surfaces use Ink (text
  buttons) — Teal stays allowed there for non-text UI (checkbox fill, progress bar).
- **P-03** — unchecked checkbox border is Ink soft (≥ 5.30:1 on every note colour), not the outline.

## SG-03 Typography

| Role | Family | Fallback |
|---|---|---|
| Display | Bricolage Grotesque 600 / 700 | system sans-serif (Roboto on Android) |
| Interface and notes | Figtree 400 – 700 | system sans-serif |

Both families are under the SIL Open Font License and are bundled in the app (no network font
loading); the licence check (V38) records them at implementation.

| Style | Token | Size / weight | Line height | Use |
|---|---|---|---|---|
| Display | `type.display` | 32 / 700, letter-spacing −0.01em | 1.2 | Screen titles |
| Editor title | `type.editor-title` | 28 / 700 | 1.25 | Note / list title in the editor |
| Title | `type.title` | 22 / 600 | 1.3 | Sheet and dialog headings |
| Note title | `type.note-title` | 16 / 600 | 1.35 | Card titles |
| Body | `type.body` | 15 / 400 | 1.5 | Note text, list items |
| Label | `type.label` | 14 / 600 | 1.3 | Buttons, chips, nav labels |
| Meta | `type.meta` | 13 / 500 | 1.4 | Timestamps, counts, tags |
| Overline | `type.overline` | 12 / 600, caps, +0.08em | 1.4 | Section labels ("PINNED", "OTHERS") |

Sizes are in sp so they scale with the system font size (SG-15). **Minimum body size: 14 sp**;
Meta (13) and Overline (12) are only for short supporting text, never for content.

## SG-04 Design tokens

Single source: `07-source-code-tests/src/shared/design-tokens/` — token JSON plus the generated
TypeScript theme the React Native app imports. Values are never re-typed in a component. Unit tests
in `tests/shared/design-tokens/unit/` check the token schema and every ✅ pair of the SG-02 contrast
table.

| Group | Tokens |
|---|---|
| Colour | SG-02 (`color.*`, `color.note.*`) |
| Typography | SG-03 (`type.*`: family, size, weight, line height, letter spacing) |
| Spacing (4-pt) | `space.1` 4 · `space.2` 8 · `space.3` 12 · `space.4` 16 · `space.6` 24 · `space.8` 32 · `space.12` 48 |
| Radius | `radius.chip` 8 · `radius.input` 12 · `radius.tag` 12 · `radius.card` 14 · `radius.fab` 18 · `radius.sheet` 20 · `radius.nav` 20 · `radius.pill` full |
| Elevation | `elevation.0` 1 dp outline · `elevation.1` `0 1 3 rgba(31,29,26,.18)` · `elevation.2` `0 8 24 rgba(31,29,26,.18)` (mapped to Android elevation in the theme) |
| Size | `size.target` 48 · `size.icon` 24 · `size.icon-stroke` 1.8 · `size.button` 48 · `size.fab` 56 · `size.chip` 36 · `size.tag` 24 · `size.search` 52 · `size.nav` 64 · `size.snackbar` 52 · `size.swatch` 44 · `size.checkbox` 20 · `size.row` 48 |
| Motion | SG-11 (`motion.duration.*`, `motion.easing.*`) |
| Z-order | `z.content` 0 · `z.fab` 10 · `z.nav` 20 · `z.snackbar` 30 · `z.sheet` 40 · `z.dialog` 50 |

## SG-05 Layout

- **Units:** dp (density-independent pixels); type in sp.
- **Spacing:** 4-pt scale (SG-04). Screen side gutter 16; gap between cards 12.
- **Home grid:** two-column masonry on every supported phone width; cards keep their natural height.
- **Device tiers** (feed the E2E device matrix in the HLD platform scope):

| Tier | Width | Notes |
|---|---|---|
| Small phone | 360 dp | Smallest supported; two columns still fit (card ≥ 158 dp) |
| Large phone | 412 – 480 dp | Reference design width |
| Tablet / foldable unfolded | — | Not supported in MVP (deferred); app runs phone layout |

- **Orientation — P-04:** portrait only in MVP. Landscape is not designed in the source;
  locking avoids untested layouts. Revisit with the tablet layout.
- Bottom navigation floats 16 dp above the system navigation bar; the snackbar sits 16 dp above
  the bottom navigation; the FAB sits above the bottom navigation, right-aligned on the gutter.

## SG-06 Components

All interactive components meet the 48 dp touch target (SG-10) even when the visible glyph is
smaller. States: default · pressed · focused · disabled · loading · error where applicable.
"Hover" does not apply on touch Android.

| Component | Spec | Variants / states | Do / don't | Accessibility |
|---|---|---|---|---|
| Button | Pill, 48 dp tall, `type.label` | Filled Teal (one primary per screen) · Tonal · Outlined (`outline-strong`) · Text · Destructive (Danger) · disabled 38 % opacity · loading = spinner replaces label, width kept | Don't put two filled buttons on one screen | role button; label text or `accessibilityLabel` |
| Icon button | 24 dp stroke glyph (1.8) in a 48 dp target | default · pressed (8 % Ink circle) · disabled | Every icon button has a label | `accessibilityLabel` ("Pin note", "Archive") |
| FAB | 56 dp, radius 18, Teal, `elevation.2`, white "+" | Long-press offers "New list" | One per screen; Home only | Label "New note" |
| Filter chip | 36 dp, pill | Unselected: Surface + `outline-strong` · Selected: Teal tonal + Teal border + check glyph | Selection is never colour only | role button, `selected` state announced |
| Tag (label / reminder) | 24 dp, radius 12, Ink at 8 % fill, `type.meta` | Label · Reminder (bell glyph + time) · Overdue: Danger tonal + the word "Overdue" | Max 3 tags on a card, then "+N" | Read as text in the card's label |
| Note card | Radius 14, padding 14 / 16, decorative outline, note-colour fill | Text note · Checklist (≤ 5 rows then "+ N more"; completed rows struck through at the foot) · Pinned (pin glyph) · Selected (2 dp Ink ring + check) | Content, not chrome; no buttons on the card | One focusable element; label = title, first line, tags, reminder |
| Search field | 52 dp pill, Surface, `elevation.1`; menu and layout toggle inside | default · focused · with text (clear button) | — | Real label "Search notes" |
| Text field | 48 dp, radius 12, `outline-strong` border; 2 dp Teal when focused; Danger border + message when invalid | default · focused · error · disabled | Errors appear below the field | Visible label; error announced |
| Checkbox | 20 dp box, Teal fill when checked, Ink-soft border when unchecked (P-03), 48 dp row | unchecked · checked · disabled | — | role checkbox; item text is its label |
| List item row | 48 dp: drag handle, checkbox, text, optional reminder meta | open · checked (strike-through, Ink soft, moved to "Completed · N") · dragging (`elevation.2`) | — | Drag also offered as "Move up" / "Move down" actions |
| Progress | Teal bar on a 12 % track + "N of M done" under the list title | — | The text always accompanies the bar | Text carries the value |
| Bottom navigation | Floating, 64 dp, radius 20, Surface, `elevation.2`: Notes · Reminders · Archive | Active: Teal tonal pill behind icon + bold label | Three destinations only | role tablist; selected announced |
| Snackbar | 52 dp, Ink fill, white text, "Undo" in Teal tonal; 5 s; 16 dp above nav | Archive · Delete · error with "Retry" | One at a time; newest replaces | Live region (polite); stays while focused by TalkBack |
| Colour tray | Row of 44 dp swatches (48 dp target) on a Surface tray / bottom sheet | Selected = 2 dp Ink ring + check; Plain swatch has `outline-strong` border (P-01) | — | Each swatch labelled by colour name ("Sage") |
| Bottom sheet | Surface, radius 20 top, `elevation.2`, drag handle, scrim Ink 32 % | Reminder sheet (W9) · Snooze and edit sheet (W12) · Label picker (W6) · Sort (W2) | Cancel / Save at the foot; Save is the one filled button | Focus moves into the sheet; Back closes it |
| Reminder sheet | Quick picks (Later today, Tomorrow, Pick date), month calendar (today dashed ring, selected date Ink fill), time, repeat, Cancel / Save | "Later today" hidden after 21:00 | — | Calendar days labelled with full dates |
| Snooze and edit sheet | Presets: In 10 minutes · In 1 hour · Tonight 8:00 PM · Tomorrow 9:00 AM · Pick date and time; divider; Edit reminder · Mark done · Remove reminder (Danger) | — | — | — |
| Reminder notification | App mark, time, note title, one-line body (lists: "N of M done · next: <item>"); actions Mark done · Snooze · Open; tap body opens the note | Overdue (fired late after boot) | — | System notification semantics |
| Navigation drawer | W7: labels list, "Edit labels", settings, sign out | — | — | — |
| Dialog | Surface, radius 20, title + body + up to two buttons | Confirmation of irreversible actions only (SG-07) | Prefer Undo over a dialog | Focus trapped; Back = cancel |

## SG-07 Patterns

| Pattern | Rule |
|---|---|
| Forms and validation | Notes autosave (no Save button in the editor). Validate on blur / submit, not per keystroke; the message says what happened and what to do (SG-09) |
| Navigation | Bottom navigation for the three top-level destinations; drawer (W7) for labels and settings; editor is a full screen with Back saving and returning |
| Search and filters | Search pill on Home; filter chips under it; "No notes match" empty state with a "Clear filters" text button |
| Multi-select | Long-press a card → selection mode: "N selected" top bar with bulk actions; selected cards show the Ink ring + check (W3) |
| Destructive actions | Archive and delete act at once and show the snackbar with **Undo** (5 s; server accepts restore for 30 s). A confirmation dialog is used only where Undo is impossible: deleting a label ("Deleting a label never deletes notes"), sign-out |
| Notifications / toasts | Snackbar only (SG-06); no toasts |
| Onboarding | Sign-in screen with "Sign in with Google"; the notification permission is asked at the first reminder with the rationale screen (SG-15), not at first launch |
| **States — P-05** (the design source lists empty / error states as not covered; copy comes from the approved Stories) | |
| Empty | Centred 48 dp line icon + one sentence + optional text button: Home "Notes you add appear here" · Reminders "No reminders" · Archive "No archived notes" · Search "No notes match" |
| Loading | First load: skeleton cards (Ink 6 % blocks in the masonry) — no spinner over content; actions: inline spinner in the button |
| Error | Inline banner on Danger tonal at the top of the content with text + "Try again"; a failed save shows "Couldn't save — tap to retry" on the affected item; missing note → Home + snackbar "Note not found" |
| Offline (online-only MVP, D-07) | Persistent banner "You're offline — changes can't be saved" under the top bar; sign-in shows "Connect to the internet to sign in"; edit fields stay readable but saving shows the retry state |
| Success | No celebration; the result is visible (card appears, snackbar where Undo applies) |

## SG-08 Iconography and imagery

- **Icons:** one custom line set drawn for Jot — 24 dp grid, 1.8 dp stroke, round caps and joins,
  Ink by default, Teal for active / selected, white on Teal. Exported as SVG and rendered as vector
  in the app. No mixed icon families.
- **Sizes:** 24 dp standard; 20 dp inside chips and tags; 48 dp for empty-state illustrations.
- **Imagery:** none in MVP (image and drawing notes are deferred).
- **Alt text / labels:** icon-only controls always carry an `accessibilityLabel` naming the action
  ("Archive note"), not the glyph ("box icon"). Decorative icons next to text are hidden from
  TalkBack.

## SG-09 Content and voice

- **Tone:** calm, short, plain. Second person when addressing the user; no exclamation marks, no
  blame ("Couldn't save", not "You failed to save").
- **Capitalisation:** sentence case everywhere, including buttons ("Sign in with Google", "Mark
  done"); Overline section labels are rendered in caps by style, written in sentence case in code.
- **Terminology:** *note* (text note), *list* (checklist), *label*, *reminder*, *archive*,
  *pin*, *snooze*, *mark done*. Never "task", "tag" (UI) or "memo".
- **Numbers, dates, times:** device locale and the device 12 / 24-hour setting. Relative where it
  helps: "Edited just now", "Today 8:00 PM", "Tomorrow 9:00 AM"; otherwise short date ("12 Oct").
  Counts: "N of M done", "N selected", "Completed · N".
- **Error messages:** what happened + what to do, ≤ 2 short sentences: "Sign-in failed. Try
  again." · "Couldn't save — tap to retry."
- **Empty states:** one sentence saying what will appear here (SG-07).
- **Permission rationale:** say why, in the user's terms: "Jot needs permission to alert you at
  the time you choose".

## SG-10 Accessibility

WCAG 2.1 AA as applied to native apps (WCAG2ICT) is the floor (`09-mobile-apps.md` §4).

- **Contrast:** SG-02 table; colour is never the sole signal (selection ring, "Overdue" text,
  progress text, bold active nav label).
- **Touch targets:** ≥ 48 dp × 48 dp (Android); 44 dp visible swatches sit inside 48 dp targets.
- **Focus indicator:** 2 dp Teal outline offset 2 dp around the focused control (keyboard / switch
  access); text fields use the 2 dp Teal border.
- **Order:** TalkBack and focus order follow the visual reading order: top bar → search → chips →
  Pinned → Others → FAB → bottom navigation.
- **Screen-reader text:** every interactive element has a role and a label; cards read as one
  item (title, first line, tags, reminder, "pinned"); state changes (checked, selected, archived)
  are announced; snackbars are polite live regions.
- **Text scaling:** layouts work at the system font scale up to 200 % (SG-15).
- **Motion:** honour the system "Remove animations" setting (SG-11).
- **Alternatives to gestures:** drag-to-reorder also offers "Move up" / "Move down"; swipe actions
  (if any) have a menu equivalent.

## SG-11 Motion

**Accepted (P-06)** — the design source defines no motion values.

| Token | Value | Use |
|---|---|---|
| `motion.duration.short` | 150 ms | Press feedback, checkbox, chip selection |
| `motion.duration.medium` | 250 ms | Bottom sheet, snackbar, card move to "Completed" |
| `motion.duration.long` | 300 ms | Screen transition (meets the ≤ 300 ms mobile NFR) |
| `motion.easing.standard` | cubic-bezier(0.2, 0, 0, 1) | Elements moving on screen |
| `motion.easing.enter` | cubic-bezier(0, 0, 0, 1) | Sheets and snackbars entering |
| `motion.easing.exit` | cubic-bezier(0.3, 0, 1, 1) | Leaving |

Animation is allowed only to show cause and effect (where something went, what changed). No
decorative or looping animation. When the system "Remove animations" setting is on, durations
become 0 and changes are instant.

## SG-12 Internationalisation

Single locale: English (THM01EPC01 coverage row 16 — N/A until public distribution). All strings
are externalised in a resource file so locales can be added later; no text inside images. Dates,
times and numbers use the device locale formats (SG-09). Layouts allow 30 % text expansion. RTL is
not supported in MVP; layout uses start / end, not left / right, so it can be added.

## SG-13 Data visualisation

N/A — no charts. The checklist progress bar is a component (SG-06) and always carries its value as
text.

## SG-14 AI / chat surfaces

N/A — THM01 has no `[GenAI]` Stories.

## SG-15 Mobile platforms

| Item | Rule |
|---|---|
| Design approach | **One unified Jot brand** with Android platform adaptations (system back, edge-to-edge, system notification and permission UI). iOS adaptations are recorded here when an iOS Feature is added |
| Navigation | Floating bottom navigation (Notes, Reminders, Archive) + drawer; the system Back gesture / button closes sheets and dialogs first, then returns from the editor, then exits from Home |
| System bars, insets | Edge-to-edge: content draws behind the status and navigation bars and respects their insets; status-bar icons dark on Paper; gesture-navigation inset respected by the floating nav, FAB and snackbar |
| Gestures and haptics | Long-press selects a card; drag handle reorders list items; light haptic on long-press and on drag pick-up only; every gesture has a visible alternative (SG-10) |
| Touch targets | ≥ 48 dp (SG-10) |
| Font scaling | Respect the system font size up to 200 %: text wraps, cards grow, nothing truncates mid-word in titles; the bottom navigation keeps icons and allows labels to wrap |
| Dark mode | Not in MVP (deferred). The app forces the light theme so system dark mode does not invert colours |
| App icon — **Accepted (P-07)** | Adaptive icon: Teal background layer, white "J" note-card mark foreground; monochrome layer for themed icons. Final artwork is a `[DESIGN]` Work Item in the first slice |
| Launch screen — **Accepted (P-07)** | Android 12+ splash API: Paper background, the app mark centred, no text, no delay beyond app start |
| Notification styling | W11: small icon = monochrome app mark; accent colour Teal; title = note title; body = one line; actions Mark done · Snooze · Open; one channel "Reminders" (high importance) |
| Permission rationale | Before asking for notification / exact-alarm permission: an in-app sheet with the SG-09 rationale, "Enable notifications" (filled) and "Not now" (text); if denied: "Enable in settings" opens system settings |
| Offline and sync indicators | Online-only MVP: the offline banner and retry states in SG-07; no sync indicator (offline-first is deferred) |
| Token export per platform | One TypeScript theme generated from the token JSON (SG-04), consumed by the React Native app; platform-specific values (elevation, fonts) mapped there |

---

## Changes

| Version | Date | Change | Approved by |
|---|---|---|---|
| 1.0 | 2026-10-08 | First record, from the Jot design source v1; P-01…P-07 added to meet the SG minimums and accepted | UX Lead, Product Owner, Tech Lead (@abalas4) |

## Approval

| Role | Name | Date | Decision |
|---|---|---|---|
| UX Lead | @abalas4 | 2026-10-08 | Approved |
| Product Owner | @abalas4 | 2026-10-08 | Approved, incl. P-01…P-07 |
| Tech Lead (tokens are consumable) | @abalas4 | 2026-10-08 | Approved |
| Accessibility reviewer | N/A — none in the organisation | | |
