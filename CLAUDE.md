# CLAUDE.md — Pace Prototype (v2, goal-first)

This file is read automatically by Claude Code at the start of every session.
Follow every rule here without being asked. Never deviate unless the user
explicitly overrides a specific rule in the session.

This is the **v2** system. v1 (the calm light "Measured" design, DM Sans,
violet, bento dashboard) is preserved as the `v1-pace` tag on `main`. Its rules
no longer apply to v2 pages. The product thinking behind v2 is in `CONCEPT.md`;
read it before designing anything new.

---

## Project

**Pace** — a cycling app for beginner cyclists that **reads every ride against
the goal you set**, so after each ride you know whether you got closer and
what to do next. Portfolio piece for a mid-level Product Designer showing UX
process and AI tooling. Built in HTML + CSS + vanilla JS. No frameworks, no
build tools. Allowed external dependencies:
- Google Fonts: **Archivo** (400, 500, 600, 700), via `<link>`.
- Leaflet.js 1.9.4 from cdnjs + OpenStreetMap raster tiles, for the ride route
  map only. Load without `integrity` attributes (the cdnjs SRI hash mismatched).

Flag any other new dependency before adding it.

**Scope:** phone-first, responsive to desktop. Every screen is a single HTML
file. Navigation uses `<a href>` or `location.href`.

---

## Where things live

```
pace-prototype/
├── CLAUDE.md               ← this file (v2 rules)
├── CONCEPT.md              ← v2 brief: the idea, goal model, scope test, status
├── PROJECT.md              ← research, flows and the decision log (v2 entries from 2026-09-25)
├── css/tokens.css          ← tokens + shared baseline, imported by every app page
├── index.html              ← Home, between rides
├── onboarding/
│   ├── welcome.html        ← first run, step 1
│   └── connect.html        ← first run, step 3 (mocked Garmin / Strava connect)
├── goal/index.html         ← goal flow, 3 steps (see query params below)
├── rides/
│   ├── index.html          ← history + calendar
│   ├── recap.html          ← ride recap (Home right after a ride)
│   └── detail.html         ← raw data layer below the recap
├── progress/index.html     ← goal trajectory
├── settings/index.html     ← Profile + Settings (avatar menu), optional Body section
├── concepts/
│   ├── index.html          ← prototype map for reviewers (not part of the design)
│   └── recap-a/b/c.html    ← archived explorations, own local tokens on purpose
└── assets/                 ← avatar-alex.png
```

- **First run:** Welcome → `goal/index.html?from=onboarding` → Connect →
  `rides/recap.html?first=1` (adds the intro line and the account prompt).
- **Goal flow entry points:** `?from=onboarding` for first run; in-app
  `?from=home | recap | progress | settings` returns to that page on save or back.
- v1 (light theme, its onboarding steps, Body page, tokens-v1.css) is gone from
  the working tree and lives only at the `v1-pace` tag. Don't recreate it.
- Every page imports `css/tokens.css?v=N` (path relative to its folder) right
  after the Google Fonts link. Never redefine a token in a page. Bump `N` in
  every page whenever `tokens.css` changes (the dev server sends no cache headers).
- When copying chrome (top bar, nav) between folders, re-check relative links:
  a page's own-folder `index.html` means something different in each folder.
- Serve with the `pace-static` launch config (`python -m http.server 8420`) and
  open pages at `http://localhost:8420/...`. `file://` snapshots break links.

---

## Design tokens (css/tokens.css)

```css
:root {
  color-scheme: dark;
  /* Surfaces */
  --bg: #1B1A17;  --raised: #25241F;  --line: #34332D;  --line-strong: #5C5A52;
  /* Text */
  --text: #EDEBE4;  --text-2: #AEACA3;  --text-3: #928F86;
  /* Accent and status */
  --lime: #C8E83A;  --lime-track: #3A4220;  --amber: #F2B653;  --red: #FF8A7A;  --paper: #ECE9E0;
  /* Text on colored fills */
  --ink: #1B1A17;  --on-lime: #2A3110;  --on-lime-meta: #3A4516;
  /* Heart rate zones (ordinal, validated) */
  --zone-1: #5A6B1F;  --zone-2: #7E9624;  --zone-3: #A3C12A;  --zone-4: #C8E83A;  --zone-5: #E6FF7A;
  /* Type */
  --font: 'Archivo', Arial, sans-serif;
  /* Radius */
  --radius-tag: 4px;  --radius-input: 8px;  --radius-button: 10px;
  --radius-card: 12px;  --radius-block: 14px;  --radius-pill: 999px;
  /* Layout */
  --content-width: 560px;  --chrome-width: 960px;  --gutter: 20px;
  /* Motion */
  --motion: 150ms ease;
}
```

