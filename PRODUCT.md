# PRODUCT.md — RecompSys

<!-- impeccable:product-schema 1 -->

## Platform
web

## Users
The owner — a single user (33M, 105kg, 20 years training experience, based in South Goa) running a 12-week strength + cardio recomposition program. Uses it daily on mobile during workouts and meals, occasionally on desktop.

## Product Purpose
Track a structured 12-week body recomposition cut: daily macro targets across three deficit phases, a 5-day training split with rest timers and PR tracking, a South Goa home-cooked meal plan, and adherence/progress logging — replacing spreadsheets and notes with one purpose-built daily tool.

## Positioning
RecompSys isn't a configurable tracker — it's this one 12-week program (exact TDEE, phase deficits, South Goa recipes, real exercise list) hard-coded as the product, not settings a generic app would ask you to fill in.

## Operating Context
Daily use in two settings: at the gym (Training tab, rest timers, set logging — must work offline with no signal) and at meal times (Nutrition tab, macro quick-add). Regional context is load-bearing: the meal plan is built around South Goa's available fish (Lepo, Bangda, prawns) and home-cooked Indian preparation, not generic "chicken and rice" macros. No backend — all state lives in the browser (localStorage) and the app is installed as a PWA via GitHub Pages.

## Capabilities and Constraints
- **Dashboard** — phase progress, daily macro targets (2800→2700→2600 kcal across 3 phases), body stats heatmap
- **Training** — day-by-day workout planner with exercise tables, rest timers, set logging, 1RM calculator, PR badges
- **Nutrition** — 7-day home-cooked Indian meal plan per phase, macro tracking bars, macro quick-add
- **Progress** — measurement tracking, cardio log, water intake (cup tracker), body weight log
- **Plan** — 12-week phase overview, deload protocol, supplement stack, shopping list by week

Constraints: single-file PWA (HTML/CSS/JS), no build step, no backend/database — all data is local to the device (no cross-device sync), single-user only (no auth/accounts), offline-capable via service worker.

## Brand Commitments
Name: RecompSys. App icon is an "RS" monogram (`icons/icon.svg`, `icons/icon-maskable.svg`). Visual identity is BMW M's motorsport-engineering design system — see Design Language below.

## Evidence on Hand
The training program, nutrition plan, and tracking protocols in [training/12-week-program.md](training/12-week-program.md), [nutrition/meal-plan.md](nutrition/meal-plan.md), and [tracking/implementation-guide.md](tracking/implementation-guide.md) are the owner's real, in-use 12-week plan (TDEE ~3,100 kcal, phase targets 2,800/2,700/2,600 kcal, 240g daily protein, 5 training days/week) — not placeholder or sample content. Future work must not invent substitute numbers, exercises, or recipes.

## Product Principles
1. Design serves the function — the numbers, the workout, the plan.
2. Single-user, no accounts — never add multi-tenant complexity.
3. Real data only — the program, macros, and recipes are the owner's actual plan, never placeholder content.
4. Offline-first — must work in a gym with no signal.

## Accessibility & Inclusion
No project-specific requirement beyond standard hygiene: the BMW M component system already targets 48×48px touch targets (WCAG AAA) and the dark canvas is paired with white/light-gray text for contrast.

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
