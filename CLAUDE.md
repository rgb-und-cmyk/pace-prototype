# CLAUDE.md — Pace Prototype

This file is read automatically by Claude Code at the start of every session.
Follow every rule here without being asked. Never deviate unless the user
explicitly overrides a specific rule in the session.

---

## Project

**Pace** — a cycling data dashboard for beginner cyclists.
Portfolio piece for a mid-level Product Designer demonstrating UX process
and AI tooling skills. Built entirely in HTML + CSS + vanilla JS.
No frameworks. No build tools. No external dependencies except:
- Google Fonts (DM Sans / DM Mono), loaded via `<link>`
- Leaflet.js (via CDN `<script>`/`<link>`) + OpenStreetMap tiles, for the
  ride route map only (see Component rules → Route map). Not a general
  license to add other libraries — flag any other new dependency before
  adding it.

**Prototype scope:** desktop + mobile responsive. All screens are single HTML
files. Navigation between screens uses `<a href>` links or JS `location.href`.

---

## File structure

```
pace-prototype/
├── CLAUDE.md               ← this file
├── index.html              ← dashboard (home)
├── onboarding/
│   ├── welcome.html
│   ├── account.html
│   ├── profile.html
│   ├── connect.html
│   ├── goal.html
│   ├── body.html
│   └── confirmation.html
├── rides/
│   ├── index.html          ← rides list
│   └── detail.html         ← ride detail
├── progress/
│   └── index.html
├── body/
│   └── index.html
├── settings/
│   └── index.html
├── css/
│   └── tokens.css          ← design tokens (auto-imported by all pages)
└── assets/
    └── (any SVG illustrations)
```

Every HTML file imports `../css/tokens.css` (adjust path depth as needed)
and the Google Fonts `<link>` tag. Never duplicate token definitions
across files — they live only in `tokens.css`.

The static dev server (`.claude/launch.json`, plain `python -m http.server`)
sends no cache headers, so browsers can serve a stale `tokens.css` for a long
time after an edit. The stylesheet link carries a cache-busting query string
(`tokens.css?v=N`) in every HTML file for this reason — bump `N` in every
file whenever `tokens.css` changes, so edits are guaranteed to show up on
reload instead of silently rendering with old token values.

---

## Design tokens (tokens.css)

```css
:root {
  /* Color */
  --color-bg:        #F5F4F0;  /* Chalk — page background */
  --color-surface:   #FAFAF8;  /* Off-white — cards, tiles */
  --color-border:    #E2E0D9;  /* Stone — all borders */
  --color-border-mid: #C8C5BF; /* Slightly stronger border, inputs */
  --color-text:      #2E2E2E;  /* Slate — primary text */
  --color-text-mid:  #4A4A4A;  /* Medium-dark gray — nav items */
  --color-text-sub:  #5C5A56;  /* Supporting text */
  --color-text-muted:#8A8880;  /* Ash — labels, hints, secondary */
  --color-accent:    #6B5B8C;  /* Muted Violet — primary accent */
  --color-accent-tint:#EDE9F4; /* Violet Mist — hover, tint bg */

  /* Typography */
  --font-sans: 'DM Sans', Arial, sans-serif;
  --font-mono: 'DM Mono', 'Courier New', monospace;

  /* Spacing */
  --space-xs:  4px;
  --space-sm:  8px;
  --space-md:  16px;
  --space-lg:  24px;
  --space-xl:  40px;

  /* Radius */
  --radius-sm: 4px;   /* chips, tags */
  --radius-md: 6px;   /* buttons, inputs */
  --radius-lg: 8px;   /* tiles, cards */

  /* Transitions */
  --transition: 150ms ease;
}
```

---

## Typography rules

- **Font family:** DM Sans for all UI. DM Mono for numeric data values only.
- **Weights:** 400 (body, labels), 600 (headings, strong emphasis), 700 (page titles, metric values).
- **Case:** sentence case everywhere. Never ALL CAPS in UI copy. Never Title Case except proper nouns.
- **Line height:** 1.5 for body text, 1.2 for headings, 1 for metric values.
- **Line length:** max 68 characters for body text blocks. Never let paragraphs run full-width.
- **Minimum size:** 12px. Never smaller.
- **Scale:**
  - Page title (h1): 20px / 700
  - Section heading (h2): 16px / 600
  - Label (uppercase, muted): 11px / 700 / letter-spacing 0.5px
  - Body: 14px / 400
  - Secondary / hint: 13px / 400
  - Caption / meta: 12px / 400
  - Metric value (DM Mono): size varies by context, always 700

