# Eye path

Used to decide, before code, where the eye goes and in what order. The measurements in this file were read from the pages' DOM at 1440×900 on 23 November 2026.

## Contents
1. Definitions and attention drivers
2. Template choice (decision tree)
3. Templates A–E
4. Pre-code block (locked format)
5. Competing elements and suppression
6. Validation tests
7. Section-level eye path
8. App screens

---

## 1. Definitions and attention drivers

- **1st look:** The element the user locks onto in the first half second. There is only one on the first screen.
- **2nd look:** The element that explains or proves the 1st look.
- **3rd look:** The primary action (CTA). The CTA must be read third at the latest. On Corvera the testimonial gets ahead of the CTA, so the action drops to 4th place; that is a violation.

**Drivers of attention (strongest to weakest):**

| # | Driver | Measure | Gallery example |
|---|---|---|---|
| 1 | Size × contrast | Largest area with the highest contrast against the background | Stoa 115px headline, Panta 120px |
| 2 | Saturation | The only saturated element on a neutral page | AgentMail's orange envelope, Ramp's lime CTA |
| 3 | Isolation | Empty space around it | Cursor: a 26px headline is the 1st look because the space around it is empty |
| 4 | Position | Top left (start of the F), ends of the Z path | Linear, Sim, Willow: top-left headline |
| 5 | Photographic object / face | A real object, a human face | tash's card, the video-call thumbnails on Granola |
| 6 | Motion | Ticker, animation, rotating word | Stoa's ticker (controlled), Corvera's word animation (uncontrolled) |

Motion (6) ranks weakest, but it is also the easiest way to steal the 1st look. If there is animation, write it on the "Competitor" line of the pre-code block.

---

## 2. Template choice (decision tree)

Ask the questions in order; stop at the first "yes".

