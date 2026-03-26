# Capstone Review — Quill Landing Page (Text + Responsiveness)

This is a targeted review for the “text + responsive typography” parts of the capstone. It tells you **what to change**, **where**, and **why**—so you can apply the concepts intentionally instead of guessing.

## 1) What you already did well

- **Design tokens + `rem`**: You defined color + type tokens and used `rem` everywhere (`12-capstone-quill-project/style.css:3`, `12-capstone-quill-project/style.css:20`).
- **Global reset + base typography**: You set `box-sizing`, `font-family`, and base `line-height` (`12-capstone-quill-project/style.css:38`, `12-capstone-quill-project/style.css:48`).
- **Layout patterns from the drills**: Container, flex nav, calc hero, grid features are all in place (`12-capstone-quill-project/style.css:73`, `12-capstone-quill-project/style.css:84`, `12-capstone-quill-project/style.css:111`, `12-capstone-quill-project/style.css:175`).

## 2) The big idea you’re missing: “Text is layout”

Responsive typography isn’t just “make the font smaller on mobile.” It’s **preventing bad layouts caused by text**:

- Headings wrap unpredictably as width shrinks.
- Paragraphs become hard to read when too wide (desktop) or too tight (mobile).
- Fixed heights cause overflow when text wraps onto more lines.

So your job is to make the system resilient when text takes *more space than you expected*.

## 3) High-priority fixes (in the order pros do them)

### A) Avoid overflow: use `min-height` for hero, not `height`

**Where:** `12-capstone-quill-project/style.css:111`  
**Current:** `.hero { height: calc(100vh - var(--nav-height)); }`

**Why it matters**
- `height` is a hard ceiling. If your title/subtitle wraps more (small screens, bigger OS font, zoom), the hero can’t grow—so content can overflow or get cramped.
- `min-height` says: “be at least this tall, but grow if content needs it.” That’s what you want for text-heavy sections.

**Concept to learn:** *Intrinsic content size beats fixed size for text containers.*

### B) Make the type scale responsive (don’t keep tokens fixed)

**Where:** `12-capstone-quill-project/style.css:20`  
**Current:** `--fs-900: 6.2rem;` etc.

**Why it matters**
- Your `--fs-900` hero size is locked. On phones, 6.2rem can dominate the screen and force awkward wrapping.
- Pros make the **tokens** responsive so every component inherits improved behavior automatically.

**How to think about it**
- Tokens should represent *intent* (“hero title”, “section title”) and adapt by screen size.
- The cleanest “one-rule” tool for this is `clamp(min, fluid, max)`.

**Concept to learn:** *Put responsiveness into tokens; keep components simple.*

### C) Control line length (readability): add a “measure” for paragraphs

**Where text lives (good targets):**
- Hero subtitle: `12-capstone-quill-project/starter.html:34`
- Features section subtitle: `12-capstone-quill-project/starter.html:66`
- CTA description: `12-capstone-quill-project/starter.html:106`

**Why it matters**
- On wide screens, paragraphs can become too long per line, which reduces readability.
- A common professional rule of thumb: keep body text around **55–70 characters per line**.

**How it works**
- CSS supports `ch` units (approx “width of the 0 character”), which is useful for setting readable measures like `max-width: 60ch`.

**Concept to learn:** *“Measure” is a typography constraint, not a layout hack.*

### D) Make the feature grid wrap (3 fixed columns will crush cards)

**Where:** `12-capstone-quill-project/style.css:175`  
**Current:** `grid-template-columns: repeat(3, 1fr);`

**Why it matters**
- At smaller widths, 3 fixed columns means each card gets too narrow and the text wraps badly.
- You want either:
  - a responsive grid (`auto-fit` + `minmax()`), or
  - breakpoints that reduce columns from 3 → 2 → 1.

**Concept to learn:** *Let layout respond so text doesn’t have to “fight” for space.*

### E) Replace huge fixed spacing with responsive spacing

**Where:**
- `12-capstone-quill-project/style.css:190` (`.cta { padding: 10rem 0; }`)
- `12-capstone-quill-project/style.css:200` (`.cta-card { padding: 5rem; }`)

