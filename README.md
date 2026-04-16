# Pet Central — Design System

Single source of truth for every Pet Central interface. Every consumer — the marketing site, dashboard, campaign-intelligence app, future products, and any agent-generated output — should reference the tokens, fonts, and logo defined here.

**Live preview:** https://petcentralsa.github.io/pet-central-design-system/

---

## What's in here

```
pet-central-design-system/
├── design-preview.html     ← Visual reference. Open in any browser.
├── tokens/
│   ├── tokens.css          ← CSS custom properties — drop into any stylesheet
│   ├── tokens.json         ← Machine-readable (W3C Design Tokens format)
│   └── tokens.scss         ← Sass variables + breakpoint mixin
├── fonts/                  ← Kefir Bold (header), Jost (UI, variable + italic)
├── assets/
│   ├── logo.svg            ← Wordmark — fill via currentColor or CSS
│   └── favicon.png         ← 32px favicon
└── .github/workflows/      ← Auto-deploys preview to GitHub Pages
```

The preview page is the canonical visual reference. The `tokens/` files are the canonical machine reference. They are kept in sync.

---

## How to use these tokens

### Option 1 — CSS (recommended for most projects)

Copy `tokens/tokens.css` into your project, or import it from a CDN reference:

```html
<link rel="stylesheet" href="https://petcentralsa.github.io/pet-central-design-system/tokens/tokens.css">
```

Then use the custom properties anywhere in your CSS:

```css
.card {
  background: var(--cream-0);
  border: 1px solid var(--navy-50);
  border-radius: var(--r-md);
  box-shadow: var(--shadow-sm);
  color: var(--brand-primary);
}
.card h2 {
  color: var(--brand-primary-deep);
  font-family: var(--font-header);
}
```

### Option 2 — Sass

Import `tokens/tokens.scss` for build-time use. Use variables directly, or the `breakpoint()` mixin for responsive rules:

```scss
@use 'pet-central-design-system/tokens/tokens' as *;

.product-grid {
  padding: 16px;
  background: $cream-50;

  @include breakpoint(md) {
    padding: 32px;
  }
  @include breakpoint(lg) {
    max-width: $content-default;
  }
}
```

### Option 3 — JSON (for tooling, agents, generators)

Parse `tokens/tokens.json` to drive Figma plugins, agent prompts, code generators, or any non-CSS consumer. Format follows the [W3C Design Tokens Community Group](https://design-tokens.github.io/community-group/format/) spec.

```js
import tokens from 'pet-central-design-system/tokens/tokens.json';
const navy = tokens.brand['primary-deep'].$value; // "#163E6F"
```

---

## Token families

| Family | What it covers |
|---|---|
| **Brand** | `brand.primary`, `primary-deep`, `cream`, `terracotta` |
| **Functional** | `info`, `success`, `warning`, `danger`, `seasonal` (each has `bg`/`border`/`text`) |
| **Neutral — cream** | Warm surfaces (`cream-0` → `cream-200`) |
| **Neutral — navy** | Cool text, borders, hints (`navy-0` → `navy-200`) |
| **Radius** | `r-sm` (4px) → `r-xl` (16px), plus `r-full` |
| **Elevation** | `shadow-sm` → `shadow-xl` (navy-tinted, never black) |
| **Focus ring** | `focus-ring-color`, `width`, `offset` |
| **Z-index** | 9 rungs, `z-base` (0) → `z-tooltip` (800) |
| **Content widths** | `content-narrow` (640) → `content-wide` (1440) |
| **Breakpoints** | `bp-sm` (480) → `bp-xl` (1440) |
| **Chart** | 8 categorical colours (`chart-1` → `chart-8`) |
| **Icon sizes** | `icon-xs` (12px) → `icon-xl` (32px) |
| **Logo sizes** | `logo-xs` (16px) → `logo-xl` (88px) |
| **Motion** | Durations (`fast/base/slow`) + easings (`out/inout`) |
| **Type families** | `font-header` (Kefir), `font-ui` (Jost), `font-numbers` (Inter), `font-mono` (JetBrains Mono) |
| **Dark mode** | Scoped to `.dark-stage` or `[data-theme="dark"]` |

See `design-preview.html` for the full visual reference.

---

## Logo usage

Three fill colours, paired with approved backgrounds:

| Fill | Approved on | When to use |
|---|---|---|
| `brand.primary-deep` | cream, neutral | Default — 90% of moments |
| `brand.primary` | cream, primary-deep (tonal) | Surface is busy, deep feels too punchy |
| `brand.cream` | primary-deep, primary | Dark or saturated brand fills |

Apply via the SVG `fill` attribute or `currentColor`:

```html
<svg style="height: 36px; color: var(--brand-primary-deep);">
  <use href="path/to/logo.svg#pc-logo"/>
</svg>
```

Never: distort, recolour outside the matrix above, place on busy patterns, add shadows, rotate, or render below 16px.

---

## Fonts

Self-hosted in `fonts/`. The CSS file declares `@font-face` for Kefir and Jost; Inter and JetBrains Mono are loaded from Google Fonts.

| Font | Use |
|---|---|
| **Kefir Bold** | Headings — distinctive display weight |
| **Jost** (variable + italic) | Body, UI, default text |
| **Inter** | Numerals, data, tabular figures |
| **JetBrains Mono** | Code, design tokens, technical labels |

---

## Updating the system

1. Make your edit in `design-preview.html` first — that's the visual reference.
2. Mirror the change into `tokens/tokens.css`, `tokens.json`, and `tokens.scss`.
3. Bump the `$version` in `tokens.json`.
4. Commit with a descriptive message (`feat: add focus-ring tokens`, `fix: cool down success green`).
5. Push — GitHub Pages will rebuild the preview automatically.

The three token files **must stay in sync**. If you only have time to update one, prefer `tokens.css` (the most-consumed format) and flag the others as TODO.

---

## License

Internal Pet Central use only. Do not redistribute.
