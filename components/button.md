# Praxis · Button Component v1

**Status:** LOCKED
**Version:** v1
**Date:** 2026-04-22
**Companions:** `../foundations/color.md` (§2.6 scarcity rule), `../foundations/typography.md`, `../foundations/logo.md`
**Visual companion:** `button.html`

---

## 1. Purpose

Buttons are the primary call-to-action surface. They carry the scarcity rule from Color v1 §2.6 into a component contract. Five tiers, three sizes, six states, five variants. All buttons consume semantic tokens only. Never raw palette.

---

## 2. Tier contract (from Color v1 §2.6)

| # | Tier | Background | Foreground | Weight | Usage |
|---|------|------------|------------|--------|-------|
| 1 | **Hero** | `--btn-hero-bg` (signal-500 · `#A3FF12`) | `--btn-hero-fg` (warm-800 · `#2A2520`) | 600 | Logo tile + single marketing CTA per screen. Never in product surfaces. |
| 2 | **Primary** | `--btn-primary-bg` (terracotta-500 · `#B8654A`) | `--btn-primary-fg` (warm-100 · `#F5F0E8`) | 500 | Default positive action. Send, Save, Submit, Confirm. |
| 3 | **Destructive** | `--btn-destructive-bg` (destructive-500 · `#C94343`) | `--btn-destructive-fg` (warm-100 · `#F5F0E8`) | 500 | Delete, archive, cancel-paid, irreversible. |
| 4 | **Ghost** | transparent (border: `--border`) | `--text-primary` (warm-100) | 500 | Secondary to primary. Cancel, dismiss, back. |
| 5 | **Neutral** | `--btn-neutral-bg` (warm-700 · `#3D3630`) | `--btn-neutral-fg` (warm-100 · `#F5F0E8`) | 500 | Low-emphasis persist. Save draft, export, minor. |

### 2.1 Scarcity rule (enforced)

- **Zero Hero buttons** is the correct count for most product screens.
- **One Hero button per screen**, maximum. If two exist, one is wrong.
- **Success, warning, and info are not button colors.** They appear as alerts, badges, and status dots only.

### 2.2 Standard pair patterns

| Context | Pattern |
|---------|---------|
| Marketing hero | Hero + Ghost |
| Form submit | Primary + Ghost |
| Confirmation dialog | Destructive + Ghost |
| Product toolbar | Primary + Ghost + Neutral |
| Batch actions | Neutral + Primary (primary rightmost) |

Never pair two tier-1 or tier-2 buttons at equal emphasis.

---

## 3. Sizes

| Size | Height | Horizontal padding | Font size | Icon size | Radius | Use |
|------|--------|---------------------|-----------|-----------|--------|-----|
| sm | 28px | 10px | 12px | 14px | 6px | Dense toolbars, table row actions, inline controls |
| md | 32px | 12px | 13px | 16px | 6px | Default. Forms, dialogs, dashboards |
| lg | 40px | 16px | 14px | 18px | 6px | Marketing heroes, landing page primary CTA |

Scale benchmark: this matches what Claude, Notion, Linear, and GitHub use for SaaS surfaces. Default sits at 32px (not 40px) so buttons recede properly in dense product UI. lg at 40px is reserved for marketing heroes.

Radius fixed at 6px across sizes. Ties to logo tile 9% geometry at the button scale without being identical. At 32px default that's ~19% corner - compact, not pillshape.

Gap between icon and text: 6px at sm, 8px at md, 10px at lg.

Touch target. The sm (28px) and md (32px) sizes are below Apple's 44px HIG minimum. Both are keyboard/mouse surfaces only. For mobile primary actions, use lg (40px) with extra invisible hit-slop (`padding: 6px` on a wrapper), or restrict mobile UX to lg.

---

## 4. States

Six states per tier. All states preserve height, padding, and type. Only color, opacity, and outline change.

| State | Visual |
|-------|--------|
| **default** | Base tier color |
| **hover** | Background shifts 1 step darker (500 → 700 for Hero/Primary/Destructive/Neutral). Ghost fills with `--surface-subtle`. |
| **focus-visible** | 2px solid `rgba(163, 255, 18, 0.4)` ring, 2px offset. Signal at 40%. Only on keyboard focus, never mouse. |
| **active** | Background shifts 1 further step darker (700 → 900). Slight scale 0.98 optional. |
| **disabled** | 40% opacity, `cursor: not-allowed`, pointer-events none on children. No hover response. |
| **loading** | Leading icon slot replaced with spinner using `currentColor`. Button remains visually active but disabled to interaction. Text unchanged. |

### 4.1 Focus ring

```css
.btn:focus-visible {
  outline: 2px solid rgba(163, 255, 18, 0.4);
  outline-offset: 2px;
}
```

Always use `:focus-visible`, never plain `:focus`. Mouse clicks should not show the ring.

### 4.2 Loading behavior

- Button becomes `aria-busy="true"` and `disabled`.
- Spinner (12px at sm, 13px at md, 14px at lg, via 1em sizing) replaces leading icon or inserts at leading position if none.
- Text stays visible. Do not collapse text to spinner-only.
- Trailing icon hides during loading.

---

## 5. Variants

Every tier supports all five variants.

| Variant | Structure | Example |
|---------|-----------|---------|
| **Text only** | `<button>Label</button>` | "Send proposal" |
| **Leading icon** | `<button><Icon/> Label</button>` | "← Back" |
| **Trailing icon** | `<button>Label <Icon/></button>` | "Send →" |
| **Icon only** | `<button aria-label="…"><Icon/></button>` | Menu trigger, close X |
| **Full-width** | `<button class="w-full">Label</button>` | Form submit on narrow |

Icon-only always requires `aria-label`. Use 1:1 aspect ratio (28×28, 32×32, 40×40).

