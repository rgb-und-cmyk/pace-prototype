# Pace — usability test plan

> **Draft 1 for Juliana's review.** Fills the pending Phase 5 (validation) in
> PROJECT.md. Results go into the case study's "What's next" section.

---

## 1. Goal of the test

Find out whether Pace's core promise works for real beginners: **after a ride,
can they tell whether they got closer to their goal and what to do next,
without help?**

## 2. What we want to learn (hypotheses)

| # | Hypothesis | Screen | Passes if |
|---|---|---|---|
| H1 | The recap verdict is understood in seconds | Ride recap | 4 of 5 say, unprompted, that the ride was too hard for its plan |
| H2 | Riders know what to do on their next ride | Recap, Home | 4 of 5 say "easy / Z2 / under 132 bpm, about 75 min" |
| H3 | Riders can tell whether they're on track for the goal | Progress | 4 of 5 name the pillar that's behind (speed) |
| H4 | Zones make sense in plain language | Recap, Progress | Most explain "Z2" in their own words (easy, can talk) |
| H5 | "You can still make it on time" motivates without misleading | Recap, Progress | Riders feel encouraged *and* understand they're currently behind |
| H6 | Setting the goal in onboarding is clear | Goal flow | 4 of 5 finish without help; deferring the account doesn't bother them |
| H7 | The calendar symbols are clear | Rides | Riders read "too hard" and "missed" correctly |

## 3. Method

- **Moderated, remote, think-aloud**, about 30 minutes per session (video call
  with screen sharing, or in person).
- **5 participants.** Enough to find most of the major issues in a first round.
  A second round of 3–5 after fixes, if time allows.
- **Device:** their own phone if possible (Pace is mobile-first), otherwise a
  laptop browser at phone width.
- **Pilot** with one friend first to check the timing and the wording of the
  tasks.

## 4. Participants

**Screener (all must be true):**
- Rides a bike for fitness or fun at least once a week
- Has been riding with a tracker (Garmin, Wahoo, Strava, Apple Watch…) for
  less than about 2 years
- Doesn't follow a structured training plan or use TrainingPeaks / intervals.icu

**Nice to have:** a mix of genders and ages; at least one person who has never
used heart rate zones; at least one who has thought about joining a group ride.

**Where to find them:** friends of friends, local cycling clubs' beginner rides,
cycling groups on social media. Offer a small thank-you (coffee or a voucher)
if possible.

## 5. Session script

**Intro (3 min).** Thank them, explain that we're testing the app, not them,
ask them to think out loud, get consent to take notes (and to record, if
recording).

**Warm-up (3 min).**
- "How do you check your rides today? What do you look at after a ride?"
- "Do you have a goal for your riding right now?"

**Scenario.** "You're Alex. You want to join a Saturday group ride: 60 km at
26 km/h by 14 November. You just finished a morning ride and opened Pace."

**Tasks (about 18 min).**

| # | Task (say to the participant) | Start page | Tests |
|---|---|---|---|
| 1 | **5-second look.** Show the recap for 5 seconds, hide it. "What did that screen tell you?" | `rides/recap.html` | H1 |
| 2 | "How did this ride go, compared with what you planned?" | Recap | H1, H4 |
| 3 | "What should you do on your next ride?" | Recap | H2 |
| 4 | "Are you going to be ready for the group ride? What's holding you back?" | Recap → Progress | H3, H5 |
| 5 | "What does Z2 mean, in your own words?" | Any | H4 |
| 6 | "Look at your rides this month. Which ones didn't go to plan?" | `rides/index.html` | H7 |
| 7 | "Imagine you're new to Pace. Set up your goal." | `onboarding/welcome.html` | H6 |

Don't help unless they're stuck for more than about a minute. If they ask
"is this right?", reply "What do you think?"

**After each task:** "How easy or hard was that, from 1 (very hard) to 7
(very easy)?" (Single Ease Question)

**Wrap-up (5 min).**
- "How did the message about your goal make you feel?" (H5)
- "Compared with how you check your rides today, would this help? Why?"
- "What would you change first?"

## 6. What to record

For each task: **success** (done / done with help / not done), **SEQ score**,
what they said (quotes), where they hesitated or tapped something wrong.

One note-taking sheet per participant, one row per task. A friend taking notes
while you moderate makes this much easier.

## 7. Analysis

1. After every session, write down the top 3 observations while they're fresh.
2. After all sessions, group the observations into themes (affinity map).
3. Rate each issue: **critical** (blocks the task), **serious** (slows or
   confuses), **minor** (cosmetic).
4. Check each hypothesis: passed / partly / failed, with evidence.
5. Pick the top 3 fixes, change the prototype, and (if possible) retest them.

## 8. Known limits of the prototype (tell participants if they hit them)

- The data is static: all participants see Alex's rides, not their own.
- Every ride in the history opens the same ride detail.
- Connecting Garmin/Strava is simulated.
- Name these limits in the case study too, so the results are read honestly.

## 9. Logistics and timeline

| Step | When |
|---|---|
| Finalize plan, recruit, pilot | Week 1 |
| 5 sessions (about 30 min each, plus 15 min of notes) | Week 2 |
| Analysis, top fixes, case study update | Week 3 |

**Total time:** roughly 8–10 hours.

## 10. In the case study

A short section: who you tested with, what passed, what failed, and **what you
changed because of it**. A before/after of one fix is worth more than a table of
scores.
