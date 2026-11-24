# Pace: reading every ride against your goal

> **Draft 2** · Portfolio case study for Squarespace · Audience: hiring teams ·
> Target: 6–7 min read. Notes for Juliana are in `[brackets]`. Screenshots are
> marked `[IMG: …]` and saved in `docs/case-study-images/`.

---

## Overview

Pace is a cycling app built for beginners, though not only for them. After
every ride it tells you whether you got closer to your goal, why, and what to
do next.

- **Role:** Product Designer, end to end (research, concept, UX, UI, prototype)
- **Timeline:** 20 Aug – 6 Oct 2026, a side project of about 25–30 hours over
  11 days, including desk research and talking it through with friends
- **Tools:** Claude Code. No Figma: I designed every screen directly as a
  working HTML/CSS prototype
- **Outcome:** a clickable prototype of the whole core loop, from onboarding to
  ride recap, home, progress, ride history, goal setting and settings, checked
  for accessibility on mobile and desktop
- **Data:** Alex and every ride, number and date in the prototype are made up,
  to show how the app behaves over a few weeks of riding

[Try the prototype](https://rgb-und-cmyk.github.io/pace-prototype/) ·
[See the code and design history on GitHub](https://github.com/rgb-und-cmyk/pace-prototype)

`[Both links only work once the repo is public and GitHub Pages is on. See
the notes in chat.]`

`[IMG: hero, ride recap on a phone next to Home]`

---

## The problem

A beginner who buys a Garmin or a Wahoo gets a lot of data on day one, and it
ends up spread across three or four apps. Garmin Connect syncs the device,
Strava is social, Fitbit tracks sleep. None of them answers what a beginner
actually wants to know: am I improving, and what should I do next?

Desk research and community threads kept pointing to the same things:

1. **The fragmentation is built in.** Even experienced riders complain about
   it. These apps are organized around a device or a social feed, not around
   your progress.
2. **Social features get in the way** when you're trying to understand your
   own training. Segments and leaderboards pull attention and can discourage.
3. **The advanced tools assume sports science.** intervals.icu and
   TrainingPeaks are powerful, but not for someone who doesn't know what Z2
   means.
4. **Getting the data is easy. Understanding it is where people get stuck.**

I put this into one persona, Alex: early 30s, office job, an entry-level
Garmin Edge, occasional Strava. Alex checks two or three apps after every ride
without knowing what to look for, skips heart rate zones because they're
confusing, and would like to feel ready for a group ride one day. Alex is
the rider you follow through the whole prototype.

> "I'm struggling to find an app that clearly shows my performance evolution
> over time."
> — a rider on [Reddit, r/cycling](https://www.reddit.com/r/cycling/comments/1rvnjd5/whats_your_goto_app_for_analyzing_your_rides/)

`[IMG: persona card or a short competitor comparison]`

---

## Version 1: correct but generic

The first version answered the research one need at a time: zones in plain
language, all sources in one place, a calm interface. It had a dashboard of
equal tiles (last ride, zones, week, streak, body, goal), a five-step
onboarding, ride detail, progress and a body page.

Each part was reasonable. Together they looked like a thinner Garmin Connect
crossed with Strava, because both apps already have every one of those tiles.
And a grid of equal cards has no hierarchy, which is a big part of why it felt
generic.

When I went back to the research, it wasn't asking for more features. It kept
asking one question, and "am I doing this right?" only has an answer relative
to a goal. Neither Garmin nor Strava reads a ride against a goal you set.

`[IMG: v1 dashboard, bento grid, light theme]`

---

## The pivot: goal-first

v2 starts from one sentence: Pace reads every ride against the goal you set,
so after each ride you know whether you got closer and what to do next.

That gives the app a loop:

1. Set one goal, concrete and measurable.
2. Ride. Garmin or Strava syncs automatically.
3. Open Pace and see the recap: did this ride move you closer, by how much,
   and the main reason why.
4. Get one next step, like "Thursday: 75 minutes, all in Z2". Not a full
   training plan.
5. Repeat. Goal progress is visible on every screen.

I ran every v1 feature through one question: does it help answer "am I getting
closer to my goal?"

| Kept and reframed | Cut or shrunk | Parked |
|---|---|---|
| Last ride tile → ride recap | Grid of equal tiles | Nutrition |
| Zone chart → "did this ride do its job?" | Streak tile (engagement, not progress) | Sleep and resting HR |
| Progress page → goal trajectory | Body as a main nav item | Social |
| Rides list → history, each ride tagged by its effect on the goal | Separate summary cards | Body-composition goals |

Navigation went from five items to three: Home, Rides, Progress.

---

## The goal model

"Get fitter" can't tell you whether a ride was a good one, so the goal had to
be concrete. Alex's goal from the research was joining group rides, and a group
ride has a real entry bar: a distance and an average speed you need to hold.

So the main example goal is "Join the Saturday group ride: 60 km at 26 km/h,
by 14 Nov", tracked on three pillars:

| Pillar | Getting closer means | Alex today |
|---|---|---|
| Distance | Longest ride moving toward the target | 41.2 of 60 km |
| Average speed | Speed held on long rides (30 km+), not short sprints | 23.0 of 26 km/h |
| Consistency | Rides a week vs the target | 3 a week in 6 of the last 8 weeks |

Zones are the way to get there. Holding speed over long distances comes from a
lot of easy riding, which beginners rarely do. So instead of a chart to
decode, zones became something the app teaches ride by ride. Each ride gets a
purpose based on what the goal needs that week (you can change it), and the
recap tells you whether you hit it.

`[IMG: Progress, the three pillars and the training mix vs what the goal needs]`

---

## Finding the look

I explored the post-ride recap in three directions: **A, Editorial** (the
verdict as a headline, little chrome), **B, Cockpit** (dark and dense, every
number in a grid) and **C, Coach** (the goal trajectory up front).

I kept B's dark look and took the best part of each: A's headline, B's data
grid, C's trajectory chart. That mix became the design system: Archivo, warm
charcoal and a single lime accent.

The early explorations also looked AI-generated in places: a word highlighted
in the headline, status pills with ✓/✕, a card around every section, gray
eyebrow labels, giant countdowns. I added those to a banned list in the design
system so they wouldn't come back.

`[IMG: A / B / C side by side, then the final recap]`

---

## Key screens

**Ride recap.** The headline is the verdict in plain words: "Strong ride. But
your goal asked for an easy one." Below it: planned Z2 vs what you rode, why
easy rides make you faster, what this ride means for the goal, and your next
ride. Map and heart rate are one tap away.

`[IMG: recap]`

**Home.** "Good morning, Alex. Today is an easy one." Today's ride is the one
thing that stands out, followed by the goal, this week's plan and the last
ride.

`[IMG: Home]`

**Progress.** "58 days to go. Two of three on track." Each pillar shows where
you are and where you need to be. The training mix compares your last three
weeks of zones with what the goal needs.

`[IMG: Progress]`

**Onboarding.** Welcome, goal, connect, then your first recap. You only create
an account after Pace has shown you something useful, through a "Keep your
progress" prompt with an emailed sign-in link and no password.

`[IMG: onboarding sequence + Rides calendar]`

---

## Decisions up close

**Honest, but encouraging.** The first version of the goal message showed the
bare projection: 24.9 km/h by the date, against a target of 26. People would
read that as "you're going to fail". It now says "You can still make it on
time", shows what the plan projects next to your current pace, and links to
the plan. Same numbers, different framing.

**One thing stands out per page.** Lime appears once per page, on what to do
next. Everywhere else it only marks data and good news, so it keeps its
meaning.

**Use the words riders already know.** Zone names follow Garmin (Warm up,
Easy, Aerobic, Threshold, Maximum), and "Splits" and "Elevation gain" follow
Strava. My first names clashed with both. Someone learning zones in Pace
should recognize them on their bike computer.

**Ask only when it's needed.** v1 asked for height, age, gender identity, sex
assigned at birth and hormone therapy up front, following the CDPH SOGI 2025
guidance. It was careful work, but it delayed the first recap. In v2 each
question waits until a feature needs it.

---

## What I left out on purpose

- **Body-composition goals.** A ride can't show muscle gained, and weight loss
  is mostly about food. These goals would turn Pace back into a general
  fitness tracker, and body data is sensitive. Weight stays an optional
  setting, used only for calories.
- **Nutrition, sleep and resting heart rate.** Only worth adding if they
  change what the recap tells you. Generic tips would just add noise.
- **Social.** Out from the start. The research showed it distracts beginners.

---

## Accessibility

Every page is checked at 375px and on desktop before it ships: text at least
12px, WCAG AA contrast, 44px touch targets, no horizontal scroll, one h1.
Color is never the only signal. Calendar days use shapes as well as color,
and zones have names. One example: missed weeks in a chart failed the 3:1
contrast minimum for graphics, so I recolored them.

`[IMG: before/after of that contrast fix]`

---

## Designing with AI

I designed Pace in code with Claude Code, with no Figma, to see what my process
looks like when the prototype is the design file.

- **The design system is written for the AI to read.** Tokens, type, color
  rules, components and banned patterns are in documents it reads every
  session, so it doesn't slide back to generic defaults.
- **The decisions are mine.** Every direction, cut and copy change here was my
  call, recorded with the reason in a decision log of nearly 80 entries.
- **Pull requests are the design history.** Every change has its own branch
  and pull request, so you can follow how the design changed.

What surprised me most: left alone, the AI went straight to the patterns that
make interfaces look generated. The fix wasn't better prompts. It was writing
down what the design is not, and checking against that list.

`[Check the paragraph above is true to your experience, or swap in your own
lesson.]`

---

## What's next

- **Test it with real beginners.** I haven't run usability tests yet. The plan
  is five sessions, checking whether people understand the recap without help
  and know what their next ride should be.
- **Desktop layout.** For now it's the phone layout, centered. A two-column
  layout for wide screens is still open.
- **Power zones,** for riders who connect a power meter.
- **How I'd measure success:** riders can explain what their last ride meant
  without help, know whether they're improving without opening another app,
  and come back after their next ride, not just after setup.

---

## Reflection

`[DRAFT for your approval, written in your voice. Edit freely.]`

My first version did what the research asked, point by point, and still
missed. Pace only started to make sense once I stopped adding features and
asked what question every screen should answer. Designing in code meant every
decision had to be concrete straight away, from copy to color, which made
weak ideas obvious faster than a mockup would have. In a real scenario I would
put the first version in front of beginners much earlier, before building the
second one, or run a concept test with both versions if possible.
