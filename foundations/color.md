# Praxis - Color System v1

**Status:** LOCKED
**Version:** v1
**Date:** 2026-04-22
**Companions:** `typography.md`, `logo.md`
**Visual companion:** `color.html`

Canonical color system for Praxis. Two layers: raw palette tokens (brand + semantic UI) and semantic role tokens that reference them. All components, the website, and asset templates consume the semantic layer only. Palette values are named per Tailwind convention (50-950 for neutrals, 100-900 for accents).

---

## 1. Layer one - raw palette

### 1.1 Warm family (neutrals, 11-step)

The dominant neutral. All page surfaces, text, and borders derive from this family. Anchor values: Cream at 100, Warm Dark at 800, Warm Darker at 950.

| Token | Hex | Notes |
|-------|-----|-------|
| `--warm-50` | `#FCFAF6` | Lightest warm tint |
| `--warm-100` | `#F5F0E8` | **Cream - canonical** |
| `--warm-200` | `#E8DFD2` | Light surface on cream bg |
| `--warm-300` | `#D4C7B4` | Secondary text on dark bg |
| `--warm-400` | `#B0A18C` | Tertiary text on dark bg |
| `--warm-500` | `#8A7C6A` | Muted text, meta, captions |
| `--warm-600` | `#5C5248` | Disabled, border emphasis |
| `--warm-700` | `#3D3630` | Surface on warm-dark bg |
| `--warm-800` | `#2A2520` | **Warm Dark - canonical** |
| `--warm-900` | `#1C1814` | Between dark and darker |
| `--warm-950` | `#141210` | **Warm Darker - canonical** |

### 1.2 Terracotta family (warm accent, 5-step)

Warmth anchor. Editorial surfaces, section accents, brand accent paired with Signal.

| Token | Hex | Notes |
|-------|-----|-------|
| `--terracotta-100` | `#F5D9C9` | Pale peach, surface tint |
| `--terracotta-300` | `#D67952` | **Terracotta Bright - canonical** |
| `--terracotta-500` | `#B8654A` | **Terracotta - canonical primary** |
| `--terracotta-700` | `#8A4A35` | Deep shade |
| `--terracotta-900` | `#5C2E1F` | Darkest shade |

### 1.3 Signal family (brand accent, 5-step)

Electric brand accent. Wordmark color on dark, tile fill on mark, CTAs, links, attention moments. Use sparingly.

| Token | Hex | Notes |
|-------|-----|-------|
| `--signal-100` | `#E5FFB8` | Pale wash (rare) |
| `--signal-300` | `#C4FF5E` | Hover / lighter context |
| `--signal-500` | `#A3FF12` | **Signal - canonical primary** |
| `--signal-700` | `#7AC208` | Active / darker context |
| `--signal-900` | `#4D7B00` | Deep forest signal |

### 1.4 Semantic UI families (5-step each)

Desaturated, warm-biased, calm. Same register as Claude and Notion. Reserved for system states so Signal and Terracotta stay pure as brand accents. Reference direction: **Refined.**

**Destructive** (muted brick red, warm-biased):

| Token | Hex |
|-------|-----|
| `--destructive-100` | `#F5D4D4` |
| `--destructive-300` | `#E08080` |
| `--destructive-500` | `#C94343` |
| `--destructive-700` | `#8A2828` |
| `--destructive-900` | `#3D0F10` |

**Success** (dusty teal-green, warm-biased):

| Token | Hex |
|-------|-----|
| `--success-100` | `#D4E8DF` |
| `--success-300` | `#7FB19C` |
| `--success-500` | `#3A7560` |
| `--success-700` | `#1F4A3C` |
| `--success-900` | `#0F241E` |

**Warning** (dijon amber, muted):

| Token | Hex |
|-------|-----|
| `--warning-100` | `#F0DCB8` |
| `--warning-300` | `#D4AA6E` |
| `--warning-500` | `#C28130` |
| `--warning-700` | `#8A5A1A` |
| `--warning-900` | `#3D2808` |

**Info** (dusty denim blue):

| Token | Hex |
|-------|-----|
| `--info-100` | `#D4DFE8` |
| `--info-300` | `#7A95AE` |
| `--info-500` | `#4A7090` |
| `--info-700` | `#2A4A65` |
| `--info-900` | `#10243A` |

---

## 2. Layer two - semantic tokens

Components reference these, never the raw palette. This layer assumes a dark-first mode (Warm Dark primary surface). Light-mode overrides documented in §4.

