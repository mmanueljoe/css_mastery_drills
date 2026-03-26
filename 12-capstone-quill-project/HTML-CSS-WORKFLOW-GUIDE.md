# HTML + CSS Workflow Guide (From Blank IDE → Professional UI)

Use this as a “how I’d build it” reference when you’re unsure:
- how to structure HTML so it’s easy to style
- what should get a class
- where to apply typography/layout/responsive rules
- how to proceed from tokens → layout → components

This is written to help you build pages like a professional frontend engineer, using the same ideas your drills are trying to teach—just with the *why* made explicit.

---

## 0) The core principle: responsibilities

Most confusion comes from mixing responsibilities. In a maintainable UI, each layer has a clear job:

- **HTML**: meaning + document structure (what it is)
- **CSS tokens**: design system values (what it looks like, globally)
- **Layout wrappers**: spacing, alignment, responsive structure (how it’s arranged)
- **Components**: reusable UI pieces (how it behaves + looks in many places)
- **Utilities** (optional): single-purpose helpers used sparingly

If you keep those separate, you stop “randomly styling things” and start engineering UI.

---

## 1) A repeatable build order (the professional workflow)

When you open a blank project, use this exact order:

1. **Write semantic HTML structure first** (no styling yet)
2. Add a **layout skeleton** (`.container`, section spacing)
3. Create **design tokens** (colors, type scale, spacing)
4. Apply **global typography defaults**
5. Build **layout for each section** (flex/grid + spacing)
6. Build **components** (buttons, cards, badges, etc.)
7. Make it **responsive** (tokens + layout breakpoints)
8. Polish **states + accessibility** (focus, hover, reduced motion)

Why this order works:
- tokens + global defaults reduce “per-element tweaking”
- layout decisions happen once, not scattered everywhere
- components stay reusable because they’re built after the system exists

---

## 2) How to structure HTML so it’s easy to style

### A) Use landmarks (the page outline)

Start with a predictable skeleton:

```html
<header class="site-header">
  <nav class="nav" aria-label="Primary">...</nav>
</header>

<main>
  <section class="hero" aria-label="Hero">...</section>
  <section class="features" aria-label="Features">...</section>
  <section class="cta" aria-label="Call to action">...</section>
</main>

<footer class="footer">...</footer>
```

Why:
- screen readers and browsers understand it
- you (and future you) instantly know where each style belongs

### B) The “section pattern” (almost always the right move)

For most sections, use:

- `.section` (outer): background + vertical spacing (padding)
- `.section__inner` (inner): width constraint + centering
- content blocks inside (grid/flex)

Example:

```html
<section class="features" aria-label="Features">
  <div class="features__inner">
    ...
  </div>
</section>
```

Why:
- you avoid applying `max-width` and centering to random children
- you get consistent spacing across sections

### C) What should get a class?

Give a class when you need one of these:

1. **Layout control** (flex/grid, alignment, spacing)
2. **Component styling** (button/card/badge)
3. **Typography styling that differs from default** (hero title, section subtitle)
4. **State styling** (active, selected, error, open)
5. **JS hook** (if needed later; ideally prefixed like `js-...`)

Don’t add classes just because you can. Many elements can inherit global typography.

### D) Naming: choose one convention and stick to it

Your project already uses a BEM-ish approach (`.hero__title`, `.cta-card__actions`). That’s good.

Rules that keep it clean:
- **Block**: standalone component/section (`.hero`, `.cta-card`, `.btn`)
- **Element**: part of that block (`.hero__title`, `.cta-card__actions`)
- **Modifier**: variant/state (`.btn--primary`, `.feature--featured`)

Why BEM works:
- the class name tells you where it belongs
- selectors stay simple (you avoid nesting selectors that fight each other)

---

## 3) How to decide “where do I apply this CSS?”

Use this decision tree:

### A) Is this a global default?

Examples:
- base font family
- base font size
- base line-height
- default text color

Apply to: `body`, headings, and a small set of global elements.

Why:
- avoids repeating the same rule across 15 selectors

### B) Is this a reusable component?

Examples:
- buttons
- cards
- badges/highlights
- stats pills

Apply to: a **component class** (`.btn`, `.card`, `.highlight`).

Why:
- components can move to other sections without breaking

### C) Is this section layout?

Examples:
- hero alignment
- feature grid columns
- footer columns

Apply to: the section wrapper or layout child (`.features`, `.feature-grid`, `.footer__inner`).

Why:
- layout is contextual; don’t bake layout into leaf nodes like `h2`/`p`

### D) Is this typography for a specific text block?

Examples:
- hero subtitle line length
- section subtitle spacing

Apply to: the class on that text block (`.hero__subtitle`, `.section-header__subtitle`).

Why:
- readability constraints (like line length) should not accidentally apply to all paragraphs

---

## 4) Typography that scales (the deep concepts)

### A) Rems: what you already learned

- `rem` is based on the root font size (`html`).
- With `html { font-size: 62.5%; }`, `1rem ≈ 10px` (since 16px × 0.625 = 10px).

Why people do it:
- math becomes easier (1.6rem ≈ 16px)

### B) Why “fixed type scale tokens” still break on mobile

If your hero title is always `6.2rem`, it’s huge on small screens. Then:
- it wraps into 3–5 lines
- it pushes everything down
- you run out of vertical space

So the *token itself* must become responsive.

### C) `clamp()` (the most important responsive type tool)

`clamp(min, fluid, max)` means:
- never smaller than **min**
- grows fluidly with viewport (the middle value)
- never larger than **max**

This is how pros get smooth scaling without a dozen breakpoints.

### D) Line length (“measure”) is a real design constraint

