# 05 — Dynamic Calc Hero

## Objective
Create a “perfect” hero section that always fits above the fold **without hiding behind the navbar**.

## Key Tools
### `:root` Variables
CSS variables let you define reusable design tokens:
```css
:root {
  --nav-height: 72px;
}
```

### `calc()`
`calc()` lets you compute values with mixed units:
```css
height: calc(100vh - var(--nav-height));
```

This is ideal when you need the hero to be “viewport height minus fixed header”.

## Challenge
In `style.css`:
1. Define `--nav-height` on `:root`
2. Set `.nav` height to `var(--nav-height)`
3. Set `.hero` height to `calc(100vh - var(--nav-height))`

## Done When
- The hero fills the remaining viewport under the navbar.
- Changing `--nav-height` updates both the navbar and hero automatically.

