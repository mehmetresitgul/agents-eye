# Swiss system

Type scale, spacing, grid, color and radius tokens. **Measured** values come from the 23 November 2026 scan (1440×900, DOM `getComputedStyle`). Values marked **recommended** were not measured in the gallery; they are derived from the measured ones.

Core principle: the system comes first, and exceptions need a justification. If a value is not one of the tokens in this file, write its justification in the AUDIT.

## Contents
1. Type scale (φ-based)
2. Tracking, leading, weight
3. Spacing (8px)
4. Grid (1440 viewport)
5. Color tokens
6. Radius, lines, shadows
7. Ready-made CSS starter file
8. Checklist

---

## 1. Type scale (φ-based)

Base 16px, multiplier φ = 1.618: **16 → 26 → 42 → 68 → 110**. Line heights are rounded to multiples of 4px.

| Token | px | Line (px) | Role | Weight | Tracking |
|---|---|---|---|---|---|
| `--text-meta` | 12–13 | 16–20 | Mono metadata, label, ticker | 400 | 0 |
| `--text-small` | 14 | 20 | Nav, button, footnote | 400–500 | 0 |
| `--text-body` | 16 | 24 | Body | 400 | 0 |
| `--text-body-l` | 18 | 28 | Hero body | 400 | 0 / -0.01em |
| `--text-lead` | 26 | 32 | Lead, second-layer heading | 400 | -0.01em |
| `--text-h2` | 42 | 44–48 | Section heading | 500 | -0.02em |
| `--text-display` | 68 (56–72) | 68 | Hero headline | 400 (300–500) | -0.02 / -0.04em |
| `--text-display-xl` | 110 (96–120) | 104 | Poster headline (template D) | 400 | -0.035 / -0.05em |

`--text-body-l` (18px) is not a φ step, but most hero body text in the gallery is 18px (Willow, Ramp, Asimov, Resend). It is kept as a practical in-between step.

**Measured hero headlines:** the 64px cluster dominates (Linear, Vercel, Spaceflow, Sim, Kernel, Casey, Hyperspell, Ramp, Raycast). The φ step 68 sits at the upper edge of this cluster. The poster cluster is 86–120px (Granola 86, Resend 96, Stoa 115, Panta 120).

### Ratio rule
The display ÷ body ratio should be **between 3.3 and 4.4**; the target is **φ³ ≈ 4.24**.

| Reference | Display / body | Ratio |
|---|---|---|
| Linear | 64 / 15 | 4.27 |
| Granola | 86.4 / 20 | 4.32 |
| ProvenMetal | 65.5 / 15.2 | 4.31 |
| Spaceflow | 64 / 16 | 4.0 |
| Marengo | 73.8 / 18.9 | 3.9 |
| Ramp | 64 / 18 | 3.56 |
| Zomma | 77.8 / 22 | 3.53 |
| Arga Labs | 54 / 16 | 3.38 |
| Willow | 60 / 18 | 3.33 |

- In the poster template (D) the ratio can rise to 5–6.4: Panta 5.0, Resend 5.3, Stoa 6.4.
- Ratios below 2.5 are valid only if color or opacity carries the hierarchy (Parallel 36/26 = 1.38, gray lead; Hyperspell 64/30 = 2.1).

### Mobile (recommended, 375px)
Each role drops one φ step: display 68 → 42 (line 44), display-xl 110 → 68 (line 64), h2 42 → 26 (line 32), lead 26 → 20 (line 28). Body stays at 16px.

---

## 2. Tracking, leading, weight

### Tracking (by size)
| Size | Tracking | Measured |
|---|---|---|
| ≥ 96px | -0.035 … -0.05em | Stoa -0.035 · Panta -0.035 |
| 56–95px | -0.02 … -0.04em | Linear -0.022 · Sim -0.025 · Zomma -0.03 · Spaceflow -0.04 · Arga -0.045 · Marengo -0.05 |
| 32–55px | -0.01 … -0.03em | Chronicle -0.02 · witharc -0.03 |
| 18–31px | 0 … -0.02em | Willow -0.01 · Kernel -0.013 |
| ≤ 16px | 0 … +0.02em | Sim +0.0175 |
| Mono | 0 | — |
| Uppercase mono metadata | 0 … +0.04em | Ramp counter, Panta eyebrow |

