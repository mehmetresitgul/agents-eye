# Swiss Sistem

Tip skalası, boşluk, ızgara, renk ve radius tokenları. **Ölçülen** değerler 23 Kasım 2026 taramasından (1440×900, DOM `getComputedStyle`) gelir. **Önerilen** olarak işaretlenenler galeride ölçülmedi, ölçülenlerden türetildi.

Temel ilke: Önce sistem gelir, istisnalar gerekçe ister. Bir değer bu dosyadaki tokenlardan biri değilse, DENETİM'de gerekçesini yaz.

## İçindekiler
1. Tip skalası (φ tabanlı)
2. Tracking, leading, ağırlık
3. Spacing (8px)
4. Izgara (1440 viewport)
5. Renk tokenları
6. Radius, çizgi, gölge
7. Hazır CSS başlangıç dosyası
8. Kontrol listesi

---

## 1. Tip skalası (φ tabanlı)

Taban 16px, çarpan φ = 1.618: **16 → 26 → 42 → 68 → 110**. Satır yükseklikleri 4px'in katına yuvarlanır.

| Token | px | Satır (px) | Rol | Ağırlık | Tracking |
|---|---|---|---|---|---|
| `--text-meta` | 12–13 | 16–20 | Mono metaveri, etiket, ticker | 400 | 0 |
| `--text-small` | 14 | 20 | Nav, buton, dipnot | 400–500 | 0 |
| `--text-body` | 16 | 24 | Gövde | 400 | 0 |
| `--text-body-l` | 18 | 28 | Hero gövdesi | 400 | 0 / -0.01em |
| `--text-lead` | 26 | 32 | Lead, ikinci katman başlık | 400 | -0.01em |
| `--text-h2` | 42 | 44–48 | Bölüm başlığı | 500 | -0.02em |
| `--text-display` | 68 (56–72) | 68 | Hero başlığı | 400 (300–500) | -0.02 / -0.04em |
| `--text-display-xl` | 110 (96–120) | 104 | Poster başlığı (D şablonu) | 400 | -0.035 / -0.05em |

`--text-body-l` (18px) φ adımı değil, ama galerideki hero gövdelerinin çoğu 18px (Willow, Ramp, Asimov, Resend). Pratik bir ara adım olarak tutuldu.

**Ölçülen hero başlıkları:** 64px kümesi baskın (Linear, Vercel, Spaceflow, Sim, Kernel, Casey, Hyperspell, Ramp, Raycast). φ adımı 68 bu kümenin üst sınırına oturuyor. Poster kümesi 86–120px (Granola 86, Resend 96, Stoa 115, Panta 120).

### Oran kuralı
display ÷ body oranı **3.3 ile 4.4 arasında** olmalı; hedef **φ³ ≈ 4.24**.

| Referans | Display / body | Oran |
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

- Poster şablonunda (D) oran 5–6.4'e çıkabilir: Panta 5.0, Resend 5.3, Stoa 6.4.
- 2.5'in altındaki oranlar ancak hiyerarşiyi renk ya da opaklık taşıyorsa geçerlidir (Parallel 36/26 = 1.38, gri lead; Hyperspell 64/30 = 2.1).

### Mobil (önerilen, 375px)
Her rol bir φ adımı küçülür: display 68 → 42 (satır 44), display-xl 110 → 68 (satır 64), h2 42 → 26 (satır 32), lead 26 → 20 (satır 28). Body 16px'te kalır.

---

## 2. Tracking, leading, ağırlık

### Tracking (boyuta göre)
| Boyut | Tracking | Ölçülen |
|---|---|---|
| ≥ 96px | -0.035 … -0.05em | Stoa -0.035 · Panta -0.035 |
| 56–95px | -0.02 … -0.04em | Linear -0.022 · Sim -0.025 · Zomma -0.03 · Spaceflow -0.04 · Arga -0.045 · Marengo -0.05 |
| 32–55px | -0.01 … -0.03em | Chronicle -0.02 · witharc -0.03 |
| 18–31px | 0 … -0.02em | Willow -0.01 · Kernel -0.013 |
| ≤ 16px | 0 … +0.02em | Sim +0.0175 |
| Mono | 0 | — |
| Büyük harf mono metaveri | 0 … +0.04em | Ramp sayacı, Panta eyebrow |

