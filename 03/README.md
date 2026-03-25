# 03 — Display Logic Buttons

## Objective
Turn plain `<a>` links into large, clickable “button” blocks with padding and spacing.

## Why Inline Elements Fight You
Anchors are **inline** by default, which means:
- `width` and `height` don’t behave like you expect
- vertical margins (`margin-top`, `margin-bottom`) are unreliable

To style links like buttons while still letting them sit on one line, use:
- `display: inline-block`

## Challenge
In `style.css`, change the `.btn` from inline to `inline-block` so:
- padding feels like a real button
- spacing between buttons works as expected

## Done When
- The links look like large buttons.
- The buttons have clean spacing around them.

