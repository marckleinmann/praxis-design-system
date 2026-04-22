# Praxis - Typography Spec v1

**Status:** LOCKED
**Version:** v1
**Date:** 2026-04-22
**Visual companion:** `typography.html`

Canonical source for Phase 3 onward. All components, the website, and asset templates build from this doc.

---

## 1. Wordmark

**Face:** Fraunces (Google Fonts, variable)
**Style:** italic
**Weight:** 500
**Optical size:** opsz 144
**Soft axis:** SOFT 100 (at 64px+), SOFT 50 (at 20–48px), SOFT 0 (below 20px)
**Tracking:** letter-spacing −0.01em (display), −0.02em (hero 120px+)
**Line height:** 1 (display), 1.05 (hero)

The wordmark is set in Fraunces italic only. Roman Fraunces is not a wordmark variant.

---

## 2. Type stack

**Display and wordmark:** Fraunces italic (variable, opsz 9–144)
**Body and UI:** Inter (400 regular, 500 medium, 600 semibold)
**Mono (labels, case-study meta, code, kickers):** JetBrains Mono (400, 500, 600)

No fourth face. No decorative substitutions.

---

## 3. Size ladder (validated)

| Size | Face | Weight | opsz | Usage |
|------|------|--------|------|-------|
| 120px+ | Fraunces italic | 500 | 144 | Hero wordmark |
| 64px | Fraunces italic | 500 | 144 | Section head |
| 32px | Fraunces italic | 500 | 48 | Sub head |
| 20px | Fraunces italic | 500 | 24 | Body display |
| 14px | Fraunces italic | 600 | 14 | Meta / byline |
| 10px | Fraunces italic | 700 | 9 | Caption / footnote |

The 10px caption is small but approved. Use sparingly. Reserve for footer legal, copyright lines, meta on dense case-study tables. Never for prose.

---

## 4. Authorized wordmark treatments

Pairings validated against the stress test. Only these six are allowed.

| Surface | Wordmark color | Context |
|---------|----------------|---------|
| Warm Dark `#2A2520` | Signal `#A3FF12` | **Primary.** Hero, nav, all marketing surfaces |
| Cream `#F5F0E8` | Terracotta `#B8654A` | Long-form reading, editorial surfaces |
| Terracotta `#B8654A` | Cream `#F5F0E8` | Section-level, full-bleed moments |
| Warm Darker `#141210` | Terracotta Bright `#D67952` | Inverted, sparingly - terminal / technical surfaces |
| Warm Dark `#2A2520` | Terracotta Bright `#D67952` | Section accent, secondary marketing |
| Cream `#F5F0E8` | Warm Dark `#2A2520` | Neutral / print / low-color contexts |

Any other surface/color pairing is off-spec. Specifically disallowed: Signal on Cream (too hot), Signal on Terracotta (clash), anything on gradients.

---

## 5. Greek and monogram

Fraunces italic handles the Greek set (πρᾶξις) natively. No glyph substitution. The capital Π in Fraunces italic is the starting point for monogram exploration in the logo phase.

---

## 6. Variable axes

Fraunces exposes `opsz`, `wght`, `SOFT`, `WONK`. Praxis uses:

- `opsz`: scale-matched per size ladder
- `wght`: 500 for wordmark; 400–600 range for body display; 600–700 for small-caption wordmark
- `SOFT`: 0–100, scaled with size (smaller = harder terminals for legibility)
- `WONK`: locked at 0. No alt-form swashes. Keeps the wordmark consistent across sizes.

CSS: `font-variation-settings: 'opsz' 144, 'SOFT' 100, 'WONK' 0;`

---

## 7. Licensing and loading

All three faces are open-source and free for commercial use.

- **Fraunces** - OFL, Undercase Type → Google Fonts
- **Inter** - OFL, Rasmus Andersson → Google Fonts
- **JetBrains Mono** - OFL, JetBrains → Google Fonts

Production loading: self-host via `fonts.bunny.net` or Google Fonts CDN with `font-display: swap`. Preconnect to font host. Subset to Latin + Greek + extended punctuation. No licensing cost at any traffic volume.

---

## 8. Rejected alternates

Per the stress test, none of these beat Fraunces. Kept for the record in case Fraunces ever has to be replaced.

- Playfair Display - too didone, feels fashion-magazine
- Cormorant Garamond - softer terminals, reads more classical than applied
- EB Garamond - survives at small sizes but loses the editorial weight
- GT Sectra, Publico, Recoleta (commercial) - not tested against; would require licensing if revisited

---

## 9. What this locks

- Wordmark spec for logo exploration (next phase)
- Type stack for all components, the website, and asset templates
- Color-pairing rules for any surface that carries the mark
- The size ladder that component design must respect

Any change to wordmark face, weight, or opsz bumps this doc to v2 and triggers a re-stress-test.
