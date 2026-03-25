# 01 — Specificity Sports Table

## Objective
Resolve a selector conflict where the same `<h1>` is targeted by:
- a **Type selector** (`h1`)
- a **Class selector** (`.title`)
- an **ID selector** (`#title`)

## The “Sports Table” (Priority)
Think of specificity like a sports league table:
1. **ID** selectors win over everything else in normal CSS (`#title`)
2. **Class** selectors beat type selectors (`.title`)
3. **Type** selectors are the lightest weight (`h1`)

If two selectors have the same specificity, the rule that appears **later** wins (source order).

## Challenge
1. Write **three rules** in `style.css`:
   - `h1 { ... }` (Type)
   - `.title { ... }` (Class)
   - `#title { ... }` (ID) but keep it **commented out**
2. With the ID rule commented, make the heading text **Green** using **only** the class selector.
3. (Self-check) Uncomment the ID rule: the heading should immediately turn **Red**.

## Done When
- The `<h1>` is green with `#title` commented.
- The `<h1>` becomes red when `#title` is uncommented.