- Serif display'de tracking'i yarıya indir (-0.01 / -0.02em): Resend -0.01, Granola -0.02, ProvenMetal -0.02.
- Display boyutunda pozitif tracking gevşek görünür (Mastra +0.005em). Kullanma.
- -0.06em sınırdır (Vercel, Hyperspell). Ötesi harfleri yapıştırır.

### Leading
| Rol | Leading | Ölçülen |
|---|---|---|
| display-xl | 0.94–0.98 | Marengo 0.94 · Panta 0.96 · Stoa 0.98 |
| display (sans) | 1.0–1.05 | Linear, Vercel, Ramp, Spaceflow 1.0 · Zomma 1.04 |
| display (serif) | 0.93–1.3 | Granola 0.93 · Resend 1.0 · Cursor 1.25 · Char 1.3 (x-yüksekliğine göre test et; 0.92'nin altına inme) |
| h2 | 1.05–1.15 | — |
| lead | 1.25–1.45 | Parallel 1.23 · Kernel 1.25 · Zomma 1.45 |
| body | 1.5–1.6 | Willow 1.56 · Linear 1.6 · ProvenMetal 1.65 |
| meta | 1.33–1.5 | — |

### Ağırlık
- **Display varsayılanı 400.** Light ton için 300 (Zomma, Kernel), ultra light 200 yalnızca serif ve ≥ 64px'te (Balance). 500'ün üstü gerekçe ister.
- Ara ağırlıklar (450, 480, 510, 550) değişken fontlarda mikro hiyerarşi kurar: Linear 510, Mercury 360/420/480, xAI 450.
- Body 400, buton 500, mono 400.
- **Hiyerarşiyi ağırlıkla değil ölçekle kur.** Spaceflow, Stoa, Willow, Ramp ve Sim'de başlık ve gövde aynı ağırlıkta (400); fark yalnızca boyutta.

### Satır uzunluğu
- Gövde: 45–75 karakter (`max-width: 60–68ch`).
- Hero başlığı: 2–3 satır, 5–7 kolon (≈ 526–746px). Ölçülen: Interfere 450, Willow 543, Cua 547, ProvenMetal 560, Spaceflow 584, Char 608, Sim 621, Casey 720, Marengo 747.
- `text-wrap: balance` başlıkta, `text-wrap: pretty` gövdede.

---

## 3. Spacing (8px)

| Token | px | Kullanım |
|---|---|---|
| `--space-1` | 4 | İkon–etiket, inline mikro boşluk |
| `--space-2` | 8 | Buton içi ikon aralığı, sıkı liste |
| `--space-3` | 16 | Başlık → lead (sıkı), form alanı aralığı |
| `--space-4` | 24 | Başlık → lead (standart), lead → CTA, gutter |
| `--space-5` | 32 | Lead → CTA (ferah), kart iç boşluğu |
| `--space-6` | 48 | Hero metni → ürün ekranı (min), blok arası |
| `--space-7` | 64 | Logo şeridi üstü, ürün ekranı üstü |
| `--space-8` | 96 | Bölümler arası (1440) |
| `--space-9` | 128 | Büyük bölüm arası, poster hero üst boşluğu |

**Hero iç ritmi (ölçülen):**
| Referans | Başlık → lead | Lead → CTA |
|---|---|---|
| Willow | 24 | 24 |
| Chronicle Labs | 24 | 32 |
| Asimov | 24 | 32 |
| tash | 16 | 24 |
| Wato | 16 | 32 |
| Parallel | 16 | 16 |
| Zomma | 36 | 48 |

- Kural: başlık → lead **16–24**, lead → CTA **24–32**. Zomma'nın 36/48'i poster tonunda bilinçli artan ritim (36 = 4px ızgarasında; 8px ızgarası için 32/48 kullan).
- Izgara dışı ölçülenler (kaçın): Cua 22, Autumn 25, Arga 28.
- Buton yüksekliği: **40 / 44 / 48**. Yatay iç boşluk 16–24.
- Kart iç boşluğu: 24 ya da 32.

---

## 4. Izgara (1440 viewport)

| Değer | 1440 |
|---|---|
| Kolon | 12 |
| Gutter | 24px |
| Dış kenar | `clamp(24px, 5vw, 96px)` → 72px |
| İçerik genişliği | 1296px |
| Kolon genişliği | 86px |
| Kolon n başlangıcı | 72 + (n − 1) × 110 px |
| n kolon genişliği | 110n − 24 px (5 → 526, 6 → 636, 7 → 746) |

**Ölçülen sol kenarlar:** 16 (B&B) · 24 (Vercel) · 32 (Asimov) · ≈48 (Linear) · 63–64 (Cursor, Ramp, Kernel) · 72–77 (ProvenMetal, Parallel, Willow, Arga, Cua) · 88–133 (Panta, Interfere, Granola, Zomma). 64–96 aralığı çoğunluk. 16–32 yalnızca E şablonunda ya da çok sade sayfalarda.

### Şablona göre yerleşim
| Şablon | Yerleşim |
|---|---|
| A1 | Metin kolon 1–5, ürün 6–12 (φ bölünmesi 7+5) ya da 1–6 / 7–12 |
| A2 | Başlık 1–6; açıklama + CTA 8–12, başlık tabanına hizalı; altta ürün 1–12 |
| B | Başlık 1–5; nesne 6–12 ya da merkezde, first screen alanının %25–45'i |
| C | Tam bleed fotoğraf; metin 1–5 (sol alt) ya da 3–10 (ortalanmış üst) |
| D | Başlık 1–9 … 1–12, 2–4 satır |
| E | Nav 1–2, içerik 4–9 |

### Dikey yerleşim
- Hero başlığının üst kenarı viewport yüksekliğinin **%20–32'sinde**. Ölçülen medyan %27: Spaceflow 228px, Linear 242, Panta 242, Sim 245, Asimov 245, Marengo 248, Kernel 274, Zomma 289, Willow 291 (900px'te). Arga 153px (%17) aralığın üstünde kalıyor.
- Alt yaslı varyant (B/C): metin bloğu alt üçte birde (Chronicle 636px, Balance 520px). Bu durumda 1. bakış görsele aittir; ön-kod bloğunda böyle yaz.

