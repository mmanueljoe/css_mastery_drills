# 09 — Precision Positioning

## Objective
Pin a “Sale” badge to the corner of a card image.

## Relative vs Absolute
For “pin to corner” UI:
- Set the **parent** to `position: relative` (it becomes the positioning context)
- Set the **child** to `position: absolute` and place it with `top/right/bottom/left`

## Challenge
In `style.css`, position the `.badge`:
- `top: 10px`
- `right: 10px`

## Done When
- The badge stays attached to the card’s top-right corner.
- Resizing the page doesn’t break the badge positioning.

