# Praxis Design System

Source of truth for the Praxis brand visual system. Authored April 2026. Open-sourced under MIT license.

## What this is

A small, opinionated design system for a marketing website, proposals, email, and LinkedIn. Three components, two foundations, one composition layer. No framework dependencies. No app-specific opinions.

If you're here to extract tokens, start with `tokens/tokens.css`. If you're here to copy the system for your own project, fork the repo and replace the brand colors.

## Repo layout

```
design-system/
├── README.md                    you are here
├── CHANGELOG.md                 Keep a Changelog format, semver
├── LICENSE                      MIT
├── tokens/
│   └── tokens.css               CSS variable contract (the source of truth)
├── foundations/
│   ├── color.md                 palette, WCAG pairings, scarcity rules
│   ├── color.html               visual palette, contrast tests, good / bad
│   ├── typography.md            Fraunces / Inter / JetBrains Mono, size ladder
│   ├── typography.html          live type scale and pairings
│   └── logo.md                  mark + wordmark + lockup geometry
├── components/
│   ├── button.md                5 tiers, 3 sizes, 6 states
│   ├── button.html              every variant x size x state rendered
│   ├── card.md                  4 variants, 3 sizes, 6 states, 4 slots
│   └── card.html                variant grid, state matrix, slot composition
├── patterns/
│   ├── website.md               7 marketing surfaces, icon direction, scarcity
│   └── website.html             full marketing page composed from primitives
└── assets/                      (future: logo SVGs, favicons, OG cards)
```

## Critical tokens

```
Brand colors
  Signal     #A3FF12   acid lime, reserved for brand emphasis
  Terracotta #B8654A   warm clay, primary CTA
  Warm scale Warm-50 (#FCFAF6) to Warm-950 (#141210), 11 steps

Type families
  Display: Fraunces (variable: opsz, SOFT, wght)
  Body:    Inter
  Mono:    JetBrains Mono

Radius family
  Button   6px
  Card     8px
  Tile     9% of container width (logo tile only)

Focus ring
  2px solid rgba(163, 255, 18, 0.4) at 2px offset
  One contract, used everywhere
```

Full token set in `tokens/tokens.css`. Dark is canonical. Light theme via `.theme-light` class override.

## Scarcity rules

Two rules keep the system from being loud:

1. **Signal is scarce.** Reserved for the logo tile, one Hero CTA per screen, eyebrow labels for emphasis, and case result lines. Two to three Signal appearances per marketing page, maximum.
2. **Feature cards are scarce.** Zero Feature cards on public marketing surfaces. One Feature card per dashboard view, maximum.

Both rules are enforced in the visual companions with good vs bad examples.

## What this does not include

- **No full forms system.** Only the four input types the contact form needs (text, email, select, textarea), specified inside the website pattern. Build a real forms system when a real form needs it.
- **No mobile nav pattern.** Hamburger is standard, deferred to the site build.
- **No feedback system.** No toasts, banners, or modals yet. Add on first real need.
- **No icon library.** Decision: Lucide, 1.75 stroke weight, sized to container. Not bundled.
- **No shadows.** Depth is color and border, not elevation.
- **No motion spec.** Hover and focus transitions are stated per component.

## Versioning

Semver. v1.0.0 is the initial release. Git tags mark releases. See `CHANGELOG.md`.

- Patch: doc fixes, typos, clarifications.
- Minor: new component or token, backward-compatible.
- Major: renamed or removed token, changed radius family, anything consumers must update for.

## License

MIT. Fork it, rebrand it, ship it. See `LICENSE`.

## Origin

Built by Praxis, an applied-AI studio in New York. The system shipped here is the one that powers praxis.com. It's published because small teams need small design systems, and because the decision reasoning in each `.md` file is more useful than the tokens themselves.
