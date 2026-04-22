# Praxis - Logo Spec v1

**Status:** LOCKED
**Version:** v1
**Date:** 2026-04-22
**Companions:** `typography.md`, `color.md`

Canonical source for the Praxis primary mark and wordmark. All components, the website, invoice/proposal templates, and asset exports build from this doc.

---

## 1. Mark (monogram)

A Signal-green rounded square tile with a capital Π centered on it.

**Tile**
- Shape: square (1:1)
- Color: Signal `#A3FF12`
- Corner radius: 9% of tile width (8px at 88px; scale proportionally)

**Letter**
- Glyph: capital Π (Greek, Unicode U+03A0)
- Face: Fraunces roman (not italic - italic is reserved for the wordmark)
- Weight: 600
- Color: Warm Dark `#2A2520`
- `opsz`: scaled per size
- `SOFT`: scaled per size (50 at display, 0 at 16px)
- `WONK`: 0

The letter is centered optically, not mathematically. Π is wider than tall; nudge down 2-3% of tile height to sit the horizontal beam visually centered.

---

## 2. Wordmark

References `typography.md` §1.

- Face: Fraunces italic
- Weight: 500
- `opsz`: 144 at hero (120px+), scaled per Typography v1 size ladder
- `SOFT`: 100 at 64px+, 50 at 20-48px, 0 below 20px
- `WONK`: 0
- Tracking: −0.02em at hero (120px+), −0.01em default
- Text: `praxis` (lowercase)

Roman Fraunces is never a wordmark variant. Only italic.

---

## 3. Lockup

Horizontal arrangement. Mark on the left, wordmark on the right.

| Context | Tile size | Gap | Wordmark size | Notes |
|---------|-----------|-----|---------------|-------|
| Favicon | 16 | - | - | Mark only |
| Browser tab | 16 | 8 | 12 | Gap tight |
| Nav (inline) | 28 | 10 | 24 | Standard site header |
| Email signature | 40 | 12 | 32 | Lockup anchor |
| Avatar card | 56 | 14 | 44 | Social / profile |
| Hero | 80 | 20 | 64 | Landing page, proposal covers |
| Hero XL | 120 | 28 | 96 | Launch surfaces, print cover |

Baseline: wordmark sits on the tile's optical center. The Π horizontal beam aligns roughly with the wordmark's x-height midline.

---

## 4. Color pairings

Lockup uses the tile (Signal) as the color anchor. Wordmark color flexes per surface.

| Surface | Tile | Π | Wordmark | Usage |
|---------|------|---|----------|-------|
| Warm Dark `#2A2520` | Signal | Warm Dark | Cream `#F5F0E8` | **Primary** |
| Warm Dark `#2A2520` | Signal | Warm Dark | Signal | High-signal hero (rare) |
| Cream `#F5F0E8` | Warm Dark | Cream | Warm Dark | Print / low-color / letterhead |
| Terracotta `#B8654A` | Cream | Terracotta | Cream | Section-level, full-bleed |
| Warm Darker `#141210` | Terracotta Bright `#D67952` | Warm Darker | Terracotta Bright | Inverted / terminal surfaces |

Authorized only. Any other pairing is off-spec. Specifically disallowed: Signal tile on Cream (too hot), Signal on Terracotta (clash), tile on any gradient.

---

## 5. Clear space

Minimum clear space around the lockup on all sides: **0.5× tile width**.

At 28px tile: 14px clear on all sides.
At 80px tile: 40px clear on all sides.

No other element (text, image, rule, border) enters this zone.

---

## 6. Minimum sizes

- Mark-only (favicon floor): **14px** tile
- Wordmark-only floor: **10px** with SOFT 0, weight 700 (per Typography v1 size ladder)
- Full lockup floor: **18px** tile + 14px wordmark

Below these, use mark-only.

---

## 7. Don't

- No italic Π in the mark. Italic is the wordmark voice. The monogram is roman.
- No outlined tile. Solid fill only.
- No Signal Π on Warm Dark surface without the tile. The tile is the mark; the letter alone is not the mark.
- No weight change on Π. 600 only.
- No skew, rotate, or distort. The tile is square, the letter is upright.
- No gradient fills on tile or letter.
- No Π substitution with P or pi (π). Those were explored and rejected.

---

## 8. Exports

**Mark (tile + Π):**
- Master: SVG, 100×100 viewBox
- PNG raster: 16, 32, 48, 64, 128, 256, 512, 1024
- Favicon: `favicon.ico` (16/32/48 multi-res), `favicon.svg`, `apple-touch-icon.png` (180×180)

**Wordmark:**
- SVG outline (for cases where Fraunces can't load)
- Live type is preferred where possible (Google Fonts CDN, `font-display: swap`)

**Lockup:**
- SVG master with mark + wordmark as live type
- PNG at each Lockup size from §3

Export folder: `/assets/logo/` (to be created).

---

## 9. What this locks

- Primary mark geometry (Signal tile + roman Π wt 600 + radius 9%)
- Wordmark variant (A - italic wt 500 SOFT-scaled)
- Lockup scaling across all production contexts
- Five authorized color pairings
- Clear space, minimum sizes, and prohibited treatments

Any change to mark shape, wordmark face, or color pairings bumps this doc to v2 and triggers a re-export of all assets.

---

## 10. Next deliverables (Phase 3 continuation)

- Full color system: tints, shades, accessibility pairs, semantic role map
- Base components: buttons, cards, form elements, navigation
- Icon direction: scale, stroke weight, corner radius philosophy (should inherit from tile geometry)
- Asset export: run §8 exports once color system is locked

Reference for component work: this logo spec establishes geometry (radius, stroke, proportion) that component design should inherit for visual coherence.
