# Praxis · Website Patterns v1

**Status:** LOCKED
**Version:** v1
**Date:** 2026-04-22
**Companions:** `../foundations/typography.md`, `../foundations/color.md`, `../foundations/logo.md`, `../components/button.md`, `../components/card.md`
**Visual companion:** `website.html`

## Purpose

Phase 3 closes here. Seven marketing surfaces the Praxis site needs, composed from already-locked primitives. No new components. No per-surface specs. The HTML visual is the spec.

This document captures the decisions baked into the HTML so they don't have to be re-derived during Phase 4 (website MVP build).

## Surfaces (all in the HTML)

1. **Top nav.** Logo tile + wordmark left. Four text links + one terracotta CTA right. 20px vertical padding. Wordmark 22px.
2. **Hero.** Fraunces 72px headline with one italic phrase for accent. Signal eyebrow label. 19px supporting paragraph. Hero button paired with Ghost. Meta row below the fold: engagement shapes + location.
3. **Metric row.** 4-tile grid. Value in Fraunces 40px. Eyebrow uppercase 11px. Caption 12px muted. Tiles on surface warm-700, page band on warm-900.
4. **Case study cards.** 3-up grid. Extension of Card v1 Flat variant. Industry eyebrow, Fraunces 22px headline, signal-colored result line (JetBrains Mono), body copy, tag chips, read-more row at bottom with arrow.
5. **CTA band.** Full-width warm-950 band. Signal eyebrow, Fraunces 44px headline, hero + ghost pair centered.
6. **Contact form.** 2-column: copy left, form right. Inputs 40px height, 6px radius, warm-950 fill, border-subtle. Focus ring identical to button (2px signal 40%, offset 2px). Select has custom chevron. Textarea min-height 120px. Helper text 12px muted.
7. **Footer.** 4-column grid. Brand block left with tagline, three link columns. Copyright row bottom with legal links.

## Decisions baked in

**Icon direction.** Lucide. Stroke weight 1.75. Sizes tied to container: 14/16/18px inside sm/md/lg buttons; 20px for nav and body use; 24px for feature treatments. `currentColor`, no fills. No custom icons unless the brand needs one.

**Type in marketing register.** Fraunces italic 500 stays reserved for the wordmark only. Fraunces roman 500 carries hero and section headlines (44 to 72px). Inter 400 body, Inter 500 UI labels and buttons. JetBrains Mono for case results and metric captions.

**Color discipline on public surfaces.**
- Warm-800 is page default.
- Warm-900 for hero background and metric row band (subtle contrast step).
- Warm-950 for CTA band and input fills (deeper contrast step).
- Signal appears on: logo tile, single hero CTA, eyebrow labels for emphasis, case result lines. Nowhere else.
- Zero Feature cards on public marketing surfaces. The "feature card" role is played by the CTA band itself.
- Primary button stays terracotta. Hero button (Signal) appears once in the nav CTA and once in the hero, and once in the CTA band. Across the page, Signal buttons should total 2 to 3 max.

**Form inputs.** Not a full forms system. Just what the site needs: text input, email input, select, textarea. All inherit the 6px button radius, the focus ring contract, and the border-subtle baseline. States (error, disabled) appear if and when a real form needs them. No speculative building.

**Case result line convention.** JetBrains Mono, signal-500 color, format: "before → after" or "metric + change." Example: `5 hours per intake → 20 minutes`. Always quantified. Always specific. Never adjective-led.

## What this does not cover

- Blog post / playbook article template. Typography will handle it when needed. No decision required now.
- Pricing page layout. Defer until you have pricing to show. Metric row + CTA band cover most of the need.
- Navigation on mobile. Hamburger pattern is standard; revisit during Phase 4 build.
- Form error states. Add when the real form has validation logic wired in.
- Dark/light toggle. Dark is the canonical. Light is available per Color v1 if the site ever needs it.

## Asset exports (triggered for Phase 4)

Logo assets needed before website goes live:

- Logo tile SVG master (square, rounded, Π centered)
- Tile PNG at 32 / 64 / 128 / 256 / 512 / 1024
- Favicon set: 16, 32, 180 (apple-touch-icon), SVG
- OG / Twitter card: 1200×630, tile + wordmark on Warm-900 background
- LinkedIn company cover: 1128×191, tile left, tagline right
- Wordmark SVG (Fraunces italic 500 opsz 144) for email signatures and embeds
- Horizontal lockup SVG (tile + wordmark, nav use)

Wordmark and tile specs are in `../foundations/logo.md` §8. This list is what to ask for, in what format.

## What this locks

- Six + one marketing surfaces composed from Typography v1, Color v1, Logo v1, Button v1, Card v1.
- Icon direction (Lucide, 1.75 stroke, sized to container).
- Type register (Fraunces roman for headlines, italic for wordmark only, Inter for body/UI, JetBrains Mono for metrics and results).
- Color discipline on marketing: warm-800 / 900 / 950 layering, Signal appears 2-3 times per page max, zero Feature cards.
- Form input baseline (40px height, 6px radius, matching focus ring). Minimal, not a forms system.
- Case result convention (mono, signal, quantified before-after).
- Asset export list for Phase 4.

## Next: Phase 4

Website MVP build. Homepage + Work index + 3 case study detail pages + Playbooks hub + About + Contact. Static site (Next.js or Astro, pick during Phase 4 kickoff). Case study content is the next real copywriting task.
