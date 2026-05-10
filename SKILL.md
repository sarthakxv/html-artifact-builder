---
name: html-artifact-builder
description: 'Creates pure HTML + CSS artifacts as a single self-contained file with no build step, no JavaScript, and no framework dependencies. Use whenever the user asks for an artifact, UI mockup, document, dashboard, form, card, landing page, table, tool, or any visual/interactive interface that should be shareable as a single HTML file. Triggers for: "make a page", "create an artifact", "build a UI", "design a dashboard", "I need something visual", "can you make an HTML...", "create a tool that shows...", "build me a...", or any request that calls for rendering information visually in a browser. Prefer this over web-artifacts-builder for anything that doesn''t explicitly require React or complex cross-component state management.'
---

# HTML Artifact Builder

Write a single self-contained `artifact.html` with an inline `<style>` block. No build step. No bundler. No dependencies beyond an optional Google Fonts `<link>`. Share the file directly as an artifact.

**Stack**: HTML5 + CSS3 (custom properties, grid, flexbox) + Google Fonts (CDN, optional) + CSS-only interactions

## Workflow

1. Understand the content type and intended use (reading-heavy? data-dense? interactive?)
2. Choose a font pairing from the curated list below
3. Define CSS custom properties at `:root` (colors, fonts, spacing, radius)
4. Write semantic HTML — use meaningful elements (`<article>`, `<nav>`, `<aside>`, `<figure>`)
5. Write the `<style>` block — reset → tokens → layout → components → states
6. Share the `.html` file

---

## Design Philosophy

The goal is work that looks designed, not generated. Every decision should feel intentional.

### The slop list — never do these

- **Centered everything** — `display:flex; justify-content:center; align-items:center` with a floating card is the most recognizable AI layout. Use real layouts: sidebars, editorial columns, split grids.
- **Purple/blue gradients** — `linear-gradient(135deg, #667eea, #764ba2)` and its relatives are the AI-generated web's signature. Extend this to all gradients: flat color surfaces always look more intentional than gradient fills.
- **Uniform border-radius** — applying `border-radius: 8px` or `12px` to everything creates a toy-like look. Use it intentionally: 0 for tables, 2px for inputs, never `16px` on cards.
- **Inter as default font** — it signals "this wasn't designed." Choose something with personality.
- **Centered hero section** — a huge centered heading + subtitle + call-to-action button on a gradient background is the most AI-generated layout in existence. Avoid unless the user is explicitly building a marketing landing page.
- **Shadow on every card** — `box-shadow: 0 4px 6px rgba(0,0,0,0.1)` on everything creates visual noise. Use borders or background contrast to separate surfaces.
- **Filling every corner** — resist the urge to put content in every quadrant. Empty space is a design tool.

### Layout principles

- Think in columns and editorial flows, not floating cards.
- Asymmetry reads as more designed than symmetry. A 2/3–1/3 split beats 1/2–1/2.
- Left-align body text. Center only short headings and captions.
- Pick a base unit (e.g., `0.75rem`) and space in multiples of it.
- Let content breathe — generous outer margins with a clear inner boundary.

### Typography

Three typefaces, each with a distinct job — never use one family for everything:

- **Serif** (`--font-heading`) — headings, display text, titles. Gives authority and editorial character. Use for `h1`–`h3`.
- **Sans-serif** (`--font-body`) — body paragraphs, prose, UI labels. Maximizes legibility at reading size.
- **Monospace** (`--font-mono`) — code, technical labels, metadata, ALL-CAPS tags. Signals precision.

The contrast between serif headings and sans body *is* the typographic texture. A single font throughout — especially a monospace for body — flattens hierarchy and kills legibility.

Other rules:
- Max 3 size steps for body content. Headings can scale beyond.
- Use `clamp()` for responsive heading sizes: `font-size: clamp(1.8rem, 4vw, 3rem)`.
- Letter-spacing only for ALL-CAPS labels and small captions.
- Line height: 1.5–1.65 for body, 1.05–1.2 for headings.

### Color