### Breakpoint'ler (önerilen)
| Viewport | Kolon | Gutter | Kenar |
|---|---|---|---|
| ≥ 1440 | 12 | 24 | 72–96 |
| 1024 | 12 | 20 | 40 |
| 768 | 8 | 16 | 32 |
| 375 | 4 | 16 | 20 |

A1 ve B 768'in altında dikey yığına döner: önce 1. bakış öğesi. B'de mobilde nesne başlığın altına iner ve göz yolu 1 başlık → 2 nesne → 3 CTA olur. Bunu ön-kod bloğuna not et.

---

## 5. Renk tokenları

Yapı sabittir; değerler `type-and-color.md` §6'daki kurallardan ve paletlerden seçilir.

| Token | Rol | Kural |
|---|---|---|
| `--bg` | Zemin | Sıcak nötr: RGB kanal farkı ≤ 12, R ≥ G ≥ B |
| `--fg` | Ana metin | Açık temada #111–#25221D; koyu temada #EDEDED–#F7F8F8 ya da krem |
| `--fg-muted` | İkincil metin | `--fg` %55–65 opaklık ya da sabit gri; kontrast ≥ 4.5:1 |
| `--line` | Ayırıcı çizgi | `--fg` %8–12 opaklık, 1px |
| `--accent` | Birincil CTA | Tek doygun renk; başka hiçbir yerde kullanılmaz (istisna: B nesnesi, başlıkta tek kelime) |
| `--accent-fg` | CTA metni | `--accent` üzerinde ≥ 4.5:1 |

