# Typography and color

Rules for font choice, font pairing and color palettes. Measurements come from the 23 November 2026 scan (1440×900, DOM `getComputedStyle`). The size and tracking tables are in `swiss-system.md` §1–2; this file answers **which font and which color**.

## Contents
1. The 2-font maximum
2. Three font recipes
3. Banned fonts and watch list
4. Recommended alternatives
5. Typography rules
6. Color rules
7. Measured palettes
8. Checklist

---

## 1. The 2-font maximum

**Rule:** At most **2 typeface families** on the first screen and across the page.

**How to count**
- Cuts and optical sizes of the same family count as 1: ABC Oracle Regular + Medium = 1; Arcadia + Arcadia Display = 1.
- A member of a superfamily from a different class counts separately: Geist + Geist Mono = 2.
- Icon fonts do not count.
- System fallback fonts that show up in the computed style (`sans-serif`, `ui-sans-serif`, `system-ui`, `-apple-system`, SF Pro, Roboto, Arial) **do count**, and are also a "fallback font leak" flag: the brand font was not applied to that element. Examples seen in the gallery: `sans-serif` on Chronicle's and Wato's buttons, SF Pro on Char's button, Roboto on Spaceflow's button.

**Why:** A third font almost always covers for a missing decision. In the gallery, Casey and Resend (page-wide) with 4 fonts and Waybill with 3 fonts all have a scattered first-screen tone. A large share of the strong examples settle for a single family (Ramp, Sim, Willow, Stripe, B&B, baked.design).

**There is no third-font exception.** In the gallery, Panta adds Cormorant Garamond for a single word, and witharc.co adds Caveat for a single handwritten note. These are recorded as observations, but the agent builds the same effect within 2 fonts: with an italic cut, the accent color or a weight difference.

**Font roles**
| Slot | Role |
|---|---|
| Font 1 | Display + body (recipes 1 and 2) or display only (recipe 3) |
| Font 2 | Mono system layer (recipe 2), body (recipe 3) or empty (recipe 1) |

---

## 2. Three font recipes

### Recipe 1 — Single grotesk (hierarchy without weight)
**When:** Fintech, B2B infrastructure, products that want "quiet confidence". When the product screen carries the hero.

**Settings**
- Display 64–72 / **400** / -0.02…-0.04em / 1.0
- Body 16–18 / 400 / 1.5–1.6
- Hierarchy is built only with size and opacity (`--fg-muted` 55–65%).
- The second slot can stay empty, or hold a mono used only for code.

**References:** Ramp (Lausanne 64/400, body 18), Sim (Season 64/400/-0.025em), Willow (ABC Oracle 60/400/-0.02em), bakkenbaeck.com (bbSans 50/500).

### Recipe 2 — Grotesk + mono
**When:** Developer tools, APIs, infrastructure, industry, hardware. When you want to show the "machine" side of the product.

**Settings**
- Grotesk: display, lead, body.
- Mono only for: metadata/eyebrows, tickers, code, numeric data, and (optionally) nav and button labels.
- Mono does not exceed about 15% of the visible text on the first screen (recommended).
- Uppercase is used only in mono; tracking 0…+0.04em, one line per region.

**References:** Linear (Inter Variable + Berkeley Mono), Arga Labs (Geist + IBM Plex Mono on buttons), AgentMail (custom sans + JetBrains Mono in nav and code), Parallel (Gerstner Programm + FT System Mono on buttons), Marengo (Inter + JetBrains Mono on labels), Stoa (PP Neue Montreal + Geist Mono in the ticker).

### Recipe 3 — Serif display + grotesk body
**When:** When warmth, authority or an editorial tone is needed. Note-taking, financial advisory, consumer-pro products. When you want to deliberately break the category default (sans) (Resend: a serif on a developer tool).

**Settings**
- Serif only at ≥ 42px (display, h2). Body, nav and buttons in the grotesk.
- Serif tracking -0.01/-0.02em (half of the sans value); leading 0.93–1.3, tested against the x-height.
- Serif weight 400 (ultra-light 200 only at ≥ 64px and on a high-contrast background).
- **Industrial variant:** serif + mono (ProvenMetal: Rhetorik Serif + a custom mono). When the body is mono, size 15–16px, leading ≥ 1.6.