- Background: not pure `#fff` or `#000`. Off-whites (`#f7f4ef`, `#fafaf8`) and near-blacks (`#111`, `#1a1a1a`) read as considered.
- Max 4 semantic colors: background, text, muted text, accent.
- Accent appears rarely — links, active states, key actions only.
- Don't use color to separate every element; use spacing and borders first.

---

## Font Pairings

```html
<!-- Always include before your <style>. System fallbacks are mandatory. -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=FONT_STRING&display=swap" rel="stylesheet">
```

Each pairing assigns the three roles: **heading** (serif), **body** (sans), **mono** (labels/code).

| Mood | Heading | Body | Mono | Google Fonts string |
|------|---------|------|------|---------------------|
| Editorial | **Fraunces** | **DM Sans** | Space Mono | `Fraunces:ital,wght@0,200;0,700;1,700&family=DM+Sans:wght@400;500&family=Space+Mono:wght@400;700` |
| Technical | **Instrument Serif** | **Space Grotesk** | Space Mono | `Instrument+Serif:ital@0;1&family=Space+Grotesk:wght@400;500&family=Space+Mono:wght@400` |
| Warm, literary | **Spectral** | **Literata** | Space Mono | `Spectral:ital,wght@0,300;0,600;1,400&family=Literata:ital,wght@0,400;1,400&family=Space+Mono:wght@400` |
| No CDN | Georgia | system-ui | monospace | no import needed |

CSS token assignment (always declare all three):
```css
--font-heading: 'Fraunces', Georgia, serif;
--font-body:    'DM Sans', system-ui, -apple-system, sans-serif;
--font-mono:    'Space Mono', ui-monospace, 'Courier New', monospace;
```

---

## CSS Reset + Token Template

Every artifact needs a `<meta name="viewport">` tag and a CSS reset. Start with:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body {
  font-family: var(--font-body);
  font-size: 1rem; /* never go below 16px — mobile browsers scale down text otherwise */
  background: var(--bg);
  color: var(--text);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}
img, svg { display: block; max-width: 100%; }
a { color: var(--accent); }
```

### Light mode tokens

```css
:root {
  --bg:           #f7f4ef;
  --bg-surface:   #eeebe4;
  --text:         #1c1a17;
  --text-muted:   #6b6560;
  --accent:       #b5451b;
  --border:       rgba(0,0,0,0.1);

  --font-heading: 'Fraunces', Georgia, serif;
  --font-body:    'DM Sans', system-ui, sans-serif;
  --font-mono:    'Space Mono', ui-monospace, monospace;

  --s1: 0.25rem; --s2: 0.5rem;  --s3: 0.75rem; --s4: 1rem;
  --s6: 1.5rem;  --s8: 2rem;    --s12: 3rem;   --s16: 4rem;

  --r-sm: 2px; --r-md: 4px; --r-pill: 999px;
}
```

### Dark mode tokens

Dark mode demands higher contrast than light mode. The eye adjusts to the dark background and becomes more sensitive to contrast differences — what looks fine on a light surface can feel dim and illegible on dark.

```css
:root {
  --bg:           #131310;   /* very dark warm near-black */
  --bg-surface:   #1d1c18;   /* slightly lighter for cards/tables */
  --text:         #ede9df;   /* warm off-white — use for ALL body/paragraph text */
  --text-muted:   #b0a898;   /* for labels, timestamps, captions ONLY — never prose */
  --accent:       #c8a84b;   /* warm gold reads well on dark */
  --border:       rgba(255,255,255,0.09);

  /* same font tokens as above */
}
```

**Token usage — this is where legibility breaks down most often:**

| Token | Use for | Never use for |
|-------|---------|---------------|
| `--text` | All paragraphs, descriptions, summaries, body copy, section text | — |
| `--text-muted` | Single-line metadata: timestamps, tab labels, column headers, disabled states | Paragraphs, descriptions, any multi-line text |

The most common mistake is applying `--text-muted` to description or summary text because it "looks secondary" conceptually. Visually, a description is body copy — it must be `--text`. Reserve `--text-muted` for items that are genuinely peripheral: a date stamp, a nav label, a table column heading.

---

## Layout Skeletons

All layouts are **mobile-first**: the default CSS targets small screens, `@media` queries layer in the multi-column version. This is what makes text stay legible at phone widths instead of shrinking.

### Editorial / long-form

```css
.prose {
  max-width: 42rem;
  margin: 0 auto;
  padding: var(--s8) var(--s4);   /* tight on mobile */
}
@media (min-width: 640px) {
  .prose { padding: var(--s16) var(--s6); }
}
```

### Sidebar + main

On mobile: sidebar collapses to a horizontal nav strip at top. On desktop: sticky side column.

```css
/* mobile: stacked */
.layout { display: block; min-height: 100vh; }
.sidebar {
  border-bottom: 1px solid var(--border);
  padding: var(--s4);
  display: flex; flex-wrap: wrap; gap: var(--s3);
}
.main { padding: var(--s6) var(--s4); }

