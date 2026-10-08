# CLAUDE.md — Pace

Cycling app for beginner cyclists: **reads every ride against the rider's goal**,
so after each ride you know whether you got closer and what to do next.
Portfolio piece for a Product Designer (Juliana). v2 (goal-first) is on `main`;
v1 is the `v1-pace` tag. Juliana may write in Portuguese: **reply in English**
unless she asks for PT.

## Session start
1. Read `NOTES.md` first (where we are, open issues, next step).
2. Read only the files for the task. Detail is in `docs/`, not here.
3. Before designing something new, read `CONCEPT.md`.

## Stack
HTML + CSS + vanilla JS. No build tools, no frameworks, no test suite.
Archivo (Google Fonts). Leaflet + OpenStreetMap on ride detail only.
Flag any new dependency before adding it.

## Run and check
- Serve with the `pace-static` launch config (`python -m http.server 8420`);
  open `http://localhost:8420/...`. `file://` breaks links.
- **QA before every commit**, at 375px and desktop: all text ≥ 12px, WCAG AA
  contrast, 44px touch targets, no horizontal scroll, one h1. Fix what it finds.
- Charts follow the `dataviz` skill; validate any new color ramp.

## Key files
`css/tokens.css` (tokens, imported by every page) · `index.html` (Home) ·
`rides/{index,recap,detail}.html` · `progress/` · `goal/` (3-step flow,
`?from=onboarding|home|recap|progress|settings`) · `settings/` ·
`onboarding/{welcome,connect}.html` · `concepts/` (prototype map + archived A/B/C) ·
`CONCEPT.md` (the idea) · `PROJECT.md` (research + decision log) · `NOTES.md` (handoff)

Every page imports `css/tokens.css?v=N` right after the Google Fonts link; bump
`N` in every page when tokens change. When copying nav chrome between folders,
re-check relative links.

## Read on demand (not every session)
- `docs/DESIGN-SYSTEM.md`: tokens, type scale, color rules, every component,
  charts, accessibility detail, copy and terminology, banned patterns.
- `docs/PROTOTYPE-DATA.md`: Alex's numbers that must match across pages.
- `PROJECT.md` is 900+ lines: grep for the section you need, never read it whole.

## Non-negotiables (full rules in docs/DESIGN-SYSTEM.md)
- Dark only. Tokens only, never hardcode a hex that exists as a token.
- One lime block per page. Lime elsewhere = data and positive status only.
- Minimum text 12px; touch targets 44px; color is never the only signal.
- Use Garmin/Strava terms (zones: Warm up, Easy, Aerobic, Threshold, Maximum).
- No card per section, no highlighted words, no AI-looking UI patterns.
- Copy: sentence case, plain language, realistic but motivating.
- Mobile < 768px: bottom nav, no top bar. ≥ 768px: sticky top bar.

## Workflow
- **Branch per change** from an up-to-date `main` (kebab-case name) → pull
  request with `gh pr create` → she merges on GitHub → delete the branch.
  Never commit to `main`. `gh` is at `C:\Program Files\GitHub CLI\gh.exe`,
  signed in as `rgb-und-cmyk`.
- **Commit, push and open PRs only when she asks.** Commit as
  `git -c user.name="Juliana" -c user.email="ju.penna@gmail.com"` and pass
  multi-line messages with `-F <file>` (PowerShell mangles quotes).
- **Plan mode first** for: new screens or flows, changes across many pages
  (tokens, nav, shared data, renames), deletions, restructures and merges.
  Skip it for copy tweaks, single-page fixes and logging a decision.
- Log notable decisions in `PROJECT.md`'s decision log when asked.
- Parked for the case study: nutrition, sleep, social, body-composition goals.

## Session hygiene
- One task per session. `/clear` between unrelated tasks; `/compact` only for a
  long session worth continuing; `/context` and `/cost` to check usage (don't
  trust self-reported token counts).
- Smaller model for simple tasks (copy, logging, small fixes); larger for new
  screens, planning and hard reasoning.
- **Before ending a session, overwrite `NOTES.md`** (Goal, What's done, Key
  decisions and why, Open issues, Next step). Permanent history goes in the
  `PROJECT.md` decision log, not in NOTES.md.