**References:** Resend (Domaine 96/400 + body), Granola (Quadrant 86/400 + Melange), Char (Besley 63/500 + Geist), Balance (PP Editorial New 72/200 + Suisse Intl), Hyperspell (Exposure 64/400 + Geist), ProvenMetal (serif + mono).

### Choosing a recipe
| Brand character | Recipe |
|---|---|
| Serious, financial, corporate but modern | 1 |
| Technical, developer, infrastructure, industry | 2 |
| Warm, human, editorial, advisory | 3 |
| Industry + weight/authority | 3 (serif + mono variant) |
| Unclear | 1 (lowest risk) |

Write the recipe you chose and **why** you chose it in the SYSTEM block. "Looks nice" is not a rationale; "B2B fintech, the product screen carries the hero, typography should step back" is.

---

## 3. Banned fonts and watch list

### Banned
| Font | Scope | Why |
|---|---|---|
| **Inter** | Inter, Inter Display, InterVariable, Inter Tight | The most common AI and template default. Wato (Inter + Inter Display) and Waybill show it untuned. |
| **Poppins** | All cuts | Corvera: Poppins 600 + centered hero. Geometric, rounded; a "startup template" signal. |
| **Montserrat** | All cuts | Same category; a common template default. |
| System font as the brand font | `system-ui`, `-apple-system`, `ui-sans-serif`, Arial, Helvetica (default), Roboto | Typography that was never decided. On Vela the body is `ui-sans-serif`. |
| Default serif display | Georgia, Times New Roman (in headlines, especially at 700) | Vela: a centered Georgia 700 headline. |
| Trial fonts | Any font with "Trial" in its name | License risk in production. Seen in the gallery: "Kalice Trial" (Chronicle), "Rhetorik Serif Trial" (ProvenMetal). |

**Why can Linear, Panta, Kernel and Marengo use Inter?** The font is not what saves them; the tuning is: Linear 510 weight + -0.022em; Kernel 300 weight + lowercase + a giant wordmark; Panta 120px + -0.035em + leading 0.96; Marengo 600 + -0.05em + halftone imagery. Inter stays banned because an agent cannot hit this tuning reliably. If the user's corporate font is Inter, apply this tuning and write a justification in the AUDIT.

### Watch list (justification required)
| Font | Status |
|---|---|
| **Geist** (+ Geist Mono) | Present on 13 of the roughly 50 sites whose fonts were measured (Vercel, Axiom, Arga, Browser Use, HUD, Autumn, Traycer, Char, Hyperspell, Chronicle, Asimov, Stoa, Inkbox). On its way to becoming "the new Inter". |
| Outfit | On Cua in the gallery; a weak pairing with Inter. |
| Manrope | On Asimov in the gallery; two similar sans fonts alongside Geist. |
| DM Sans, Plus Jakarta Sans, Space Grotesk, Sora | Not measured in the gallery; watched as common template fonts. |

If you choose a font from the watch list, write in the SYSTEM block why you chose it and the tuning that will set it apart (weight, tracking, pairing).

---

## 4. Recommended alternatives

Always check the license before production. Paid fonts require a license for commercial use.

| Role | Paid (foundry) | Free (OFL) | In the gallery |
|---|---|---|---|
| Grotesk | Söhne (Klim) · Lausanne (Weltkern) · Suisse Int'l (Swiss Typefaces) · PP Neue Montreal (Pangram Pangram) · ABC Oracle (Dinamo) · Gerstner Programm (Forgotten Shapes) | Archivo · Instrument Sans · Schibsted Grotesk · Hanken Grotesk · IBM Plex Sans | Stripe (Söhne), Ramp (Lausanne), Balance (Suisse), Stoa (Neue Montreal), Willow (Oracle), Parallel (Gerstner), Zomma (Archivo) |
| Serif display | Domaine Display (Klim) · PP Editorial New (Pangram Pangram) | Besley · Newsreader · Source Serif 4 · EB Garamond | Resend (Domaine), Balance (Editorial New), Char (Besley) |
| Mono | Berkeley Mono (U.S. Graphics) | JetBrains Mono · IBM Plex Mono · Commit Mono · Geist Mono (watch list) | Linear, Cursor, Interfere (Berkeley); Panta, Marengo, AgentMail (JetBrains); Arga, Zomma (Plex Mono); Mastra (Commit) |