@media (min-width: 768px) {
  .layout  { display: grid; grid-template-columns: 15rem 1fr; }
  .sidebar {
    display: block;
    border-bottom: none;
    border-right: 1px solid var(--border);
    padding: var(--s8) var(--s6);
    position: sticky; top: 0; height: 100vh; overflow-y: auto;
  }
  .main { padding: var(--s8); }
}
```

### Two-column (2/3 + 1/3)

```css
.two-col { max-width: 72rem; margin: 0 auto; padding: var(--s6) var(--s4); }
@media (min-width: 768px) {
  .two-col { display: grid; grid-template-columns: 2fr 1fr; gap: var(--s8); padding: var(--s8) var(--s6); }
}
```

### Card grid

```css
.grid {
  display: grid;
  grid-template-columns: 1fr;   /* single column on mobile */
  gap: var(--s4);
  padding: var(--s4);
}
@media (min-width: 480px) {
  .grid { grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); }
}
```

### Full-bleed section

```css
.section        { padding: var(--s8) var(--s4); }
.section__inner { max-width: 64rem; margin: 0 auto; }
@media (min-width: 640px) {
  .section { padding: var(--s12) var(--s6); }
}
```

---

## Page Header

Document-style artifacts (reports, specs, reference docs, architecture write-ups) should open with a clear title moment. This is distinct from the banned "hero section" — it is left-aligned, has no CTA, and uses a kicker + serif title + summary structure rather than a centered gradient splash. Skip this for tools, forms, and single-screen dashboards.

A kicker (category/date in mono), a large serif title, and a short summary in body text — this three-layer hierarchy establishes the visual key for the rest of the page.

```html
<header class="page-header">
  <p class="kicker">Category — Month Year</p>
  <h1 class="title">Document title here</h1>
  <p class="summary">One or two sentences describing what this document covers or the key takeaway. Written in body font, giving the heading room to breathe above it.</p>
</header>
```

```css
.page-header {
  padding: var(--s12) 0 var(--s8);
  border-bottom: 1px solid var(--border);
  margin-bottom: var(--s12);
}
.kicker {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: var(--s4);
}
.title {
  font-family: var(--font-heading);
  font-size: clamp(2.4rem, 6vw, 4rem);  /* responsive without media queries */
  font-weight: 700;
  line-height: 1.08;
  letter-spacing: -0.02em;
  color: var(--text);
  margin-bottom: var(--s4);
}
.summary {
  font-family: var(--font-body);
  font-size: 1.05rem;
  line-height: 1.65;
  color: var(--text);   /* --text, not --text-muted — this is primary reading content */
  max-width: 52rem;
}
```

The `clamp()` on `.title` handles responsive sizing without a media query — the heading stays proportional at any viewport width.

---

## CSS-Only Interaction Patterns

No JavaScript. These use native HTML + CSS selectors.

### Accordion

```html
<details class="accordion">
  <summary>Section title</summary>
  <div class="accordion__body"><p>Content.</p></div>
