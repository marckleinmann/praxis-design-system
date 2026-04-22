# Praxis · Card Component v1

**Status:** LOCKED
**Version:** v1
**Date:** 2026-04-22
**Companions:** `../foundations/color.md`, `../foundations/typography.md`, `button.md`
**Visual companion:** `card.html`

---

## 1. Purpose

Cards are the generic content surface. Everything that groups related information into a bounded block is a card: a metric tile, a list section, a record preview, an empty state, a settings panel. This component locks the container contract. Specialized cards (metric card, media card, list card) compose from it.

---

## 2. Anatomy

A card is a container plus up to four optional slots. All slots are optional except body.

```
┌─────────────────────────────────────┐
│ [media]                             │ ← optional, bleeds to edges
├─────────────────────────────────────┤
│ eyebrow                   [action]  │ ← header: text block + trailing slot
│ title                               │
│ subtitle                            │
│                                     │
│ body content                        │ ← the only required slot
│                                     │
├─────────────────────────────────────┤
│ meta · timestamp    [btn] [btn]     │ ← footer: meta left, actions right
└─────────────────────────────────────┘
```

Slots:

- **Media** (optional). Image, chart, or video at top. Bleeds to card edges (negative margin equal to card padding).
- **Header** (optional). Eyebrow (uppercase micro-label), title, subtitle, plus a trailing action slot for one icon-only button or a badge. One trailing item, not a list.
- **Body** (required). The content.
- **Footer** (optional). Meta text left (timestamp, author, count). Actions right (Ghost or Neutral buttons, sm size). Divider above footer is off by default, opt in via `.card-footer-divided`.

---

## 3. Variants

Four variants. Every card is one of these.

| # | Variant | Background | Border | Usage |
|---|---------|------------|--------|-------|
| 1 | **Flat** | `var(--surface)` (warm-700) | none | Default. The workhorse. |
| 2 | **Outlined** | transparent | `1px var(--border-subtle)` | Nested cards, or when you don't want elevation against the page. |
| 3 | **Subtle** | `var(--surface-subtle)` | none | Low-emphasis groupings. Sidebar sections, aside content, informational notices. |
| 4 | **Feature** | `var(--surface)` | `1px rgba(163, 255, 18, 0.3)` | The attention card. Hero-equivalent. Scarcity rule applies. |

No shadows. No drop-shadow on any variant. Dark-first systems read better with flat surfaces and border contrast than with elevation shadows.

### 3.1 Scarcity rule (Feature)

- **One Feature card per view**, maximum. If two exist, one is wrong.
- Feature is for the single item that should pull attention: current focus in a dashboard, the recommended action, the active primary.
- Feature never pairs with a Hero button inside it. Pick one attention anchor per view.
- Product surfaces default to zero Feature cards. Feature appears when there's an obvious "this one" call.

### 3.2 Pair and grid patterns

| Context | Pattern |
|---------|---------|
| Dashboard metric row | 3-4 Flat cards, equal weight |
| Dashboard with active focus | 1 Feature card + surrounding Flat cards |
| Settings page sections | Flat cards stacked, each with header + body |
| Nested detail panel | Outer Flat card + inner Outlined cards |
| Sidebar informational | Subtle cards, no header, short body |
| Empty state | Flat card, centered body, one action in body (not footer) |

---

## 4. Sizes

| Size | Padding | Gap (between slots) | Use |
|------|---------|---------------------|-----|
| sm | 12px | 8px | Dense grids, metric tiles, list item previews |
| md | 16px | 12px | Default. Dashboards, settings, most product UI |
| lg | 24px | 16px | Marketing surfaces, feature callouts, detail pages |

Radius fixed at **8px** across sizes. Sits between button radius (6px) and modal radius (future: 12px) so container hierarchy reads cleanly. At 8px the card reads modern-editorial, not pillshape and not boxy.

---

## 5. States

Six states. States apply to interactive cards. Static cards have only default.

| State | Visual |
|-------|--------|
| **default** | Base variant styling |
| **hover** | Interactive only. Border shifts to `rgba(163, 255, 18, 0.2)` (signal hint). Cursor pointer. Bg unchanged. |
| **focus-visible** | 2px `rgba(163, 255, 18, 0.4)` ring, 2px offset. Keyboard only. Same ring contract as buttons. |
| **selected** | Persistent border at `rgba(163, 255, 18, 0.4)`. Used for single-select lists, active filter, current step. |
| **disabled** | 40% opacity, `pointer-events: none`, `cursor: not-allowed` on wrapper. |
| **loading** | Skeleton lines replace text content. Border and padding unchanged. Skeleton pulses at 0.6s. |

### 5.1 Interactive mode

Cards are **non-interactive by default**. Opt in via `.card-interactive` class. This adds:

