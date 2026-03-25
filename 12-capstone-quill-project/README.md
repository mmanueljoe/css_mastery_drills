# 12 — Capstone: Quill Landing Page (Project Roadmap)

Your goal: build a clean, modern landing page using the exact workflow patterns from the course. Work in order. Don’t skip ahead.

## Phase 1 — Global Setup (Foundations)
1. Create a new stylesheet (use `style.css` in this folder).
2. Apply the universal selector reset:
   - `* { margin: 0; padding: 0; box-sizing: border-box; }`
3. Set global font inheritance and baseline readability:
   - `body { font-family: ...; line-height: ...; color: ...; background: ...; }`

**Deliverable:** Page renders with no default browser spacing surprises.

## Phase 2 — The Design System (REM + Font)
1. Apply the 62.5% REM trick:
   - `html { font-size: 62.5%; }`
2. Add the Poppins Google Font:
   - Add the Google Fonts `<link>` in `starter.html`
   - Set `--font-family` tokens and apply the font on `body`
3. Define your type scale (use the variables already prepared in `style.css`).

**Deliverable:** All typography uses `rem` and looks intentionally scaled.

## Phase 3 — Component Engineering (BTN + HIGHLIGHT)
Build components as reusable classes using “base + variant” styling.

### 3A) Buttons (`.btn`)
1. Create a base `.btn` class with:
   - `display: inline-block`
   - padding, border-radius, font-weight
   - `cursor: pointer`, `text-decoration: none`
2. Create variants:
   - `.btn--primary`
   - `.btn--secondary`
   - `.btn--outline`
3. Handle interaction states with pseudo-classes:
   - `:hover`
   - `:focus-visible`
   - `:active`

### 3B) Highlight text (`.highlight`)
Create a reusable `.highlight` class for short “callout” text that uses:
- a background tint
- stronger font weight
- subtle border radius / padding

**Deliverable:** Buttons and highlight are reusable across sections without rewriting styles.

## Phase 4 — Layout & Above-the-Fold (Flex + calc)
1. Use **nested flexbox** to align:
   - Navbar: brand left, links right, vertically centered
   - Footer: grouped content aligned cleanly
2. Make the hero perfectly “above the fold”:
   - Define `--nav-height`
   - Navbar uses `height: var(--nav-height)`
   - Hero uses `min-height: calc(100vh - var(--nav-height))`

**Deliverable:** Hero content fits the viewport under the fixed (or sticky) navbar on different screen heights.

## Phase 5 — Responsive Features (Grid + Motion Polish)
1. Implement CSS Grid for the features:
   - 3 columns on desktop
   - sensible wrapping for smaller screens
2. Add “AI-era custom” polish:
   - transitions on `.btn` (color, background, transform, shadow)
   - subtle hover lift for cards/feature blocks

**Deliverable:** Features adapt to screen size and interactions feel premium.

## What to Edit
- Start with `starter.html` (structure is done; you’ll add classes/links as needed).
- Build your CSS in `style.css` (expand beyond tokens as you complete phases).

