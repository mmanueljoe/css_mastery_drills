# 02 — Box Sizing Predictability

## Objective
Make two boxes visually identical in width even though one of them has massive padding.

## Why This Happens
By default, elements use `box-sizing: content-box`, which means:
- `width` applies to **content only**
- `padding` and `border` are added **on top** of that width

That’s why adding `padding: 50px` makes an element appear wider than expected.

## Best Practice Reset
A common best practice is to set `box-sizing: border-box` globally so:
- `width` includes content + padding + border
- layouts become more predictable

## Challenge
Implement the universal reset in `style.css`:
- Use the universal selector (`*`) to apply `box-sizing: border-box`
- After the fix, both boxes should render at the same visible width

## Done When
- Box A and Box B look the same width on screen.
- You used the universal selector to solve it.

