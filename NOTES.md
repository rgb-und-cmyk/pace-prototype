# NOTES — session handoff

Overwrite at the end of every session. Keep it short. Permanent decisions go in
the `PROJECT.md` decision log; this file is only "where we are right now".

## Goal
Pace v2 (goal-first cycling app prototype) is live on `main`. Current focus:
polish, keeping the repo easy to work in, and preparing the portfolio case study.

## What's done
- v2 built, audited at 375px and desktop, and merged via PR #1 (6 Oct 2026).
- Git workflow documented and in use: branch per change → PR → delete branch (PR #2).
- Session handoff setup: slim CLAUDE.md, `docs/` for on-demand detail, this file,
  exclusions for archived files, stale v1 `SKILL.md` archived (this PR).

## Key decisions and why
Full list in `PROJECT.md` (decision log, 2026-09-25 onward). Most relevant:
- Goal-first concept: every ride is read against the rider's goal (CONCEPT.md).
- One lime block per page; dark only; Garmin/Strava terminology.
- Body-composition goals, nutrition, sleep and social are parked on purpose
  (to be covered in the case study as scope decisions).
- CLAUDE.md is kept short; design detail lives in `docs/DESIGN-SYSTEM.md`.

## Open issues
- PR #3 (decision-log entries: merge, git workflow, nav by device) awaiting merge.
- The installed `cycling-dashboard-project` skill still carries v1-era context and
  says to be used every session. Update or disable it in Claude's skills settings.
- Desktop layout is one centered column; a two-column version is undecided.
- Where power zones appear when a power meter is connected: undecided.
- PROJECT.md's v2 log entries still say "see CLAUDE.md" for rules now in
  `docs/DESIGN-SYSTEM.md` (fix once PR #3 is merged, to avoid a conflict).

## Next step
Merge PR #3, merge this PR, then `/clear` and start the next task in a fresh
session (e.g. a design polish item or the case-study outline).
