# NOTES — session handoff

Overwrite at the end of every session. Keep it short. Permanent decisions go in
the `PROJECT.md` decision log; this file is only "where we are right now".

## Goal
Pace v2 (goal-first cycling app prototype) is live on `main`. Current focus:
the portfolio case study, to be published on Juliana's Squarespace portfolio.

## What's done
- v2 built, audited and merged (PR #1, 6 Oct 2026). Git workflow, session
  handoff setup and doc references sorted (PRs #2–#5).
- On branch `case-study-draft` (nothing committed yet):
  - `docs/CASE-STUDY.md` draft 2: new opening line, prototype + GitHub links,
    less "AI-sounding" wording, ~20% shorter, fictional-data note (Overview
    "Data" bullet + persona section), reflection drafted and edited by Juliana.
  - `docs/USABILITY-TEST-PLAN.md` draft 1 (5 sessions, hypotheses H1–H5).
  - `README.md` for visitors arriving from the case study's GitHub link.
  - `docs/case-study-images/`: v1 dashboard (desktop), 11 screens at 375px
    (2x), recap on desktop.

## Key decisions and why
- Case study lives on Squarespace; the repo Markdown is the working draft.
- Persona quote in the case study swapped for the sourced r/cycling quote
  (PROJECT.md Quote 4), also in PROJECT.md's persona; the old "I have all
  this data…" line had no link. CONCEPT.md still quotes the old line.
- Usability testing is framed as "What's next", not run before publishing.
- Prototype will be hosted on GitHub Pages (needs the repo public).

## Open issues
- Repo is private and Pages is off, so both case-study links 404.
- Prototype link: point at Home (root) or `onboarding/welcome.html`? README
  already uses welcome.
- `gh` login expired; run `& "C:\Program Files\GitHub CLI\gh.exe" auth login`.
- "Designing with AI" lesson paragraph needs Juliana's check.
- Still undecided: two-column desktop layout; where power zones appear.

## Next step
Make the repo public + turn on Pages, then commit
the branch and open a PR. After that, lay out the case study in Squarespace.
