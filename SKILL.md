---
name: agents-eye
description: Use when designing, coding (HTML/CSS/React/Tailwind), redesigning or critiquing a web interface, landing page, hero, marketing site, product/SaaS/startup page, portfolio or any UI screen. Requires an eye-path analysis (1st/2nd/3rd focus) before code; applies a Swiss grid, a φ-based type scale, 8px spacing, at most 2 fonts and measurable anti-AI bans (Inter/Poppins/Montserrat, purple-indigo gradients, three equal cards, tracked caps, centered generic hero, fake social proof); derives rules from 48 measured YC, studio and gold-standard references. Trigger when the user says "build a landing page", "design a hero", "make a site", "make it look less AI", "YC style", "like Linear/Vercel/Stripe", "redesign", "website", "make it look designed", or whenever a visual page is being produced, even if not explicitly asked.
license: MIT
---

# agents-eye

The problem with AI-generated interfaces is usually not ugliness but **the absence of decisions**: the default font, the default centered skeleton, the default purple, the same soft corner everywhere. This skill turns every default into a measurable decision. The order is always the same: first decide where the eye goes, then apply a measured system, and measure last.

Target tone: YC/SF. Clear, restrained, product-focused, with no "AI vibe" at all.

---

## Protocol

Follow the steps in order. Skipping a step makes the ones after it meaningless.

### 1. Pick an eye-path template (A–E)
Read `references/eye-path.md` and pick a template with the decision tree:

| Template | When | Summary |
|---|---|---|
| **A** Split hero | The product interface can be shown | Left headline → product screen → CTA |
| **B** Object/signature-first | The product is abstract but can be told with a single object, or the brand has a signature element | Object → headline → CTA |
| **C** Photo narrative | There is a brand-specific photo that tells a story | Photo → headline → CTA (the only template that allows centering) |
| **D** Type-first | The message is strong in one sentence and the product cannot be shown yet | Giant headline → emphasis/lead → CTA |
| **E** System/editorial | The personality is carried by text (studio, research) | One type size, hierarchy through order and opacity |

If unsure, pick **A**; it is the safest.

### 2. Write the pre-code block
Pick 2 references for the template, extract **3 measurable rules** from each and fill in the block. The format is locked (details: `references/eye-path.md` §4):

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

Do not write an adjective such as "eye-catching" on a "why" line; write numbers ("64px, the largest and darkest mass on the page, top left"). If you cannot write a number, the decision has not been made yet.

### 3. Apply the system rules
- `references/swiss-system.md`: φ type scale, 8px spacing, 1440 grid, color and radius tokens.
- `references/type-and-color.md`: at most 2 fonts, three font recipes, banned and recommended fonts, color rules.

Before coding, write a short SYSTEM block:

```
SYSTEM
Fonts: [font 1] (role) + [font 2] (role) — recipe: [1|2|3] — rationale: [brand character]
Display: [px]/[weight]/[tracking em]/[leading] · Body: [px]/[weight]/[leading]
Color: bg [hex] · fg [hex] · muted [hex/opacity] · accent [hex] (primary CTA only)
Radius: [0|2|4|6] (+ pill on primary CTA only: yes/no)
Grid: 12 columns, gutter 24, margin [px]; headline [n] columns
```

### 4. Code
Translate the blocks into code one to one. If you need to deviate from a block while coding, update the block first, then change the code.

### 5. Audit
- With a browser: run the audit script in `references/anti-ai.md` §5 at 1440×900.
- Without a browser: run the static audit (grep) in `references/anti-ai.md` §6.
- Then run the 4 validation tests in `references/eye-path.md` §6 (blur, color count, CTA distance, element count).

For every flag, write a one-line justification or fix it. **A flag is not an automatic rejection; it is a requirement to justify.** Linear also gets a "banned font" flag; the difference is that it has a justification.

---

## Hard rules

Each of these rules has a reason measured in the gallery behind it. Knowing why they matter helps you recognize a real exception.