- Halve the tracking for serif display (-0.01 / -0.02em): Resend -0.01, Granola -0.02, ProvenMetal -0.02.
- Positive tracking at display size looks loose (Mastra +0.005em). Do not use it.
- -0.06em is the limit (Vercel, Hyperspell). Beyond that, letters collide.

### Leading
| Role | Leading | Measured |
|---|---|---|
| display-xl | 0.94–0.98 | Marengo 0.94 · Panta 0.96 · Stoa 0.98 |
| display (sans) | 1.0–1.05 | Linear, Vercel, Ramp, Spaceflow 1.0 · Zomma 1.04 |
| display (serif) | 0.93–1.3 | Granola 0.93 · Resend 1.0 · Cursor 1.25 · Char 1.3 (test against the x-height; do not go below 0.92) |
| h2 | 1.05–1.15 | — |
| lead | 1.25–1.45 | Parallel 1.23 · Kernel 1.25 · Zomma 1.45 |
| body | 1.5–1.6 | Willow 1.56 · Linear 1.6 · ProvenMetal 1.65 |
| meta | 1.33–1.5 | — |

### Weight
- **The display default is 400.** 300 for a light tone (Zomma, Kernel); ultra-light 200 only for serif and at ≥ 64px (Balance). Anything above 500 needs a justification.
- Intermediate weights (450, 480, 510, 550) build micro-hierarchy in variable fonts: Linear 510, Mercury 360/420/480, xAI 450.
- Body 400, button 500, mono 400.
- **Build hierarchy with scale, not weight.** On Spaceflow, Stoa, Willow, Ramp and Sim, the headline and body share the same weight (400); the only difference is size.

### Line length
- Body: 45–75 characters (`max-width: 60–68ch`).
- Hero headline: 2–3 lines, 5–7 columns (≈ 526–746px). Measured: Interfere 450, Willow 543, Cua 547, ProvenMetal 560, Spaceflow 584, Char 608, Sim 621, Casey 720, Marengo 747.
- `text-wrap: balance` on headlines, `text-wrap: pretty` on body text.

---

## 3. Spacing (8px)

| Token | px | Use |
|---|---|---|
| `--space-1` | 4 | Icon–label, inline micro spacing |
| `--space-2` | 8 | Icon gap inside buttons, tight lists |
| `--space-3` | 16 | Headline → lead (tight), form field spacing |
| `--space-4` | 24 | Headline → lead (standard), lead → CTA, gutter |
| `--space-5` | 32 | Lead → CTA (airy), card padding |
| `--space-6` | 48 | Hero text → product screen (min), between blocks |
| `--space-7` | 64 | Above the logo strip, above the product screen |
| `--space-8` | 96 | Between sections (1440) |
| `--space-9` | 128 | Between large sections, top space of a poster hero |

**Hero inner rhythm (measured):**
| Reference | Headline → lead | Lead → CTA |
|---|---|---|
| Willow | 24 | 24 |
| Chronicle Labs | 24 | 32 |
| Asimov | 24 | 32 |
| tash | 16 | 24 |
| Wato | 16 | 32 |
| Parallel | 16 | 16 |
| Zomma | 36 | 48 |

- Rule: headline → lead **16–24**, lead → CTA **24–32**. Zomma's 36/48 is a deliberately expanding rhythm in a poster tone (36 is on a 4px grid; for an 8px grid use 32/48).
- Off-grid measurements (avoid): Cua 22, Autumn 25, Arga 28.
- Button height: **40 / 44 / 48**. Horizontal padding 16–24.
- Card padding: 24 or 32.

---

## 4. Grid (1440 viewport)

| Value | 1440 |
|---|---|
| Columns | 12 |
| Gutter | 24px |
| Outer margin | `clamp(24px, 5vw, 96px)` → 72px |
| Content width | 1296px |
| Column width | 86px |
| Start of column n | 72 + (n − 1) × 110 px |
| Width of n columns | 110n − 24 px (5 → 526, 6 → 636, 7 → 746) |