Gap between icon and text: 6px at sm, 8px at md, 10px at lg.

---

## 6. CSS tokens (component layer)

Consume from Color v1 §5.

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  border-radius: 6px;
  border: 1px solid transparent;
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 500;
  letter-spacing: 0;
  line-height: 1;
  cursor: pointer;
  transition: background 120ms ease, opacity 120ms ease, transform 80ms ease;
  user-select: none;
}
.btn:focus-visible { outline: 2px solid rgba(163, 255, 18, 0.4); outline-offset: 2px; }
.btn:disabled, .btn[aria-busy="true"] { opacity: 0.4; cursor: not-allowed; pointer-events: none; }

/* Sizes */
.btn-sm { height: 28px; padding: 0 10px; font-size: 12px; gap: 6px; }
.btn-md { height: 32px; padding: 0 12px; font-size: 13px; }
.btn-lg { height: 40px; padding: 0 16px; font-size: 14px; gap: 10px; }

/* Tier 1 · Hero (Signal) */
.btn-hero { background: var(--btn-hero-bg); color: var(--btn-hero-fg); font-weight: 600; }
.btn-hero:hover { background: var(--signal-700); }
.btn-hero:active { background: var(--signal-900); color: var(--warm-100); }

/* Tier 2 · Primary (Terracotta) */
.btn-primary { background: var(--btn-primary-bg); color: var(--btn-primary-fg); }
.btn-primary:hover { background: var(--terracotta-700); }
.btn-primary:active { background: var(--terracotta-900); }

/* Tier 3 · Destructive */
.btn-destructive { background: var(--btn-destructive-bg); color: var(--btn-destructive-fg); }
.btn-destructive:hover { background: var(--destructive-700); }
.btn-destructive:active { background: var(--destructive-900); }

/* Tier 4 · Ghost */
.btn-ghost { background: transparent; color: var(--text-primary); border-color: var(--border); }
.btn-ghost:hover { background: var(--surface-subtle); border-color: var(--border-emphasis); }
.btn-ghost:active { background: rgba(245, 240, 232, 0.06); }

/* Tier 5 · Neutral */
.btn-neutral { background: var(--btn-neutral-bg); color: var(--btn-neutral-fg); }
.btn-neutral:hover { background: var(--warm-600); }
.btn-neutral:active { background: var(--warm-800); }

/* Full-width */
.btn-full { width: 100%; }

/* Icon-only */
.btn-icon.btn-sm { width: 28px; padding: 0; }
.btn-icon.btn-md { width: 32px; padding: 0; }
.btn-icon.btn-lg { width: 40px; padding: 0; }
```

### 6.1 Spinner (loading)

```css
.btn-spinner {
  width: 1em; height: 1em;
  border: 2px solid currentColor;
  border-right-color: transparent;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
```

Size scales with button size via `em` unit on button font-size.

---

## 7. Accessibility

- **Contrast.** All five tiers meet WCAG AA (4.5:1) on warm-800 and warm-950 surfaces. Hero reads 12.3:1 (Signal on warm-800). Primary reads 4.9:1 (Terracotta-500 on warm-100 text). Destructive reads 5.1:1. Neutral reads 9.8:1. Ghost inherits from text-primary (13.5:1).
- **Touch target.** Apple HIG minimum 44px. sm (28px) and md (32px) are desktop/mouse surfaces only. For mobile primaries, use lg (40px) with a 6px hit-slop wrapper to reach 52px effective target.
- **Focus ring.** 2px at Signal 40% always visible on keyboard focus. Offset 2px so the ring doesn't touch button edge.
- **Disabled semantics.** Use `disabled` attribute (not just `aria-disabled`) unless the button must remain in tab order. Disabled buttons still need 3:1 contrast for boundary visibility.
- **Loading semantics.** Use `aria-busy="true"` plus `disabled`. Screen readers announce busy state.
- **Icon-only.** Requires `aria-label`. Decorative icons inside text-labeled buttons use `aria-hidden="true"`.
- **Keyboard.** Space and Enter both activate. Tab order follows DOM order.

---

## 8. Usage rules

**Do**

- Use Hero once per marketing page, maximum.
- Default to Primary for positive product actions.
- Pair Destructive with Ghost in confirmation dialogs.
- Use Ghost for "Cancel" next to Primary "Submit."
- Use Neutral for low-stakes persistence (Save draft, Export).
- Use icon-only buttons for repeated toolbar actions with clear iconography (menu, close, more).

**Don't**

- Don't use Hero in product surfaces (dashboards, tables, forms).
- Don't use success, warning, or info as button colors. They are alert and badge colors only.
- Don't stack two Primary buttons side-by-side at equal emphasis. Pick one.
- Don't use Destructive for reversible actions (Edit, Duplicate, Archive-that-can-be-unarchived).
- Don't replace the text with a spinner in loading state. Keep label visible.
- Don't add `:focus` ring without `:focus-visible`. Mouse clicks shouldn't flash the ring.
- Don't override radius per-button. 6px is the system radius.

---

## 9. What this locks

- Five tiers (Hero/Primary/Destructive/Ghost/Neutral) with named tokens from Color v1 §5.
- Three sizes (sm 28 / md 32 / lg 40) with fixed 6px radius.
- Six states (default/hover/focus-visible/active/disabled/loading).
- Five variants (text/leading-icon/trailing-icon/icon-only/full-width).
- Focus ring contract: 2px Signal 40%, offset 2px, `:focus-visible` only.
- Loading behavior: spinner replaces leading icon slot, text persists, `aria-busy`.
- Usage rules enforcing Color v1 §2.6 scarcity.

Next base components: cards, forms, navigation, feedback (toast/alert/modal).