1. **Do not write code without an eye-path analysis.** An interface without a pre-code block is the sum of its defaults. In every anti-example, the owner of the 1st look is unclear.
2. **Do not copy references; extract rules from them.** Do not take the layout, imagery, copy or color palette verbatim. What you extract must be a measurement (size, weight, tracking, spacing, number of colors). Ramp and Comp AI use the same font; the rules decide the outcome, not the font.
3. **At most 2 font families.** The mono member of a superfamily counts as a second font (Geist + Geist Mono = 2). Instead of a third accent font, use italics or color within the 2 fonts.
4. **Banned fonts: Inter (all variants), Poppins, Montserrat.** Linear, Panta and Kernel rescue Inter with 510/300 weights and -0.02/-0.05em tracking; it is banned because an agent cannot hit that fine-tuning reliably.
5. **One saturated color = one action.** Saturated color appears only on the primary CTA; as an exception it may be used on the object in template B or on a single word in the headline, in the same color as the CTA.
6. **No purple/indigo.** A hue of 230–290° with HSL saturation above 35% in a gradient, glow or CTA fill is a violation. If the user's brand color is purple, use it only as a flat CTA color and write a justification for the flag.
7. **Display headline at 400 weight by default (300–500) with negative tracking.** In most strong examples, headlines are 300–510 weight with -0.02/-0.05em tracking. In the anti-examples they are 600–700 with zero or positive tracking.
8. **Spacing in multiples of 8px.** Headline → lead 16–24px, lead → CTA 24–32px. Values such as 22, 25 or 28 are off-grid.
9. **No fake social proof.** Do not use star badges, anonymous testimonials or a gray logo wall labeled "Trusted by". Use a live/exact number or real product data instead.
10. **At most 6 elements on the first screen, excluding the nav.** Linear uses 3, Zomma 4.
11. **A centered headline only in template C or in a single display phrase above 96px.** The skeleton badge → centered headline → gray text → two CTAs → glow/logo wall appears in every centered anti-example in the gallery.
12. **Sentence case.** No Title Case headlines and no sans-serif tracked-caps labels. Capitals only in mono metadata, once per line.

---

## Which file to read when

| File | When |
|---|---|
| `references/eye-path.md` | Every task, in step 1. Template definitions, pre-code block, competing elements, validation tests. |
| `references/swiss-system.md` | In step 3. Measurements and tokens; a ready-made CSS starter file is in §7. |
| `references/type-and-color.md` | In step 3. Font choice and color palette. |
| `references/anti-ai.md` | In step 5, and for the self-check in §4 before writing code. |

---

## Output order

The response you show the user follows this order:

1. **EYE PATH** block
2. **SYSTEM** block
3. Code
4. **AUDIT** block (format: `references/anti-ai.md` §7):

```
AUDIT — [page]
Method: [script | static]
Flags: [list or "0 flags"]
Justifications:
  - [flag]: [why it is deliberate] — [basis: user request | brand | template permission | gallery rule]
Tests: blur [pass/fail] · saturated colors [n] · CTA distance [px] · elements [n]
Result: [delivered | fixed and re-audited]
```

If the audit shows a flag or a failed test and you cannot write a justification, fix the code and run the audit again.

---

## Special cases

**Critiquing or redesigning an existing page.** First write the page's *current* eye path in the pre-code block format (competitors included). Run the audit on the current page. Then pick the closest template and list the fixes in order of impact: owner of the 1st look → color → typography → spacing.

**The user has a brand system.** The user's corporate font, logo color or design system takes precedence over this skill's defaults. If there is a conflict (e.g. the corporate font is Montserrat), use it but record it in the AUDIT as a flag with a justification. Balance it with typographic tuning (weight 400–500, -0.02em tracking).

**App/dashboard screens.** Templates A–E are for the marketing first screen. On app screens, write `app` on the template line. The 1st look is the screen's primary data or task, the 2nd look is context, the 3rd look is the primary action. The pre-code block and the audit are still required.

**Sections (after the first screen).** Each section has a single 1st look. Instead of three equal cards, use an asymmetric split (8+4, 7+5) or a list. Details: `references/eye-path.md` §7.

**The user explicitly asks for something banned** (e.g. "use a purple gradient"). The user's request wins; do it. Show the flag in the AUDIT and state in one line why the ban exists.