Most body text is easiest to read at roughly **55–70 characters per line**.

Practical CSS approach:
- set `max-width: 60ch` (or similar) on long paragraphs
- center that block (`margin-inline: auto`) if the section is centered

Why it’s hard to “feel” without the concept:
- the page can look “fine” but still feel unprofessional because reading is uncomfortable

### E) Line-height: headings vs body

- Body text usually likes `1.4–1.7`
- Large headings often need tighter line-height like `1.05–1.2`

Why:
- headings have large glyphs; too much line-height looks loose

---

## 5) Layout responsiveness (so text doesn’t have to suffer)

### A) The `height` trap

Avoid fixed `height` for text-heavy containers (hero, cards).

Preferred:
- `min-height` for “at least viewport height”
- padding for breathing room
- allow content to grow naturally

Why:
- text wraps differently on different widths/zoom settings

### B) Grid that adapts (avoid “3 columns always”)

If you force 3 columns, the text gets squeezed and wraps badly.

Better patterns:
- responsive grid with min column width (cards wrap automatically)
- or breakpoints: 3 → 2 → 1 columns

Why:
- layout should adapt so typography remains readable

### C) Spacing must be responsive too

Giant padding that looks great on desktop can destroy mobile layout.

Best practice:
- use a spacing scale (tokens)
- scale with `clamp()` or adjust tokens in media queries

---

## 6) Components: what “done” looks like

### A) Buttons (base + variants + states)

A real `.btn` includes:
- base structure (display, padding, radius, font-weight)
- variants (`--primary`, `--secondary`, `--outline`)
- interaction states (`:hover`, `:active`, `:focus-visible`)
- transitions (color/background/transform/shadow)

Why:
- “professional UI” is 50% states

### B) Cards

A card component usually owns:
- background + border + radius + padding
- hover elevation (optional)
- internal spacing between title and text

Why:
- your grid layout shouldn’t know card styling details

### C) “Highlight” / “Badge” text

A highlight component should still look like a highlight anywhere:
- background tint
- padding
- radius
- font-weight

Why:
- you want reuse, not one-off styling

---

## 7) A demo problem (from scratch) to practice the concepts

### The problem

Build a simple marketing section:
- A centered heading and paragraph
- Two buttons
- A 3-card grid of features that wraps on smaller screens

### Step 1: HTML (structure only)

```html
<section class="launch" aria-label="Product launch">
  <div class="launch__inner">
    <header class="section-header">
      <p class="highlight">New</p>
      <h2 class="section-header__title">Launch faster with less design debt</h2>
      <p class="section-header__subtitle">
        A lightweight toolkit that keeps typography readable and layouts resilient.
      </p>
    </header>

    <div class="launch__actions">
      <a class="btn btn--primary" href="#">Start free</a>
      <a class="btn btn--outline" href="#">View docs</a>
    </div>

    <div class="feature-grid">
      <article class="feature">
        <h3 class="feature__title">Tokens</h3>
        <p class="feature__desc">Define type, color, and spacing once.</p>
      </article>
      <article class="feature">
        <h3 class="feature__title">Components</h3>
        <p class="feature__desc">Build reusable UI with variants and states.</p>
      </article>
      <article class="feature">
        <h3 class="feature__title">Responsive</h3>
        <p class="feature__desc">Let layout adapt so text stays readable.</p>
      </article>
    </div>
  </div>
</section>
```

What this teaches:
- `section → __inner` pattern
- header block pattern
- actions wrapper owns layout (buttons don’t)
- grid wrapper owns layout (cards don’t)

### Step 2: CSS system (tokens + global defaults)

Start with:
- reset
- tokens (`:root`)
- base typography (`body`, headings)

Key concept:
- **components should mostly consume tokens**, not invent magic numbers

### Step 3: Layout (section spacing + grid)

Apply:
- `.launch` vertical padding
- `.launch__inner` max-width/centering
- `.launch__actions` flex layout + wrap
- `.feature-grid` responsive grid behavior

### Step 4: Typography rules (specific, not global)

Apply:
- a readable measure (`max-width: 60ch`) to `.section-header__subtitle`
- center alignment only for the header block

### Step 5: Components (btn + highlight + feature card)

Apply:
- `.btn` base + variants + states
- `.highlight` background/padding/radius
- `.feature` card styling

---

## 8) Debugging checklist (when styling feels “random”)

1. **Is the HTML nesting correct?** (DOM structure)
2. **Am I styling layout and typography in the same selector?** (separate them)
3. **Did I apply a rule too high up the tree?** (e.g. centering a whole section)
4. **Is the container constrained?** (max-width and padding)
5. **Is line length controlled for paragraphs?** (measure)
6. **Does layout adapt before text gets crushed?** (grid wrap / breakpoints)

---

## 9) How this maps to your capstone specifically

When you’re working in `12-capstone-quill-project/`:
- Use tokens in `12-capstone-quill-project/style.css:3` as the single source of truth for type and spacing.
- Make typography responsive by changing tokens near `12-capstone-quill-project/style.css:20`.
- Put “readability” (`max-width` in `ch`) on text blocks in hero/section header/CTA (see `12-capstone-quill-project/starter.html:34`, `12-capstone-quill-project/starter.html:66`, `12-capstone-quill-project/starter.html:106`).
- Put layout responsiveness on the layout wrappers like `.feature-grid` (`12-capstone-quill-project/style.css:175`) instead of shrinking font sizes to “make it fit”.

If you want, describe one specific situation you face (example: “hero title wraps awkwardly at 375px”) and I’ll translate it into: (1) what layer it belongs to, (2) exactly where you should change CSS, and (3) how to verify it in DevTools.

