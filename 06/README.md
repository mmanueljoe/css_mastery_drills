# 06 — Responsive Containers

## Objective
Create a container that looks great on:
- tiny phones
- big 4K monitors

## Width vs Max-Width
- `width: 1200px` is **fixed** — it can overflow on smaller screens.
- `max-width: 1200px` is **responsive** — it can shrink when needed.

A great pattern is:
- `width: 90%` (mobile-friendly fallback)
- `max-width: 1200px` (prevents lines from getting too long on large screens)
- `margin: 0 auto` (centers the container)

## Challenge
In `style.css`, update `.container` to:
- `max-width: 1200px`
- `width: 90%`
- `margin: 0 auto`

## Done When
- The text is centered with comfortable line length on large screens.
- The container fits nicely on mobile without horizontal scrolling.