`tokens.css` also holds the only shared baseline (box-sizing, body font and
colors). No component styles live there.

---

## Typography

- **Archivo for everything**, numbers included. Numeric values get
  `font-variant-numeric: tabular-nums`. No mono font.
- **Minimum size 12px. Never smaller**, including SVG chart text and `<small>`
  (set `small { font-size: 12px }` explicitly; the browser default shrinks it).
- **Sentence case everywhere.** No ALL CAPS, no Title Case except proper nouns.
- **Scale:**

| Use | Size / weight |
|---|---|
| h1 — the page verdict | `clamp(34px, 9vw, 46px)` / 400, with a **700 `<strong>` first line** on its own line; line-height 1.05; letter-spacing −1.2px |
| Feature line (lime block, goal name) | 28px / 700 |
| h2 — every section heading | 20px / 600, line-height 1.25 |
| Lead line under an h2 | 18px / 600 |
| Data value in a cell | 20px / 600, unit in `<small>` 12px |
| Body | 15px / 400, `--text-2`, max ~34em |
| Links, rows, nav, table | 14px |
| Meta, tags | 13px (`--text-3` for meta) |
| Labels, captions, chart text | 12px |

- One h1 per page (in multi-step pages, only the visible step's h1 is exposed).
  Every section heading is an h2 at the same size. h3 (15px / 600) only for
  sub-groups inside a section, e.g. weeks in Rides history.

---

## Color rules

- **Dark only.** v2 is a deliberate dark design (bike-computer feel); there is
  no light theme. `color-scheme: dark` is set in tokens.
- **One loud block per page.** The lime block (`--lime` background, `--ink`
  text, `--radius-block`) is used once per page, for the page's single most
  important thing: "Today's ride" on Home, "Your next ride" on the recap,
  "Your goal" on Progress. Never two on one page.
- **Lime elsewhere is for data and positive status only:** chart lines and
  bars, meters, "Well done" / "On plan" / "On track" / "Realistic" tags, the
  active bottom-nav item, the focus ring. Never for links or body text.
- **Status tags** (text always carries the meaning, color is the second cue):
  - lime: Well done, On plan, On track, Realistic
  - amber: To work on, Too hard, A stretch
  - red: Missed (and form errors)
  - paper: Today, Current goal (neutral)
- **Emphasis is weight, never a colored word.** Don't highlight a word in lime
  inside a sentence.
- **Contrast:** `--text-3` is the floor for small text (4.81:1 on `--raised`).
  Never use a darker gray for text. Text on lime uses `--ink`, `--on-lime`,
  `--on-lime-meta` only.
- **Never:** gradients, glassmorphism, drop shadows on content, colored section
  backgrounds (other than the one lime block).

---

## Components

Each page carries its own component CSS (no shared component stylesheet yet),
so copy these exactly from an existing v2 page rather than re-inventing them.

### Page frame
- **Top bar (tablet and desktop, ≥ 768px):** logo "Pace" (link to Home, min
  44×44) · pill nav · avatar button. **Sticky** at the top while the page
  scrolls, solid `--bg` background, 1px `--line` divider underneath. Contents
  sit in `.topbar-inner` (max width `--chrome-width`, padding `12px 20px`).
- **Mobile (< 768px): no top bar at all.** No logo, no avatar; the bottom nav
  carries everything, including Profile.
- Focused flows without nav (Welcome, Connect, goal flow) keep a simple,
  non-sticky header with the logo.
- **Main column:** max width `--content-width`, centered, padding `24px 20px 64px`
  (`104px` bottom on mobile to clear the bottom nav).
- **Page opener:** `.meta` date/context line → h1 verdict → optional `.notes`.
- **Sections:** separated by a 1px `--line` top border, 32px margin, 24px
  padding. **No card per section**, no gray eyebrow labels above headings.

### Navigation
- Three destinations: **Home, Rides, Progress.** Body is not in the nav
  (see CONCEPT.md). Profile and Settings (one page, `settings/index.html`)
  are reached from the avatar.
- **Tablet and desktop (≥ 768px):** pills in the sticky top bar. Active =
  filled `--paper` pill, `--ink` text, 700. Resting = `--text-2`, hover `--raised`.
- **Mobile (< 768px):** fixed bottom bar with 1px `--line` top border, icon +
  label, 60px min height, four items: Home, Rides, Progress, **Profile** (the
  24px avatar photo as its icon, linking to Settings). Active = lime icon +
  label, 700, a 3px lime bar on top; the active avatar gets a 2px lime ring.
- `aria-current="page"` on the active item. Ride detail and the recap sit under
  **Rides**; Settings is the active Profile item on mobile and has no active
  pill on desktop.
- **Avatar menu (tablet/desktop):** `button[aria-haspopup="menu"]` with a 36px
  photo in a 44px target; menu items Profile, Settings; Arrow keys, Escape and
  outside-click close.
- Anchors on pages with the sticky bar need `scroll-margin-top` (~84px) so
  jumped-to headings don't land under it.

### Text link / toggle
One look for every text action (`.text-link`): 14px / 600, `--text`, underline
offset 4px in `--text-3`, min-height 44px. Toggles add a chevron that rotates
180° when `aria-expanded="true"` (transition only under no-preference motion).
Back links use a left chevron and no underline.

### Tags and notes
`.tag`: 13px / 700, `--ink` on the status color, `--radius-tag`, min-width 86px
(76px inside week rows) so sentences line up. `.notes` = list of tag + sentence.

### Data cells
`dl.cells`: grid of `--raised` cells separated by 1px `--line` gaps inside a
`--radius-card` frame. 4 columns (2 under 480px). dt 12px `--text-3`, dd 20px /
600 with unit in `<small>`.

### Lime block
`--lime` background, `--radius-block`, padding 22px. h2 → meta line
(`--on-lime-meta`, 13px / 600) → 28px / 700 feature line → note (`--on-lime`).
Links inside use `--ink` text, underline and focus outline.

### Rows (week plan, ride history)
Grid `48px 1fr auto`: day (weekday bold + date) · title + sub line · tag or
status. 14px vertical padding, `--line` dividers. When a row links somewhere,
**the whole row is the link** (never a small inline link inside it).

### Forms (goal flow)
- Inputs and selects: `--raised`, 1px `--line-strong` border, `--radius-input`,
  48px min height, unit shown inside the field on the right.
- Selects are custom (`appearance: none`) with an SVG chevron. Never the bare
  browser arrow.
- Every field has a visible label; hints sit between label and field; errors
  sit under the field in `--red`, linked with `aria-describedby`, and the first
  invalid field gets focus.
- Option cards: real radio inputs, a ring-and-dot indicator (shape, not just
  color) and a lime border when selected.
- Primary button: full-width lime, `--ink` 16px / 700, 52px min height. One
  per step.
- Secondary button (`.btn-secondary`): no fill, 1px `--line-strong` border,
  `--radius-input`, 14px / 600, 44px min height. For row actions like
  Connect / Disconnect and the account prompt.
- Segmented choice: real radios styled as equal buttons; selected = lime fill
  with `--ink` text.
- Switch: a real checkbox with a visible label; the knob position and an
  "On"/"Off" text carry the state, lime track when on.
- Settings save as you go: a "Saved" status (`role="status"`) appears next to
  the section heading for a few seconds.

### Route map
Leaflet + OSM tiles in a `--radius-card` frame, 240px tall. Tiles darkened with
`filter: invert(1) hue-rotate(180deg) brightness(.85) contrast(.9) saturate(.4)`
on `.leaflet-tile-pane`. Route in lime, weight 4. Start = circle, finish =
square. Non-interactive (no zoom, drag or keyboard pan), `fitBounds` without
animation. The map is `aria-hidden` with an sr-only figcaption describing the
route. The OpenStreetMap credit is always visible under the map, 44px target.

---

## Charts and data viz

Follow the `dataviz` skill for any chart. Project specifics:
- Draw SVG in JS at the container's **real pixel width** (redraw on resize), so
  text and strokes never scale down.
- 2px lines, 4px rounded data ends anchored to the baseline, 2px gaps between
  bars and stacked segments. No dashed gridlines; gridlines are `--line`.
- Direct labels are selective (now, the goal, the peak) and get a halo:
  `stroke: var(--bg); stroke-width: 4; paint-order: stroke`.
- Ridden vs planned: solid vs outlined/dashed. Never color alone.
- A legend for 2+ series; a single series needs none.
- Hover: crosshair + tooltip on lines, per-mark tooltip on bars. Tooltips
  enhance, they never gate information.
- Every chart has an sr-only table twin inside `<div class="sr-only">`
  (a `table.sr-only` overflows the page).
- Zone colors come from `--zone-1…5` (mirrored in JS). Segment labels only when
  the share is ≥12%. Validate any new ramp with the dataviz validator
  (`python validate_palette.py … --ordinal`; set `PYTHONIOENCODING=utf-8`).

---

## Layout

- **Phone-first.** Design at 375px first, then check desktop. Single centered
  column on both for now (a desktop two-column layout is an open item).
- Breakpoints: `max-width: 767px` = mobile (bottom nav, no top bar), so a
  768px tablet in portrait gets the top bar; ≤ 480px data cells go to 2 columns.
- 16–20px side gutter, no horizontal scroll at any width.

---

## Accessibility non-negotiables

1. **Contrast:** WCAG 2.1 AA (4.5:1 text, 3:1 large text and non-text marks).
2. **Keyboard:** everything reachable and operable; tab order = reading order.
3. **Focus:** `outline: 2px solid var(--lime); outline-offset: 2px` (dark
   outline inside the lime block). Never `outline: none` without a replacement.
4. **Labels:** visible `<label for>` on every field; never placeholder-only.
5. **Color is never the only signal:** tag text, marker shapes (circle, diamond,
   cross, ring), solid vs outlined marks.
6. **Touch targets:** 44×44px minimum, including inline credits.
7. **Semantic HTML:** `<nav>`, `<main>`, `<section aria-labelledby>`,
   `<button>` for actions, `<a>` for navigation, one h1.
8. **ARIA:** `aria-label` on icon-only controls, `aria-current="page"` on the
   active nav item, `aria-expanded`/`aria-controls` on toggles,
   `aria-live="polite"` on dynamic messages, `aria-hidden` on decoration.
9. **Reduced motion:** transitions only inside
   `@media (prefers-reduced-motion: no-preference)`.
10. **Errors:** tied to their field with `aria-describedby`.

**QA before every commit:** run the in-page audit used so far (every visible
text node ≥12px and passing contrast against its real background, every
link/button ≥44px, no horizontal overflow, heading list) at 375px and desktop,
and fix everything it reports.

---

## Copy rules

- Sentence case. Active voice. Plain language. CTAs say what happens
  ("Save goal and connect my rides", "See what it means each week").
- **Realistic but motivating.** Never tell the rider they'll fail. Pair any
  shortfall with the way to close it ("You can still make it on time…").
- **One next step**, not a training plan dump.
- No filler: never "successfully", "please", "simply", "just". Never "leverage",
  "unlock", "seamless", "empower".
- **Use the market's terms (Garmin Connect / Strava).** Check before inventing
  a label. Current decisions:

| Concept | Term |
|---|---|
| Heart rate zones (Garmin names) | Z1 Warm up · Z2 Easy · Z3 Aerobic · Z4 Threshold · Z5 Maximum |
| Equal-distance chunks of a ride | Splits (e.g. "Every 5 km") |
| Device lap-button / Auto Lap segments | Laps |
| Time | Moving time, Elapsed time |
| Climbing | Elevation gain |
| Others | Avg speed, Max speed, Avg HR, Max HR, Cadence, Calories, Long ride, Tempo, Hill repeats, Group ride |

- Ride **purposes** (Easy endurance, Long ride, Tempo, Hill repeats) are
  separate from zone names; a ride's purpose may target a zone.

---

## What this design is NOT

Reject these patterns; they read as generic or AI-generated UI:

- A card for every section, cards inside cards, gray eyebrow labels above headings
- A word highlighted in color inside a heading or sentence
- Status pills with ✓ / ✕ icons, checkmark-circle lists
- Giant countdown numbers or decorative hero stats
- Brand-dot flourishes ("Pace."), gradients, glass, drop shadows, emojis
- More than one lime block per page, or lime used for links
- Arrow characters decorating copy (chevron icons only in toggles, back links
  and the select control)
- Ride names like "Morning ride on the river path"; show the ride's purpose

---

## Prototype data (keep consistent across pages)

Rider: **Alex**, 32, alex@example.com, Garmin Connect + Strava, no power
meter, weight 74.2 kg (Settings only). "Today" on Home, Rides and Progress is
**Thursday 17 Sep 2026**; the recap is **Tuesday 15 Sep, 7:42**.

- **Heart rate zones** (from Garmin, default % of max HR, max **188**):
  Z1 under 113 · Z2 113–131 · Z3 132–150 · Z4 151–169 · Z5 170+ bpm.

- **Goal:** Saturday group ride, **60 km at 26 km/h by 14 Nov** (set 20 Jul).
  58 days to go from 17 Sep (60 from 15 Sep).
- **Pillars:** longest ride **41.2 of 60 km** (Thu 10 Sep); long-ride speed
  **23.0 of 26 km/h** (21.5 in the week of 27 Jul); **3 rides in 6 of the last
  8 weeks** (light weeks: 27 Jul and 17 Aug).
- **Projections:** 24.9 km/h by 14 Nov at the current pace; 26 with the plan.
  The plan adds ~5 km a week to the Saturday long ride: 46, 51, 56, then
  **60 by 10 Oct**, then hold.
- **Weekly plan:** Tue and Thu 75 min in Z2 (HR under **132 bpm**), Saturday
  long ride in Z2, one harder ride a week when fresh.
- **The recap ride (15 Sep):** 24.3 km · 58:12 · 25.0 km/h · 187 m · avg HR
  142 · max 170 · 82 rpm · 612 kcal. Zones 4 / 22 / 38 / 28 / 8 %. Planned
  easy, rode mostly Z3–Z4 ("Too hard").
- **Training mix, last 3 weeks:** 6 / 19 / 41 / 26 / 8 %; the goal needs about
  10 / 60 / 15 / 10 / 5 %.
- **September rides:** 3 (on plan), 5 (long, 35.0 km, on plan), 8 (too hard),
  10 (long, 41.2 km, on plan), 12 (missed), 13 (tempo, on plan), 15 (too hard);
  planned 17 and 19. 154 km, 6h 32m, 4 of 6 on plan.

If a change touches any of these numbers, update every page that shows them.

---

## Working agreements

- Juliana writes in Portuguese or English; **reply in English** unless she asks
  for Portuguese.
- **Branch per change:** `main` always holds the current prototype. Start each
  change on a new short-lived branch from an up-to-date `main` (descriptive
  kebab-case name, e.g. `ride-detail-laps`), open a GitHub pull request into
  `main` with `gh pr create`, and delete the branch after it's merged
  (locally and on GitHub). Never commit directly to `main`.
- **Commit, push and open PRs only when she asks.** She reviews and merges PRs
  herself on GitHub. The GitHub CLI is installed at
  `C:\Program Files\GitHub CLI\gh.exe` and signed in as `rgb-und-cmyk`.
- Global git identity isn't set, so commit with
  `git -c user.name="Juliana" -c user.email="ju.penna@gmail.com"`, and pass
  multi-line messages with `-F <file>` (PowerShell mangles quotes otherwise).
- Log notable v2 decisions in `PROJECT.md`'s decision log when asked.
- History: v2 was built on `concept-goal-first` and merged into `main` via
  PR #1 (2026-10-06); v1 is the `v1-pace` tag.
- Parked topics to carry into the case study: nutrition, sleep, social,
  body-composition goals (see CONCEPT.md and session notes).

---

## Session startup checklist

1. Re-read this file and `CONCEPT.md`.
2. Check which screen is being built and where it sits in the core loop.
3. Import `tokens.css` and Archivo before writing any component CSS; copy
   components from an existing v2 page.
4. Never hardcode a hex that exists as a token (JS chart constants mirror the
   tokens; keep them in sync).
5. Build the 375px layout first, then desktop.
6. Keep prototype data consistent with the list above.
7. Run the accessibility and QA audit before asking to commit.
