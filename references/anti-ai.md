# Anti-AI

Measurable definitions, detection methods and fixes for the patterns that recur in AI-generated interfaces. The evidence comes from the 23 November 2026 scan (roughly 60 YC sites and 20 studio/gold-standard sites, 1440×900).

## Contents
0. Core principle: flag = justification required
1. Core bans (measurable)
2. New patterns observed in the scan
3. Watch list
4. Pre-code self-check
5. Audit script (browser)
6. Static audit (no browser)
7. AUDIT block and justification format
8. Anti-pairs

---

## 0. Core principle: flag = justification required

A flag does not mean automatic rejection; it means **a justification must be written**. Linear gets a "banned font" flag, Mercury gets a "centered headline" flag. The difference is that both can be explained by a deliberate decision.

A valid justification rests on one of these:
- The user's explicit request or brand system (corporate font, logo color).
- Template permission (e.g. a centered headline in template C).
- A concrete rule from the gallery and the tuning that carries it ("Inter, but 300 weight + lowercase + a wordmark signature element; the Kernel rule").

Invalid justifications: "looks modern", "trendy", "users will like it", "more premium".

If you cannot write a justification, fix it.

---

## 1. Core bans (measurable)

### 1.1 Banned fonts: Inter / Poppins / Montserrat
- **Definition:** The first value of the computed `font-family` of any visible text matches `/^(inter|poppins|montserrat)/i` (Inter Display, InterVariable and Inter Tight included).
- **Detection:** Script → `banned font`. Static → §6 grep 1.
- **Why:** The most common template and AI defaults. Corvera (Poppins 600, centered), Wato (Inter + Inter Display, centered) and Waybill (Inter + 2 more fonts) show them untuned.
- **Note:** Linear, Panta, Kernel and Marengo use Inter. The tuning that saves them: 300/510 weight, -0.02/-0.05em tracking, a signature element. It is banned because an agent cannot hit this reliably.
- **Fix:** Pick one of the recipes in `type-and-color.md` §2; take a font from the alternatives in §4.

