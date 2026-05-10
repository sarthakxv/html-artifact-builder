# html-artifact-builder

An agent skill that writes single-file HTML + CSS artifacts. Open one in a browser. Send it to anyone.

## What it does

Ask for a dashboard, landing page, form, or document. The skill writes `artifact.html` to your working directory.

The skill bans the defaults that mark a page as AI-generated: gradient cards on tinted backgrounds, centered-everything layouts, Inter at 16px on every text element.

**Activates on phrases like:**

- "make a page", "create an artifact", "build a UI"
- "design a dashboard", "I need something visual"
- "can you make an HTML...", "create a tool that shows..."
- "build me a..."

## Stack

- HTML5 + CSS3.
- Custom properties, grid, flexbox for layout.
- CSS-only patterns for accordions, tabs (`:target`), modals (`:checked`), and tooltips.
- Optional Google Fonts via CDN.
- Zero JavaScript, zero build step.

## Install

```bash
npx skills add sarthakxv/html-artifact-builder
```

Or clone manually:

```bash
git clone https://github.com/sarthakxv/html-artifact-builder ~/.claude/skills/html-artifact-builder
```

## Examples

```
Make an HTML dashboard showing monthly revenue by region.
Build a product spec for a new onboarding feature.
Create a card layout for a team directory.
```

## Design principles

- **Flat color surfaces over gradient fills.** Gradients read as decorative; flat blocks read as deliberate.
- **Three typefaces.** Serif headings, sans body, mono for labels and code.
- **Mobile-first.** Single column by default; multi-column at media query breakpoints.
- **Considered border-radius.** 0 for tables, 2px for inputs, larger only where the surface earns it. The uniform 8px-on-everything look is the giveaway.
- **Dark mode.** Near-white on near-black.
- **Real page structures.** Sidebars, editorial columns, split grids. A centered card on a flat background is the fallback, not the goal.

## License

MIT
