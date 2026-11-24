# Pace

A cycling app prototype built for beginners, though not only for them. Pace
reads every ride against the goal you set, so after each ride you know whether
you got closer and what to do next.

This is a portfolio project by Juliana, Product Designer. It was
designed directly in code with Claude Code, without Figma.

## Try it

- **[Open the prototype](https://rgb-und-cmyk.github.io/pace-prototype/onboarding/welcome.html)**,
  starting from the first-run flow
- **[Prototype map](https://rgb-und-cmyk.github.io/pace-prototype/concepts/index.html)**,
  every screen in one list
- Best viewed at phone width. On desktop it shows the phone layout, centered.

All the data is made up. Alex, the rider you follow through the prototype, is
a persona, and every ride, number and date is example data.

## What's in it

| Screen | File |
|---|---|
| Welcome and connect | `onboarding/welcome.html`, `onboarding/connect.html` |
| Set a goal (3 steps) | `goal/index.html` |
| Home | `index.html` |
| Ride recap | `rides/recap.html` |
| Rides history and ride detail | `rides/index.html`, `rides/detail.html` |
| Progress toward the goal | `progress/index.html` |
| Settings | `settings/index.html` |
| Early recap explorations (A, B, C) | `concepts/` |

## Design record

- [`CONCEPT.md`](CONCEPT.md): the idea behind v2
- [`PROJECT.md`](PROJECT.md): research, sources and the decision log
- [`docs/DESIGN-SYSTEM.md`](docs/DESIGN-SYSTEM.md): tokens, components,
  accessibility rules
- Every change went through its own pull request, so the
  [closed PRs](https://github.com/rgb-und-cmyk/pace-prototype/pulls?q=is%3Apr+is%3Aclosed)
  show how the design changed
- The first version is kept under the `v1-pace` tag

## Run it locally

Plain HTML, CSS and JavaScript, with no build step. From the repo folder:

```bash
python -m http.server 8420
```

Then open http://localhost:8420/onboarding/welcome.html. Opening the files
directly (`file://`) breaks some links.