### 1.2 Purple/indigo gradient
- **Definition:** On the first screen, a hue of 230–290° with HSL saturation > 35% in a gradient, a glow or a button/link fill.
- **Detection:** Script → `purple/indigo × n` (reads only `rgb()/rgba()`). Static → §6 greps 2–3.
- **Evidence:** Autumn (purple-magenta panel + purple CTA), Vela (#737DE7 CTA + lavender wash), Traceforce (indigo glow), Unisson (pink-purple gradient). Borderline: Mercury #5266EB (232°), Axiom #526FFF (≈230°).
- **Why Stripe can do it:** The gradient is a brand asset owned for years. An agent cannot copy it; it reads it.
- **Fix:** Remove the gradient and use a flat surface. Pick the accent according to `type-and-color.md` §6.7. If the brand color is purple, use it only as a flat CTA color and write a justification.

### 1.3 Three equal cards
- **Definition:** 3 cards of the same width and the same inner structure (icon + heading + text, or number + label) placed side by side. Variants: 3 equal stat cards (Oximy), 3 demo cards (xAI).
- **Detection:** Static → §6 grep 7 (`grid-cols-3`, `repeat(3, 1fr)`). Visual check.
- **Allowed:** When the content type and size differ (e.g. one large product screen and two small numbers).
- **Fix:** An asymmetric split (8+4, 7+5), a numbered list, or one large proof + a side list.

### 1.4 Tracked all-caps labels
- **Definition:** `text-transform: uppercase` + `letter-spacing` > 0.05em, in a **sans-serif** font.
- **Detection:** Script → `tracked caps (sans) × n`. Static → §6 grep 4.
- **Evidence:** Waybill (60 elements across the page), Chronicle (the "BACKED BY Y COMBINATOR" label), Autumn and Hyperspell (nav).
- **Allowed:** In a mono font, tracking 0…+0.04em, one line of metadata per region (Panta eyebrow, Ramp counter, Stoa ticker).
- **Fix:** Switch to sentence case or convert it to mono metadata. Remove the eyebrow above section headings or turn it into a number ("01 — Reconciliation").

### 1.5 Centered generic hero
- **Definition:** ≥ 3 of these 5 elements appear together: (1) a badge/pill above the headline, (2) a centered headline, (3) centered gray body text, (4) 2 CTAs of equal weight, (5) a logo wall or glow.
- **Detection:** Script → `centered headline` (count the other elements visually). Static → §6 grep 5.
- **Evidence:** Traceforce (4/5), Corvera (4/5), Vela (4/5), Waybill (4/5), Comp AI (4/5), Wato (3/5).
- **Allowed:** Template C (narrative photo: Mercury, Balance) or a single ≥ 96px display phrase (Stoa).
- **Fix:** Move the headline to the left (template A or D), move the badge next to the CTA or to the bottom strip, demote the second CTA to a text link, remove the glow.

### 1.6 Soft radius everywhere
- **Definition:** A radius of 12px or more used together on more than 2 component types (card, input, badge, button, image); or decorative blob shapes.
- **Detection:** Static → §6 grep 6 (count). Visual check.
- **Evidence:** Unisson (blob + rounded button + gradient circle), Traceforce (1600px pills).
- **Allowed:** A pill only on the primary CTA (Spaceflow, Granola, Char).
- **Fix:** Pick one system radius (0/2/4/6); see `swiss-system.md` §6.

### 1.7 Fake social proof
- **Definition:** A star/rating badge on the first screen; an anonymous or unsourced testimonial; unsourced round numbers ("10,000+ teams"); a gray logo wall labeled "Trusted by".
- **Detection:** Visual/text check: "★", "4.9/5", "Trusted by", "Loved by", round numbers ending in "+".
- **Evidence:** Comp AI (a G2 4.9/5 badge as the hero's first element), Corvera (logo wall + italic testimonial, larger than the CTA).
- **Fix:** Live or exact data (Stripe's GDP counter, Ramp's payment percentage, Stoa's price ticker, HUD's "8,526,902 task runs"), a real product screen, or an unlabeled black logo row (B&B).

---

## 2. New patterns observed in the scan

| # | Pattern | Measurable definition | Evidence | Fix |
|---|---|---|---|---|
| 2.1 | "Backed by YC" badge above the headline | The hero's first element is an investor badge | On roughly a third of the YC sites scanned; on both good and bad sites | Next to the CTA or in the bottom strip, 12–13px mono (Asimov, Stoa) |
| 2.2 | Title Case headline | 3+ words in the headline start with a capital | Traceforce, Chronicle, Marengo | Sentence case |
| 2.3 | Glow behind the product | Radial gradient/blur behind the product screen or headline, in any hue | Traceforce (purple), Waybill and Axiom (blue) | Remove the glow; place the product on a flat background close to the headline (Linear) |
| 2.4 | Gradient-filled CTA | A gradient `background-image` on a button | Hyperspell, Unisson | Flat `--accent` |
| 2.5 | Pre-headline noise stack | Announcement bar + "New" pill + badge: 2 or 3 of them together | Sim, Mastra | Keep at most one |
| 2.6 | Heavy display + positive/zero tracking | Display ≥ 48px with weight ≥ 600 or tracking ≥ 0 | Vela (Georgia 700), Waybill (700), Traceforce (500, normal) | 400–500 weight, -0.02…-0.04em |
| 2.7 | Fallback font leak | The computed font of a visible element is `sans-serif`, `ui-sans-serif`, `system-ui`, SF Pro, Roboto or Arial | Chronicle and Wato (button), Char (button), Spaceflow (button) | Apply the font to buttons too; `font: inherit` |
| 2.8 | Trial font in production | The font name contains "Trial" | Chronicle (Kalice Trial), ProvenMetal (Rhetorik Serif Trial) | Buy a license or choose an alternative |
| 2.9 | Rotating word | A word in the headline that changes through animation | Corvera, Stoa | A single, fixed headline |
| 2.10 | Equal-weight CTA pair | Two filled buttons side by side | Traceforce, Casey (green + pink) | Make the second one outlined or a text link |

---

## 3. Watch list

Not banned, but if chosen, a justification is required in the SYSTEM or AUDIT block.

- **Geist / Geist Mono:** Present on 13 of the roughly 50 sites whose fonts were measured. On its way to becoming "the new Inter".
- **Outfit, Manrope, DM Sans, Plus Jakarta Sans, Space Grotesk, Sora:** Template-default risk (the first two were seen on weak examples in the gallery).
- **Pastel blur background:** A member of the same family even when not purple (borderline on Zomma).
- **Announcement bar:** Not banned on its own, but a competitor if it is read before the headline (see `eye-path.md` §5).
- **Blue CTAs at 220–230°:** Just at the edge of the purple range; they can read as indigo (Axiom #526FFF).

---

## 4. Pre-code self-check

Before writing code, check the SYSTEM block against this list:

- [ ] The fonts are not on the banned list; if one is on the watch list, the justification is ready.
- [ ] At most 2 families.
- [ ] Display weight 300–500, negative tracking.
- [ ] The headline is in sentence case and fixed (no rotating word).
- [ ] Unless the template is C, the headline is left-aligned (or a single ≥ 96px phrase in D).
- [ ] Badge/announcement/pill: at most one, and not above the headline.
- [ ] A single saturated color; not 230–290°.
- [ ] No gradient (except photos); no glow.
- [ ] No three equal cards; one system radius.
- [ ] Proof: a real product or an exact number; no star badge and no "Trusted by".

---

## 5. Audit script (browser)

After coding, run it in the browser console at a 1440×900 viewport. The script is a simplified version of the method used for the gallery measurements.

```js
// agents-eye · first-screen audit
(() => {
  const vis = e => { const r = e.getBoundingClientRect(), s = getComputedStyle(e);
    return r.width > 0 && r.height > 0 && s.visibility !== 'hidden' && +s.opacity > 0.05; };
  const fam = s => s.fontFamily.split(',')[0].replace(/["']/g, '').trim();
  const leaves = [...document.querySelectorAll('body *')].filter(e =>
    vis(e) && e.getBoundingClientRect().top < innerHeight &&
    [...e.childNodes].some(n => n.nodeType === 3 && n.textContent.trim().length > 1));
  const fonts = [...new Set(leaves.map(e => fam(getComputedStyle(e))))];
  const h = leaves.map(e => [e, parseFloat(getComputedStyle(e).fontSize)]).sort((a, b) => b[1] - a[1])[0]?.[0];
  const hs = h && getComputedStyle(h), hr = h && h.getBoundingClientRect();
  // centered: text-align center, or a narrow box centered in the viewport
  const centered = !!hr && (hs.textAlign === 'center' ||
    (Math.abs(hr.left + hr.width / 2 - innerWidth / 2) < 40 && hr.width < innerWidth * 0.8));
  const trackedCapsSans = leaves.filter(e => { const s = getComputedStyle(e);
    return s.textTransform === 'uppercase' && parseFloat(s.letterSpacing) / parseFloat(s.fontSize) > 0.05 && !/mono/i.test(s.fontFamily); }).length;
  const gradients = [...document.querySelectorAll('body *')].filter(e =>
    vis(e) && e.getBoundingClientRect().top < innerHeight && /gradient/.test(getComputedStyle(e).backgroundImage)).length;
  const trackingEm = hs ? (parseFloat(hs.letterSpacing) || 0) / parseFloat(hs.fontSize) : 0;
  const leading = hs ? parseFloat(hs.lineHeight) / parseFloat(hs.fontSize) : NaN;
  // purple/indigo: hue 230–290°, saturation > 35% in gradients and button/link fills (reads rgb/rgba only)
  const hsl = (r, g, b) => { r /= 255; g /= 255; b /= 255; const mx = Math.max(r, g, b), mn = Math.min(r, g, b), d = mx - mn;
    if (!d) return [0, 0]; let h = mx === r ? ((g - b) / d) % 6 : mx === g ? (b - r) / d + 2 : (r - g) / d + 4;
    h *= 60; if (h < 0) h += 360; return [h, d / (1 - Math.abs(mx + mn - 1))]; };
  const purpleHits = [...document.querySelectorAll('body *')].filter(e => vis(e) && e.getBoundingClientRect().top < innerHeight)
    .filter(e => { const s = getComputedStyle(e);
      const src = s.backgroundImage + ' ' + (/^(A|BUTTON)$/.test(e.tagName) ? s.backgroundColor : '');
      return [...src.matchAll(/rgba?\((\d+),\s*(\d+),\s*(\d+)/g)].some(m => { const [h, sat] = hsl(+m[1], +m[2], +m[3]);
        return h >= 230 && h <= 290 && sat > 0.35; }); }).length;
  return {
    fonts,
    headline: hs && { font: fam(hs), size: hs.fontSize, weight: hs.fontWeight,
      trackingEm: +trackingEm.toFixed(3), leading: isNaN(leading) ? 'normal' : +leading.toFixed(2),
      left: Math.round(hr.left), width: Math.round(hr.width), centered },
    flags: [
      fonts.length > 2 && `font count ${fonts.length} (>2)`,
      fonts.some(f => /^(inter|poppins|montserrat)/i.test(f)) && 'banned font',
      fonts.some(f => /trial/i.test(f)) && 'trial font',
      fonts.some(f => /^(sans-serif|ui-sans-serif|system-ui|-apple-system|blinkmacsystemfont|sf pro.*|roboto|arial|helvetica)$/i.test(f)) && 'fallback font leak',
      purpleHits > 0 && `purple/indigo × ${purpleHits}`,
      hs && +hs.fontWeight >= 600 && 'display weight ≥ 600',
      hs && parseFloat(hs.fontSize) >= 48 && trackingEm >= 0 && 'display tracking ≥ 0',
      centered && 'centered headline (violation unless template C/D)',
      trackedCapsSans > 0 && `tracked caps (sans) × ${trackedCapsSans}`,
      gradients > 2 && `first-screen gradient × ${gradients}`
    ].filter(Boolean)
  };
})()
```

**Test result (23 November 2026):** Corvera 4 flags (banned font, weight ≥ 600, centered, gradient); Ramp 0 flags. The purple check returned 4 hits on Autumn, 6 on Vela and 0 on Linear. Linear still gets the "banned font" flag.

**Limitations**
- The purple check reads only `rgb()/rgba()` values. Colors written in `oklch()`/`lab()` and purple inside images are not caught; check those visually.
- Three equal cards, fake social proof, Title Case and radius sprawl are outside the script; check them with §6 and visually.
- The "largest font" is taken as the headline. If there is a giant wordmark (Kernel), it may measure that instead of the headline. Compare the result with the 1st look in the pre-code block.
- Fonts are read from the computed `font-family` declaration. A web font that is declared but fails to load is not detected; check the Network panel or `document.fonts`.

---

## 6. Static audit (no browser)

Run these on the source code (replace `src/` with the project folder). They are heuristic searches; verify every match by eye.

```bash
# 1 — banned font
grep -rniE "font-family[^;]*(inter|poppins|montserrat)|['\"](inter|poppins|montserrat)['\"]|font-(inter|poppins|montserrat)\b" src/

# 2 — purple/indigo (Tailwind classes and common hex values)
grep -rnE "(from|via|to|bg|text|ring|shadow|border)-(purple|violet|indigo)-[0-9]{2,3}|#(6366f1|4f46e5|8b5cf6|7c3aed|a855f7|9333ea)" src/

# 3 — gradient and glow
grep -rnE "linear-gradient|radial-gradient|conic-gradient|bg-gradient-to-|bg-linear-to-|bg-radial|blur-(2xl|3xl)|drop-shadow-\[" src/

# 4 — tracked caps
grep -rnE "uppercase[^\"'>]*tracking-(wide|wider|widest)|tracking-(wide|wider|widest)[^\"'>]*uppercase|letter-spacing:\s*0?\.(0[6-9]|[1-9])" src/

# 5 — centered hero headline
grep -rnE "<h1[^>]*(text-center|mx-auto)|text-center[^\"'>]*text-(5xl|6xl|7xl|8xl)" src/

# 6 — radius sprawl (count; flag if you see it on 3+ component types)
grep -rnoE "rounded-(xl|2xl|3xl|\[1[2-9]px\]|\[[2-9][0-9]px\])|border-radius:\s*(1[2-9]|[2-9][0-9])px" src/ | wc -l

# 7 — three equal cards
grep -rnE "grid-cols-3|repeat\(3,\s*(1fr|minmax)" src/

# 8 — heavy display
grep -rnE "<h1[^>]*font-(semibold|bold|extrabold|black)|h1[^{]*\{[^}]*font-weight:\s*(6|7|8|9)00" src/

# 9 — fake social proof
grep -rniE "trusted by|loved by|★|4\.[5-9]/5|[0-9]+k\+ (users|teams|companies)" src/

# 10 — fallback font and trial font
grep -rniE "font-family:\s*(system-ui|-apple-system|sans-serif|arial|helvetica|roboto)\b|font-family[^;]*trial|['\"][^'\"]* trial['\"]" src/
```

What the static audit cannot measure: the eye-path tests (blur, CTA distance). Estimate them by reading the code and mark them "static — estimated" in the AUDIT block.

---

## 7. AUDIT block and justification format

```
AUDIT — [page]
Method: [script | static]
Flags: [list or "0 flags"]
Justifications:
  - [flag]: [why it is deliberate] — [basis: user request | brand | template permission | gallery rule]
Tests: blur [pass/fail] · saturated colors [n] · CTA distance [px] · elements [n]
Result: [delivered | fixed and re-audited]
```

**Example** (the Tally page from `eye-path.md` §4)
```
AUDIT — Tally home page
Method: script
Flags: banned font
Justifications:
  - banned font: Tally's brand guide specifies Inter; set at 400 weight, -0.03em tracking, 64px, with a single grotesk and no second family — user's brand system (Linear rule)
Tests: blur pass · saturated colors 1 · CTA distance 24px · elements 5
Result: delivered
```

---

## 8. Anti-pairs

Pairs that produce different results under the same conditions.

| Good | Anti | Lesson |
|---|---|---|
| Ramp | Comp AI | Same font (Lausanne). Difference: left-aligned headline + live counter + product screen vs. gradient panel + star badge. |
| Linear | Traceforce | Dark theme + product screen. Difference: product adjacent to the headline and flat vs. glow from below + Title Case. |
| Panta | Corvera | B2B, sector-specific headline. Difference: concrete verb + single-word emphasis vs. Poppins + rotating word. |
| Kernel | Wato | Both use Inter. Difference: wordmark + 300 weight + lowercase vs. centered template. |
| Browser Use | Waybill | Dark, centered, short headline. Difference: product diagram vs. glow + product-less hero. |
| Granola / Char | Vela | Serif headline. Difference: serif 400 + real product vs. Georgia 700 + indigo. |
| Willow / Asimov | Autumn | Left-aligned, square-cornered. Difference: single neutral CTA vs. a purple gradient panel stealing the 1st look. |
