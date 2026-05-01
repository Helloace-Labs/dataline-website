# Tearline Brand Guide

Working spec for the rebuilt tearline.io site. Lifted from the live CSS and the
`/logos` design exploration. UI handoff doc — copy values directly into Figma /
design system.

---

## 1. Typography

### Fonts

Both fonts ship from **Google Fonts** — no bundled font package in this repo.
Self-host if you need it; spec below.

| Family | Use | Source |
|---|---|---|
| **DM Sans** | All UI / display / body text | https://fonts.google.com/specimen/DM+Sans |
| **Fragment Mono** | Mono accents (eyebrows, metadata, code, micro-stats) | https://fonts.google.com/specimen/Fragment+Mono |

**Weights actually used:**
- DM Sans — 300 (display), 400 (body, default), 500 (emphasis / wordmark)
- Fragment Mono — 400 (only weight available)

### CSS @import

```css
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500&family=Fragment+Mono&display=swap');
```

### CSS variables

```css
--font-main: 'DM Sans', -apple-system, BlinkMacSystemFont, sans-serif;
--font-mono: 'Fragment Mono', ui-monospace, monospace;
```

### Type scale

| Role | Size | Weight | Letter-spacing | Notes |
|---|---|---|---|---|
| Hero H1 | `clamp(2.5rem, 6vw, 5.5rem)` | 300 | -0.025em | line-height 1.05 |
| Section title | `clamp(1.8rem, 3.5vw, 2.8rem)` | 300 | -0.025em | line-height 1.15 |
| Wordmark (header) | 1.05rem | 500 | -0.01em | DM Sans |
| Body | 1rem | 400 | -0.005em | line-height 1.55 |
| Small body | 0.85–0.92rem | 400 | -0.005em | nav, secondary |
| Mono accent / eyebrow | 0.7rem | 400 (mono) | 0.06–0.08em | uppercase |
| Mono micro | 0.62rem | 400 (mono) | 0.08em | live ticker, frame head |

### Self-host (optional)

If the team wants the font files bundled instead of CDN-loaded, grab the woff2
files from google-webfonts-helper:
https://gwfh.mranftl.com/fonts/dm-sans?subsets=latin
https://gwfh.mranftl.com/fonts/fragment-mono?subsets=latin

Drop `dm-sans-*.woff2` and `fragment-mono-*.woff2` into `/fonts/` and replace
the `@import` with `@font-face` blocks. Same family names, same CSS variables.

---

## 2. Color palette

```css
--bg:              #0A0A0A     /* page bg */
--bg-elev:         #111111     /* elevated surface (sticky header bg) */
--bg-card:         #0E0E0E     /* card surface */

--ink:             #E8E6E0     /* primary text — warm cream */
--ink-dim:         #888880     /* secondary text */
--ink-muted:       #555550     /* tertiary text + idle leaves */

--hairline:        rgba(232, 230, 224, 0.10)   /* default 1px border */
--hairline-strong: rgba(232, 230, 224, 0.22)   /* mark-tile, button border */
--hairline-bright: rgba(232, 230, 224, 0.55)   /* high-emphasis line */

--green:       #34d399              /* active state · brand accent */
--green-dim:   rgba(52, 211, 153, 0.55)
--green-faint: rgba(52, 211, 153, 0.18)

--red:         #ef4444              /* alert state */
--red-dim:     rgba(239, 68, 68, 0.55)
```

### Usage rules

- **`--ink` for body text only.** Never use `--green` for prose; reserve it for
  the active state in the mark, hover affordances, and the rare hero accent.
- **Red appears in exactly 2 leaves** per logo render (mirror-balanced). Never
  used for text or buttons.
- **Hairline ladder** carries the layout. Default border is `--hairline`;
  emphasized rows step up to `--hairline-strong`.

---

## 3. Logo / Mark

### The tree (primary mark)

A vertical, animated SVG mark generated procedurally from data attributes.

