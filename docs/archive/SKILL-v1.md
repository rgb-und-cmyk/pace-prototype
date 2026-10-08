---
name: cycling-dashboard-project
description: >
  Project context and protocol file for the Cycling Dashboard portfolio project.
  Use this skill at the start of every session related to this project, or whenever
  the user mentions "cycling dashboard", "portfolio project", "our project", or
  references any of the project phases (discovery, research, prototype, etc.).
  This file is the single source of truth for project state, decisions, protocols,
  and research. Always read this before generating any project-related output.
---

> **ARCHIVED (2026-10-08).** This is the v1-era project skill (last updated 2026-09-14, Phase 3). It is stale: it predates the goal-first v2 pivot. Current context: CLAUDE.md, CONCEPT.md, NOTES.md, PROJECT.md. The research quotes below are duplicated in PROJECT.md section 1.2.


# Cycling Dashboard — Project Skill File

> Last updated: 2026-09-14
> Current phase: Phase 3 — Design

---

## 1. Project Overview

A portfolio piece for a mid-level Product Designer (Juliana) demonstrating end-to-end
UX process and AI tooling skills.

**Product concept:** A cycling data dashboard for beginner cyclists that unifies
fragmented data from multiple devices and apps, and uses an AI layer to explain
progress in plain language.

**Portfolio goals:**
- Demonstrate structured UX process (discovery through prototype)
- Demonstrate ability to use AI tools (Claude) as both a process aid and a product feature
- Produce an interactive prototype built entirely in Claude Code (no Figma)

---

## 2. Problem Statement

Beginner cyclists who invest in tracking devices (Garmin, Wahoo, etc.) end up managing
multiple disconnected apps with no unified view of their progress. The data exists but
the interpretation layer is missing — leaving users overwhelmed, not informed.

---

## 3. Target User

Beginner cyclist who:
- Owns at least one tracking device (Garmin or similar)
- Uses multiple apps (Garmin Connect, Strava, Fitbit, etc.)
- Does not have a coaching background or sports science knowledge
- Wants to understand their progress, not just collect data

---

## 4. Scope

**Core flow:**
Onboarding + first ride experience → unified cycling-focused dashboard

**Data sources in scope:**
- Primary: Garmin Connect, Strava
- Secondary: Fitbit (sleep, resting HR), manual scale input
  (weight, fat %, muscle %, bone %, water %)

**AI layer (in-product):**
- Guides onboarding and user profile/goal creation
- Explains data in plain language
- Surfaces what the user should pay attention to
- Does not replace medical or coaching advice

**HR monitoring:** Secondary feature. Dashboard is customizable.

**Out of scope:**
- Social/community features
- Recovery or sleep as core features
- Survey-based user research

---

## 5. Deliverables

| Deliverable | Format | Status |
|---|---|---|
| Project skill file | SKILL.md | ✅ Complete |
| Project documentation | PROJECT.md | ✅ In progress |
| Discovery doc (Phase 1) | Section in PROJECT.md | ✅ Complete |
| Competitive analysis (Phase 2) | Section in PROJECT.md | ✅ Complete |
| Information architecture (Phase 2) | Section in PROJECT.md | ✅ Complete |
| Core use cases + metrics (Phase 2) | Section in PROJECT.md | ✅ Complete |
| UI style definition (Phase 3) | Section in PROJECT.md | ⬜ Next |
| Core flows + wireframes (Phase 3) | Section in PROJECT.md | ⬜ Pending |
| Interactive prototype | Claude Code (desktop + mobile) | ⬜ Pending |
| Portfolio-facing case study | MD or web | ⬜ Future deliverable |

---

## 6. Project Phases

```
Phase 1 — Discovery ✅
  ├── Desk research (verified Reddit + forum quotes)
  ├── Designer inputs (Juliana's direct experience)
  └── Problem statement + persona + HMW questions

Phase 2 — Define ✅
  ├── Competitive landscape (Garmin Connect, Strava, intervals.icu, TrainingPeaks)
  ├── Information architecture (6 sections)
  └── Core use cases + success metrics

Phase 3 — Design (current)
  ├── UI style definition ← next
  ├── Core flows + wireframes
  └── Interactive prototype (Claude Code, desktop + mobile)

Phase 4 — AI Integration
  └── Define and document AI layer behavior within the product

Phase 5 — Validation (future)
  └── Propose validation method (survey, usability test, etc.)

Phase 6 — Documentation
  └── Living PROJECT.md updated each phase + portfolio case study
```

---

## 7. Protocols (non-negotiable)

These rules apply to every session and every output in this project.

### 7.1 Language
- All project outputs, responses, and documentation: **English**
- Portuguese (BR) allowed only when Juliana explicitly asks for an explanation in PT/BR
- Never switch languages mid-response without being asked

### 7.2 Source integrity
- **No fabricated quotes.** Every quote used must have a verifiable URL.
- If a source cannot be confirmed, it must be flagged as "unverified" or labeled
  as a synthesized insight from community patterns — never presented as a real quote.
- If a topic needs research before a response can be generated, flag it first.
- Reddit is a valid source only when direct post/comment links can be confirmed by
  the user.

### 7.3 Tone and content
- Factual and grounded. No corporate warmth, no filler phrases.
- No AI-sounding patterns: no em-dashes for stylistic effect, no overly symmetrical
  structure, no "certainly!" or "great question!" openers.
- Concise. Don't use more tokens than the task requires.

### 7.4 Decision-making
- Propose before building. For any significant output, summarize the approach first
  and wait for confirmation if there's meaningful ambiguity.
- Flag scope creep or contradictions with prior decisions explicitly.
- Always refer back to this file when resuming a session.