**Measured left margins:** 16 (B&B) · 24 (Vercel) · 32 (Asimov) · ≈48 (Linear) · 63–64 (Cursor, Ramp, Kernel) · 72–77 (ProvenMetal, Parallel, Willow, Arga, Cua) · 88–133 (Panta, Interfere, Granola, Zomma). The 64–96 range is the majority. 16–32 only in template E or on very minimal pages.

### Placement by template
| Template | Placement |
|---|---|
| A1 | Text columns 1–5, product 6–12 (φ split 7+5) or 1–6 / 7–12 |
| A2 | Headline 1–6; description + CTA 8–12, aligned to the headline's baseline; product 1–12 below |
| B | Headline 1–5; object 6–12 or centered, 25–45% of the first-screen area |
| C | Full-bleed photo; text 1–5 (bottom left) or 3–10 (centered top) |
| D | Headline 1–9 … 1–12, 2–4 lines |
| E | Nav 1–2, content 4–9 |

### Vertical placement
- The top edge of the hero headline sits at **20–32%** of the viewport height. Measured median 27%: Spaceflow 228px, Linear 242, Panta 242, Sim 245, Asimov 245, Marengo 248, Kernel 274, Zomma 289, Willow 291 (at 900px). Arga at 153px (17%) sits above the range.
- Bottom-aligned variant (B/C): the text block is in the bottom third (Chronicle 636px, Balance 520px). In that case the 1st look belongs to the image; write it that way in the pre-code block.

### Breakpoints (recommended)
| Viewport | Columns | Gutter | Margin |
|---|---|---|---|
| ≥ 1440 | 12 | 24 | 72–96 |
| 1024 | 12 | 20 | 40 |
| 768 | 8 | 16 | 32 |
| 375 | 4 | 16 | 20 |

Below 768, A1 and B collapse into a vertical stack: the 1st-look element first. In B on mobile, the object moves below the headline and the eye path becomes 1 headline → 2 object → 3 CTA. Note this in the pre-code block.

---

## 5. Color tokens

The structure is fixed; values are chosen from the rules in `type-and-color.md` §6 and the palettes in §7.

| Token | Role | Rule |
|---|---|---|
| `--bg` | Background | Warm neutral: RGB channel spread ≤ 12, R ≥ G ≥ B |
| `--fg` | Main text | #111–#25221D in light themes; #EDEDED–#F7F8F8 or cream in dark themes |
| `--fg-muted` | Secondary text | `--fg` at 55–65% opacity or a fixed gray; contrast ≥ 4.5:1 |
| `--line` | Divider line | `--fg` at 8–12% opacity, 1px |
| `--accent` | Primary CTA | The single saturated color; used nowhere else (exceptions: the B object, a single word in the headline) |
| `--accent-fg` | CTA text | ≥ 4.5:1 on `--accent` |

---

## 6. Radius, lines, shadows

| Token | Value | Measured |
|---|---|---|
| `--radius-0` | 0 | Kernel, ProvenMetal, Willow, Asimov |
| `--radius-1` | 2px | Marengo (2.7) |
| `--radius-2` | 4px | Stripe, Parallel, tash, Chronicle |
| `--radius-3` | 6px | Vercel, Ramp, AgentMail |
| `--radius-pill` | 999px | Primary CTA only (Spaceflow, Granola, Char, Zomma) |

- Pick **one system radius** for all components (card, input, badge, secondary button): 0, 2, 4 or 6.
- A pill may be used only on the primary CTA (optional).
- Do not use a radius of 12px or more on more than two component types together ("soft everything").
- Lines: 1px, `--line`. Use lines instead of shadows to separate cards.
- Shadows: none, or a single fixed low-opacity one (`0 1px 2px rgb(0 0 0 / 0.06)`). No glow, colored shadows or glassmorphism.

---

## 7. Ready-made CSS starter file

Choose fonts from `type-and-color.md` §2–4 and write the rationale in the SYSTEM block. The values below are for template A and a light warm theme.

