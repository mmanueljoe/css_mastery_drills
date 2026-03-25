# 07 — Nested Flex Navbar

## Objective
Build a professional navbar:
- logo on the left
- links on the right
- everything vertically centered

## Flexbox Axes Refresher
Flexbox is 1D layout along a direction:
- **Main axis**: the direction items flow (`flex-direction`)
- **Cross axis**: the perpendicular direction

Common navbar settings:
- `display: flex`
- `justify-content: space-between` (push ends apart on the main axis)
- `align-items: center` (center on the cross axis)

## Challenge
In `style.css`:
1. Make `.nav` a flex container and use `justify-content: space-between`
2. Make the link group (`.nav__links`) a flex row and add spacing using `gap`

## Done When
- Logo sits left, links sit right.
- Everything looks vertically aligned and evenly spaced.