| Param | Value | Notes |
|---|---|---|
| Orientation | vertical | T-shape |
| Roots (bottom) | 5 | inside a 16% width "trunk" band |
| Leaves (top) | 18 | 9+9 mirror, 22% center gap |
| Curve | arched blade | vertical rise then sweep to leaf |
| Crossover | top-left → rightmost root | left-flowing branches paint over right-flowing in overlap |
| States | green / red / idle | exactly 2 red, ~78% green, rest idle |

### Lockup

Symbol on the left, **"Tearline"** wordmark on the right in DM Sans 500.
No border around the symbol. Examples on `/logos` page (full logo card).

### Sizing rules

| Surface | Size | Density | Roots | Notes |
|---|---|---|---|---|
| Top-nav header | 22 sq | 7 | 1 | dance on, no pulse |
| Marketing hero | 420×320 | 18 | 5 | full motion |
| Favicon | 32 sq | 9 | 1 | static, no animation |
| Email / OG / print | 64 sq | 9 | 1 | static |

### Motion gates (for animated marks)

- **Dance** kicks in at min(w, h) ≥ 22 sq
- **Pulse** kicks in at min(w, h) ≥ 30 sq
- **Static class** (`.static`) suppresses both regardless of size

### Don't

- Don't add a frame / border around the symbol
- Don't change the green / red ratio (always exactly 2 reds, mirror-balanced)
- Don't render in a color outside the palette
- Don't use the horizontal "delta" variant as the primary mark — it's reserved
  for wide-strip surfaces only

---

## 4. Motion vocabulary

| Layer | Timing | Easing |
|---|---|---|
| Streaming dashes (per path) | 8–18s loop, randomized per line | linear |
| Pulse lights (per path) | 2.6–4.8s loop, randomized per line; fade in at 15%, out at 85% | linear (motion) + linear (opacity) |
| Leaf dance (per leaf) | 2.0–3.8s loop, asymmetric (up more than down), amplitude 1.1–2.5× leaf radius | spline `0.4 0 0.2 1` (cubic ease-in-out) |
| Live dot pulse (header `live` indicator) | 1.6s | ease-in-out |
| Hover transitions | 0.15–0.2s | default |

### Per-line independence

Each path / leaf gets its own randomized duration and start offset (deterministic
per density). The mark never marches in lockstep.

---

## 5. Layout primitives

| Token | Value | Used for |
|---|---|---|
| Page padding | 2.5rem | side gutters |
| Max content width | 1100px (logos page) · 1440px (marketing site) | |
| Card gap | 1px | hairline grid (cards live on `--hairline` background) |
| Border weight | 1px | hairline borders, dividers |
| Section spacing | 4rem top, 3.5rem internal | between concept blocks |

### Hairline grid pattern

Cards in a row sit on a `var(--hairline)` background with `gap: 1px`, so the
1px gap reads as a hairline divider. Then the row itself has a 1px border.
This is the page's defining structural rhythm.

---

## 6. Tone

- Dev-first. Show numbers (latency, uptime, confidence), not adjectives.
- Banned phrases: "revolutionary", "next-gen", "synergy", "unleash".
- Hero CTA: **"Try Playground"** — never "Book a demo".
- Tagline: **"Plug intent. Get data."**

---

## 7. Files

- `/site.html` — marketing homepage (live `/`)
- `/data.html` — Tearline Data product page (live `/data`)
- `/logos.html` — design exploration / logo concept gallery (live `/logos`)
- `/index.html` — staging hub (placeholder)
- `/logo-original.png` — reference: original Tearline favicon, 256 sq

The mark is generated by the `buildDelta()` function inline at the bottom of
`/logos.html`. Geometry lives in JS, styling in CSS, both per-instance via
`data-*` attributes on the `<svg class="delta-mark">` element.

---

_Doc owner: design + engineering. Update this file when palette / type / motion
specs change._