- `cursor: pointer`
- Hover state (border hint)
- `:focus-visible` ring
- Requires `role="button"` or `role="link"`, or wrapping the card in `<button>` / `<a>`

If the whole card is clickable, use a wrapping anchor or button with `.card-interactive` on the card. If only a nested element is clickable (header action, footer button), do not mark the card interactive.

### 5.2 Focus ring

```css
.card-interactive:focus-visible {
  outline: 2px solid rgba(163, 255, 18, 0.4);
  outline-offset: 2px;
}
```

Always `:focus-visible`, never `:focus`. Same contract as buttons.

### 5.3 Loading (skeleton)

When a card is loading its own data, swap text slots for skeleton bars. Keep the container, border, padding, and footer structure visible so layout doesn't jump on data arrival.

```css
.card-skeleton-line {
  height: 12px;
  border-radius: 4px;
  background: rgba(245, 240, 232, 0.06);
  animation: pulse 0.6s ease-in-out infinite alternate;
}
@keyframes pulse { to { background: rgba(245, 240, 232, 0.12); } }
```

Title skeleton: 60% width, 16px tall. Body skeletons: 100% + 80% widths, 12px tall. Footer: hidden or preserved with reduced opacity.

---

## 6. Slots detail

### 6.1 Header

```html
<div class="card-header">
  <div class="card-header-text">
    <div class="card-eyebrow">LABEL</div>
    <h3 class="card-title">Title text</h3>
    <div class="card-subtitle">Subtitle or supporting text</div>
  </div>
  <div class="card-header-action">
    <!-- one icon-only button or badge -->
  </div>
</div>
```

- Eyebrow: 11px, uppercase, 0.08em tracking, `var(--text-muted)`. Optional.
- Title: 15px Inter 600, `var(--text-primary)`, line-height 1.3. Required if header exists.
- Subtitle: 13px, `var(--text-muted)`, line-height 1.4. Optional.
- Trailing action: one item. Icon-only button (sm) or badge. Truncation: `min-width: 0` on text block so long titles can ellipsis cleanly.

### 6.2 Body

No fixed styling. Consumer controls typography inside. Default inherits `var(--text-primary)` at 14px / line-height 1.5 if no overrides.

### 6.3 Media

Bleeds to card edges. Negative margin equal to the card's padding. Width 100%, height auto, object-fit cover for images.

```css
.card-md .card-media { margin: -16px -16px 0; }
```

Media is always the top slot. No "media-in-middle" or "media-in-footer" patterns.

### 6.4 Footer

```html
<div class="card-footer">
  <div class="card-footer-meta">2 hours ago · Marc</div>
  <div class="card-footer-actions">
    <button class="btn btn-ghost btn-sm">Dismiss</button>
    <button class="btn btn-primary btn-sm">View</button>
  </div>
</div>
```

- Meta: 12px, `var(--text-muted)`. Left aligned.
- Actions: right aligned, gap 8px. Use `btn-sm` size. Tier: Ghost, Neutral, or Primary (Primary sparingly, see scarcity logic).
- Divider above footer: off by default. Opt in with `.card-footer-divided` when visual separation helps readability (long body + distinct actions).
- On narrow widths (<320px card), footer stacks: meta top, actions bottom, both full-width.

---

## 7. CSS tokens

```css
.card {
  display: flex;
  flex-direction: column;
  gap: 12px;
  border-radius: 8px;
  border: 1px solid transparent;
  background: var(--surface);
  overflow: hidden;
  transition: background 120ms ease, border-color 120ms ease;
}

/* Sizes */
.card-sm { padding: 12px; gap: 8px; }
.card-md { padding: 16px; gap: 12px; }
.card-lg { padding: 24px; gap: 16px; }

/* Variants */
.card-flat     { background: var(--surface); }
.card-outlined { background: transparent; border-color: var(--border-subtle); }
.card-subtle   { background: var(--surface-subtle); }
.card-feature  { background: var(--surface); border-color: rgba(163, 255, 18, 0.3); }

/* States */
.card-interactive { cursor: pointer; }
.card-interactive:hover { border-color: rgba(163, 255, 18, 0.2); }
.card-interactive:focus-visible {
  outline: 2px solid rgba(163, 255, 18, 0.4);
  outline-offset: 2px;
}
.card-selected { border-color: rgba(163, 255, 18, 0.4); }
.card-disabled { opacity: 0.4; pointer-events: none; cursor: not-allowed; }

/* Slots */
.card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
}
.card-header-text { display: flex; flex-direction: column; gap: 2px; min-width: 0; flex: 1; }
.card-eyebrow {
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--text-muted);
}
.card-title {
  font-size: 15px;
  font-weight: 600;
  color: var(--text-primary);
  line-height: 1.3;
  margin: 0;
}
.card-subtitle {
  font-size: 13px;
  color: var(--text-muted);
  line-height: 1.4;
}
.card-header-action { flex-shrink: 0; }

.card-body {
  color: var(--text-primary);
  font-size: 14px;
  line-height: 1.5;
}

.card-media { margin: calc(-1 * var(--card-pad, 16px)) calc(-1 * var(--card-pad, 16px)) 0; }
.card-sm .card-media { margin: -12px -12px 0; }
.card-md .card-media { margin: -16px -16px 0; }
.card-lg .card-media { margin: -24px -24px 0; }
.card-media img, .card-media video { display: block; width: 100%; height: auto; }

.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
}
.card-footer-divided { padding-top: 12px; border-top: 1px solid var(--border-subtle); }
.card-footer-meta { font-size: 12px; color: var(--text-muted); }
.card-footer-actions { display: flex; gap: 8px; flex-shrink: 0; }
```