---

## 6. Radius, çizgi, gölge

| Token | Değer | Ölçülen |
|---|---|---|
| `--radius-0` | 0 | Kernel, ProvenMetal, Willow, Asimov |
| `--radius-1` | 2px | Marengo (2.7) |
| `--radius-2` | 4px | Stripe, Parallel, tash, Chronicle |
| `--radius-3` | 6px | Vercel, Ramp, AgentMail |
| `--radius-pill` | 999px | Yalnızca birincil CTA (Spaceflow, Granola, Char, Zomma) |

- Tüm bileşenler (kart, input, rozet, ikincil buton) için **tek bir sistem radius'u** seç: 0, 2, 4 ya da 6.
- Pill yalnızca birincil CTA'da kullanılabilir (opsiyonel).
- 12px ve üstü radius'u ikiden fazla bileşen tipinde birlikte kullanma ("soft everything").
- Çizgi: 1px, `--line`. Kart ayırmak için gölge yerine çizgi.
- Gölge: yok ya da tek, sabit, düşük opaklıkta (`0 1px 2px rgb(0 0 0 / 0.06)`). Glow, renkli gölge ve glassmorphism yok.

---

## 7. Hazır CSS başlangıç dosyası

Fontları `type-and-color.md` §2–4'ten seç ve gerekçesini SİSTEM bloğuna yaz. Aşağıdaki değerler A şablonu ve açık sıcak tema içindir.

```css
:root {
  /* Fontlar — type-and-color.md'den seç (en fazla 2 aile) */
  --font-1: "FONT_1", ui-sans-serif, sans-serif;   /* display + gövde */
  --font-2: "FONT_2", ui-monospace, monospace;     /* mono sistem katmanı ya da gövde */

  /* Tip skalası (φ) */
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

  /* Izgara */
  --columns: 12;
  --gutter: 24px;
  --margin: clamp(24px, 5vw, 96px);
  --container: 1440px;

  /* Renk — type-and-color.md §6 paletlerinden */
  --bg: #F9F7F2;
  --fg: #141410;
  --fg-muted: rgb(20 20 16 / 0.6);
  --line: rgb(20 20 16 / 0.1);
  --accent: #1F5C3A;      /* yalnızca birincil CTA */
  --accent-fg: #FFFFFF;

  /* Radius */
  --radius: 4px;          /* tek sistem radius'u: 0 | 2 | 4 | 6 */
  --radius-pill: 999px;   /* yalnızca birincil CTA */
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

/* A1 hero örneği */
.hero { padding-block: clamp(var(--space-8), 22vh, 240px) var(--space-8); }
.hero__text { grid-column: 1 / span 5; }
.hero__product { grid-column: 7 / span 6; opacity: 0.85; }
.hero__cta { margin-top: var(--space-5); display: flex; gap: var(--space-3); }

@media (max-width: 767px) {
  :root { --text-display: 42px; --lh-display: 44px; --text-display-xl: 68px; --lh-display-xl: 64px; --text-lead: 20px; --lh-lead: 28px; --gutter: 16px; }
  .hero__text, .hero__product { grid-column: 1 / -1; }
}
```

---

## 8. Kontrol listesi

- [ ] Tüm font boyutları skala tokenlarından biri (ya da gerekçeli).
- [ ] Display/body oranı 3.3–4.4 (D şablonunda ≤ 6.4).
- [ ] Display ağırlığı 300–500; tracking boyut tablosuna uygun ve negatif.
- [ ] Hero'daki bütün dikey boşluklar 8px katı; başlık → lead 16–24, lead → CTA 24–32.
- [ ] Başlık 5–7 kolon, 2–3 satır; üst kenarı viewport'un %20–32'sinde.
- [ ] Tek sistem radius'u; pill yalnızca birincil CTA'da.
- [ ] Renkler token yapısında: bg, fg, muted, line, accent. Accent yalnızca birincil CTA'da.
