# Anti-AI

AI üretimi arayüzlerde tekrar eden kalıpların ölçülebilir tanımları, tespit yöntemi ve düzeltmeleri. Kanıtlar 23 Kasım 2026 taramasından (yaklaşık 60 YC sitesi ve 20 stüdyo/altın standart, 1440×900).

## İçindekiler
0. Temel ilke: bayrak = gerekçe zorunluluğu
1. Çekirdek yasaklar (ölçülebilir)
2. Taramada gözlenen yeni kalıplar
3. İzleme listesi
4. Kod öncesi öz-kontrol
5. Denetim scripti (tarayıcı)
6. Statik denetim (tarayıcı yoksa)
7. DENETİM bloğu ve gerekçe formatı
8. Anti-çiftler

---

## 0. Temel ilke: bayrak = gerekçe zorunluluğu

Bir bayrak otomatik ret anlamına gelmez; **gerekçe yazma zorunluluğu** anlamına gelir. Linear "yasaklı font" bayrağı alır, Mercury "ortalanmış başlık" bayrağı alır. Fark, ikisinin de bilinçli bir kararla açıklanabilmesi.

Geçerli gerekçe şunlardan birine dayanır:
- Kullanıcının açık talebi ya da marka sistemi (kurumsal font, logo rengi).
- Şablon izni (ör. C şablonunda ortalanmış başlık).
- Galeriden somut bir kural ve onu taşıyan ayar ("Inter, ama 300 ağırlık + küçük harf + wordmark imza öğe; Kernel kuralı").

Geçersiz gerekçeler: "modern duruyor", "trend", "kullanıcı beğenir", "daha premium".

Gerekçe yazamıyorsan düzelt.

---

## 1. Çekirdek yasaklar (ölçülebilir)

### 1.1 Yasaklı fontlar: Inter / Poppins / Montserrat
- **Tanım:** Herhangi bir görünür metnin computed `font-family` ilk değeri `/^(inter|poppins|montserrat)/i` ile eşleşiyor (Inter Display, InterVariable, Inter Tight dahil).
- **Tespit:** Script → `yasaklı font`. Statik → §6 grep 1.
- **Neden:** En yaygın şablon ve AI varsayılanları. Corvera (Poppins 600, ortalanmış), Wato (Inter + Inter Display, ortalanmış) ve Waybill (Inter + 2 font daha) ayarsız hallerini gösteriyor.
- **Not:** Linear, Panta, Kernel ve Marengo Inter kullanıyor. Kurtaran ayar: 300/510 ağırlık, -0.02/-0.05em tracking, imza öğe. Agent bunu güvenilir şekilde tutturamadığı için yasak.
- **Düzeltme:** `type-and-color.md` §2'deki tariflerden birini seç; §4'teki alternatiflerden font al.