</details>
```
```css
.accordion { border-bottom: 1px solid var(--border); }
.accordion summary {
  list-style: none; cursor: pointer;
  padding: var(--s4) 0; font-weight: 500;
  display: flex; justify-content: space-between;
}
.accordion summary::after { content: '+'; }
.accordion[open] summary::after { content: '−'; }
.accordion__body { padding-bottom: var(--s4); color: var(--text-muted); }
```

### Tabs (radio inputs)

```html
<div class="tabs">
  <input type="radio" name="t" id="t1" checked hidden>
  <input type="radio" name="t" id="t2" hidden>
  <nav class="tabs__nav">
    <label for="t1">Tab 1</label>
    <label for="t2">Tab 2</label>
  </nav>
  <div class="tabs__panels">
    <section id="p1">Panel 1 content</section>
    <section id="p2">Panel 2 content</section>
  </div>
</div>
```
```css
.tabs__panels section { display: none; padding: var(--s6) 0; }
#t1:checked ~ .tabs__panels #p1,
#t2:checked ~ .tabs__panels #p2 { display: block; }

.tabs__nav label { padding: var(--s3) 0; margin-right: var(--s6); cursor: pointer; border-bottom: 2px solid transparent; color: var(--text-muted); }
#t1:checked ~ .tabs__nav label[for="t1"],
#t2:checked ~ .tabs__nav label[for="t2"] { border-color: var(--accent); color: var(--text); }
```

### Toggle / reveal

```html
<input type="checkbox" id="menu" hidden>
<label for="menu" class="toggle-btn">Menu</label>
<nav class="toggle-panel">…</nav>
```
```css
.toggle-panel { display: none; }
#menu:checked ~ .toggle-panel { display: block; }
```

### Modal (`:target`)

```html
<a href="#modal" class="btn">Open</a>
<div class="modal" id="modal">
  <div class="modal__box">
    <a href="#" class="modal__close" aria-label="Close">×</a>
    <p>Modal content.</p>
  </div>
</div>
```
```css
.modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.45); place-items: center; }
.modal:target { display: grid; }
.modal__box { background: var(--bg); padding: var(--s8); max-width: 32rem; width: 90%; position: relative; }
.modal__close { position: absolute; top: var(--s4); right: var(--s4); text-decoration: none; font-size: 1.25rem; color: var(--text-muted); line-height: 1; }
```

### Tooltip (hover)

```html
<span class="tip" data-tip="Tooltip text">hover me</span>
```
```css
.tip { position: relative; cursor: default; border-bottom: 1px dashed var(--text-muted); }
.tip::after {
  content: attr(data-tip);
  position: absolute; bottom: calc(100% + 6px); left: 50%; transform: translateX(-50%);
  background: var(--text); color: var(--bg); padding: var(--s1) var(--s3);
  font-size: 0.8rem; white-space: nowrap; border-radius: var(--r-sm);
  opacity: 0; pointer-events: none; transition: opacity 0.15s;
}
.tip:hover::after { opacity: 1; }
```

---

## Pre-share checklist

**Mobile**
- `<meta name="viewport" content="width=device-width, initial-scale=1">` present in `<head>`?
- Layout is mobile-first (single column by default, grid added via `@media min-width`)?
- Body `font-size` is at least `1rem` (16px) — never smaller?
- Content still readable at 375px viewport width?

**Typography**
- Three font roles declared: `--font-heading` (serif), `--font-body` (sans), `--font-mono`?
- Headings use `--font-heading`, body paragraphs use `--font-body`, labels/code use `--font-mono`?
- Heading uses `clamp()` for fluid responsive sizing?
- If document-style (report/spec/doc): opens with kicker → title → summary? If tool/form/dashboard: skip this.

**Color & contrast**
- Dark mode: `--text` is near-white (`#ede9df` range)? `--text-muted` is at least `#aaa` brightness?
- Is `--text-muted` used ONLY for single-line metadata (labels, timestamps, column headers) — not for any paragraph or description text?
- All descriptions, summaries, and body paragraphs use `--text`, not `--text-muted`?
- Max 4 semantic color variables in `:root`?

**Design**
- Uses a real layout (not just a centered card on a background)?
- Border-radius is intentional, not uniform `8px` everywhere?
- No gradients unless genuinely intentional?
- Passes the squint test — is the visual hierarchy clear at a glance?
- Interactions (if any) use CSS-only patterns from above?