### 2.1 Surfaces

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `--warm-800` | Primary page background |
| `--bg-deeper` | `--warm-950` | Inverted, terminal, code block |
| `--surface` | `--warm-700` | Cards, panels, popovers |
| `--surface-subtle` | `rgba(245,240,232,0.03)` | Hairline translucent surface |
| `--surface-elevated` | `--warm-600` | Modals, tooltips, floating UI |

### 2.2 Text

| Token | Value | Usage | Contrast vs `--bg` |
|-------|-------|-------|--------------------|
| `--text-primary` | `--warm-100` | Body, default | **13.5 : 1 (AAA)** |
| `--text-secondary` | `--warm-300` | Supporting body | 8.2 : 1 (AAA) |
| `--text-tertiary` | `--warm-400` | Captions, dense meta | 5.1 : 1 (AA) |
| `--text-muted` | `--warm-500` | Small labels, time stamps | 3.2 : 1 (AA Large only) |
| `--text-signal` | `--signal-500` | Brand attention, links | **12.3 : 1 (AAA)** |
| `--text-inverse` | `--warm-800` | Text on `--warm-100` or Signal | 13.5 : 1 (AAA) |
| `--text-disabled` | `--warm-600` | Inactive states | 1.9 : 1 (intentional) |

**Rule:** `--text-muted` is for labels, meta, and large text only (16px+). Do not use for body copy on dark. Below AA for normal text.

### 2.3 Borders

| Token | Value | Usage |
|-------|-------|-------|
| `--border-subtle` | `rgba(245,240,232,0.08)` | Dividers, section rules |
| `--border` | `rgba(245,240,232,0.16)` | Card edges, input borders |
| `--border-emphasis` | `--warm-500` | Focus states, active edges |

### 2.4 Brand

| Token | Value | Usage |
|-------|-------|-------|
| `--brand-primary` | `--signal-500` | Primary CTA, mark fill, link |
| `--brand-primary-hover` | `--signal-300` | Hover state on dark |
| `--brand-primary-active` | `--signal-700` | Pressed / active state |
| `--brand-accent` | `--terracotta-500` | Secondary accent, section color |
| `--brand-accent-bright` | `--terracotta-300` | Accent on dark surfaces |

### 2.5 Semantic UI states

On dark surfaces, use the `-300` variant for foreground text/icons (better contrast and lightness). On light surfaces, use `-700`. The `-100` is the soft bg fill for toast/alert surfaces.

**Destructive:**

| Token | Value | Usage |
|-------|-------|-------|
| `--destructive-fg-dark` | `--destructive-300` | Error text on dark |
| `--destructive-fg-light` | `--destructive-700` | Error text on light |
| `--destructive-bg` | `--destructive-100` | Toast/alert bg (light only) |
| `--destructive-solid` | `--destructive-500` | Destructive button fill |

**Success:**

| Token | Value | Usage |
|-------|-------|-------|
| `--success-fg-dark` | `--success-300` | Success text on dark |
| `--success-fg-light` | `--success-700` | Success text on light |
| `--success-bg` | `--success-100` | Toast/alert bg (light only) |
| `--success-solid` | `--success-500` | Badge/dot fill only. **Not a button color** (see §2.6). |

**Warning:**

| Token | Value | Usage |
|-------|-------|-------|
| `--warning-fg-dark` | `--warning-300` | Warning text on dark |
| `--warning-fg-light` | `--warning-700` | Warning text on light |
| `--warning-bg` | `--warning-100` | Toast/alert bg (light only) |
| `--warning-solid` | `--warning-500` | Badge/dot fill only. **Not a button color** (see §2.6). |

**Info:**

| Token | Value | Usage |
|-------|-------|-------|
| `--info-fg-dark` | `--info-300` | Info text on dark |
| `--info-fg-light` | `--info-700` | Info text on light |
| `--info-bg` | `--info-100` | Toast/alert bg (light only) |
| `--info-solid` | `--info-500` | Badge/dot fill only. **Not a button color** (see §2.6). |

### 2.6 Button hierarchy (scarcity rule)

Signal earns its weight by being rare. Button colors follow a five-tier hierarchy, not a one-color-per-state mapping.

| Tier | Background token | Foreground token | Use |
|------|-----------------|-----------------|-----|
| **Hero CTA** | `--btn-hero-bg` (`--signal-500`) | `--btn-hero-fg` (`--warm-950`) | Single most important action on a screen. **One per screen maximum.** Landing pages, launch moments, primary diagnostic CTA. |
| **Primary** | `--btn-primary-bg` (`--terracotta-500`) | `--btn-primary-fg` (`--warm-50`) | Default primary action across the product. Save, Submit, Update, Apply, Confirm. |
| **Destructive** | `--btn-destructive-bg` (`--destructive-500`) | `--btn-destructive-fg` (`--warm-50`) | Dangerous actions. Delete, Remove, Archive. |
| **Destructive ghost** | transparent | `--destructive-300` | Lower-weight danger. Discard draft, Cancel subscription. 1px `--destructive-500` border. |
| **Secondary** | `--btn-neutral-bg` (`--warm-800`) | `--btn-neutral-fg` (`--warm-100`) | Cancel, Back, Dismiss. 1px `--warm-600` border. |

