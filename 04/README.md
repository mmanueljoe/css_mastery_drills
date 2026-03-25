# 04 — The REM Trick (62.5%)

## Objective
Set up a scalable type system using the “62.5% trick”.

## Why 62.5%?
Browsers commonly default to `16px` font-size on the root (`html`).

If you set:
- `html { font-size: 62.5%; }`

Then the root becomes:
- `16px * 0.625 = 10px`

Meaning:
- `1rem ≈ 10px`

This makes rem-based sizing easier to reason about (and scales well if the user changes base font settings).

## Challenge
In `style.css`:
1. Apply the 62.5% trick on `html`
2. Create a type scale using **only rem units**:
   - `h1` = `6.2rem`
   - `p` = `2rem`

## Done When
- No `px` units are used for typography.
- The heading is visually much larger than the paragraph.

