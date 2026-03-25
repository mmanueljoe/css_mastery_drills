# CSS Mastery Drills — Glossary

This glossary is the shared reference for every drill in `css-mastery-drills/`.

## The Cascade
The **cascade** is the algorithm the browser uses to decide which CSS declaration “wins” when multiple rules target the same element/property. It considers (in order): **importance** (`!important`), **origin** (user-agent vs user vs author), **specificity**, and **source order** (later rules win when specificity is tied).

## Specificity
**Specificity** is a score for a selector that determines how strongly it targets an element. Higher specificity overrides lower specificity when rules conflict on the same property.

Common comparison (highest → lowest):
- Inline styles (e.g. `style="color: red"`)
- `#id`
- `.class`, `[attr]`, `:pseudo-class`
- `element`, `::pseudo-element`

## Box Model (Content, Padding, Border, Margin)
The **box model** describes how an element’s size is calculated and how it occupies space:
- **Content**: the inner area where text/images live.
- **Padding**: space between content and border.
- **Border**: the outline around padding/content.
- **Margin**: outside space that separates the element from others.

## Inline vs. Block
**Inline** elements flow within a line of text (e.g. `a`, `span`). They typically ignore `width`/`height`, and vertical margins behave differently.
**Block** elements start on a new line and expand to fill available width by default (e.g. `div`, `p`). They respect `width`/`height` and margins predictably.

## Relative Units (REM/EM)
Relative units scale based on font size:
- `rem`: relative to the **root** (`html`) font-size.
- `em`: relative to the **current element’s** computed font-size (can compound through nesting).

## Viewport Units (VH/VW)
Viewport units scale to the browser window:
- `vh`: 1% of the viewport **height**
- `vw`: 1% of the viewport **width**

## Main Axis vs. Cross Axis
In Flexbox, alignment depends on direction:
- **Main axis**: the direction items are laid out (`flex-direction`).
- **Cross axis**: the perpendicular direction.

Examples:
- `flex-direction: row` → main axis is horizontal, cross axis is vertical.
- `flex-direction: column` → main axis is vertical, cross axis is horizontal.

## Above the Fold
**Above the fold** is the portion of a web page that is visible in the viewport **without scrolling**. In UI work, you’ll often size hero sections so the primary message and call-to-action are immediately visible.

## Component-Based Styling
**Component-based styling** is a way of writing CSS where reusable UI pieces (like buttons, cards, badges) are defined by a **base class** (e.g. `.btn`) and modified by additional classes (e.g. `.btn--primary`, `.btn--outline`) and state pseudo-classes (e.g. `:hover`, `:focus-visible`).

## Spacing System
A **spacing system** is a set of predefined spacing increments (e.g. 4px/8px/12px/16px or 5px/10px/20px) used consistently for padding, margin, and gaps. It helps layouts feel cohesive and reduces “random spacing”.

## Type Scale
A **type scale** is a structured hierarchy of font sizes (and often line-heights) used across headings, body text, and UI labels to create consistent visual rhythm and readable hierarchy.

## Responsive Design
**Responsive design** means building layouts that adapt across screen sizes using fluid techniques (relative units like `rem`, `%`, and viewport units, plus media queries). The goal is that the UI remains readable and usable on phones, tablets, and desktops.
