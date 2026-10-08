# Pace v2 — Concept brief: goal-first

> Branch: `concept-goal-first` · Baseline: tag `v1-pace` on `main`
> Status: decided 2026-09-25, built and promoted to the real paths 2026-10-03

---

## The problem with v1

v1 answers the research correctly module by module (plain-language zones,
unified data, calm UI), but as a whole it's a set of modules: last ride,
zones, week, streak, body, goal, progress. Garmin Connect and Strava already
have every one of those modules. So v1 reads as a thinner mix of the two,
and a flat grid of equal cards is where the "generic" look comes from.

The research never asked for more modules. It asked one question:

> *"I have all this data but I still don't know if I'm doing this right."* (persona, Phase 1)
> *Am I improving, and what should I do next?* (problem statement, Phase 1)

"Right" only means something relative to a goal. Neither Garmin nor Strava
reads a ride against the rider's own goal.

---

## The idea (one sentence)

**Pace reads every ride against the goal you set, so after each ride you know
whether you got closer and what to do next.**

---

## Core loop

1. **Set one goal.** Concrete and measurable (see goal types below).
2. **Ride.** Garmin/Strava syncs.
3. **Open Pace → ride recap.** The hero answer: *"This ride moved you closer"*
   (or didn't), how much, and the one reason why, in plain language.
4. **One next step.** "Next ride: keep it easy, 45 min." Just one, never a
   training plan.
5. Repeat. The goal's progress is visible on every screen, not in one tile.

Everything in the app either serves this loop or gets cut.

---

## Scope test

A feature stays only if it helps answer **"am I getting closer to my goal?"**

### Keep (reframed around the goal)
| v1 feature | v2 role |
|---|---|
| Last ride tile | Becomes the **ride recap**, the main screen after a ride |
| Time-in-zone chart + ride focus | Answers "did this ride hit its purpose?" The focus is inferred from the goal, not asked |
| *(new)* Training mix | Zone mix across recent weeks vs what the goal needs. This is where the rider learns zones |
| AI insight blocks | Become the recap's "why" and "next step", instead of floating strips |
| Progress page | Becomes the **goal trajectory**: are you on track for the goal's date? |
| Rides list + calendar | Stays as history; each ride tagged with its contribution to the goal |
| Ride detail (map, HR, metrics) | Stays as the "raw data" layer, one tap below the recap |
| Onboarding goal step | Moves to **first** after welcome; it's the spine of the product |

### Cut or shrink
| v1 feature | Why |
|---|---|
| Dashboard bento grid (6 equal tiles) | Equal tiles = no hierarchy. Replaced by goal + last-ride recap |
| Streak tile | Engagement mechanic, not goal progress (unless the goal *is* consistency) |
| Body page as a main nav destination | Only relevant for weight goals; becomes a secondary view |
| Separate summary cards on Progress | Absorbed into the goal trajectory |

### Park (not in v2 prototype, mention in the case study as "next")
| Idea | Condition to revisit |
|---|---|
| Nutrition tips | Only if tied to the goal + last ride ("long ride, recover for Thursday"). Generic tips add complexity without value |
| Fitbit sleep / resting HR | Only if it clearly changes the recap's answer |
| Social / sharing | Out of scope since Phase 1 |

### Move later (progressive profiling)
The onboarding profile step (height, age, gender identity, sex, hormone
therapy) is careful, inclusive work and stays. But asked up front it delays
the core loop. In v2 it's asked **when it's needed**: age when zones first
matter, sex/hormone therapy only for calorie or body-composition features.

---

## The goal model (decided 2026-09-25)

### Long-term goal: be ready for a group ride

The persona's own goal in Phase 1 was *"build enough confidence to join group
rides eventually."* A group ride has a concrete entry ticket: a distance and an
**average speed** you must hold. So the lead goal combines three measurable
pillars:

| Pillar | "Closer" means | Prototype data (Alex) |
|---|---|---|
| **Distance** | Longest ride trending toward the target | 41.2 of 60 km |
| **Average speed** | Speed you can *hold on long rides* (≥ 30 km), not short sprints | 23.0 of 26 km/h |
| **Consistency** | Rides/week vs target, sustained | 3/week met in 6 of 8 weeks |

Example goal: **"Join the Saturday group ride: 60 km at 26 km/h, by 14 Nov."**
Weight is deprioritized (sensitive; see v1's care on body data).

### How you get there: zones, learned along the way

Speed over distance comes from training in the right zones, so zones become
the app's **teaching thread**, not a chart to decode. Heart rate zones by
default. Power zones only when a power meter is connected, since most beginner
setups don't have one. The app says so plainly and doesn't assume either.

### Two goal layers

1. **Long-term goal:** the group ride (above).
2. **Each ride's purpose:** e.g. "Endurance (Z2)", "Tempo", "Recovery".
   Inferred from what the goal needs this week and editable by the user. The
   recap says whether the ride **hit its purpose**, and a **training mix**
   view tracks development over weeks. Example: *"Z2 is 19% of your riding in
   the last 3 weeks. Your goal needs about 70%, and here's why."*

---

## What this means for the visual (input for the next step)

- **One hero per screen.** The goal and this ride's contribution to it are
  big and unmistakable; everything else is quieter. No grid of equal cards.
- **The goal has a shape.** A trajectory, a distance-to-finish, a line
  toward a date. It's the app's signature visual, repeated across screens.
- **Recap is readable in 3 seconds.** Closer / not closer, how much, why.
  The detail is one tap below, never in the way.
- **Relax v1's "Measured" rules where they caused blandness.** Muted palette,
  borders only and uniform tiles were deliberate, but they made everything
  equal. v2 needs contrast and hierarchy, not decoration.

---

## Decisions (Juliana, 2026-09-25)

1. **Goal:** distance + consistency, **plus average speed** (the entry ticket
   to group rides). Zones (HR, power when available) are how the rider learns
   to get there. See "The goal model" above.
2. **Home = ride recap after a ride, and the recap carries all the ride
   data.** v1's promise stays: one app instead of 3–4, with every source
   summarized in one place. The recap is data + meaning, and the full detail
   (map, HR trace) is one tap away.
3. **Per-ride purpose is inferred from the goal, not asked.** The long-term
   goal is split into rides with their own purpose. The rider tracks their
   development across rides and learns what's missing and why (e.g. "you're
   short on Z2 riding, and that's why you fade after 30 km").
4. **Onboarding:** Welcome → Goal → Connect → first recap, with account
   creation deferred until value is shown.

## Open for discussion

- ~~How the plan for the week is shown~~ → **Resolved:** Home shows "This week"
  as one row per planned ride, and the recap ends with one next ride.
- ~~Whether a ride that misses its purpose still counts toward consistency~~ →
  **Resolved: yes.** Consistency is about showing up; the purpose is judged separately.
- Where power zones appear when a power meter is connected. *(Still open.)*
- Desktop layout: the phone column, centered, for now. *(Still open.)*

---

## Where it stands (2026-10-03)

The look came from three explorations of one screen, the post-ride recap
(A Editorial, B Cockpit, C Coach, archived in `concepts/`). **D** combined them
and became the v2 system: `docs/DESIGN-SYSTEM.md` and `css/tokens.css` describe it.

Built, on their real paths:

| Screen | File |
|---|---|
| First run: Welcome → Goal → Connect → first recap (+ light account prompt) | `onboarding/welcome.html`, `goal/index.html?from=onboarding`, `onboarding/connect.html`, `rides/recap.html?first=1` |
| Home, between rides | `index.html` |
| Ride recap | `rides/recap.html` |
| Ride detail (raw data) | `rides/detail.html` |
| Rides history | `rides/index.html` |
| Progress = goal trajectory | `progress/index.html` |
| Review or change goal | `goal/index.html?from=home\|recap\|progress\|settings` |
| Settings (incl. optional Body) | `settings/index.html` |

`concepts/index.html` is the prototype map for reviewers. Decisions made while
building are logged in PROJECT.md's decision log (2026-09-25 onwards).

Parked for the case study, as deliberate scope decisions: nutrition, sleep,
social, and body-composition goals (weight loss, muscle gain).