1. Can the product's real interface be shown, and is it understood at a glance? → **A**
2. Is the product abstract (API, infrastructure, service) but can it be told with a single object (envelope, card, key, drawing), or does the brand have an owned signature element (wordmark, logo form, geometric module)? → **B**
3. Is there a brand-specific photo that tells an idea (not stock and not an AI render)? → **C**
4. Is the message strong and concrete in one sentence, and the product cannot be shown yet? → **D**
5. Is the brand personality carried by text (studio, agency, research, personal)? → **E**
6. If none apply → **A** (if there is no product, show the product's output: a report, a message, a result).

---

## 3. Templates A–E

Grid terms follow `swiss-system.md` §4: 12 columns at 1440, column ≈ 86px, gutter 24px, margin 72px.

### A — Split hero
**Eye path:** 1 headline → 2 product screen → 3 primary CTA

**Variant A1 (side by side):** Text in columns 1–5/6, product in columns 6/7–12. φ split: 12 ÷ φ ≈ 7.4 → 7 + 5.
**Variant A2 (top/bottom):** In the top band, the headline in columns 1–6, description + CTA in columns 8–12 aligned to the headline's baseline (split header). In the bottom band, a full-width product screen 48–96px below the headline.

**Rules**
- The product screen must have real content, not lorem ipsum.
- The product screen must have lower contrast than the headline (60–80% opacity, a gray textured background or a low-contrast frame).
- Nothing goes between the headline and the product screen (logo strip, badge, second headline).
- In A1, the CTA sits 24–32px below the body. In A2, the CTA is in the right column, at the headline's baseline.

**Typical mistakes:** A glow behind the product; a product screen brighter than the headline; a mock carrying fake data.

**References**
- **Linear** (A2): display 64/510/-0.022em/1.0; the product screen starts right below the headline; 3 elements on the first screen.
- **Sim** (A2): display 64/400/-0.025em; description + CTA in the right column at the headline's baseline; product pushed back with a gray marble texture.
- **Willow** (A1): display 60/400/-0.02em; headline → body 24px, body → CTA 24px; square 48px CTA.
- More: Interfere, Arga Labs, Spaceflow, Ramp.

### B — Object/signature-first
**Eye path:** 1 object/signature element → 2 headline → 3 CTA

**Layout:** The object sits in the center or on the right (columns 6–12) and covers 25–45% of the first-screen area. The headline sits top left (columns 1–5) or above the object on the left.

**Rules**
- The object is the only saturated or the only photographic element on the page.
- The object must derive from the brand's name, logo or product metaphor: envelope = email API, card = card investing, key = computer, halftone = infrastructure/print.
- Because the headline is the 2nd look, it stays calm: 400–500 weight, neutral color.
- A single color link may connect the object and the headline (one word in the headline, in the same color as the object).

**Typical mistakes:** An abstract blob, sphere or shiny 3D shape; two objects competing; an object that stays decorative and does not explain the product.

**References**
- **AgentMail:** orange envelope in the center; headline on the left, tagline on the right (asymmetric triad); orange as the single accent.
- **tash:** graded card in the middle column; visible column lines; color only on the object.
- **Kernel:** cropped giant wordmark; headline 64/300 and lowercase; square-cornered CTA.
- More: Marengo (halftone), Casey (geometric module), Vercel (logo), Raycast (light derived from the logo).

### C — Photo narrative
This is the only template that allows centering.

**Eye path:** 1 the photo's focal point → 2 headline → 3 CTA

**Layout:** Full-bleed photo. The text sits in the calmest region of the photo: centered top (Mercury) or bottom-left quadrant (Balance). The text block has at most 4 elements (headline, lead, CTA, secondary link).

**Rules**
- The photo must carry a brand-specific idea: a desk on a mountain = freedom from the office; columns = Stoa.
- The photo region under the text must be calm. If needed, use a flat black overlay (10–25%), not a gradient.
- If you use an ultra-thin (200–300) font, the display must be ≥ 64px and the contrast ≥ 3:1.

**Typical mistakes:** A stock "team meeting" photo or an AI render; text falling on a busy region of the photo; photo + glow.

**References**
- **Mercury:** the desk is the focal point; headline 49px/480, centered at the top; intermediate weights 360/420/480.
- **Balance:** sky; headline 72/200 serif, in the bottom-left quadrant.
- **Stoa:** column photo + a 115px single-line headline (between C and D).

### D — Type-first (poster)
**Eye path:** 1 giant headline → 2 emphasis within the headline or lead → 3 CTA

**Layout:** The headline is 7–12 columns wide, 2–4 lines, ≥ 86px or a display/body ratio ≥ 4.3. The first screen has at most 3 elements besides the headline.

**Rules**
- Leading 0.94–1.0, tracking -0.03/-0.05em.
- One typographic surprise is allowed: one word in italics or in the accent color. **No new font is added.** Panta does this with a third font; the agent builds the same effect within 2 fonts using italics or color.
- Rotating words are banned: the headline looks incomplete at first (Stoa's "The market behind", Corvera's "intel→agent").

**Typical mistakes:** 700 weight; gradient text; a headline breaking into 5+ lines and pushing the CTA off screen.

**References**
- **Panta:** 120/600/-0.035em/0.96; one word in italics and sage green; mono eyebrow.
- **Zomma:** 78/300/-0.03em/1.04; 4 elements on the first screen; headline → lead 36px, lead → CTA 48px.
- **Resend:** 96px serif/400, ratio 5.3; monochrome.
- More: Granola (86px serif, leading 0.93), Browser Use (84px + diagram).

### E — System/editorial
**Eye path:** 1 first line → 2 rhythm element (underline, list) → 3 CTA

**Layout:** A narrow nav column (columns 1–2) + a content column (columns 4–9), or a single full-width sentence set against the margin. One type size (28–50px), many layers.

**Rules**
- Hierarchy is built not with size but with order, opacity (100% / 85% / 70%), color (dark / gray) and underlines.
- The size difference is at most one φ step (e.g. 36/26).
- Use it only for brands whose personality is carried by text. On a product site the value proposition gets lost.

**References**
- **witharc.co:** everything is 32px; the first line at 85% opacity + 500 weight, the rest at 70% + 400; underlined client names.
- **bakkenbaeck.com:** a single 50px/500 sentence, left margin 16px; one font, one weight.
- **Parallel:** 36px dark headline + 26px gray lead; color builds the hierarchy.

---

## 4. Pre-code block (locked format)

The line order and labels do not change. "Extracted rules" records the measurements taken from the two references; "First-screen elements" feeds test 4 in §6.

```
EYE PATH — [page/screen name]
Template: [A|B|C|D|E|app] (+variant) — references: [ref 1], [ref 2]
Extracted rules:
  - [ref 1]: [rule 1]; [rule 2]; [rule 3]
  - [ref 2]: [rule 1]; [rule 2]; [rule 3]
1st look: [element] — why: [size / contrast / position / color, with numbers]
2nd look: [element] — why: [...]
3rd look: [element] — why: [...]
Competitor: [element that could steal the 1st look]
Suppression: [how you pulled that element back]
Saturated colors: [0|1] — [which element]
First-screen elements: [n ≤ 6] — [list]
```

**Writing rules**
- A "why" line contains at least one number (px, columns, opacity, position percentage).
- "Extracted rules" must be measurements, not feelings. Right: "display 64/400/-0.04em". Wrong: "clean and modern".
- The "Competitor" line is never left empty. If there is no competitor, write "none — the first screen has [n] elements, all neutral".

**Filled-in example** (fictional product: "Tally — AI bookkeeping for small businesses")

```
EYE PATH — Tally home page
Template: A (A1) — references: Willow, Ramp
Extracted rules:
  - Willow: display 60/400/-0.02em/1.03; headline→body 24, body→CTA 24; square 48px CTA
  - Ramp: one font, one weight; single accent on the CTA only; live counter in the eyebrow
1st look: Left headline "Let Tally close the books." — why: 64px/400, columns 1–5, at 27% of the viewport, the darkest mass on the page
2nd look: Real reconciliation screen on the right — why: columns 7–12, 75% opacity, lower contrast than the headline
3rd look: "Start free" CTA — why: the only saturated color (#1F5C3A), 24px below the body, 48px tall
Competitor: top announcement bar
Suppression: bar removed; the announcement moved to the footer as 13px mono
Saturated colors: 1 — primary CTA
First-screen elements: 5 — eyebrow counter, headline, body, CTA, product screen
```

---

## 5. Competing elements and suppression

| Competitor | Why it steals the 1st look | Suppression |
|---|---|---|
| Announcement bar (very top) | Saturated color + the very top of the page | Remove it, or reduce it to a neutral tone on a single 12–13px line. On Sim and Mastra it is read before the headline. |
| "Backed by YC" / "New" pill | Above the headline, framed, first line | Move it next to the CTA or to the bottom strip as 12–13px mono (the Asimov, Stoa model). |
| Glow / radial gradient | The brightest region of the page | Remove it. Show the product on a flat background (Linear). |
| Logo wall | Many small, high-contrast elements | Move it off the first screen, or keep it to one row, ≤ 24px tall, with ≥ 64px of space above it and no label. |
| Second CTA | A second button of equal weight splits the eye | Demote it to a text link or an outlined button. |
| Motion (ticker, rotating word, counter) | Motion beats everything | Use it only if it carries proof (Stoa's price ticker) and is not in the same region as the headline. Rotating words are banned. |
| Cookie banner | A modal in the middle of the screen | A small, neutral card at the bottom left. Do not use a modal (on Granola it cuts the headline). |
| Decorative texture/pattern | Density attracts the eye | Limit it to the edges (Context.dev's dot patterns); keep it out of the content area. |

---

## 6. Validation tests

After the code is written, run the four tests and write the results in the AUDIT block.

### Test 1 — Blur
Blur a 1440×900 screenshot by about 8px. Temporarily, in the browser:
```js
document.documentElement.style.filter = 'blur(8px)'   // to undo: ''
```
**Pass:** There is a single dominant mass and that mass is the 1st-look element. The 2nd and 3rd elements are distinguishable.
**Fail:** There are two or more equal masses; or the brightest mass is a glow, an announcement bar or decoration.

### Test 2 — Saturated color count
Count the saturated colors on the first screen (excluding photo and product-screen content).
- Saturated: HSL saturation > 35% **and** RGB channel spread (max − min) ≥ 40.
- **Pass:** 0 or 1 (the primary CTA; in template B the object or a single word in the headline may share the same color).
- **Fail:** 2 or more different hues (Mastra: orange + green; Casey: green + pink).

### Test 3 — CTA distance
The vertical distance from the bottom edge of the 2nd-look element to the top edge of the CTA.
- **Pass:** ≤ 48px in templates A1, D and E. In A2, the CTA is in the right column at the headline's baseline. In B and C, inside the headline block.
- **Fail:** > 48px without justification. On Spaceflow this distance is 262px; the CTA is deliberately pushed below the hero. If you do this, write the justification.

### Test 4 — Element count
Count the separate elements on the first screen, excluding the nav. A logo strip counts as one element, a pair of buttons as two.
- **Pass:** ≤ 6. (Linear 3, Zomma 4, Willow 5.)
- **Fail:** ≥ 7. Cut the badge, announcement, second CTA and logo wall first.

---

## 7. Section-level eye path

The rules for each section after the first screen are below. These were not measured in the gallery; they are recommendations derived from the first-screen rules.

- Each section has a single 1st look: one headline + one proof (image, number or product screen) + at most one action.
- Instead of three equal cards, use an asymmetric split (8+4, 7+5), or write the information as a list if it is a list.
- Do not use sans-serif tracked-caps eyebrows above section headings. If needed, use mono, sentence case or a number ("01 — Reconciliation").
- Vertical space between sections is 96–128px (at 1440).

---

## 8. App screens

On dashboards and app screens, write `Template: app` instead of A–E.
- 1st look: the screen's primary data or task (e.g. today's balance, number of open tasks).
- 2nd look: the context that explains that data (trend, filters, recent activity).
- 3rd look: the primary action (a single filled button; the others in a secondary style).
- The tests are the same: a single mass when blurred, a single saturated color (excluding status colors: error, warning, success), and "number of primary actions = 1" instead of the element count.