**Why it matters**
- Big padding looks premium on desktop, but wastes space on mobile and pushes content too far down.
- Pros use:
  - `clamp()` to scale spacing smoothly, or
  - breakpoints that reduce padding at smaller widths.

**Concept to learn:** *Spacing is part of responsiveness, not just fonts.*

## 4) Components: what “professional” means here

### A) `.highlight` should match the roadmap (background + padding + radius)

**Where:** `12-capstone-quill-project/style.css:126`  
**Why it matters**
- Right now `.highlight` is basically “small gray text.” The roadmap expects it to be a reusable callout component that can be dropped anywhere.

**Concept to learn:** *A component should still look like itself if moved to another section.*

### B) Buttons need interaction states + motion polish

**Where:** `12-capstone-quill-project/style.css:251`  
**Missing pieces**
- `:hover`, `:active`, `:focus-visible`
- transitions (color/background/transform/shadow)

**Why it matters**
- “Professional” UI is as much about states as it is about base styling.
- `:focus-visible` is critical for keyboard users (accessibility + real-world quality signal).

**Concept to learn:** *Components are defined by their states, not just their default look.*

## 5) HTML structure issue (will affect layout + styling)

**Where:** `12-capstone-quill-project/starter.html:44` (inside `.hero__meta`)

The indentation and closing tags look mismatched: the first `.stat` block doesn’t close cleanly before the next `.stat` begins, and the wrappers close out of order (`12-capstone-quill-project/starter.html:45` to `12-capstone-quill-project/starter.html:58`).

**Why it matters**
- CSS layout bugs are often HTML nesting bugs.
- If the DOM structure isn’t what you think it is, your flex/grid alignment will feel “random.”

**Concept to learn:** *When layout is confusing, validate the DOM first.*

## 6) Font loading: “works” vs “professional”

**Where:** `12-capstone-quill-project/style.css:1` uses `@import`  
**Roadmap expects:** a Google Fonts `<link>` in `12-capstone-quill-project/starter.html` (see `12-capstone-quill-project/README.md`)

**Why it matters**
- In production, `<link>` is the common pattern because it’s clearer and typically loads earlier.
- Your current approach still renders, but it’s not the pattern you were asked to practice in the capstone roadmap.

**Concept to learn:** *Follow the intended workflow; it teaches transferable habits.*

## 7) Practical steps (do this in DevTools)

1. Open the page and test widths: ~360px, ~768px, ~1024px.
2. In the hero, check:
   - Does the title wrap cleanly?
   - Does anything overflow vertically?
3. Toggle device font scaling / zoom if you can (text should still fit).
4. On desktop, check readability:
   - Do long paragraphs get too wide?
5. Check grid behavior:
   - Do feature cards stay readable when the screen narrows?

## 8) Mental model: “Where should I apply typography rules?”

- **Global (apply once):** `body` font + base size + base line-height; heading line-height (`12-capstone-quill-project/style.css:48`, `12-capstone-quill-project/style.css:56`)
- **Tokens (system-level):** responsive type scale + spacing scale (`12-capstone-quill-project/style.css:20`)
- **Layout (section-level):** grid wrapping, hero min-height, footer stacking (`12-capstone-quill-project/style.css:111`, `12-capstone-quill-project/style.css:175`, `12-capstone-quill-project/style.css:226`)
- **Text blocks (element-level):** readable line length (`max-width` in `ch`) on *specific paragraphs*, not every `p` (`12-capstone-quill-project/starter.html:34`, `12-capstone-quill-project/starter.html:66`, `12-capstone-quill-project/starter.html:106`)
- **Components:** buttons + highlight defined by base + variants + states (`12-capstone-quill-project/style.css:251`, `12-capstone-quill-project/style.css:126`)

If you want, tell me which viewport is worst for you (e.g. 375px wide iPhone) and which text looks “off” (hero title vs subtitle vs cards). I’ll give you a tight checklist of exactly what to tweak first and how to verify it (still no code edits unless you ask).