---

## 8. Research Log

### 8.1 Verified quotes — General (Phase 1)

**Quote 1** — Road Bike Review forum
> "I'm pretty new to cycling and recently started using a bike computer. I've noticed
> there are tons of metrics available—heart rate, power, cadence, speed, and more—
> and honestly, it's a bit overwhelming!"
URL: https://www.roadbikereview.com/threads/looking-for-advice-which-cycling-metrics-should-i-focus-on.387260/

**Quote 2** — Cycling Unbound
> "I just started getting serious about cycling after years of casual rides...
> I was getting overwhelmed trying to track everything from day one."
URL: https://cyclingunbound.org/master-your-cycling-performance-the-10-essential-metrics-every-cyclist-should-track/

**Quote 3** — Roadman Cycling (July 2026), expert framing
> "The riders who improve track a small number of metrics consistently. The ones who
> stagnate track everything reactively — drowning in colourful graphs that tell them
> nothing useful."
URL: https://roadmancycling.com/blog/cycling-data-analysis-basics-guide

**Quote 4** — Reddit r/cycling
> "I'm struggling to find an app that clearly shows my performance evolution over time."
URL: https://www.reddit.com/r/cycling/comments/1rvnjd5/whats_your_goto_app_for_analyzing_your_rides/

**Quote 5** — Reddit r/cycling (same thread)
> "What are you guys using to see the 'big picture' of my training? Are there any
> hidden gems that focus on clean data visualization rather than just social
> leaderboards or basic summaries?"
URL: https://www.reddit.com/r/cycling/comments/1rvnjd5/whats_your_goto_app_for_analyzing_your_rides/

---

### 8.2 Verified quotes — Competitive research (Phase 2, 2024+ only)

**Garmin Connect**
> "The UX feels clunky and bloated. Navigation is frustrating, finding things isn't
> intuitive, and there's a pretty steep learning curve."
> — r/Garmin, Sep 2026 · https://www.reddit.com/r/Garmin/comments/1weestr/garmin_connect_app_sucks/

> "I've learned from a friend that the last revamp of the iOS app was a major UX downgrade."
> — r/Garmin, Sep 2026 · https://www.reddit.com/r/Garmin/comments/1weestr/garmin_connect_app_sucks/

**Strava**
> "Seems like this is the most confusing metric. Anyone care to spend a minute to
> explain it to this noob?"
> — r/Strava, Jun 2026 · https://www.reddit.com/r/Strava/comments/1uc3to2/fitness_score/

> "this type of data stuff can very easily get overwhelming"
> — r/Strava, Mar 2024 · https://www.reddit.com/r/Strava/comments/1bb76qs/strava_data_vs_actual_progress/

> "Strava's fitness graph does not track fitness but chronic training load"
> — r/Strava, Aug 2026 · https://www.reddit.com/r/Strava/comments/1vj6xoc/more_confirmation_that_the_fitness_graph_is/

**intervals.icu**
> "I really dislike intervals' interface (even as a decade long wko user)."
> — r/Velo, Oct 2024 · https://www.reddit.com/r/Velo/comments/1g15v81/

> "The interface looks decent on intervals, although bits are a bit cluttered."
> — r/Velo, Oct 2024 · https://www.reddit.com/r/Velo/comments/1g15v81/

**intervals.icu vs TrainingPeaks**
> "Intervals.icu eats TP for lunch all day, every day."
> — r/triathlon, Feb 2026 · https://www.reddit.com/r/triathlon/comments/1qv49ln/ditching_trainingpeaks_for_intervalsicu_with_a/

---

### 8.3 Key patterns from research

- Fragmentation is not only a beginner problem — even experienced users struggle to
  get a unified view of progress.
- The Strava social layer actively distracts from training analysis.
- Existing deep tools (intervals.icu, Golden Cheetah, TrainingPeaks) have steep
  learning curves not suited to beginners.
- No current tool combines onboarding, plain-language explanation, and unified data
  in a beginner-friendly interface.
- Even Garmin's own AI layer (Connect+) is paywalled and not designed around
  beginner comprehension.

---

## 9. Decision Log

| Date | Decision | Rationale |
|---|---|---|
| 2026-08-20 | No Figma — prototype in Claude Code only | Demonstrates AI tooling skills for portfolio |
| 2026-08-20 | No survey in immediate workflow | Replaced by designer inputs + verified community research |
| 2026-08-20 | HR monitoring = secondary feature | Not universal; dashboard will be customizable |
| 2026-08-20 | Skill file format: SKILL.md with YAML frontmatter | Future-proof, installable as Claude skill |
| 2026-09-14 | PROJECT.md = working document; case study = separate future deliverable | Keeps documentation focused |
| 2026-09-14 | Phase 1 complete | Problem statement, persona, HMW, research finalized |
| 2026-09-14 | Body section confirmed in scope | User wants weight/composition snapshot on dashboard |
| 2026-09-14 | Fitbit confirmed as secondary data source | Sleep + resting HR included if user activates it |
| 2026-09-14 | Phase 2 complete | Competitive landscape, IA, use cases, metrics finalized |

---

## 10. Open Questions

**Project decisions pending:**
- [ ] UI style direction (to be defined in Phase 3 — next step)
- [ ] Coded prototype format: HTML or React?
- [ ] Validation method for Phase 5

**Learning questions (no urgency — for future exploration):**
- [ ] When and why should a CLAUDE.md file be created? Is it always best practice?
- [ ] Should this project have multiple SKILL.md files or one unified project skill?
      What are the tradeoffs?

---

*This file is the single source of truth for the project.
Update it at the end of every working session or when a decision is made.*
