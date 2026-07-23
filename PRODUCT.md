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
- **Brand color:** Coral `#FF385C` (Airbnb-inspired) with warm orange accent `#FC642D`
- **Theme:** Light-first (Airbnb light as default), full dark mode via `[data-theme="dark"]` toggle
- **Typography:** Barlow Condensed (headings/display) + Barlow (body) from Google Fonts
- **Radius:** Cards 20px, pills 980px (full-pill), inputs 10px
- **Motion:** ease-out-expo `cubic-bezier(0.16,1,0.3,1)` for all interactions; `appleReveal` for scroll entrance

## Absolute Bans (enforced)
- No `border-left` side-stripe accents on cards
- No gradient text (`background-clip: text`)
- No bounce/elastic easing (`cubic-bezier(.34,1.56,...)`)
- No glassmorphism decoration

## Service Worker
Cache key: `recompsys-v{N}` — bump N on every deploy that changes cached assets.

## Deployment
GitHub Pages (legacy build, `.nojekyll` present). Trigger rebuild: `gh api -X POST repos/singhgenics/health/pages/builds`
