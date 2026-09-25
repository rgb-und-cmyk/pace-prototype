# Cycling Dashboard — Project Documentation

> Type: Working document
> Last updated: 2026-09-17
> Current phase: Phase 3 complete — every screen built. Phase 4 (AI Integration) up next.
> Prototype format: HTML + CSS + vanilla JS (no framework)
> Model for Claude Code: Claude Sonnet 5

---

## Table of Contents

0. [Protocols](#protocols)
1. [Project Overview](#project-overview)
2. [Phase 1 — Discovery](#phase-1--discovery)
3. [Phase 2 — Define](#phase-2--define)
4. [Phase 3 — Design](#phase-3--design)
5. [Phase 4 — AI Integration](#phase-4--ai-integration)
6. [Phase 5 — Validation](#phase-5--validation)
7. [Decision Log](#decision-log)
8. [Open Questions](#open-questions)

---

## Protocols

> These rules apply to every session and every output in this project —
> in Claude chat and in Claude Code. Read this section before starting any work.

### Language
- All outputs, responses, and documentation: **English**
- Portuguese (BR) only when Juliana explicitly asks for an explanation in PT/BR
- Never switch languages mid-response without being asked

### Source integrity
- **No fabricated quotes.** Every quote used must have a verifiable URL.
- If a source cannot be confirmed, it must be flagged as "unverified" or labeled
  as a synthesized insight — never presented as a real quote.
- Reddit is a valid source only when direct post/comment links can be confirmed
  by the user.

### Tone and content
- Factual and grounded. No corporate warmth, no filler phrases.
- No AI-sounding patterns: no overly symmetrical structure, no "certainly!" or
  "great question!" openers.
- Concise. Don't use more tokens than the task requires.

### Decision-making
- Propose before building. For any significant output, summarize the approach
  first and wait for confirmation if there's meaningful ambiguity.
- Flag scope creep or contradictions with prior decisions explicitly.
- Always re-read this file at the start of every session.

### Prototype rules (Claude Code specific)
- Read CLAUDE.md before writing any code.
- Never hardcode a color hex that exists as a design token.
- Build mobile layout alongside desktop — not as an afterthought.
- After each screen, do a contrast and accessibility check before moving on.
- One screen or component per session prompt — don't batch too much at once.

---

## Project Overview

**Product:** Pace — a cycling data dashboard for beginner cyclists.
Unifies fragmented data from Garmin, Strava, Fitbit, and manual scale input.
Uses an AI layer to explain progress in plain language.

**Portfolio goals:**
- Demonstrate structured UX process (discovery through prototype)
- Demonstrate ability to use AI tools as both process aid and product feature
- Produce an interactive prototype built entirely in Claude Code (no Figma)

**Target user:** beginner cyclist who owns at least one tracking device (Garmin
or similar), uses multiple apps, has no coaching background, and wants to
understand their progress — not just collect data.

**Persona:** Alex — early 30s, European city, office worker, entry-level Garmin
+ occasional Strava. Core quote: *"I have all this data but I still don't know
if I'm doing this right."*

**Data sources in scope:**
- Primary: Garmin Connect, Strava
- Secondary: Fitbit (sleep, resting HR), smart scales (Fitbit Aria, Withings
  Body+, Garmin Index S2, Xiaomi Mi Body Scale 2), manual body data input

**AI layer:** onboarding support, plain-language explanation of ride data,
progress insights. Not medical or coaching advice.

**Out of scope:** social features, recovery/sleep as core, survey-based research.

---

## Phase 1 — Discovery

### 1.1 Problem Statement

Beginner cyclists who invest in tracking devices (Garmin, Wahoo, etc.) immediately face
a fragmentation problem: their data lives across multiple apps — Garmin Connect, Strava,
Fitbit, Google Health — each optimized for a different purpose. Garmin syncs device data.
Strava drives social engagement. Fitbit tracks sleep and steps. None of them are designed
to answer the question a beginner actually has:

> *Am I improving, and what should I do next?*

The result is a user who has more data than ever but less clarity than expected. The
interpretation layer is missing. Data collection happens automatically; making sense of
it does not.

This is not a beginner-only problem. Even experienced cyclists with advanced hardware
report the same fragmentation frustration — the problem is structural, not a matter of
experience level.

---

### 1.2 Research — Verified Sources

All quotes below are sourced from real, publicly available posts. No synthesized or
fabricated quotes are used in this project (see SKILL.md, Protocol 7.2).

---

**Quote 1 — Beginner overwhelm (forum)**
> "I'm pretty new to cycling and recently started using a bike computer. I've noticed
> there are tons of metrics available — heart rate, power, cadence, speed, and more —
> and honestly, it's a bit overwhelming!"

Source: Road Bike Review forum
URL: https://www.roadbikereview.com/threads/looking-for-advice-which-cycling-metrics-should-i-focus-on.387260/

---

**Quote 2 — Overwhelm from day one**
> "I just started getting serious about cycling after years of casual rides...
> I was getting overwhelmed trying to track everything from day one."

Source: Cycling Unbound
URL: https://cyclingunbound.org/master-your-cycling-performance-the-10-essential-metrics-every-cyclist-should-track/

---

**Quote 3 — Expert framing**
> "The riders who improve track a small number of metrics consistently. The ones who
> stagnate track everything reactively — drowning in colourful graphs that tell them
> nothing useful."

Source: Roadman Cycling (July 2026)
URL: https://roadmancycling.com/blog/cycling-data-analysis-basics-guide

---

**Quote 4 — No clear progress view (Reddit)**
> "I'm struggling to find an app that clearly shows my performance evolution over time."

Source: Reddit r/cycling
URL: https://www.reddit.com/r/cycling/comments/1rvnjd5/whats_your_goto_app_for_analyzing_your_rides/

---

**Quote 5 — Social vs. training focus (Reddit, same thread)**
> "What are you guys using to see the 'big picture' of my training? Are there any
> hidden gems that focus on clean data visualization rather than just social
> leaderboards or basic summaries?"

Source: Reddit r/cycling
URL: https://www.reddit.com/r/cycling/comments/1rvnjd5/whats_your_goto_app_for_analyzing_your_rides/

---

### 1.3 Key Research Patterns

Four consistent patterns emerged from desk research and designer input:

1. **Fragmentation is structural.** The problem exists regardless of experience level.
   Apps are built around device ecosystems or social engagement — not around the user's
   understanding of their own progress.

2. **Social layers create noise.** Strava's community features (segments, kudos,
   leaderboards) pull attention away from personal training analysis. Users who want
   progress clarity find it actively distracting.

3. **Advanced tools have a steep entry cost.** Platforms like intervals.icu, Golden
   Cheetah, and TrainingPeaks are powerful but require sports science literacy to use
   effectively. They are not designed for beginners.

4. **The interpretation gap is the real problem.** Data collection is solved. Making
   that data meaningful — in plain language, at the right moment — is not.

---

### 1.4 Persona

**Name:** Alex (gender-neutral)
**Age:** Early 30s
**Location:** Mid-size European city
**Occupation:** Office worker, sedentary during the day

**Device setup:**
- Garmin Edge (entry-level) or similar cycling computer
- Occasional Strava use
- May also use Fitbit or similar for sleep and daily activity

**Goals:**
- Get fitter through cycling
- Understand if training is actually working
- Build enough confidence to join group rides eventually

**Behaviors:**
- Opens 2–3 apps after every ride without knowing what to look for
- Ignores heart rate zones because the concept is confusing
- Compares themselves to others on Strava and feels discouraged
- Has a scale at home but doesn't connect body metrics to training

**Frustrations:**
- Too much data, no interpretation
- Cannot see progress over time in a simple, readable way
- Does not know which metrics actually matter for a beginner
- Feels like they are doing something wrong, but can't pinpoint what

**Core quote:**
> "I have all this data but I still don't know if I'm doing this right."

---

### 1.5 How Might We Questions

Design opportunities derived from the problem statement and persona:

1. HMW help beginner cyclists understand their progress without requiring sports
   science knowledge?

2. HMW unify data from multiple sources without overwhelming the user with more
   complexity?

3. HMW make the onboarding experience set realistic expectations and meaningful goals?

4. HMW use AI to explain data in plain language at the right moment — not all at once?

5. HMW design a dashboard that feels personal and focused rather than generic
   and cluttered?

---

### 1.6 Scope Definition

**Core flow:**
Onboarding + first ride experience → unified cycling-focused dashboard

**Data sources:**
- Primary: Garmin Connect, Strava
- Secondary (TBC): Fitbit (sleep, resting HR), manual scale input
  (weight, body fat %, muscle %, bone %, water %)

**AI layer (in-product):**
- Guides onboarding and user profile/goal creation
- Explains data in plain language
- Surfaces what the user should pay attention to
- Does not replace medical or coaching advice

**Customization:**
Dashboard layout is customizable so users can prioritize their own relevant metrics.
HR monitoring is a secondary feature, not a default focus.

**Out of scope for now:**
- Social or community features
- Recovery as a core feature
- Sleep as a core feature (may appear as secondary data)

---

## Phase 2 — Define

> Status: Complete
> Sections: Competitive landscape, Information architecture, Core use cases,
> Success metrics

### 2.1 Competitive Landscape

#### The four main players for a beginner cyclist

---

**Garmin Connect**
The default companion app for Garmin devices. Offers the deepest training data available
in a consumer app — training load, VO2max estimates, acute-to-chronic balance, HR zones,
cadence, full multisport support. As of 2026, an optional Connect+ tier ($6.99/mo) adds
AI insights and nutrition tracking, but the core analysis remains free.

The problem for our target user: the app's data firehose and cluttered navigation
overwhelm casual users. One independent review (March 2026) summarized it directly:
for endurance and multisport athletes willing to learn the metrics, Garmin Connect is
the strongest training platform available. For everyone else, it is too much app.

Source: https://independent-app-reviews.org/reviews/garmin-connect-review/

User voices (Reddit, 2026):
> "The UX feels clunky and bloated. Navigation is frustrating, finding things isn't
> intuitive, and there's a pretty steep learning curve."
> — r/Garmin, Sep 2026 · https://www.reddit.com/r/Garmin/comments/1weestr/garmin_connect_app_sucks/

> "I've learned from a friend that the last revamp of the iOS app was a major UX downgrade."
> — r/Garmin, Sep 2026 · https://www.reddit.com/r/Garmin/comments/1weestr/garmin_connect_app_sucks/

**Gap for our product:** Garmin Connect is built for depth, not for onboarding or
interpretation. A beginner lands in it after buying a device and is immediately
confronted with a firehose of metrics with no guidance on what matters.

---

**Strava**
The dominant social and discovery layer for running and cycling. Segment leaderboards,
route discovery, and social feed are best-in-class for motivation. The subscription
(~$11.99/mo or $79.99/yr) is required for the features most users come for.

The problem for our target user: Strava is best for intermediate athletes who value
data tracking over personalized instruction. The social layer is a feature — but it
pulls attention away from personal progress analysis, which is what a beginner needs.
Beginners wanting personalized guidance are explicitly listed as users Strava is not
suited for.

Source: https://independent-app-reviews.org/reviews/strava-review/
Source: https://barbend.com/strava-app-review/

User voices (Reddit, 2024–2026):
> "Seems like this is the most confusing metric. Anyone care to spend a minute to
> explain it to this noob?"
> — r/Strava, Jun 2026 · https://www.reddit.com/r/Strava/comments/1uc3to2/fitness_score/

> "this type of data stuff can very easily get overwhelming"
> — r/Strava, Mar 2024 · https://www.reddit.com/r/Strava/comments/1bb76qs/strava_data_vs_actual_progress/

> "Strava's fitness graph does not track fitness but chronic training load"
> — r/Strava, Aug 2026 · https://www.reddit.com/r/Strava/comments/1vj6xoc/more_confirmation_that_the_fitness_graph_is/

**Gap for our product:** Strava excels at community and motivation but does not explain
data or guide improvement. Subscription cost is hard to justify for a beginner not
using social features.

---

**intervals.icu**
Free (optional $4/mo supporter tier). Built by David Tinker (developer and cyclist,
Cape Town), grown from a Strava analysis side project in 2018 to 160,000+ active
athletes and 193M+ analyzed activities. Fitness chart, power curve, and interval
detection rival software costing hundreds of euros per year.

The problem for our target user: the interface requires a real learning curve. Built
explicitly for self-coached, data-savvy athletes. Power users can write JavaScript
inside the platform to compute custom metrics — a signal of how far from
beginner-friendly it is.

Source: https://coachbox.app/en/compare/intervals-icu-review/

User voices (Reddit, 2024):
> "I really dislike intervals' interface (even as a decade long wko user)."
> — r/Velo, Oct 2024 · https://www.reddit.com/r/Velo/comments/1g15v81/

> "The interface looks decent on intervals, although bits are a bit cluttered."
> — r/Velo, Oct 2024 · https://www.reddit.com/r/Velo/comments/1g15v81/

**Gap for our product:** intervals.icu solves data depth for advanced users but creates
a new barrier for beginners. No onboarding, no plain-language explanation, no
guided experience.

---

**TrainingPeaks**
Industry standard for coached athletes. Strong fitness/fatigue/form tracking, structured
workout planning, coach marketplace with 70,000+ plans and 35+ federation partnerships.
Notable: as of July 2026, Garmin has acquired TrainingPeaks and TrainHeroic from
Peaksware Holdings.

The problem for our target user: designed around the coach-athlete relationship.
Without a coach, a beginner is navigating a professional tool without a guide.

Source: https://coachbox.app/en/compare/intervals-icu-vs-trainingpeaks/

User voices (Reddit, 2026):
> "Intervals.icu eats TP for lunch all day, every day."
> — r/triathlon, Feb 2026 · https://www.reddit.com/r/triathlon/comments/1qv49ln/ditching_trainingpeaks_for_intervalsicu_with_a/

**Gap for our product:** assumes a coaching context most beginners don't have.

---

#### Competitive gap summary

| | Garmin Connect | Strava | intervals.icu | TrainingPeaks |
|---|---|---|---|---|
| Beginner-friendly | ✗ | Partial | ✗ | ✗ |
| Unified data view | Partial | ✗ | ✓ | ✓ |
| Plain-language explanations | Partial (Connect+) | ✗ | ✗ | ✗ |
| AI-guided onboarding | Partial (Connect+) | ✗ | ✗ | ✗ |
| Customizable dashboard | ✗ | ✗ | ✓ | Partial |
| Free core tier | ✓ | Partial | ✓ | ✗ |
| Social layer | ✗ | ✓ | ✗ | ✗ |

**The white space:** No current tool combines beginner-friendly onboarding, plain-language
data explanation, and a unified view of progress. That is the gap this product fills.

---

### 2.2 Information Architecture

The app is organized into 6 top-level areas. Onboarding runs once on first launch and
gates entry to the rest of the app. All other areas are accessible via bottom navigation
(mobile) or sidebar (desktop).

---

```
App
├── Onboarding (first launch only)
│   ├── Welcome screen
│   ├── Profile setup (name, age, fitness level)
│   ├── Goal setting (AI-guided: "What do you want from cycling?")
│   ├── Device connection (Garmin Connect, Strava)
│   ├── Optional: Fitbit connection
│   ├── Optional: Body data setup (manual scale input)
│   └── First ride prompt / dashboard preview
│
├── Dashboard (Home)
│   ├── Greeting + AI insight of the day
│   ├── Last ride snapshot (date, distance, duration, avg HR)
│   ├── Weekly summary (rides, total distance, consistency streak)
│   ├── Progress highlight (e.g. "Your avg speed improved 4% this month")
│   ├── Body snapshot (weight trend, optional — if activated)
│   └── Customizable widget area (user picks what appears here)
│
├── Ride Detail
│   ├── Map / route (if GPS data available)
│   ├── Key metrics (distance, duration, elevation, avg/max speed)
│   ├── Heart rate breakdown (zones, avg, max) — plain language label
│   ├── Cadence (if available)
│   ├── AI explanation ("What does this ride tell you?")
│   └── Compare to previous similar ride
│
├── Progress
│   ├── Fitness trend (weekly/monthly view)
│   ├── Distance over time
│   ├── Heart rate trend (resting HR + ride HR)
│   ├── Consistency tracker (rides per week)
│   ├── Personal bests
│   └── Goal progress (vs. goal set in onboarding)
│
├── Body (optional, activated in settings)
│   ├── Weight trend
│   ├── Body composition (fat %, muscle %, water %, bone %)
│   ├── Resting HR trend (from Fitbit, if connected)
│   ├── Sleep summary (from Fitbit, if connected)
│   └── Correlation hint ("On weeks you slept 7h+, your avg speed was higher")
│
└── Settings / Profile
    ├── Personal profile (name, age, goals)
    ├── Connected apps (Garmin, Strava, Fitbit)
    ├── Dashboard customization (show/hide widgets)
    ├── Units (km/mi, kg/lb)
    ├── HR zone configuration
    └── Notification preferences
```

---

### 2.3 Core Use Cases

Three primary use cases cover the jobs to be done for the target user.

---

**Use case 1 — First-time setup**
User gets a new cycling device and wants to start tracking progress meaningfully.
They connect their apps, set a goal, and get a dashboard that makes sense from day one.

Steps: connect Garmin/Strava → set goal → see first dashboard state

Maps to HMW 3: *How might we make the onboarding experience set realistic expectations
and meaningful goals?*

---

**Use case 2 — Post-ride check-in**
User finishes a ride and opens the app to understand what happened. They want to know
if the ride was good, what their heart rate means, and whether they're improving.

Steps: open app → see last ride snapshot → read AI explanation → compare to previous ride

Maps to HMW 1 + 4: *How might we help beginners understand their progress without sports
science knowledge? How might we use AI to explain data at the right moment?*

---

**Use case 3 — Weekly progress review**
User checks in once a week to see if they're moving in the right direction.
They want a simple answer: am I getting fitter?

Steps: open Progress section → see trend → read AI summary → adjust goal if needed

Maps to HMW 2 + 5: *How might we unify data without overwhelming the user? How might
we design a dashboard that feels personal and focused?*

---

### 2.4 Success Metrics

#### A — User outcomes
What the user experiences if the product is working.

- User can explain what their last ride data means without external help
- User knows whether they are improving week over week without opening another app
- User completes onboarding and reaches the dashboard in a single session
- User returns to the app after their next ride (not just after setup)
- User feels the dashboard reflects their priorities, not a generic default

---

#### B — Product metrics
What would be measured if this were a live product.

| Metric | Target | Rationale |
|---|---|---|
| Onboarding completion rate | >80% | Indicates setup flow is not too long or confusing |
| Day-7 retention | >50% | User returned after at least one ride post-setup |
| AI explanation interaction rate | >60% per ride | Users are reading the AI layer, not ignoring it |
| Dashboard customization rate | >30% | Users are making it their own |
| Body section activation rate | >20% | Optional feature being discovered and used |
| Sessions per week (active users) | 2+ | Correlates with at least 1–2 rides reviewed per week |

---

> **Note for portfolio:** Metric targets above are design hypotheses, not validated
> numbers. In a real product these would be set with a PM based on baseline data.
> They are included here to demonstrate product thinking alongside UX process.

---

- **Onboarding is a gate, not optional.** The AI needs a minimum profile to give
  meaningful insights. Users cannot skip it, but it is kept short (under 5 steps).

- **Body is opt-in.** Activated in Settings, not shown by default. Avoids overwhelming
  users who only want cycling data.

- **Dashboard is customizable.** Users control which widgets appear. Default state
  shows the most universally useful data (last ride, weekly summary, AI insight).

- **Ride Detail surfaces AI explanation at the bottom.** Not the first thing the user
  sees — they see their data first, then the interpretation. Avoids the app feeling
  like it's talking at the user.

- **Progress is a dedicated section, not buried in Dashboard.** One of the core jobs
  to be done is "show me if I'm improving" — it deserves its own space.

---

## Phase 3 — Design

> Status: Complete — every screen in the app is built (Dashboard, Ride detail,
> Rides list, Progress, Body, Settings, and the full 7-screen onboarding flow).
> Next: Phase 4 (AI Integration) and Phase 5 (Validation) are still pending,
> plus the overall design + flow review noted in Future Deliverables below.

### 3.1 UI Style Definition

**Style name:** Measured
**Feeling:** Calm, precise, confidence through restraint
**Mode:** Light only
**Platform:** Desktop + mobile (responsive)

---

#### Color palette

| Role | Name | Hex |
|---|---|---|
| Background | Chalk | `#F5F4F0` |
| Surface (cards / tiles) | Off-white | `#FAFAF8` |
| Border / divider | Stone | `#E2E0D9` |
| Body text | Slate | `#2E2E2E` |
| Secondary text | Ash | `#8A8880` |
| Accent | Muted Violet | `#6B5B8C` |
| Accent light (hover / tint) | Violet Mist | `#EDE9F4` |

**Accessibility note:** All text/background combinations meet WCAG 2.1 AA contrast
minimum (4.5:1 for body text, 3:1 for large text). Slate on Chalk = 10.2:1.
Accent violet is used for borders and highlights only — never as a background for
body text. Color is never the sole means of conveying information.

---

#### Typography

| Role | Typeface | Weight | Size scale |
|---|---|---|---|
| Headings (H1–H3) | DM Sans | 600 | 32 / 24 / 18px |
| Body text | DM Sans | 400 | 15px, 1.6 line-height |
| Labels / secondary | DM Sans | 400 | 13px |
| Data values (large metrics) | DM Mono | 400 | Context-dependent |

- Single family (DM Sans) + one monospace variant (DM Mono) for metric values
- No ALL CAPS labels
- Sentence case throughout
- Line length capped at 72 characters for body text
- Minimum font size: 13px (never smaller — accessibility)

---

#### Layout

**Desktop:**
- Top pill navigation (in the topbar, between logo and avatar) + full-width
  main content area — see Decision Log, 2026-09-21
- Content max-width: 1200px, centered
- Base grid: 12 columns, 24px gutters
- Dashboard uses bento grid — tiles vary in size by content importance

**Mobile:**
- Bottom navigation bar (5 items max)
- Single column layout
- Bento grid collapses to stacked tiles
- Touch targets minimum 44x44px (WCAG 2.5.5)

**Bento grid tile sizes (dashboard):**
- Large tile (2/3 width): Last ride snapshot
- Medium tile (1/3 width): Weekly summary
- Full-width strip: AI insight of the day
- Small tiles (1/3 or 1/2 width): Body snapshot, consistency streak, goal progress
- User can show/hide tiles — customization maps directly to bento layout

---

#### Component rules

- **Borders, not shadows.** `1px solid #E2E0D9` on all cards and tiles.
  No box-shadow anywhere.
- **Border radius:** 6px on tiles and cards. 4px on tags and chips. 0px on
  full-width containers.
- **Data values are always larger than their labels.** Number is the hero.
- **Padding inside tiles:** minimum 20px (mobile), 24px (desktop).
- **No gradients, no glassmorphism, no decorative illustration.**
- **No icons used as sole navigation labels** — always paired with text
  (accessibility).
- **Focus states:** visible keyboard focus ring using accent violet outline
  (`2px solid #6B5B8C`, 2px offset) on all interactive elements.
- **Reduced motion:** animations respect `prefers-reduced-motion`. No
  auto-playing motion. Transitions max 200ms where used.

---

#### AI layer visual treatment

- Left border: `3px solid #6B5B8C` (muted violet)
- Background: Off-white (`#FAFAF8`) — same as cards, no distinction
- Text: Ash (`#8A8880`) — quieter than primary content
- No "AI" label, no robot icon, no chat bubble
- Never interrupts a flow — always appears after the user has seen their data
- Principle: quiet copilot, not a feature announcement

---

#### What this style is NOT

- No gradients
- No glassmorphism or frosted panels
- No shadows
- No decorative illustration or iconography as decoration
- No ALL CAPS labels
- No colored section backgrounds
- No emojis in UI copy
- No generic SaaS card kit (identical rounded cards, same shadow everywhere)

---

#### Accessibility standards

- WCAG 2.1 AA compliance minimum throughout
- Keyboard navigable — all interactive elements reachable and operable via keyboard
- Focus indicators visible on all interactive elements
- No content conveyed by color alone — always paired with text or shape
- Touch targets minimum 44x44px on mobile
- Semantic HTML structure (headings hierarchy, landmark regions, ARIA labels
  where needed)
- Reduced motion support via `prefers-reduced-motion`
- Minimum contrast ratios enforced across all text/background pairs

---

#### Reference sources

- Cassette Music (cassettemusic.com) — editorial confidence, whitespace, typography
- Box Box Club (Mobbin) — cycling data card layout, personality within structure
- Oura (Mobbin) — calm health dashboard, muted tones, data hierarchy
- Notion — structural clarity, no decoration (referenced as touch, not copied)

---

### 3.2 Core Flows

> Reminder: flows 2 (post-ride check-in) and 3 (weekly progress review) are pending.
> Map after onboarding flow is complete.

---

#### Flow 1 — Onboarding

**Use case:** First-time user sets up the app to start tracking meaningful progress.
**Entry point:** App opened for the first time (no account, no data).
**Exit point:** Dashboard — either fully set up, or partially set up with resume banner.

---

##### Design decisions

- Onboarding is skippable at any point after step 1 (account creation is required)
- Skipped onboarding shows a persistent setup banner on the dashboard
- Banner resumes from last completed step, not from step 1
- Progress is persisted — each completed step is saved immediately
- Most features are locked until onboarding is complete; locked items show a
  subtle "finish setup" prompt, not a generic error
- Max steps: 5 (aligns with Phase 2 IA decision)
- OAuth connection is real-flow (login, permissions screen) — not simulated

---

##### Flow steps

**Step 0 — Welcome screen**
- App name + one-line value proposition
- Two CTAs: "Get started" / "I already have an account"
- No skip option here — account is required for any functionality
- Accessible: no auto-advancing, no timed content

---

**Step 1 — Account creation**
- Email + password (or "Continue with Google")
- Minimal fields: name, email, password
- No profile photo, no bio, no extras
- Progress indicator visible: step 1 of 5
- First point where "Skip setup" becomes available (top right, low emphasis)
- Skip state: account is saved, user lands on empty dashboard with setup banner

---

**Step 2 — Basic profile**
- Heading: "A few basics"
- Short explanation: these fields power calculations elsewhere in the app —
  not shown as a public profile, no other users
- Fields: height, age, gender identity, sex assigned at birth,
  hormone therapy status

- Why each is needed (design rationale — not shown verbatim as a wall of
  text, summarised in a "why we ask" note):
  - **Height** — required for BMI and calorie-burn estimates from ride data
  - **Age** — required for max heart rate estimation, used to interpret
    HR zones from Garmin/Strava data
  - **Gender identity** — how the user identifies; used for tone and
    personalisation of AI copy. Not used in physiological calculations.
  - **Sex assigned at birth** — used for body-fat % healthy range context
    and calorie-burn formulas (Harris-Benedict / Mifflin-St Jeor). Labelled
    clearly as "used for heart rate zones and calorie estimates" so users
    understand why it's asked.
  - **Hormone therapy** — if yes, a contextual note explains that their
    doctor is best placed to advise which sex to select for accurate
    calculations; app does not assume or override

- Gender identity options: Woman / Man / Non-binary / Genderfluid /
  Prefer to self-describe (free text) / Prefer not to say
- Sex assigned at birth options: Female / Male / Intersex /
  Prefer not to say
- Hormone therapy options: Yes / No / Prefer not to say
  - If "Yes": inline note appears — "For the most accurate calculations,
    ask your doctor which sex to select based on where you are in your
    transition."

- All fields required to proceed — but every field has a "Prefer not to
  say" option, so no one is forced to disclose
- Best practice source: two-step gender identity + sex assigned at birth
  approach established by national LGBTQIA+ advocacy organisations (CDPH
  SOGI Guidance 2025). Hormone therapy context informed by MyFitnessPal's
  published approach and digital health equity research (PMC 2025).
- Skip option remains available at this step

---

**Step 3 — Connect your data source**
- Heading: "Where does your ride data live?"
- Three options displayed as selectable tiles:
  - Garmin Connect
  - Strava
  - Both
- Selecting triggers real OAuth flow in a modal or new tab:
  - Login to provider
  - Permissions screen (read activity data, read profile)
  - Return to app on success
- On success: confirmation state shown inline ("Garmin connected ✓")
- If OAuth fails: inline error with retry option — never a dead end
- Skip option remains available — data source can be connected later via Settings
- Accessibility: tiles have visible selected state (violet border + checkmark),
  not color-only

---

**Step 4 — Set your goal**
- Heading: "What are you working towards?"
- Two modes, toggled by segmented control:
  - **Preset goals** (default): 4–5 options as selectable cards
    - "Ride consistently" (e.g. 3x per week)
    - "Build endurance" (e.g. complete a 40km ride)
    - "Lose weight"
    - "Just explore" (no specific metric goal)
  - **Custom goal**: free text field + optional metric (distance, frequency, or weight)
- User selects one goal only (radio behavior)
- Goal is used to personalize dashboard tile priority and AI insight framing
- Skip option remains available — goal can be set later via Settings

---

**Step 5 — Optional: body data**
- Heading: "Want to track how your body changes?"
- Short explanation: see weight and body composition alongside ride data
- Three equal-weight options (radio behavior):
  - **Connect a smart scale** — reveals a dropdown of supported models
    (Fitbit Aria 2, Fitbit Aria Air, Withings Body+, Withings Body Comp,
    Garmin Index S2, Xiaomi Mi Body Scale 2). Selecting a model triggers
    the OAuth flow for that provider.
  - **Enter data manually** — reveals inline fields (weight, body fat %,
    muscle %, bone, water %), all optional, so the user can add what they
    have now
  - **I'll do this later** — same visual weight as the other two, no
    guilt framing
- Body section in dashboard remains hidden until data exists (not empty,
  not broken — simply not shown) — applies whether skipped or deferred
- CTA: "Next"

---

**Step 6 — You're set**
- Confirmation screen: "You're ready to ride."
- Summary of what was connected (data source, goal, body data if applicable)
- Single CTA: "Go to my dashboard"
- No confetti, no excessive celebration — calm confirmation consistent with style

---

##### Skip state — dashboard with resume banner

When user skips at any point after step 1:

- Dashboard loads immediately in empty state
- Empty tiles show placeholder illustration + short copy:
  - Last ride tile: "Your first ride will appear here"
  - Weekly summary: "Ride this week to see your progress"
  - AI insight strip: "Connect a data source to get insights"
  - Body snapshot: hidden until connected (not shown as empty)
- Setup banner appears at the top of the dashboard (below nav, above bento grid):
  - Copy: "Finish setting up to unlock all features."
  - CTA: "Continue setup" → resumes from last completed step
  - Dismiss option: "X" to hide for this session (banner returns on next login
    until setup is complete)
- Locked features show inline prompt on hover/tap: "Finish setup to unlock this"
- Banner disappears permanently once all steps are completed

---

##### Accessibility notes (flow-specific)

- Progress indicator uses both position ("Step 2 of 5") and a visual stepper —
  not color alone
- OAuth modal/tab: focus is trapped in modal while open; returns to trigger
  element on close
- All form fields have visible labels (not placeholder-only)
- Error messages are associated with their fields via `aria-describedby`
- Skip link is keyboard accessible and clearly labeled ("Skip setup for now")
- Empty state illustrations are decorative — `alt=""` / `aria-hidden="true"`
- Confirmation screen announces completion to screen readers via `aria-live`

---

##### HMW mapping

- HMW 3: Onboarding sets realistic expectations and meaningful goals →
  addressed by goal-setting step (preset + custom) and calm confirmation screen
- HMW 1: Help beginners understand progress without sports science knowledge →
  addressed by AI insight placeholder copy even in empty state
- HMW 4: Use AI to explain data at the right moment →
  AI insight strip is present from day one, even if empty, so the pattern
  is established before the first ride

---

#### Dashboard — empty state

Wireframed. Shown immediately after onboarding completion.

**Layout:** top pill nav in the topbar (Dashboard, Rides, Progress, Body,
Settings) + full-width main content area with bento grid.

**Bento tiles in empty state:**
- Last ride (large, 2/3 width): icon + "Go for a ride with your Garmin
  and sync to see your data." Title removed — copy is the invitation.
- This week (1/3 width): "0 of 3 rides" with goal progress bar at zero —
  goal is live from day one even before any data exists
- AI insight strip (full width, violet left border): explains what the
  strip will do once data arrives — no jargon, no filler
- Streak: "0 days — Ride today to start your streak."
- Body: "No data yet — your scale will sync after your next weigh-in."
- Goal: echoes the goal chosen in onboarding ("Ride consistently —
  3 rides a week. Let's go.")

**Design decisions:**
- Personalised greeting uses name from account creation ("Good morning, Alex.")
- Body tile is visible but shows empty state — body section is never hidden
  after scale is connected during onboarding; hidden only if user deferred
  body data entirely
- Pill nav items: color `#4A4A4A` (medium-dark gray) at rest, violet with
  filled tint background when active

---

#### Flow 2 — Post-ride check-in

**Use case:** user finishes a ride and opens the app to understand
what happened.

**Entry point:** Dashboard (populated, last ride tile visible).
**Exit point:** Ride detail screen, after reading AI interpretation.

**Screens:**

**Screen 1 — Populated dashboard**
- Last ride tile (large): shows ride name, time, and three key metrics —
  distance, duration, avg HR. Below that, a time-in-zone chart (Z1–Z5,
  % of ride time per zone) compared against the ride's goal, if one was
  set. CTA: "See full ride"
- Ride goal (Endurance / Tempo / Threshold training / VO2 max) is optional
  and per-ride — if unset, an inline prompt asks for it with a one-line
  plain-language explanation per option; "Not sure" dismisses it without
  blocking the chart. See Decision Log, 2026-09-21.
- This week tile: progress bar updated (1 of 3 rides)
- AI insight strip: one-sentence teaser drawn from the ride — draws user
  into the detail screen without giving everything away
- Body tile: shows latest weight + delta vs previous entry
- Streak and goal tiles updated with current state

**Screen 2 — Ride detail**
- Back navigation: "← Dashboard"
- Ride title + metadata: date, time, source (Garmin Connect)
- **Activity section (first):** distance, duration, avg speed, elevation,
  avg cadence, calories — 2-row grid, values large, labels small
- **Heart rate section (second):** avg HR, max HR, heart rate over time
  (line + area chart, hover for time/bpm at any point). Zone distribution
  now lives on the Dashboard's Last ride tile instead (see Decision Log,
  2026-09-21) — Ride detail shows the raw trace, Dashboard shows the
  zone summary vs. goal
- **"What this ride means" section (last):** AI block with violet left
  border, labelled "Interpretation" — never the first thing seen.
  Explains zone in plain language, gives one actionable suggestion
  (cadence), confirms pacing. Ends with comparison pills:
  "↑ 2.1 km vs last ride" / "HR similar to last ride"

**Key UX decisions:**
- Data always precedes interpretation — user scrolls through raw numbers
  before reaching the AI block
- AI block is labelled "What this ride means" at section level, and
  "Interpretation" inside the block — two plain-language signals, no
  "AI" label
- Comparison pills anchor insight to progress, not just the single ride
- HR zones shown as a visual bar, not a table — a beginner can see
  at a glance where they spent the ride

**HMW mapping:**
- HMW 1: help beginners understand progress without sports science →
  zone explanation in plain language, cadence explained as a knee-stress
  concept, not a performance metric
- HMW 4: use AI to explain data at the right moment →
  AI block appears only after user has seen all raw data; never first

---

#### Flow 3 — Weekly progress review

**Use case:** user checks in once a week to see if they're improving.

**Entry point:** Progress section (sidebar nav).
**Exit point:** Goal adjustment (optional) at the bottom of the page.

**Screen — Progress page**

**Period toggle:** 4 weeks / 8 weeks (default) / 3 months.
User controls the time window. 8 weeks is default — long enough to
show a trend, recent enough to feel relevant.

**Summary cards (4, top of page):**
- Total rides — with delta vs previous period
- Total distance (km) — with delta
- Avg HR (bpm) — delta shown; context provided in chart below
- Longest ride (km) — with delta

**Rides per week bar chart:**
- Each bar = one week. Goal line implicit via section label ("Goal: 3 rides")
- Violet bars = goal met. Gray bars = missed or in progress.
- Current week is faded to signal it is incomplete
- Legend in plain text below chart — no icon key

**Avg HR trend line chart:**
- Single descending line over the period
- Values labelled directly on chart (start and end points)
- Trend label below in plain language: "↓ 7 bpm over 8 weeks —
  your heart is getting more efficient." Uses green color for positive
  framing — lower HR is a fitness gain, not a problem despite the ↓

**AI weekly summary (after both charts):**
- Ties both charts together in plain language
- Acknowledges missed weeks without framing as failure
- Notes current week is still in progress
- No label beyond "This week's summary" — consistent AI layer treatment

**Goal adjustment (bottom of page):**
- Shows current goal
- Four chips: Keep 3x/week / Increase to 4x/week / Shift to distance /
  Change goal type
- Selected chip highlighted in violet
- Adjustment happens inline — no Settings navigation required

**Key UX decisions:**
- Avg HR delta (↓) appears red in the summary card — intentionally
  corrected immediately below in the chart with a green trend label.
  This is a deliberate sequence: raw number first, meaning second,
  consistent with the AI-last principle
- Period toggle lets user self-select their window — respects that
  different users assess progress at different cadences
- Goal adjustment at the bottom of progress page (not buried in Settings)
  — a user reviewing their progress is exactly the right moment to
  reconsider their goal

**HMW mapping:**
- HMW 2: unify data without overwhelming → two focused charts, four
  summary numbers, one AI paragraph. No data dump.
- HMW 5: dashboard feels personal and focused → goal adjustment inline,
  period toggle, personalised AI summary referencing their specific goal

---

## Phase 4 — AI Integration

> Status: Pending
> Will cover: Definition and documentation of AI layer behavior within the product.

---

## Phase 5 — Validation

> Status: Pending
> Will cover: Proposed validation method (survey, usability test, or other).

---

## Decision Log

| Date | Decision | Rationale |
|---|---|---|
| 2026-08-20 | No Figma — prototype in Claude Code only | Demonstrates AI tooling skills for portfolio |
| 2026-08-20 | No survey in workflow | Replaced by designer inputs + verified community research |
| 2026-08-20 | HR monitoring = secondary feature | Not universal; dashboard is customizable |
| 2026-08-20 | Skill file format: SKILL.md | Installable as Claude skill, session context |
| 2026-09-14 | PROJECT.md = working doc; case study = separate future deliverable | Keeps documentation focused |
| 2026-09-14 | Body section confirmed in scope | User wants weight/composition snapshot on dashboard |
| 2026-09-14 | Fitbit confirmed as secondary data source | Sleep + resting HR included if user activates |
| 2026-09-14 | Phase 1 complete | Problem statement, persona, HMW, research finalized |
| 2026-09-14 | Phase 2 complete | Competitive landscape, IA, use cases, metrics finalized |
| 2026-09-14 | Style: "Measured" — light mode only, Chalk bg, Muted Violet accent | Calm, precise aesthetic aligned with 2026 UI trends |
| 2026-09-14 | Bento grid adopted for dashboard layout | Content hierarchy + customization mapped to tile size |
| 2026-09-14 | AI as quiet copilot — explicit design principle | Established after 2026 UI trend research |
| 2026-09-14 | Glassmorphism explicitly excluded | Conflicts with calm aesthetic despite 2026 trend |
| 2026-09-17 | Onboarding is skippable but resumes from last completed step | Best UX — respects user time, reduces anxiety |
| 2026-09-17 | Onboarding split into 5 steps (was 4) | Height, age, gender identity, sex assigned at birth, hormone therapy added as step 2 |
| 2026-09-17 | Two-step gender/sex approach | Best practice per CDPH SOGI Guidance 2025 — gender identity and sex assigned at birth are distinct |
| 2026-09-17 | Hormone therapy question is conditional | Only shown when gender identity and sex assigned at birth do not clearly match |
| 2026-09-17 | Scale brand not predefined — dropdown of options | More realistic and inclusive; supports Fitbit, Withings, Garmin, Xiaomi |
| 2026-09-17 | "Enter data manually" includes inline body fields | User can log current data during onboarding without a scale |
| 2026-09-17 | Empty dashboard: body tile visible if scale connected, hidden if deferred | Avoids broken-looking dashboard |
| 2026-09-17 | AI block always appears after raw data, never before | Core product principle — data first, interpretation last |
| 2026-09-17 | Phase 3 wireframes complete — all 3 flows | Onboarding, post-ride check-in, weekly progress review |
| 2026-09-17 | Prototype format: HTML + CSS + vanilla JS | No framework needed; cleaner for portfolio handoff |
| 2026-09-17 | CLAUDE.md created | Encodes design system rules for Claude Code sessions |
| 2026-09-17 | Model for prototype build: Claude Sonnet 5 | Best price/performance for coded prototype work |
| 2026-09-21 | Desktop nav: top pill nav in topbar, replacing sidebar | Requested during index.html build; sidebar spec was default-generic, pill nav fits "Measured" editorial style better. Applies to all future desktop screens, not just Dashboard |
| 2026-09-21 | Dashboard (index.html) built — populated state | Last ride, this week, insight, streak, body, goal tiles; desktop pill nav + mobile bottom nav |
| 2026-09-21 | Dashboard's Last ride tile shows time-in-zone vs. goal, not the HR-over-time chart | Time-series HR chart moved to Ride detail (rides/detail.html) where it belongs with the full data; overview needed a summary view instead |
| 2026-09-21 | New concept: per-ride goal (Endurance / Tempo / Threshold training / VO2 max), distinct from the onboarding app-level goal | Lets the zone chart compare actual time-in-zone against ride intent. Optional — prompted inline on the dashboard when unset, skippable via "Not sure", re-offered via "Add a ride goal" |
| 2026-09-21 | Ride detail (rides/detail.html) built | Back nav, Activity grid, Heart rate section (reused HR-over-time chart with hover), "What this ride means" AI block with comparison pills — per Flow 2 spec |
| 2026-09-21 | Time-in-zone chart rebuilt as a single stacked bar (was 5 stacked rows) | Saves vertical space in the Last ride tile; matches the reference layout the designer supplied (% labels above, Z1–Z5 codes below, one expanded zone name) |
| 2026-09-21 | Added categorical zone colors (--zone-1…--zone-5) to tokens.css, one exception to the single-accent rule | Zones are an identity/categorical encoding (5 fixed, ordered categories), which per the dataviz color method calls for distinct hues, not the single-accent restraint that governs UI chrome. Z3 reuses the brand accent so the "main effort" zone anchors the palette |
| 2026-09-21 | Zone colors saturated further; zone bar height cut 28px → 14px | Designer feedback: zones weren't distinct enough at a glance, and the bar should take up less vertical space |
| 2026-09-21 | Removed the shared "legend" line under the goal-focus prompt; per-option explanations moved to a native title tooltip on each button instead | Designer feedback: no persistent legend once the prompt is showing |
| 2026-09-21 | Goal result replaced with a real insight (violet-bordered, "Insight" label) comparing the chosen goal's zone % against the ride's actual dominant zone | Designer feedback: the payoff should be an insight (goal vs. actual heart rate zone), not a flat "Goal: X" statement |
| 2026-09-21 | Zone/goal copy (talk-test descriptions per zone) sourced from veloi.app's "Power Zones Explained" article, linked from the training-methods article the designer supplied | Replaces earlier made-up copy with grounded, accurate zone descriptions; paraphrased, not quoted |
| 2026-09-21 | Last ride's Distance/Duration/Avg heart rate scaled up (22px → 28px, scoped to that tile only) | Designer feedback: highlight the ride's core stats now that the tile also carries the zone chart and goal prompt |
| 2026-09-21 | Micro brightness-pulse animation on the matched zone segment + fade-in on its expanded label when a ride goal is picked | Designer feedback: the chart should visibly react to the goal selection, not just swap text. Kept to filter/opacity/transform and wrapped in the existing prefers-reduced-motion guard |
| 2026-09-21 | Progress page (progress/index.html) built — Flow 3 | Period toggle (4wk/8wk/3mo, fully data-reactive incl. summary cards), 4 summary cards, rides-per-week bar chart (violet=goal met, gray=missed, current week faded), avg-HR trend chart (JS-rendered per period, no hardcoded SVG), "This week's summary" AI block, goal-adjustment chips. AI summary paragraph is written for the 8-week default and does not reactively regenerate per period — a deliberate scope trim (see rationale below) |
| 2026-09-21 | Added --color-positive/--color-negative status tokens to tokens.css | Needed for delta framing (rides/distance/longest = green when up; avg HR delta shown red at the summary-card level on purpose, then corrected to green with plain-language context in the trend chart below — demonstrates the "raw data first, AI context second" principle at the page level, per the original Flow 3 spec's "Key UX decision" |
| 2026-09-21 | Design QA pass on Progress page, 8 findings fixed | (1) Added aria-live="polite" status region announcing period-toggle changes — CLAUDE.md accessibility rule #8 was unmet. (2) Missed-goal bars recolored from --color-border-mid to --color-text-muted (fill and border both) — the original pair computed to ~1.6:1 and ~1.3:1 against the card surface, both failing WCAG 1.4.11's 3:1 non-text minimum; the border was also lighter than its own fill. (3) .metric-label switched from --color-text-muted to --color-text-sub on this page (~3.4:1 → ~6.9:1) — the same low-contrast pattern exists on index.html and rides/detail.html but wasn't in scope for this page's QA; flagged for a follow-up pass. (4) Delta colors and the HR trend sentence were hardcoded rather than derived from the data's sign — refactored so color and copy ("more efficient" vs "worth keeping an eye on") are computed from the actual delta each render; verified both branches. (5) Renamed .tile-delta to .stat-delta on this page — it shared a name with index.html's differently-styled .tile-delta (13px/gray vs 12px/color-coded), a false-equivalence across pages with no shared stylesheet. (6) Removed "This week is still in progress" from the chart legend — it was duplicated verbatim in the AI summary paragraph. (7) Shortened the Avg heart rate card's delta copy ("over the past 8 weeks" → "over 8 weeks") — it was the only one of four cards wrapping at an awkward mid-phrase break. (8) Replaced 7 instances of inline unit styling (13px) with a shared .metric-unit class matching the 12px convention already established on the other two pages |
| 2026-09-21 | Onboarding Step 0 — Welcome (onboarding/welcome.html) built | Centered layout, no nav, max-width 480px per CLAUDE.md. Logo + one-line value prop + two CTAs ("Get started" → account.html, "I already have an account" → dashboard, simulating login since no auth flow is in scope). No progress stepper — spec has the stepper start at Step 1 (Account). Headline kept at the documented 20px/700 h1 size rather than a one-off larger "hero" size, since CLAUDE.md's type scale doesn't carve out an onboarding exception |
| 2026-09-21 | Onboarding Step 1 — Account (onboarding/account.html) built | 5-dot stepper (step 1 active) + "Step 1 of 5 — Account" text line, satisfying PROJECT.md's "position + visual, not color alone" rule. Pending-dot number color deviates from CLAUDE.md's literal --color-text-muted spec to --color-text-sub (same 11px-muted-on-white contrast fix applied twice already this project). Real `<form>` with native HTML5 validation (required, type=email, minlength=8) — JS only intercepts submit after validation passes, navigating to profile.html. "Continue with Google" jumps straight to profile.html (no fake OAuth modal for this step — real-flow OAuth is only spec'd as required for Step 3's data-source connection). "Skip setup" links to the populated dashboard as a stand-in for the not-yet-built empty-state-with-resume-banner |
| 2026-09-21 | Onboarding Step 2 — Profile (onboarding/profile.html) built | Height/age as required number inputs (no "prefer not to say" — that option only applies to the gender/sex/hormone fields per spec). Gender identity, sex assigned at birth and hormone therapy built as real `<fieldset>`/radio groups styled as selectable tiles (violet border + tint + checkmark on selection, not color alone), not the aria-pressed button pattern used elsewhere — these are genuine form fields and needed native label/fieldset/radiogroup semantics. Hormone therapy fieldset is conditionally shown only when gender + sex suggest it's relevant (non-binary/genderfluid/self-describe, or a woman/man selection that doesn't match the corresponding sex) — implements the 2026-09-17 decision log entry that was written but never built. "Prefer to self-describe" reveals a required text field; "Yes" on hormone therapy reveals the doctor-consultation note. All conditional reveals verified via direct JS assertions in every branch (match/mismatch/ambiguous/prefer-not-to-say), not just the happy path |
| 2026-09-21 | Onboarding Step 3 — Connect data source (onboarding/connect.html) built | Real modal OAuth simulation (login screen → permissions screen → Allow/Deny), not a fake instant-connect click, per PROJECT.md's explicit "real-flow, not simulated" requirement for this step. Focus trap implemented from scratch (Tab/Shift+Tab cycle within the modal, Escape closes, focus returns to the exact tile that opened it) and verified via direct focus assertions, not just visual inspection. Deny produces the spec'd inline error + "Try again" retry, never a dead end. "Both" tile runs one combined login+consent cycle rather than two sequential provider flows — a deliberate simplification — and marks all three tiles connected on success. Added --color-negative-tint to tokens.css (~12% blend of --color-negative, same ratio as --color-accent-tint) rather than hardcoding an ad-hoc hex for the error background, matching how --color-positive/--color-negative were added. Bumped tokens.css cache-bust to v=4 across all 7 pages |
| 2026-09-21 | Onboarding Step 4 — Goal (onboarding/goal.html) built | Preset/custom segmented toggle matching the Progress page's period-toggle pattern. "Ride consistently — 3 rides a week" pre-selected by default, matching the Goal tile already shown on the dashboard — this step is optional/low-friction like Step 3, so there's always a valid selection without forcing interaction. Custom mode's description field is required only while custom mode is active (same conditional-required pattern as Step 2's self-describe field); metric type (Distance/Frequency/Weight) is a single-select toggle that also supports deselecting by clicking the active one again, revealing/hiding a unit-suffixed value input. Verified every interaction via direct JS state assertions after a couple of stale-coordinate click misses (page reflow after the metric value field appears shifts everything below it) |
| 2026-09-21 | Onboarding Step 5 — Body data (onboarding/body.html) built, final input step | Reused Step 3's OAuth modal + focus-trap pattern verbatim for the smart-scale connection, adapted copy ("Read your body composition data"). Selecting a model from the dropdown opens the modal directly (matches spec: "Selecting a model triggers the OAuth flow"); Allow replaces the dropdown with "✓ Connected to [model]" + Change; Deny resets the dropdown and shows the same inline-error-with-retry pattern as Step 3. All three radio options (scale / manual / later) carry identical visual weight, no guilt framing on "I'll do this later," per spec. Manual entry (weight + 4 body-composition percentages) has no required fields — spec explicitly calls these optional. CTA reads "Next," the literal text PROJECT.md specifies for this step, rather than the "Save and continue" wording used on Steps 2 and 4 |
| 2026-09-21 | Onboarding Step 6 — Confirmation (onboarding/confirmation.html) built — Flow 1 complete | Drops the stepper/skip-setup topline entirely — setup is finished, so neither the numbered progress nor "skip" makes sense here; distinct from every other onboarding screen. Summary card shows Garmin Connect / "Ride consistently — 3 rides a week" / body data added — a deliberately hardcoded example rather than wiring real cross-page state (localStorage) through Steps 3–5, matching how the rest of the prototype (dashboard, ride detail, progress) already uses static illustrative data rather than live app state. Chose those specific values so they exactly match what the dashboard already shows (same data source, same goal text, same body weight present) — confirmed by clicking through: the summary's promise and the dashboard's actual content line up. Explicit aria-live announcement ("Setup complete. You're ready to ride.") fired via a short setTimeout after load, not just relying on normal page-load reading, per PROJECT.md's explicit aria-live requirement for this screen. No confetti or celebratory animation — the only "celebration" is a small checkmark badge reusing the stepper's existing done-dot visual language, not a new decorative element |
| 2026-09-21 | Rides list (rides/index.html) built | No spec existed for this screen — Phase 2's IA only detailed "Ride Detail," not a list view, even though the 5-item nav (built in Phase 3) has always included "Rides" as its own destination. Designed from scratch: flat reverse-chronological list of ride cards (name, date, distance/duration/avg HR, source), each linking to rides/detail.html. Deliberate, disclosed limitation: only one ride (Sept 15, "Morning ride on the river path") has real matching detail content — all 6 list cards link to the same detail.html, so 5 of them show mismatched content on click. Building 6 unique detail pages was out of scope for "add the list view"; every link is still functional (no dead ends), consistent with how "Both" in Step 3 and the hardcoded confirmation summary were handled — accepted, documented simplifications rather than hidden ones |
| 2026-09-21 | Body page (body/index.html) built | Only an IA outline existed (Weight trend, Body composition, Resting HR + Sleep "if Fitbit connected", correlation hint) — no detailed flow spec, same gap as Rides. Weight chart ends at exactly 74.2 kg to match the dashboard's Body tile, trending down from 76.0 kg over 8 weeks — deliberately colored neutral (--color-text-sub), not green/red, unlike the HR trend on Progress: weight change isn't universally "good" the way lower resting HR is, and presuming so would clash with how carefully this project already handles body-related data in onboarding (Step 2's gender/sex fields). Same reasoning applied to the 4 body-composition deltas. Resting HR, sleep, and the sleep/ride correlation insight all show empty-invitation states (not fake data) since no onboarding step ever connects Fitbit — "Connect Fitbit to see..." copy and a real link to Settings, matching the app's established empty-state tone ("an invitation to act, not an apology") |
| 2026-09-21 | Settings page (settings/index.html) built — every screen in the app now exists | Only an IA outline existed (6 bullet items), same gap as Rides and Body. Built all 6: Personal profile (Name/Age editable; Goal shown read-only with a link to Progress rather than duplicating the goal-chips UI that already lives there); Connected apps (Garmin starts connected, Strava/Fitbit don't — "Connect Fitbit" from the Body page's empty state lands here and now actually works); Dashboard customization and Notifications (toggle switches, all 6 dashboard tiles on by default); Units (segmented toggle, reusing the Progress page's pattern); Heart rate zones (auto-calculated list with zone-color swatches matching the dashboard's zone chart, or manual bpm thresholds). Connected-apps Connect/Disconnect is a direct toggle, not a third reuse of the OAuth modal — with 6 sections already on one page, mixing a heavier modal flow into just one of them would have read as inconsistent; a scope call, not an oversight. Caught and fixed a real bug before calling this done: the "calculate automatically" toggle's reveal of the manual zone fields was written as a CSS `:checked ~` sibling selector, but the checkbox is nested inside `.switch-row > .switch-control` while the fields it needed to reveal are siblings of `.switch-row`, not of the checkbox — sibling combinators can't cross that boundary. Fixed with the same hidden-attribute + JS pattern used for every other conditional reveal in this project, instead of fighting CSS specificity |
| 2026-09-22 | Ride detail's route map (rides/detail.html) rebuilt with literal map tiles (Leaflet.js + OpenStreetMap), replacing the first abstract-SVG version | Designer feedback: wanted a real map like Strava's, not a stylized line drawing. CLAUDE.md's "no external dependencies except Google Fonts" rule was amended to carve out this one exception (Leaflet + OSM tiles, route map only), since a literal map isn't achievable in pure CSS/SVG. Map is non-interactive (no zoom/pan/drag) — a static summary, not an explorable map, consistent with the calm "Measured" style. Route plotted on the Donauinsel in Vienna (ties to the "river path" ride name and the designer's Strava reference screenshot, which was also Vienna). Start/finish use different marker shapes (circle/square), not color alone. OSM attribution rendered as a normal visible text line, not hidden, per their tile usage policy |
| 2026-09-22 | Dashboard's This week/Streak and Body/Goal 2-column pairing (2026-09-21 decision) extended to mobile (index.html) | Designer feedback: the mobile media query still collapsed the whole bento grid to `grid-template-columns: 1fr`, overriding the pairing with a single-column stack — the rule was only ever applied on desktop. Removed that override so mobile inherits the same 2-column grid as desktop; Last ride and Insight keep their explicit `span 2` (full width), so only the four paired tiles end up side by side |
| 2026-09-22 | Rides nav icon (bicycle) redrawn, all 6 pages / 12 instances (pill nav + bottom nav) | Designer feedback, two rounds: (1) the original frame path ended in mid-air near the front wheel with no visible handlebar, plus a redundant disconnected stroke — rebuilt as one continuous path (rear wheel → seat → headtube → front wheel) with a straight handlebar bar added; (2) designer supplied a reference icon and asked for better — replaced the straight handlebar bar and reworked the seat with rounded "hook" curves (curling saddle + mirrored handlebar), closer in character to the reference while staying legible at the actual 18px render size |
| 2026-09-22 | Last ride / Body tiles' "see more" affordance settled on a bare chevron icon, bottom-right of the card (index.html) | Went through three versions same day, each on designer feedback: "See full ride"/"View body data" text → CLAUDE.md's "no → appended to links" rule relaxed to allow a trailing arrow, shortened to "Full ride →"/"Body data →" → designer asked for arrow-only (no copy) positioned bottom-right, became a bare `→` character with `aria-label` carrying the full accessible name → designer supplied a bold rounded-chevron reference image, swapped the text character for an inline SVG chevron (`stroke-width: 3.5`, round caps/joins) since a typed arrow glyph couldn't match that weight/roundness. SVG is `aria-hidden`, `aria-label` stays on the link — documented in CLAUDE.md as the one deliberate exception to "icon-only controls need a paired text label," justified because it's one repeated low-stakes "go deeper" affordance, not a one-off unlabeled control |
| 2026-09-22 | "Settings" removed from the pill nav and bottom nav on all 6 app pages; the avatar became an accessible dropdown menu (Profile / Settings) | Designer feedback — Settings demoted from a primary nav destination to an account-menu item, freeing the nav bar down to Home/Rides/Progress/Body. "Profile" links to Settings' existing "Personal profile" section (`#profile` anchor) rather than a new page, since none exists in this prototype. Dropdown is a real accessible disclosure: `aria-haspopup`/`aria-expanded`/`aria-controls` on the trigger, `role="menu"`/`role="menuitem"` inside, arrow-key navigation, Escape closes and returns focus to the trigger, click-outside closes. The avatar stays in the topbar on mobile (only the pill nav hides there), so Settings is still reachable on both breakpoints despite leaving the bottom nav |
| 2026-09-22 | "Pace" logo given a visible hover affordance on all 6 app pages | Designer feedback — the logo already linked to the dashboard on every page, but had no hover/pressed treatment, so it read as static text rather than a clickable control. Added the same padding + border-radius + accent-tint background hover already used for `.back-link`, for a consistent "this is a button" signal |
| 2026-09-22 | Topbar avatar switched from an "A" initial to a real photo (assets/avatar-alex.png), all 6 app pages | Designer-supplied photo, saved into assets/ per the existing file-structure convention. `.avatar` gained `overflow: hidden` + zero padding so it stays a clean 32px circle; the image itself uses `object-fit: cover` to fill it without distortion. Accessible name stays on the button (`aria-label="Account, Alex"`), so the `<img>` takes `alt=""` as decorative rather than duplicating it — the dropdown trigger's semantics are otherwise unchanged |

---

## Open Questions

**Pending decisions:**
- [ ] Validation method for Phase 5 (survey, usability test, or other)

**Learning notes (non-blocking, for future exploration):**
- [x] When and why create a CLAUDE.md? → Answered: create one for any multi-session
      Claude Code project. It caches design system rules and protocols so they don't
      need to be re-explained. The file is read automatically at session start.
- [ ] Should this project have multiple SKILL.md files or one unified skill?
      What are the tradeoffs?

---

## Future Deliverables

- [ ] Portfolio-facing case study (narrative format, audience: hiring teams)
- [x] Flows 2 and 3 mobile layouts — resolved directly in the coded prototype
      (built and verified responsive alongside desktop, no separate wireframes needed)
- [x] Rides list (rides/index.html) — built 2026-09-21
- [x] Onboarding flow (Flow 1) — complete 2026-09-21, all 7 screens
      (welcome, account, profile, connect, goal, body, confirmation)
- [x] Body page (body/index.html) — built 2026-09-21
- [x] Settings page (settings/index.html) — built 2026-09-21, last unbuilt screen in the app
- [ ] Overall design + flow review, once the core screens are built — Juliana's
      call, planned for after onboarding (not scoped yet: whether that means a
      fresh QA pass per screen, a cross-screen consistency audit, or a full
      flow walkthrough end to end)

---

*Living document. Update at the end of every working session.*
*CLAUDE.md is the source of truth for prototype build rules.*
*This file is the source of truth for all UX decisions and project content.*
