# Praxis Brand Assets

All exports build from `foundations/logo.md` v1 and `foundations/color.md` v1.
Generated 2026-04-23.

## logo/

### mark/
- `mark.svg` — master, 100x100 viewBox, geometric Π (portable, no font needed)
- `mark-{16,32,48,64,128,256,512,1024}.png` — raster exports

### favicon/
- `favicon.svg` — vector favicon (modern browsers)
- `favicon.ico` — multi-res (16/24/32/48)
- `favicon-{16,32,48}.png` — individual PNG fallbacks
- `apple-touch-icon.png` — 180x180 for iOS home-screen

### wordmark/
- `wordmark-cream.svg` — cream fill, for dark surfaces (primary)
- `wordmark-warmdark.svg` — warm-dark fill, for light surfaces

Wordmark uses Fraunces italic, weight 500, opsz 144, SOFT 100, tracking -0.01em. Glyphs outlined.

### lockup/
- `lockup-horizontal-cream.svg` — master, cream wordmark (for dark surfaces)
- `lockup-horizontal-warmdark.svg` — master, warm-dark wordmark (for light surfaces)
- `lockup-horizontal-cream.png` — 80px tile height raster (hero use)
- `lockup-horizontal-cream-email.png` — 40px tile height raster (email signature)
- `lockup-horizontal-warmdark.png` — 80px tile height raster
- `lockup-horizontal-warmdark-email.png` — 40px tile height raster

## social/

- `og-card.png` — 1200x630, Open Graph + Twitter Card + LinkedIn link preview
- `linkedin-company-logo.png` — 400x400, tile mark padded on Warm Dark (safe for circular crop)
- `linkedin-company-logo-fullbleed.png` — 400x400, Signal tile full-bleed (alternative)
- `linkedin-company-cover.png` — 1128x191, company page cover
- `linkedin-personal-banner.png` — 1584x396, Marc's personal profile banner

## Mark construction note

The Π is constructed geometrically (three rectangular shapes plus bracketed foot serifs) rather than set from a Greek-enabled Fraunces glyph. Fraunces ships Greek in its open-source variable font on GitHub, but the geometric construction was chosen deliberately: the mark reads cleaner at 16px, survives circular cropping, and is insulated from future font updates. The proportions (cap height 55% of tile, stem weight 12%, cap thickness 11.5%, bracketed serifs at 4.5% overhang) were tuned to sit in the same visual register as Fraunces roman wt 600 opsz 144.

Wordmark and tagline copy still use live Fraunces italic via glyph outlining.

## Regenerating

Run `/sessions/modest-funny-fermi/brand-assets-work/build.py`. Requires:
- Fraunces variable fonts (Roman + Italic) installed in system fonts (used for wordmark only)
- Python 3.10+ with `cairosvg`, `fonttools`, `Pillow`, `brotli`