```css
:root {
  /* Fonts — choose from type-and-color.md (at most 2 families) */
  --font-1: "FONT_1", ui-sans-serif, sans-serif;   /* display + body */
  --font-2: "FONT_2", ui-monospace, monospace;     /* mono system layer or body */

  /* Type scale (φ) */
  --text-meta: 12px;   --lh-meta: 16px;
  --text-small: 14px;  --lh-small: 20px;
  --text-body: 16px;   --lh-body: 24px;
  --text-body-l: 18px; --lh-body-l: 28px;
  --text-lead: 26px;   --lh-lead: 32px;
  --text-h2: 42px;     --lh-h2: 44px;
  --text-display: 68px;    --lh-display: 68px;
  --text-display-xl: 110px; --lh-display-xl: 104px;

  /* Spacing (8px) */
  --space-1: 4px;  --space-2: 8px;  --space-3: 16px; --space-4: 24px;
  --space-5: 32px; --space-6: 48px; --space-7: 64px; --space-8: 96px; --space-9: 128px;

  /* Grid */
  --columns: 12;
  --gutter: 24px;
  --margin: clamp(24px, 5vw, 96px);
  --container: 1440px;

  /* Color — from the palettes in type-and-color.md §7 */
  --bg: #F9F7F2;
  --fg: #141410;
  --fg-muted: rgb(20 20 16 / 0.6);
  --line: rgb(20 20 16 / 0.1);
  --accent: #1F5C3A;      /* primary CTA only */
  --accent-fg: #FFFFFF;

  /* Radius */
  --radius: 4px;          /* one system radius: 0 | 2 | 4 | 6 */
  --radius-pill: 999px;   /* primary CTA only */
}

* { box-sizing: border-box; }
body {
  margin: 0;
  background: var(--bg);
  color: var(--fg);
  font: 400 var(--text-body)/var(--lh-body) var(--font-1);
  -webkit-font-smoothing: antialiased;
}

.container { max-width: var(--container); margin-inline: auto; padding-inline: var(--margin); }
.grid { display: grid; grid-template-columns: repeat(var(--columns), minmax(0, 1fr)); column-gap: var(--gutter); }

.display {
  font-size: var(--text-display);
  line-height: var(--lh-display);
  font-weight: 400;
  letter-spacing: -0.03em;
  text-wrap: balance;
  margin: 0;
}
.display-xl { font-size: var(--text-display-xl); line-height: var(--lh-display-xl); font-weight: 400; letter-spacing: -0.04em; margin: 0; }
.lead { font-size: var(--text-body-l); line-height: var(--lh-body-l); color: var(--fg-muted); max-width: 60ch; text-wrap: pretty; margin: var(--space-4) 0 0; }
.meta { font: 400 var(--text-meta)/var(--lh-meta) var(--font-2); color: var(--fg-muted); }

.btn {
  display: inline-flex; align-items: center; gap: var(--space-2);
  height: 44px; padding-inline: var(--space-4);
  font: 500 var(--text-small)/1 var(--font-1);
  border-radius: var(--radius); border: 1px solid var(--line);
  background: transparent; color: var(--fg); text-decoration: none;
}
.btn--primary { background: var(--accent); color: var(--accent-fg); border-color: transparent; }

/* A1 hero example */
.hero { padding-block: clamp(var(--space-8), 22vh, 240px) var(--space-8); }
.hero__text { grid-column: 1 / span 5; }
.hero__product { grid-column: 7 / span 6; opacity: 0.85; }
.hero__cta { margin-top: var(--space-5); display: flex; gap: var(--space-3); }

@media (max-width: 767px) {
  :root {
    --text-display: 42px; --lh-display: 44px; --text-display-xl: 68px; --lh-display-xl: 64px;
    --text-h2: 26px; --lh-h2: 32px; --text-lead: 20px; --lh-lead: 28px;
    --columns: 4; --gutter: 16px; --margin: 20px;
  }
  .hero__text, .hero__product { grid-column: 1 / -1; }
}
```

---

## 8. Checklist

- [ ] Every font size is one of the scale tokens (or justified).
- [ ] Display/body ratio 3.3–4.4 (≤ 6.4 in template D).
- [ ] Display weight 300–500; tracking matches the size table and is negative.
- [ ] All vertical spacing in the hero is a multiple of 8px; headline → lead 16–24, lead → CTA 24–32.
- [ ] Headline 5–7 columns, 2–3 lines; its top edge at 20–32% of the viewport.
- [ ] One system radius; pill only on the primary CTA.
- [ ] Colors follow the token structure: bg, fg, muted, line, accent. Accent only on the primary CTA.
