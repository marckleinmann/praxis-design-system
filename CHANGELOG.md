# Changelog

All notable changes to the Praxis Design System are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-04-22

Initial release. Phase 3 of the Praxis brand build is locked.

### Added

- **Tokens** (`tokens/tokens.css`). Full CSS variable contract: warm neutral scale (50 to 950, 11 steps), Signal accent (100 to 900), Terracotta accent (100 to 900), four semantic UI families (destructive, success, warning, info), semantic surface and text tokens, button tokens, typography families, radius family, focus ring contract. Dark-first with optional `.theme-light` override.
- **Color system** (`foundations/color.md`, `foundations/color.html`). Two-layer architecture (raw palette plus semantic roles). WCAG AA contrast pairings. Button hierarchy scarcity rule: Signal is reserved for logo and single hero CTA per screen.
- **Typography** (`foundations/typography.md`, `foundations/typography.html`). Fraunces (variable, opsz-matched), Inter, JetBrains Mono. Validated size ladder from 10px caption to 120px hero. Six authorized wordmark treatments.
- **Logo** (`foundations/logo.md`). Mark geometry (Signal tile, roman Π weight 600, 9 percent radius). Wordmark spec (Fraunces italic 500, opsz-scaled). Seven lockup sizes. Five authorized color pairings. Export manifest.
- **Button component** (`components/button.md`, `components/button.html`). Five tiers (Hero, Primary, Destructive, Neutral, Ghost), three sizes (28 / 32 / 40), six states, five variants. 6px radius. Inter 500.
- **Card component** (`components/card.md`, `components/card.html`). Four variants (Flat, Outlined, Subtle, Feature), three sizes (sm / md / lg), six states, four slots. 8px radius. Feature variant carries Signal scarcity rule (one per view maximum).
- **Website patterns** (`patterns/website.md`, `patterns/website.html`). Seven marketing surfaces composed from the primitives: top nav, hero, metric row, case study cards, CTA band, contact form, footer. Icon direction locked (Lucide, 1.75 stroke). Signal scarcity on public surfaces: two to three appearances per page maximum.

### Decisions locked

- Radius family: 6px button, 8px card, 9 percent tile.
- Focus ring contract: 2px solid Signal at 40 percent opacity, 2px offset. One ring, used everywhere.
- No shadows. Depth is expressed with color and border only.
- Signal is scarce. Terracotta is the default primary. Success, warning, and info are not button colors.
- Feature card is scarce. Zero on public marketing surfaces. One per dashboard view maximum.
- Dark is canonical. Light theme is available via `.theme-light` override.

### Not yet included

- Full forms system. Only the four input types the contact form needs are specified, inline in the website patterns.
- Mobile navigation. The hamburger pattern is standard and deferred to the website build phase.
- Feedback system (toasts, banners, modals). Add on first real need.
- Icon library. The system specifies icon direction only. Lucide is the chosen library; it is not bundled here.
- Motion system. Hover and focus transitions are stated per component.