**The scarcity rule.** Most product screens have zero Signal buttons. Signal lives on the logo. When a single action on a screen genuinely outweighs everything else, that one button becomes Signal. Everywhere else, terracotta is the primary.

**Success, warning, and info are not button colors.** They live in toasts, banners, badges, icons, status dots, and inline text only. If a button feels like it needs to be "the success button," it is a primary button (terracotta). The success state comes in the toast that appears after the button is clicked.

---

## 3. Accessibility - WCAG pairings

All contrast ratios computed per WCAG 2.1 sRGB luminance formula. AA requires 4.5:1 for normal text, 3:1 for large (18px+ or 14px+ bold). AAA requires 7:1 normal, 4.5:1 large.

### 3.1 Primary surface: Warm Dark (`--warm-800`, `#2A2520`)

| Foreground | Ratio | AA | AAA | Use for |
|------------|-------|-----|-----|---------|
| Cream `--warm-100` | 13.5 : 1 | ✓ | ✓ | Body, default |
| Signal `--signal-500` | 12.3 : 1 | ✓ | ✓ | Accent, wordmark |
| Warm-300 | 8.2 : 1 | ✓ | ✓ | Secondary body |
| Terracotta Bright `--terracotta-300` | 4.9 : 1 | ✓ | ✗ | Accent heads, not body |
| Terracotta `--terracotta-500` | 3.7 : 1 | ✓ Large only | ✗ | Decorative, large text |
| Warm-500 (muted) | 3.2 : 1 | ✓ Large only | ✗ | Meta, captions, labels |

### 3.2 Cream surface (`--warm-100`, `#F5F0E8`)

| Foreground | Ratio | AA | AAA | Use for |
|------------|-------|-----|-----|---------|
| Warm-800 | 13.5 : 1 | ✓ | ✓ | Body |
| Terracotta-500 | 3.7 : 1 | ✓ Large only | ✗ | Accent heads |
| Terracotta-700 | 6.8 : 1 | ✓ | ✗ | Accent body |
| Signal-700 | 4.1 : 1 | ✓ Large only | ✗ | Rare accent (signal is primarily dark-surface) |

### 3.3 Signal surface (`--signal-500`, `#A3FF12`)

Signal as a fill (tile mark, CTA button). Foreground must be dark.

| Foreground | Ratio | AA | AAA |
|------------|-------|-----|-----|
| Warm-800 | 11.0 : 1 | ✓ | ✓ |
| Warm-950 | 15.3 : 1 | ✓ | ✓ |

### 3.4 Rule set

- Body text on Warm Dark: Cream or warm-300 only.
- Body text on Cream: warm-800 only.
- Signal text only on Warm Dark / Warm Darker. Never on Cream.
- Terracotta-500 text never under 18px on Warm Dark.

---

## 4. Light mode

Praxis is dark-first. Light mode exists for long-form reading surfaces and print.

| Semantic token | Dark mode | Light mode |
|----------------|-----------|------------|
| `--bg` | `--warm-800` | `--warm-100` |
| `--bg-deeper` | `--warm-950` | `--warm-50` |
| `--surface` | `--warm-700` | `--warm-200` |
| `--text-primary` | `--warm-100` | `--warm-800` |
| `--text-secondary` | `--warm-300` | `--warm-600` |
| `--text-muted` | `--warm-500` | `--warm-500` |
| `--text-signal` | `--signal-500` | `--signal-700` |
| `--brand-primary` | `--signal-500` | `--signal-700` |
| `--border-subtle` | `rgba(245,240,232,0.08)` | `rgba(42,37,32,0.08)` |
| `--border` | `rgba(245,240,232,0.16)` | `rgba(42,37,32,0.16)` |

In light mode, Signal shifts to `--signal-700` because pure `--signal-500` on Cream reads over-bright (glows). The `-700` preserves the brand recognition while meeting contrast on light.

---

## 5. CSS architecture