**Free example pairings**
- Recipe 1: Hanken Grotesk or Schibsted Grotesk (single family)
- Recipe 2: Archivo + IBM Plex Mono (Zomma's pairing) · Instrument Sans + JetBrains Mono
- Recipe 3: Newsreader + Hanken Grotesk · Besley + Schibsted Grotesk

**Rotation rule:** Do not make the first entry of the list your default. Choose for each project based on brand character and write the rationale. If every agent output picks the same free font, that font becomes the next "Inter".

---

## 5. Typography rules

1. **Sentence case.** Title Case headlines are banned (seen on Traceforce, Chronicle, Marengo).
2. **Uppercase only in mono metadata:** tracking 0…+0.04em, one line per region. Sans-serif tracked-caps eyebrows are banned.
3. **Headline emphasis on a single word:** in the accent color (the same color as the CTA or the B object) or in the italic cut of the same family. Examples: "supercomputer" on Cua (the same blue as the keys), "<Nerve Center/>" on Traycer, "has your back" on Casey, the italic "haul" on Panta.
4. **Rotating words are banned.** The headline looks incomplete at first.
5. **Exact numbers:** "8,526,902 task runs" (HUD), "1.0025014%" (Ramp). Do not write "10K+" without a source. Use `font-variant-numeric: tabular-nums` for changing numbers.
6. **Banned effects:** gradient text, text-shadow glow, outlined (stroked) text.
7. **Underlines can be a rhythm device** (witharc.co): `text-decoration-thickness: 1px; text-underline-offset: 0.2em`.
8. **Copy rules (from the gallery):** headline of 3–8 words ("Time is money. Save both."; "Find the coin. Land the trade."; "Build AI agents"). Concrete verbs ("haul", "hand off"). At most 2 sentences.

---

## 6. Color rules

### 6.1 Structure
Each palette consists of 4 main tokens and 2 helper tokens: `--bg`, `--fg`, `--fg-muted`, `--accent` + `--line`, `--accent-fg` (see `swiss-system.md` §5).

### 6.2 One saturated color = one action
- **Saturated color** = HSL saturation > 35% **and** RGB channel spread (max − min) ≥ 40.
- The first screen has at most 1 saturated color, and that color is on the primary CTA.
- Exceptions (provided it is the same color): the object in template B; a single word in the headline.
- From the gallery: Ramp lime, Parallel orange #FB631B, ProvenMetal red #FF0021, Browser Use orange #FE750E, Asimov cyan #26BECF, Panta forest green #0A3F2F.
- Two accent colors split the hierarchy (Mastra: orange bar + green word; Casey: green + pink secondary button).

### 6.3 Warm neutral background
- **Neutral** = RGB channel spread (max − min) ≤ 12.
- **Warm** = R ≥ G ≥ B.
- Light background examples: #F9F7F2 (Panta), #F2F0E7 (Kernel), #F2EFE8 (witharc), #FBFAF7 (Zomma).
- Dark background examples: #161310 (Marengo), #14120B (Cursor), #0A0A0A.
- Pure #FFFFFF and #000000 are used only in a fully monochrome system (Vercel, Resend, B&B).
- Cool neutrals (B > R) only if the brand is cool: Arga #070C0E, Asimov #0D1117.

### 6.4 Text
- `--fg` in light themes: between #111 and #25221D (Willow #25221D, Sim #1A1A1A). Do not use pure #000.
- `--fg` in dark themes: #EDEDED–#F7F8F8 (Vercel #EDEDED, Linear #F7F8F8) or cream #F1E9DC (Marengo).
- `--fg-muted`: `--fg` at 55–65% opacity (Ramp, Willow 60%) or a fixed gray (Linear #8A8F98).

### 6.5 Contrast
- Body text ≥ **4.5:1**; large text (≥ 24px, or ≥ 19px at 600+) ≥ **3:1**.
- Measured risks:
  - tash: white on a mid-gray #8A8A8A background = 3.45:1 → not enough for body text.
  - Parallel: #858483 on white = 3.73:1 → passes at 26px, fails for body text.
  - White text on orange #FB631B = 3.04:1, black text = 6.9:1 → use dark text on orange/yellow/lime accents.
  - White on red #FF0021 = 3.98:1 → fails AA on a 13px button label.
- For text on photos, measure contrast against the lightest region under the text.

### 6.6 Banned color uses
| Use | Measurable definition |
|---|---|
| Purple/indigo | Hue 230–290°, HSL saturation > 35% in a gradient, glow or CTA fill (Tailwind indigo-500 239°, violet-500 258°, purple-500 271° are in this range) |
| Gradient CTA | `background-image: *-gradient` on a button (Hyperspell, Unisson) |
| Glow | Radial gradient / blur behind the product or headline, in any hue (Traceforce purple, Waybill and Axiom blue) |
| Gradient text | `background-clip: text` + gradient |
| Pastel mesh/blur background | A blurred multicolor background. Watch: borderline on Zomma (low saturation, not purple) |
| Multiple accents | 2+ saturated hues on the first screen |

### 6.7 Where the accent comes from
1. The logo or brand color (Raycast's red comes from the logo).
2. The product itself or the template B object (AgentMail's orange envelope).
3. The physical world of the sector: industry = signal red/orange (ProvenMetal), finance/insurance = dark green (Panta, Casey), infrastructure = colorless/cream (Marengo).
4. If none apply: a colorless system (CTA = `--fg`), like Kernel and Vercel.

"AI blue-purple" (230–290°) comes out of none of these paths.

### 6.8 If the brand color is purple or indigo
Use it, but only as a flat `--accent` (CTA). Gradients, glows and background washes are banned. The background stays warm neutral. Write the justification "purple/indigo — brand color" in the AUDIT. Stripe's purple gradient is a brand asset owned for years; read it as a reference, do not imitate it.

---

## 7. Measured palettes

| Palette | `--bg` | `--fg` | `--fg-muted` | `--accent` | Source |
|---|---|---|---|---|---|
| Warm paper + forest green | #F9F7F2 | #0A1A14 | #586261 | #0A3F2F | Panta |
| Cream + charcoal (colorless) | #F2F0E7 | #212225 | fg 60% | = fg | Kernel |
| White + lime | #FFFFFF | #0C0A08 | fg 60% | #EFF02A (with dark text) | Ramp |
| White + orange | #FFFFFF | #181818 | #858483 (≥ 24px) | #FB631B (with dark text) | Parallel |
| Warm black + cream | #161310 | #F1E9DC | #B9AEA0 | = fg (cream) | Marengo |
| Black monochrome | #000000 | #EDEDED | #A1A1A1 | white | Vercel |
| Dark + signal red | #0A0A0A | #FFFFFF | fg 70% | #FF0021 (≥ 14px 500) | ProvenMetal |
| Blue-black + steel | #070C0E | #F1F7FA | fg 70% | #A4C1D5 | Arga Labs |
| Warm black, no accent | #14120B | #EDECEC | fg 55% | = fg | Cursor |

Ramp's colors were converted from Lab to hex (approximate values).

---

## 8. Checklist

- [ ] At most 2 families; no fallback font in the computed style.
- [ ] No banned font; if a watch-list font is used, the justification is written.
- [ ] A recipe is chosen and its rationale, tied to brand character, is written.
- [ ] Serif only at ≥ 42px; uppercase only in mono metadata.
- [ ] Sentence case; no rotating words and no gradient text.
- [ ] Neutral background (channel spread ≤ 12); pure #FFF/#000 only in a monochrome system.
- [ ] A single saturated color, only on the primary CTA (+ allowed exception).
- [ ] No purple/indigo, gradient CTA or glow.
- [ ] Body ≥ 4.5:1, large text ≥ 3:1; text on the accent is measured.