### 7.1 Notes on token consumption

Card consumes existing Color v1 §5 semantic tokens only: `--surface`, `--surface-subtle`, `--border-subtle`, `--text-primary`, `--text-muted`. The hover and selected border values reference the raw `--signal-500` via rgba for now. If a future Color v1 revision adds semantic tokens like `--border-attention` and `--border-selected`, the card CSS moves to those in lockstep. No per-card color overrides.

---

## 8. Accessibility

- **Contrast.** All text slots use `--text-primary` (warm-100 on warm-700) or `--text-muted` (warm-500 on warm-700). Primary reads 11.2:1, muted reads 4.8:1. Both AA.
- **Interactive wrapping.** If the whole card is the click target, wrap in `<button>` or `<a>`. Do not attach onClick to a `<div>` without the appropriate role and keyboard handler.
- **Selected semantics.** Use `aria-selected="true"` on selected cards in single-select contexts (list, filter, tab-card).
- **Loading semantics.** Use `aria-busy="true"` on cards showing skeletons. Screen readers announce busy state; skeleton bars should be `aria-hidden="true"`.
- **Focus ring.** 2px signal 40%, offset 2px, `:focus-visible` only. Identical to button contract.
- **Keyboard.** Interactive cards respond to Enter and Space. Tab order follows DOM.
- **Truncation.** Long titles ellipsis via `min-width: 0` on text block plus `overflow: hidden; text-overflow: ellipsis; white-space: nowrap` on the title element when single-line truncation is desired. Multi-line: use `-webkit-line-clamp: 2`.

---

## 9. Usage rules

**Do**

- Default to Flat for most product surfaces.
- Use Outlined for nested cards (card-inside-card) or when elevation against the page would double-stack.
- Use Subtle for low-emphasis asides, informational notes, or sidebar groupings.
- Reserve Feature for the single attention card per view. Zero Feature cards is the correct count for most screens.
- Opt in to interactivity explicitly. A card is not interactive unless it says so.
- Keep header trailing slot to one item. Put second actions in the footer.
- Hide media's negative margin discipline: if you change card padding, you also adjust media margin.

**Don't**

- Don't add drop-shadows to achieve elevation. Dark-first reads via surface contrast, not shadows.
- Don't stack two Feature cards adjacent. Scarcity rule applies.
- Don't put a Hero button inside a Feature card. One attention anchor per view.
- Don't override card radius per-instance. 8px is the system radius.
- Don't use Feature variant as a decoration. If it doesn't demand action or attention, it isn't Feature.
- Don't build custom card variants for individual screens. If you need something new, propose it as a new variant back to this spec.
- Don't put more than one icon or badge in the header trailing slot.
- Don't put multiple primary buttons in a card footer. Pick one leading action, pair with ghost.

---

## 10. What this locks

- Four variants (Flat / Outlined / Subtle / Feature) with named tokens from Color v1 §5.
- Three sizes (sm 12 / md 16 / lg 24 padding) at fixed 8px radius.
- Six states (default / hover / focus-visible / selected / disabled / loading).
- Four slots (media / header / body / footer), body required, others optional.
- Header trailing slot: one item only.
- Footer structure: meta left, actions right, optional divider.
- Focus ring contract: 2px signal 40%, offset 2px, `:focus-visible` only. Matches button.
- Interactive mode is opt-in via `.card-interactive`.
- Loading is skeleton-based, not spinner overlay. `aria-busy="true"` on loading cards.
- Scarcity rule: one Feature per view, max. Zero is the product default.
- No shadows. Ever.

Next base components: forms (input, select, textarea, checkbox, radio, switch), navigation (sidebar, top nav, breadcrumb, tabs), feedback (toast, alert, modal, dialog).