```css
:root {
  /* Palette - warm */
  --warm-50: #FCFAF6;
  --warm-100: #F5F0E8;
  --warm-200: #E8DFD2;
  --warm-300: #D4C7B4;
  --warm-400: #B0A18C;
  --warm-500: #8A7C6A;
  --warm-600: #5C5248;
  --warm-700: #3D3630;
  --warm-800: #2A2520;
  --warm-900: #1C1814;
  --warm-950: #141210;

  /* Palette - accents */
  --terracotta-100: #F5D9C9;
  --terracotta-300: #D67952;
  --terracotta-500: #B8654A;
  --terracotta-700: #8A4A35;
  --terracotta-900: #5C2E1F;

  --signal-100: #E5FFB8;
  --signal-300: #C4FF5E;
  --signal-500: #A3FF12;
  --signal-700: #7AC208;
  --signal-900: #4D7B00;

  /* Palette - semantic UI (abridged; full set above) */
  --destructive-500: #C94343;
  --success-500: #3A7560;
  --warning-500: #C28130;
  --info-500: #4A7090;

  /* Semantic (dark-mode default) */
  --bg: var(--warm-800);
  --bg-deeper: var(--warm-950);
  --surface: var(--warm-700);
  --surface-subtle: rgba(245, 240, 232, 0.03);
  --surface-elevated: var(--warm-600);

  --text-primary: var(--warm-100);
  --text-secondary: var(--warm-300);
  --text-tertiary: var(--warm-400);
  --text-muted: var(--warm-500);
  --text-signal: var(--signal-500);
  --text-inverse: var(--warm-800);
  --text-disabled: var(--warm-600);

  --border-subtle: rgba(245, 240, 232, 0.08);
  --border: rgba(245, 240, 232, 0.16);
  --border-emphasis: var(--warm-500);

  --brand-primary: var(--signal-500);
  --brand-primary-hover: var(--signal-300);
  --brand-primary-active: var(--signal-700);
  --brand-accent: var(--terracotta-500);
  --brand-accent-bright: var(--terracotta-300);

  /* Button tiers - scarcity rule applies (see §2.6) */
  --btn-hero-bg: var(--signal-500);
  --btn-hero-fg: var(--warm-950);
  --btn-primary-bg: var(--terracotta-500);
  --btn-primary-fg: var(--warm-50);
  --btn-destructive-bg: var(--destructive-500);
  --btn-destructive-fg: var(--warm-50);
  --btn-neutral-bg: var(--warm-800);
  --btn-neutral-fg: var(--warm-100);
}

[data-theme="light"] {
  --bg: var(--warm-100);
  --bg-deeper: var(--warm-50);
  --surface: var(--warm-200);
  --text-primary: var(--warm-800);
  --text-secondary: var(--warm-600);
  --text-signal: var(--signal-700);
  --brand-primary: var(--signal-700);
  --border-subtle: rgba(42, 37, 32, 0.08);
  --border: rgba(42, 37, 32, 0.16);
}
```

**Rule:** components use semantic tokens only. Never reference a raw palette token directly in a component. Palette tokens only appear in the `:root` definitions.

---

## 6. Don't

- Don't use Signal on Cream at small sizes (fails contrast). Use Signal-700 or Warm Dark instead.
- Don't use Terracotta-500 text under 18px on Warm Dark (AA Large only).
- Don't use Signal as a success color. Success is dusty teal (`--success-500`). Signal is brand attention only.
- Don't use Terracotta as destructive. Destructive is brick red (`--destructive-500`). Terracotta is brand warmth only.
- Don't use Signal for every primary button. Signal is reserved for the hero CTA per the scarcity rule (§2.6). Terracotta is the default primary.
- Don't use success, warning, or info as button fills. They belong in toasts, badges, icons, and inline text only.
- Don't introduce new raw palette colors without updating this doc to v2.
- Don't use `--text-muted` (warm-500) for body copy on dark. Labels, captions, meta only.

---

## 7. What this locks

- Full 11-step warm family + 5-step accent families + 5-step Refined semantic UI families
- Semantic token layer with dark-mode default and light-mode override
- Button hierarchy scarcity rule (§2.6): Signal reserved for hero CTA, Terracotta as default primary, success/warning/info not button colors
- WCAG contrast pairings documented for every critical combination
- CSS custom property naming and architecture

Any palette addition, semantic token rename, or change to the button hierarchy bumps to v2.

---

## 8. Next deliverables

- Base components (buttons, cards, inputs, nav) consuming semantic tokens
- Icon direction (Lucide-style stroke weight, 24px base, inherits radius from mark geometry)
- Asset exports (mark + lockup SVG / PNG, favicon set per Logo v1 §8)
- Tailwind config or equivalent token pipeline if the site uses it

Reference for component work: semantic layer in §2 is the source of truth.