### 1.2 Mor/indigo gradient
- **Tanım:** First screen'de gradient'te, glow'da ya da buton/link dolgusunda ton 230–290°, HSL doygunluğu > %35.
- **Tespit:** Script → `mor/indigo × n` (yalnızca `rgb()/rgba()` okur). Statik → §6 grep 2–3.
- **Kanıt:** Autumn (mor-macenta panel + mor CTA), Vela (#737DE7 CTA + lavanta yıkama), Traceforce (indigo glow), Unisson (pembe-mor gradient). Sınırda: Mercury #5266EB (232°), Axiom #526FFF (≈230°).
- **Neden Stripe yapabiliyor:** Gradient'i yıllardır sahiplenilmiş bir marka varlığı. Agent bunu kopyalayamaz, okur.
- **Düzeltme:** Gradient'i kaldır, düz yüzey kullan. Aksanı `type-and-color.md` §6.7'ye göre seç. Marka rengi morsa yalnızca düz CTA rengi olarak kullan ve gerekçe yaz.

### 1.3 Üç eşit kart
- **Tanım:** Aynı genişlikte, aynı iç yapıda (ikon + başlık + metin ya da sayı + etiket) 3 kartın yan yana dizilmesi. Varyantları: 3 eşit stat kartı (Oximy), 3 demo kartı (xAI).
- **Tespit:** Statik → §6 grep 7 (`grid-cols-3`, `repeat(3, 1fr)`). Görsel kontrol.
- **İzinli:** İçerik türü ve boyutu farklıysa (ör. biri büyük ürün ekranı, ikisi küçük sayı).
- **Düzeltme:** Asimetrik bölünme (8+4, 7+5), numaralı liste, ya da tek büyük kanıt + yan liste.

### 1.4 Tracked all-caps etiket
- **Tanım:** `text-transform: uppercase` + `letter-spacing` > 0.05em, **sans-serif** fontta.
- **Tespit:** Script → `tracked caps (sans) × n`. Statik → §6 grep 4.
- **Kanıt:** Waybill (sayfa genelinde 60 öğe), Chronicle ("BACKED BY Y COMBINATOR" etiketi), Autumn ve Hyperspell (nav).
- **İzinli:** Mono fontta, tracking 0…+0.04em, bir bölgede tek satır metaveri (Panta eyebrow, Ramp sayacı, Stoa ticker'ı).
- **Düzeltme:** Sentence case yap ya da mono metaveriye çevir. Bölüm başlıklarının üstündeki eyebrow'u kaldır ya da numaraya çevir ("01 — Mutabakat").

### 1.5 Ortalanmış generic hero
- **Tanım:** Şu 5 öğeden ≥ 3'ü birlikte varsa: (1) başlığın üstünde rozet/hap, (2) ortalanmış başlık, (3) ortalanmış gri gövde, (4) eşit ağırlıkta 2 CTA, (5) logo duvarı ya da glow.
- **Tespit:** Script → `ortalanmış başlık` (+ diğer öğeleri görsel say). Statik → §6 grep 5.
- **Kanıt:** Traceforce (4/5), Corvera (4/5), Vela (4/5), Waybill (4/5), Comp AI (4/5), Wato (3/5).
- **İzinli:** C şablonu (anlatı fotoğrafı: Mercury, Balance) ya da tek bir ≥ 96px display ifadesi (Stoa).
- **Düzeltme:** Başlığı sola al (A ya da D şablonu), rozeti CTA yanına/alt şeride indir, ikinci CTA'yı metin linkine düşür, glow'u kaldır.

### 1.6 Her yerde yumuşak radius
- **Tanım:** 12px ve üstü radius'un 2'den fazla bileşen tipinde (kart, input, rozet, buton, görsel) birlikte kullanılması; ya da dekoratif blob şekiller.
- **Tespit:** Statik → §6 grep 6 (sayım). Görsel kontrol.
- **Kanıt:** Unisson (blob + yuvarlak buton + gradient daire), Traceforce (1600px haplar).
- **İzinli:** Pill yalnızca birincil CTA'da (Spaceflow, Granola, Char).
- **Düzeltme:** Tek sistem radius'u seç (0/2/4/6); bkz. `swiss-system.md` §6.

### 1.7 Sahte sosyal kanıt
- **Tanım:** First screen'de yıldız/puan rozeti; isimsiz ya da kaynaksız testimonial; kaynaksız yuvarlak sayılar ("10,000+ teams"); "Trusted by" etiketli gri logo duvarı.
- **Tespit:** Görsel/metin kontrol: "★", "4.9/5", "Trusted by", "Loved by", "+" ile biten yuvarlak sayılar.
- **Kanıt:** Comp AI (G2 4.9/5 rozeti hero'nun ilk öğesi), Corvera (logo duvarı + italik testimonial, CTA'dan büyük).
- **Düzeltme:** Canlı ya da kesin veri (Stripe GDP sayacı, Ramp ödeme yüzdesi, Stoa fiyat ticker'ı, HUD "8,526,902 task runs"), gerçek ürün ekranı, ya da etiketsiz siyah logo satırı (B&B).

---

## 2. Taramada gözlenen yeni kalıplar

| # | Kalıp | Ölçülebilir tanım | Kanıt | Düzeltme |
|---|---|---|---|---|
| 2.1 | Başlık üstünde "Backed by YC" rozeti | Hero'nun ilk öğesi bir yatırımcı rozeti | Taranan YC sitelerinin yaklaşık üçte birinde; iyi ve kötü sitelerde | CTA yanına ya da alt şeride, 12–13px mono (Asimov, Stoa) |
| 2.2 | Title Case başlık | Başlıkta 3+ kelime büyük harfle başlıyor | Traceforce, Chronicle, Marengo | Sentence case |
| 2.3 | Ürün arkasında glow | Ürün ekranı ya da başlığın arkasında radial gradient/blur, ton fark etmez | Traceforce (mor), Waybill ve Axiom (mavi) | Glow'u kaldır; ürünü düz zeminde başlığa yakın koy (Linear) |
| 2.4 | Gradient dolgulu CTA | Butonda `background-image` gradient | Hyperspell, Unisson | Düz `--accent` |
| 2.5 | Başlık öncesi gürültü yığını | Duyuru şeridi + "New" hapı + rozet: 2'si ya da 3'ü birlikte | Sim, Mastra | En fazla birini bırak |
| 2.6 | Ağır display + pozitif/sıfır tracking | Display ≥ 48px, ağırlık ≥ 600 ya da tracking ≥ 0 | Vela (Georgia 700), Waybill (700), Traceforce (500, normal) | 400–500 ağırlık, -0.02…-0.04em |
| 2.7 | Yedek font sızıntısı | Görünür bir öğede computed font `sans-serif`, `ui-sans-serif`, `system-ui`, SF Pro, Roboto, Arial | Chronicle ve Wato (buton), Char (buton), Spaceflow (buton) | Font'u butonlara da uygula; `font: inherit` |
| 2.8 | Trial font production'da | Font adında "Trial" geçiyor | Chronicle (Kalice Trial), ProvenMetal (Rhetorik Serif Trial) | Lisans al ya da alternatif seç |
| 2.9 | Kelime dönüşü | Başlıkta animasyonla değişen kelime | Corvera, Stoa | Tek, sabit başlık |
| 2.10 | Eşit ağırlıkta çift CTA | İki dolu buton yan yana | Traceforce, Casey (yeşil + pembe) | İkincisi çerçeveli ya da metin linki |

---

## 3. İzleme listesi

Yasak değil, ama seçilirse SİSTEM ya da DENETİM bloğunda gerekçe istenir.

- **Geist / Geist Mono:** Font ölçümü yapılan yaklaşık 50 sitenin 13'ünde var. "Yeni Inter" olma yolunda.
- **Outfit, Manrope, DM Sans, Plus Jakarta Sans, Space Grotesk, Sora:** Şablon varsayılanı riski (ilk ikisi galeride zayıf örneklerde görüldü).
- **Pastel blur zemin:** Mor olmasa da aynı ailenin üyesi (Zomma'da sınırda).
- **Duyuru şeridi:** Tek başına yasak değil, ama başlıktan önce okunuyorsa rakiptir (bkz. `eye-path.md` §5).
- **Mavi CTA'lar 220–230°:** Mor aralığının hemen dışında; indigo algısı verebilir (Axiom #526FFF).

---

## 4. Kod öncesi öz-kontrol

Kod yazmadan önce SİSTEM bloğunu bu listeye göre kontrol et:

- [ ] Fontlar yasak listesinde değil; izleme listesindeyse gerekçe hazır.
- [ ] En fazla 2 aile.
- [ ] Display ağırlığı 300–500, tracking negatif.
- [ ] Başlık sentence case, sabit (dönen kelime yok).
- [ ] Şablon C değilse başlık sola hizalı (ya da D'de ≥ 96px tek ifade).
- [ ] Rozet/duyuru/hap: en fazla bir tane ve başlığın üstünde değil.
- [ ] Tek doygun renk; 230–290° değil.
- [ ] Gradient yok (fotoğraf hariç); glow yok.
- [ ] 3 eşit kart yok; tek sistem radius'u.
- [ ] Kanıt: gerçek ürün ya da kesin sayı; yıldız rozeti ve "Trusted by" yok.

---

## 5. Denetim scripti (tarayıcı)

Kod sonrası, tarayıcı konsolunda 1440×900 viewport'ta çalıştır. Script, galerideki ölçümlerde kullanılan yöntemin sadeleştirilmiş halidir.

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
  const centered = hr && Math.abs(hr.left + hr.width / 2 - innerWidth / 2) < 40 && hr.width < innerWidth * 0.8;
  const trackedCapsSans = leaves.filter(e => { const s = getComputedStyle(e);
    return s.textTransform === 'uppercase' && parseFloat(s.letterSpacing) / parseFloat(s.fontSize) > 0.05 && !/mono/i.test(s.fontFamily); }).length;
  const gradients = [...document.querySelectorAll('body *')].filter(e =>
    vis(e) && e.getBoundingClientRect().top < innerHeight && /gradient/.test(getComputedStyle(e).backgroundImage)).length;
  const trackingEm = hs ? (parseFloat(hs.letterSpacing) || 0) / parseFloat(hs.fontSize) : 0;
  // mor/indigo: gradient'lerde ve buton/link dolgusunda ton 230–290°, doygunluk > %35 (yalnızca rgb/rgba okunur)
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
      trackingEm: +trackingEm.toFixed(3), leading: +(parseFloat(hs.lineHeight) / parseFloat(hs.fontSize)).toFixed(2),
      left: Math.round(hr.left), width: Math.round(hr.width), centered },
    flags: [
      fonts.length > 2 && `font sayısı ${fonts.length} (>2)`,
      fonts.some(f => /^(inter|poppins|montserrat)/i.test(f)) && 'yasaklı font',
      fonts.some(f => /trial/i.test(f)) && 'trial font',
      fonts.some(f => /^(sans-serif|ui-sans-serif|system-ui|-apple-system|roboto|arial)$/i.test(f)) && 'yedek font sızıntısı',
      purpleHits > 0 && `mor/indigo × ${purpleHits}`,
      hs && +hs.fontWeight >= 600 && 'display ağırlık ≥ 600',
      hs && parseFloat(hs.fontSize) >= 48 && trackingEm >= 0 && 'display tracking ≥ 0',
      centered && 'ortalanmış başlık (şablon C/D değilse ihlal)',
      trackedCapsSans > 0 && `tracked caps (sans) × ${trackedCapsSans}`,
      gradients > 2 && `first screen gradient × ${gradients}`
    ].filter(Boolean)
  };
})()
```

**Test sonucu (23 Kasım 2026):** Corvera 4 bayrak (yasaklı font, ağırlık ≥ 600, ortalanmış, gradient); Ramp 0 bayrak. Mor kontrolü Autumn'da 4, Vela'da 6 isabet verdi, Linear'da 0. Linear yine de "yasaklı font" bayrağı alır.

**Sınırlamalar**
- Mor kontrolü yalnızca `rgb()/rgba()` değerlerini okur. `oklch()`/`lab()` ile yazılmış renkler ve görsellerin içindeki mor yakalanmaz; bunları görsel kontrol et.
- 3 eşit kart, sahte sosyal kanıt, Title Case ve radius yayılması script dışıdır; §6 ve görsel kontrolle bak.
- "En büyük font" başlık olarak seçilir. Dev bir wordmark (Kernel) varsa başlık yerine onu ölçebilir. Sonucu ön-kod bloğundaki 1. bakışla karşılaştır.

---

## 6. Statik denetim (tarayıcı yoksa)

Kaynak kodda çalıştır (`src/` yerine proje klasörünü yaz). Bunlar sezgisel aramalardır; her eşleşmeyi gözle doğrula.

```bash
# 1 — yasaklı font
grep -rniE "font-family[^;]*(inter|poppins|montserrat)|['\"](inter|poppins|montserrat)['\"]|font-(inter|poppins|montserrat)\b" src/

# 2 — mor/indigo (Tailwind sınıfları ve yaygın hex'ler)
grep -rnE "(from|via|to|bg|text|ring|shadow|border)-(purple|violet|indigo)-[0-9]{2,3}|#(6366f1|4f46e5|8b5cf6|7c3aed|a855f7|9333ea)" src/

# 3 — gradient ve glow
grep -rnE "linear-gradient|radial-gradient|conic-gradient|bg-gradient-to-|bg-linear-to-|bg-radial|blur-(2xl|3xl)|drop-shadow-\[" src/

# 4 — tracked caps
grep -rnE "uppercase[^\"'>]*tracking-(wide|wider|widest)|tracking-(wide|wider|widest)[^\"'>]*uppercase|letter-spacing:\s*0?\.(0[6-9]|[1-9])" src/

# 5 — ortalanmış hero başlığı
grep -rnE "<h1[^>]*(text-center|mx-auto)|text-center[^\"'>]*text-(5xl|6xl|7xl|8xl)" src/

# 6 — radius yayılması (sayım; 3+ bileşen tipinde görüyorsan bayrak)
grep -rnoE "rounded-(xl|2xl|3xl|\[1[2-9]px\]|\[[2-9][0-9]px\])|border-radius:\s*(1[2-9]|[2-9][0-9])px" src/ | wc -l

# 7 — üç eşit kart
grep -rnE "grid-cols-3|repeat\(3,\s*(1fr|minmax)" src/

# 8 — ağır display
grep -rnE "<h1[^>]*font-(semibold|bold|extrabold|black)|h1[^{]*\{[^}]*font-weight:\s*(6|7|8|9)00" src/

# 9 — sahte sosyal kanıt
grep -rniE "trusted by|loved by|★|4\.[5-9]/5|[0-9]+k\+ (users|teams|companies)" src/

# 10 — yedek font ve trial font
grep -rniE "font-family:\s*(system-ui|-apple-system|sans-serif|arial|helvetica|roboto)\b|trial" src/
```

Statik denetimde ölçülemeyenler: göz yolu testleri (bulanıklık, CTA mesafesi). Bunları kodu okuyarak tahmin et ve DENETİM bloğunda "statik — tahmini" olarak işaretle.

---

## 7. DENETİM bloğu ve gerekçe formatı

```
DENETİM — [sayfa]
Yöntem: [script | statik]
Bayraklar: [liste ya da "0 bayrak"]
Gerekçeler:
  - [bayrak]: [neden bilinçli] — [dayanak: kullanıcı talebi | marka | şablon izni | galeri kuralı]
Testler: bulanıklık [geçti/kaldı] · doygun renk [n] · CTA mesafesi [px] · öğe [n]
Sonuç: [teslim | düzeltildi ve yeniden denetlendi]
```

**Örnek**
```
DENETİM — Tally ana sayfa
Yöntem: script
Bayraklar: ortalanmış başlık (şablon C/D değilse ihlal)
Gerekçeler:
  - ortalanmış başlık: Şablon C; başlık, kurucunun atölye fotoğrafının sakin üst bölgesinde — Mercury kuralı
Testler: bulanıklık geçti · doygun renk 1 · CTA mesafesi 24px · öğe 4
Sonuç: teslim
```

---

## 8. Anti-çiftler

Aynı koşulda farklı sonuç veren çiftler.

| İyi | Anti | Ders |
|---|---|---|
| Ramp | Comp AI | Aynı font (Lausanne). Fark: sol hizalı başlık + canlı sayaç + ürün ekranı vs. gradient panel + yıldız rozeti. |
| Linear | Traceforce | Koyu tema + ürün ekranı. Fark: ürün başlığa bitişik ve düz vs. alttan glow + Title Case. |
| Panta | Corvera | B2B, sektöre özel başlık. Fark: somut fiil + tek kelime vurgu vs. Poppins + kelime dönüşü. |
| Kernel | Wato | İkisi de Inter. Fark: wordmark + 300 ağırlık + küçük harf vs. ortalanmış şablon. |
| Browser Use | Waybill | Koyu, ortalanmış, kısa başlık. Fark: ürün diyagramı vs. glow + ürünsüz hero. |
| Granola / Char | Vela | Serif başlık. Fark: serif 400 + gerçek ürün vs. Georgia 700 + indigo. |
| Willow / Asimov | Autumn | Sol hizalı, köşeli. Fark: tek nötr CTA vs. 1. bakışı çalan mor gradient panel. |