---

## Color usage rules

- **Background:** `--color-bg` (#F5F4F0) on all pages.
- **Cards and tiles:** `--color-surface` (#FAFAF8) background.
- **Borders:** `1px solid var(--color-border)` on tiles and cards.
  `2px solid var(--color-border-mid)` on form inputs and interactive cards.
- **Primary text:** `--color-text` (#2E2E2E).
- **Nav items (resting):** `--color-text-mid` (#4A4A4A).
- **Secondary text:** `--color-text-sub` (#5C5A56).
- **Labels, hints, muted:** `--color-text-muted` (#8A8880).
- **Accent use:** violet (`--color-accent`) on: active nav border-left,
  primary buttons, selected states, AI layer border, focus rings, active
  stepper dots. Never as a background for body text.
- **Accent tint:** `--color-accent-tint` (#EDE9F4) for hover states on
  accent elements, selected card backgrounds, stepper dot fills.
- **Never:** gradients, glassmorphism, box-shadows on content elements.
  The only shadow allowed is a focus ring: `0 0 0 3px var(--color-accent-tint)`.

---

## Component rules

### Buttons

Primary button (one per view max):
```css
background-color: var(--color-accent);
color: #FFFFFF;
border: 2px solid var(--color-accent);
border-radius: var(--radius-md);
padding: 12px 24px;
font-size: 14px;
font-weight: 600;
font-family: var(--font-sans);
```
Hover: `background-color: #5a4b7a; border-color: #5a4b7a;`
Focus-visible: `outline: 2px solid var(--color-accent); outline-offset: 3px;`
Disabled: `opacity: 0.4; cursor: not-allowed;`

Secondary button:
```css
background-color: #FFFFFF;
color: var(--color-text);
border: 2px solid var(--color-border-mid);
border-radius: var(--radius-md);
padding: 12px 24px;
font-size: 14px;
font-weight: 500;
```
Hover: `border-color: var(--color-text-mid);`

Ghost / text button:
```css
background: none;
border: none;
color: var(--color-text-mid);
font-size: 13px;
font-weight: 500;
padding: 5px 10px;
```
A tile's "see more" affordance is a bare chevron icon, no visible label —
bottom-right corner of the card (`align-self: flex-end` in a flex-column
`.tile`, pushed down with `margin-top: auto`), e.g. Last ride → Ride detail,
Body → Body page. See Decision Log, 2026-09-22 (this superseded a same-day
text-arrow version twice: first "Full ride →" trailing text, then a bare
`→` character — both replaced by this SVG chevron for a bolder, more
deliberate icon than a typed arrow character allows).
```css
.ghost-btn-icon {
  width: 16px;
  height: 16px;
  fill: none;
  stroke: currentColor;
  stroke-width: 3.5;
  stroke-linecap: round;
  stroke-linejoin: round;
}
```
`<path d="M9 6l6 6-6 6"/>` in a 24×24 viewBox. Since there's no visible
text, the link needs `aria-label` naming the destination (e.g.
`aria-label="See full ride"`) and the SVG itself is `aria-hidden="true"` —
this is the one intentional exception to "icon-only controls need a paired
text label" in Accessibility non-negotiables, justified because it's a
single low-stakes "go deeper" affordance repeated identically across every
tile, not a one-off unlabeled control.

### Form inputs

```css
width: 100%;
padding: 10px 13px;
border: 2px solid var(--color-border-mid);
border-radius: var(--radius-md);
font-size: 14px;
color: var(--color-text);
background-color: #FFFFFF;
font-family: var(--font-sans);
outline: none;
```
Focus: `border-color: var(--color-accent); box-shadow: 0 0 0 3px var(--color-accent-tint);`
Placeholder: `color: var(--color-text-muted);`
Label: `font-size: 13px; font-weight: 600; color: var(--color-text); margin-bottom: 5px;`
Sub-label (hint under label): `font-size: 11px; color: var(--color-text-muted); margin-bottom: 8px;`

### Select dropdowns

Same border/radius as inputs. Custom chevron via `background-image` SVG.
Never use default browser arrow alone — always override with custom chevron.

### Tiles and cards

```css
background-color: var(--color-surface);
border: 1px solid var(--color-border);
border-radius: var(--radius-lg);
padding: var(--space-md);
```
No box-shadow. No gradient fills. Interactive tiles get `cursor: pointer`
and hover state: `border-color: var(--color-accent);`

### AI layer (insight blocks)

```css
background-color: var(--color-surface);
border-left: 3px solid var(--color-accent);
border-radius: 0 var(--radius-lg) var(--radius-lg) 0;
padding: var(--space-md);
```
Text color: `var(--color-text-sub)` (#5C5A56) — quieter than primary content.
Label above copy: 11px / 700 / `var(--color-accent)` / letter-spacing 0.5px / uppercase.
**Never:** an "AI" label, robot icon, or chat bubble. The border is the only signal.
**Always:** appears after the raw data it's interpreting, never before — e.g.
Ride Detail's "What this ride means" follows the ride's own metrics; the
Dashboard insight strip follows Last ride. One documented exception: Progress
page's "This week's summary" sits above the period toggle and every
period-scoped chart (see Decision Log, 2026-09-22), because it isn't
interpreting the data below it — it's a fixed, period-independent read on
the current week, so nothing "raw" precedes it for it to follow.

### Top pill navigation (desktop)

Supersedes the earlier sidebar spec (see Decision Log, 2026-09-21). Lives inside
the topbar, between the logo and the avatar.

```css
display: flex;
align-items: center;
gap: 4px;
```
Nav item (pill):
```css
display: flex;
align-items: center;
gap: 6px;
padding: 8px 14px;
border-radius: 999px;
font-size: 14px;
font-weight: 500;
color: var(--color-text-mid);   /* #4A4A4A */
background: none;
```
Hover (resting item): `background-color: var(--color-bg);`
Active state:
```css
color: var(--color-accent);
font-weight: 700;
background-color: var(--color-accent-tint);
```
Nav icon: 18px, paired with text label always — never icon alone (accessibility).
Shape (filled pill vs. plain text), not color alone, signals the active item.

### Bottom navigation (mobile)

Unchanged — mobile still uses a fixed bottom nav bar. See Layout — mobile below.

### Bento grid (dashboard)

Desktop (default):
```css
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 12px;
```
Tile size mapping:
- Large (last ride): `grid-column: span 2;`
- Standard (weekly summary, streak, body, goal): 1 column
- Full-width strip (AI insight): `grid-column: span 3;`

Mobile (max-width: 768px): `grid-template-columns: 1fr;` — all tiles stack.

### Route map (ride detail)

Lives in a `.tile`, above Activity, per the IA (Map/route is the first thing
on Ride Detail). Uses real map tiles (Leaflet.js + OpenStreetMap raster
tiles) — the one exception to "no decorative illustration," since the route
is real ride data, not decoration.

```css
border: 1px solid var(--color-border);
border-radius: var(--radius-md);
overflow: hidden;
```
- **Non-interactive:** zoom, drag, scroll-zoom, double-click-zoom, touch-zoom
  and keyboard pan all disabled. This is a static summary, not an explorable
  map — consistent with the calm, restrained "Measured" style.
- **Route line:** accent violet (`var(--color-accent)`), weight 4, rounded
  caps/joins. Same treatment as the heart-rate chart line.
- **Start / finish markers:** different shapes, not color alone — circle for
  start, square for finish (accessibility rule 5).
- **fitBounds** to the route on load, no pan/zoom animation (respects
  `prefers-reduced-motion` by not animating at all).
- **Attribution:** OpenStreetMap requires visible credit. Render it as a
  normal, always-visible text line under the map (not Leaflet's default
  control, and never hidden or `aria-hidden`) — small size, `--color-text-muted`.
- **Accessibility:** the map container itself is `aria-hidden="true"` (it has
  no operable controls, so nothing is lost); pair it with a real `sr-only`
  caption describing the route (distance, shape, elevation) as text.

### Metric display (data values)

```css
font-family: var(--font-mono);
font-size: 22px;   /* or larger depending on context */
font-weight: 700;
color: var(--color-text);
line-height: 1;
font-variant-numeric: tabular-nums;
```
Unit label sits inline after the value at 12px / 600 / `--color-text-muted`.
Label sits below the value at 11px / 400 / `--color-text-muted`.
**Rule: value is always visually larger than its label.**

### Progress stepper (onboarding)

5 steps: Account · Profile · Data · Goal · Body
Dot states:
- Pending: `border: 2px solid var(--color-border-mid); background: #FFFFFF; color: var(--color-text-muted);`
- Active: `border-color: var(--color-accent); background: var(--color-accent); color: #FFFFFF;`
- Done: same as active, label replaced with ✓
Connector: `2px height; background: var(--color-border-mid);`
Done connector: `background: var(--color-accent);`

---

## Layout — desktop

- Topbar: full-width, 56px height, `background: #FFFFFF`, 1px border-bottom.
  Contains logo left, pill nav center, user avatar right.
- No sidebar. Main content spans full width below the topbar, padding 24px,
  max-width 960px, centered.
- Onboarding screens: centered layout, no nav, max-width 480px centered.

## Layout — mobile (max-width: 768px)

- No sidebar. Bottom navigation bar instead:
  5 items, icon + label, 56px height, `background: #FFFFFF`,
  1px border-top, fixed to bottom.
- Main content: single column, padding 16px, full width.
- Bento grid collapses to single column.
- Touch targets: minimum 44×44px on all interactive elements.
- Font sizes scale down 1–2px from desktop equivalents.

---

## Accessibility non-negotiables

Every screen must pass these without exception:

1. **Contrast:** all text/background pairs meet WCAG 2.1 AA (4.5:1 body,
   3:1 large text). Run a mental check before outputting any color pairing.
2. **Keyboard navigation:** all interactive elements reachable and operable
   via keyboard. Tab order follows visual reading order.
3. **Focus indicators:** visible on every interactive element.
   `outline: 2px solid var(--color-accent); outline-offset: 2px;` — never `outline: none`.
4. **Labels:** every form field has a visible `<label>` with `for` attribute.
   Never placeholder-only labels.
5. **Color not sole signal:** every state (selected, error, active) uses
   shape or text in addition to color.
6. **Touch targets:** minimum 44×44px on mobile.
7. **Semantic HTML:** use `<nav>`, `<main>`, `<header>`, `<section>`,
   `<button>` (not `<div onclick>`), `<a>` for navigation. Heading hierarchy
   must be logical (one h1 per page).
8. **ARIA:** `aria-label` on icon-only controls. `aria-current="page"` on
   active nav item. `aria-live="polite"` on dynamically updated regions.
   `aria-hidden="true"` on decorative elements.
9. **Reduced motion:** wrap all CSS transitions/animations in
   `@media (prefers-reduced-motion: no-preference)`.
10. **Error messages:** associated with their field via `aria-describedby`.

---

## Copy rules

- Sentence case everywhere. No ALL CAPS in UI copy. No Title Case.
- Active voice. CTAs describe exactly what happens: "Create account",
  not "Submit". "Go to my dashboard", not "Continue".
- No filler: never "successfully", "please", "simply", "just", "easy".
- Error messages: say what happened and what to do. Never vague.
- Empty states: an invitation to act, not an apology.
  "Go for a ride with your Garmin and sync to see your data." — not "No data yet."
- AI copy: plain language, no sports science jargon unless immediately
  explained. Never use "leverage", "unlock", "seamless", "empower".

---

## What this design is NOT

Reject these patterns if they appear in output — they are the generic defaults:

- No box-shadows on cards or tiles
- No gradients anywhere
- No glassmorphism / frosted glass
- No decorative illustrations or icons used as decoration
- No colored section backgrounds
- No ALL CAPS labels
- No identical rounded-card grid with same shadow everywhere (SaaS card kit)
- No emojis in UI copy
- No arrow characters or icons decorating body copy, nav items, or inline
  link text — the chevron icon is reserved for the bare, bottom-right "see
  more" ghost button only (see Component rules → Ghost / text button)

---

## Session startup checklist

At the start of every Claude Code session on this project:

1. Re-read this file.
2. Check which screen is being built and which flow it belongs to.
3. Import `tokens.css` and Google Fonts before writing any component CSS.
4. Never hardcode a color hex that exists as a token.
5. Build mobile layout alongside desktop — not as an afterthought.
6. After each screen, do a contrast and accessibility check before moving on.
