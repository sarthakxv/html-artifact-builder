# html-artifact-builder

A Claude Code skill that generates polished, self-contained HTML + CSS artifacts — no build step, no JavaScript framework, no dependencies beyond an optional Google Fonts link.

## What it does

Whenever you ask Claude to build a UI, dashboard, document, form, landing page, or any visual interface, this skill activates and produces a single `artifact.html` file you can open directly in a browser or share as-is.

It enforces a design system that avoids common AI-generated UI patterns (gradient cards, centered-everything layouts, Inter as default font) and produces work that looks intentional.

**Triggers on phrases like:**
- "make a page", "create an artifact", "build a UI"
- "design a dashboard", "I need something visual"
- "can you make an HTML...", "create a tool that shows..."
- "build me a...", or any request that calls for rendering something in a browser

## Stack

- HTML5 + CSS3 (custom properties, grid, flexbox)
- Google Fonts via CDN (optional)
- CSS-only interactions (accordions, tabs, modals, tooltips)
- No JavaScript, no build step, no framework

## Install

```bash
git clone https://github.com/sarthakvdev/html-artifact-builder ~/.claude/skills/html-artifact-builder
```

Restart Claude Code. The skill will be available automatically.

## Usage

Just describe what you want. Claude will invoke the skill and produce `artifact.html`.

```
Can you make an HTML dashboard showing monthly revenue by region?
Build me a product spec document for a new feature.
Create an artifact — a card layout for a team directory.
```

## Design principles enforced

- **No gradient fills** — flat color surfaces always look more intentional
- **Three-typeface system** — serif headings, sans body, mono for labels/code
- **Mobile-first layouts** — single column by default, multi-column via media queries
- **Intentional border-radius** — 0 for tables, 2px for inputs, never uniform 8px on everything
- **Dark mode tokens** — high-contrast near-white text on near-black backgrounds
- **Real layouts** — sidebars, editorial columns, split grids — not a centered card on a background

## License

MIT
