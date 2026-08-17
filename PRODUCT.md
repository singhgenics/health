# PRODUCT.md — RecompSys

## App Name
RecompSys

## What it is
A personal 12-week body recomposition tracker — a single-file PWA (HTML/CSS/JS) hosted on GitHub Pages. Built for one user, tracking a structured cut with progressive cardio.

## Register
Product (design serves the function — the numbers, the workout, the plan).

## Platform
Web (single-file PWA, offline-capable via service worker)

## Target User
The owner — a single user running a 12-week strength + cardio recomp program. Uses it daily on mobile and occasionally on desktop.

## Core Features
- **Dashboard** — phase progress, daily macro targets (2800→2700→2600 kcal across 3 phases), body stats heatmap
- **Training** — day-by-day workout planner with exercise tables, rest timers, set logging, 1RM calculator, PR badges
- **Nutrition** — 7-day home-cooked Indian meal plan per phase, macro tracking bars, macro quick-add
- **Progress** — measurement tracking, cardio log, water intake (cup tracker), body weight log
- **Plan** — 12-week phase overview, deload protocol, supplement stack, shopping list by week

## Design Language
Follows [DESIGN-bmw-m.md](DESIGN-bmw-m.md) — a BMW M motorsport-engineering system, adapted for a data-dense functional app rather than a marketing surface.
- **Canvas:** Near-pure black (`#000000`) everywhere — no light theme. The theme toggle was removed; BMW M's system "inverts almost nothing."
- **Brand accent:** M tricolor — M Blue Light `#0066b1` → M Blue Dark `#1c69d4` → M Red `#e22718` — used as a 4px sticky top stripe and sparingly elsewhere. Semantic colors: success `#0fa336`, warning/caution `#f4b400`, primary interactive `#1c69d4`.
- **Typography:** Inter (BMW's documented open-source substitute for BMW Type Next Latin) at weight 700 for display/labels/buttons and 300 for body copy — the heavy/light contrast is the system's signature. JetBrains Mono is kept for tabular numeric stats (a functional exception the marketing spec doesn't cover).
- **Voice:** Chrome (labels, tabs, buttons, badges) is UPPERCASE with ~0.06em tracking. Content (workout names, meal names) stays sentence case.
- **Radius:** `0` everywhere (cards, buttons, inputs, pills) except genuinely circular avatar-style badges (exercise number, meal number) which stay `50%`. Binary rule: 0 or full circle, nothing in between.
- **Elevation:** No drop shadows, no gradient backdrops. Flat surfaces (`--surface`/`--surface-elevated`) and hairline borders do the elevation work instead.

## Absolute Bans (enforced)
- No `border-left` side-stripe accents on cards
- No gradient text (`background-clip: text`) or decorative gradient backdrops
- No bounce/elastic easing (`cubic-bezier(.34,1.56,...)`)
- No glassmorphism decoration
- No rounded buttons/cards/pills — BMW M's rectangular silhouette is the brand
- No light theme — BMW M's canvas is black-only

## Service Worker
Cache key: `recompsys-v{N}` — bump N on every deploy that changes cached assets.

## Deployment
GitHub Pages (legacy build, `.nojekyll` present). Trigger rebuild: `gh api -X POST repos/singhgenics/health/pages/builds`
