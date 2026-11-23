# Tipografi ve Renk

Font seçimi, font eşleştirme ve renk paleti kuralları. Ölçüler 23 Kasım 2026 taramasından (1440×900, DOM `getComputedStyle`). Boyut ve tracking tabloları `swiss-system.md` §1–2'dedir; burada **hangi font, hangi renk** sorusu cevaplanır.

## İçindekiler
1. En fazla 2 font kuralı
2. Üç font tarifi
3. Yasak fontlar ve izleme listesi
4. Önerilen alternatifler
5. Tipografi kuralları
6. Renk kuralları
7. Ölçülmüş paletler
8. Kontrol listesi

---

## 1. En fazla 2 font kuralı

**Kural:** First screen'de ve sayfa genelinde en fazla **2 yazı tipi ailesi** kullanılır.

**Sayım yöntemi**
- Aynı ailenin kesimleri ve optik boyutları 1 sayılır: ABC Oracle Regular + Medium = 1; Arcadia + Arcadia Display = 1.
- Bir süper ailenin farklı sınıftaki üyesi ayrı sayılır: Geist + Geist Mono = 2.
- İkon fontları sayılmaz.
- Computed style'da görünen sistem yedek fontları (`sans-serif`, `ui-sans-serif`, `system-ui`, `-apple-system`, SF Pro, Roboto, Arial) **sayılır** ve ayrıca "yedek font sızıntısı" bayrağıdır: o öğede font yüklenmemiş demektir. Galeride görülen örnekler: Chronicle ve Wato butonlarında `sans-serif`, Char butonunda SF Pro, Spaceflow butonunda Roboto.

**Neden:** Üçüncü font neredeyse her zaman bir karar eksikliğini kapatır. Galeride 4 font kullanan Casey ve Resend (sayfa geneli) ile 3 font kullanan Waybill'de first screen'in tonu dağılıyor. Güçlü örneklerin önemli bir kısmı tek aileyle yetiniyor (Ramp, Sim, Willow, Stripe, B&B, baked.design).

**Üçüncü font istisnası yok.** Galeride Panta tek bir kelime için Cormorant Garamond'u, witharc.co tek bir el yazısı notu için Caveat'ı ekliyor. Bunlar gözlem olarak kayıtlı ama agent aynı etkiyi 2 font içinde kurar: italik kesim, aksan rengi ya da ağırlık farkıyla.

**Font rolleri**
| Slot | Rol |
|---|---|
| Font 1 | Display + gövde (Tarif 1 ve 2) ya da yalnızca display (Tarif 3) |
| Font 2 | Mono sistem katmanı (Tarif 2), gövde (Tarif 3) ya da boş (Tarif 1) |

---

## 2. Üç font tarifi

### Tarif 1 — Tek grotesk (ağırlıksız hiyerarşi)
**Ne zaman:** Fintech, B2B altyapı, "sessiz güven" isteyen ürünler. Ürün ekranı hero'yu taşıyorsa.

**Ayarlar**
- Display 64–72 / **400** / -0.02…-0.04em / 1.0
- Body 16–18 / 400 / 1.5–1.6
- Hiyerarşi yalnızca boyut ve opaklıkla kurulur (`--fg-muted` %55–65).
- İkinci slot boş kalabilir ya da yalnızca kod için mono kullanılır.

**Referanslar:** Ramp (Lausanne 64/400, body 18), Sim (Season 64/400/-0.025em), Willow (ABC Oracle 60/400/-0.02em), bakkenbaeck.com (bbSans 50/500).

### Tarif 2 — Grotesk + mono
**Ne zaman:** Geliştirici aracı, API, altyapı, endüstri, donanım. Ürünün "makine" tarafını göstermek istediğinde.

**Ayarlar**
- Grotesk: display, lead, gövde.
- Mono yalnızca şunlar için: metaveri/eyebrow, ticker, kod, sayısal veri, (isteğe bağlı) nav ve buton etiketleri.
- Mono, first screen'de görünen metnin yaklaşık %15'ini geçmez (önerilen).
- Büyük harf yalnızca mono'da kullanılır; tracking 0…+0.04em, bir bölgede tek satır.

**Referanslar:** Linear (Inter Variable + Berkeley Mono), Arga Labs (Geist + IBM Plex Mono butonlarda), AgentMail (özel sans + JetBrains Mono nav ve kodda), Parallel (Gerstner Programm + FT System Mono butonlarda), Marengo (Inter + JetBrains Mono etiketlerde), Stoa (PP Neue Montreal + Geist Mono ticker'da).

### Tarif 3 — Serif display + grotesk gövde
**Ne zaman:** Sıcaklık, otorite ya da editoryal ton gerektiğinde. Not alma, finans danışmanlığı, consumer-pro ürünler. Kategorinin varsayılanını (sans) bilinçli kırmak istediğinde (Resend: geliştirici aracında serif).

**Ayarlar**
- Serif yalnızca ≥ 42px'te (display, h2). Gövde, nav ve buton grotesk.
- Serif tracking'i -0.01/-0.02em (sans'ın yarısı); leading 0.93–1.3, x-yüksekliğine göre test edilir.
- Serif ağırlığı 400 (ultra light 200 yalnızca ≥ 64px'te ve yüksek kontrastlı zeminde).
- **Endüstriyel varyant:** serif + mono (ProvenMetal: Rhetorik Serif + özel mono). Gövde mono olduğunda boyut 15–16px, leading ≥ 1.6.

**Referanslar:** Resend (Domaine 96/400 + gövde), Granola (Quadrant 86/400 + Melange), Char (Besley 63/500 + Geist), Balance (PP Editorial New 72/200 + Suisse Intl), Hyperspell (Exposure 64/400 + Geist), ProvenMetal (serif + mono).

### Tarif seçimi
| Marka karakteri | Tarif |
|---|---|
| Ciddi, finansal, kurumsal ama modern | 1 |
| Teknik, geliştirici, altyapı, sanayi | 2 |
| Sıcak, insani, editoryal, danışmanlık | 3 |
| Sanayi + ağırlık/otorite | 3 (serif + mono varyantı) |
| Belirsiz | 1 (en az risk) |

Seçtiğin tarifi ve **neden** seçtiğini SİSTEM bloğuna yaz. "Güzel duruyor" bir gerekçe değildir; "B2B fintech, ürün ekranı hero'yu taşıyor, tipografi geri çekilmeli" gerekçedir.

---

## 3. Yasak fontlar ve izleme listesi

### Yasak
| Font | Kapsam | Neden |
|---|---|---|
| **Inter** | Inter, Inter Display, InterVariable, Inter Tight | En yaygın AI ve şablon varsayılanı. Wato (Inter + Inter Display) ve Waybill bunun ayarsız halini gösteriyor. |
| **Poppins** | Tüm kesimler | Corvera: Poppins 600 + ortalanmış hero. Geometrik, yuvarlak; "startup şablonu" sinyali. |
| **Montserrat** | Tüm kesimler | Aynı kategori; yaygın şablon varsayılanı. |
| Sistem fontu marka fontu olarak | `system-ui`, `-apple-system`, `ui-sans-serif`, Arial, Helvetica (varsayılan), Roboto | Karar verilmemiş tipografi. Vela'da gövde `ui-sans-serif`. |
| Varsayılan serif display | Georgia, Times New Roman (başlıkta, özellikle 700) | Vela: Georgia 700 ortalanmış başlık. |
| Trial fontlar | Adında "Trial" geçen her font | Production'da lisans riski. Galeride görülenler: "Kalice Trial" (Chronicle), "Rhetorik Serif Trial" (ProvenMetal). |

**Linear, Panta, Kernel ve Marengo neden Inter kullanabiliyor?** Onları kurtaran font değil, ayar: Linear 510 ağırlık + -0.022em; Kernel 300 ağırlık + küçük harf + dev wordmark; Panta 120px + -0.035em + leading 0.96; Marengo 600 + -0.05em + halftone görsel. Agent bu ayarı güvenilir şekilde tutturamadığı için Inter yasak kalır. Kullanıcının kurumsal fontu Inter ise bu ayarları uygula ve DENETİM'de gerekçe yaz.

### İzleme listesi (gerekçe zorunlu)
| Font | Durum |
|---|---|
| **Geist** (+ Geist Mono) | Font ölçümü yapılan yaklaşık 50 sitenin 13'ünde var (Vercel, Axiom, Arga, Browser Use, HUD, Autumn, Traycer, Char, Hyperspell, Chronicle, Asimov, Stoa, Inkbox). "Yeni Inter" olma yolunda. |
| Outfit | Galeride Cua'da; Inter ile zayıf eşleşme. |
| Manrope | Galeride Asimov'da; Geist ile iki benzer sans. |
| DM Sans, Plus Jakarta Sans, Space Grotesk, Sora | Galeride ölçülmedi; yaygın şablon fontları olarak izlenir. |

İzleme listesindeki bir fontu seçersen SİSTEM bloğuna neden onu seçtiğini ve onu ayıracak ayarı (ağırlık, tracking, eşleşme) yaz.

---

## 4. Önerilen alternatifler

Lisansı production'dan önce mutlaka kontrol et. Ücretli fontlar ticari kullanım için lisans ister.

| Rol | Ücretli (dökümhane) | Ücretsiz (OFL) | Galeride |
|---|---|---|---|
| Grotesk | Söhne (Klim) · Lausanne (Weltkern) · Suisse Int'l (Swiss Typefaces) · PP Neue Montreal (Pangram Pangram) · ABC Oracle (Dinamo) · Gerstner Programm (Forgotten Shapes) | Archivo · Instrument Sans · Schibsted Grotesk · Hanken Grotesk · IBM Plex Sans | Stripe (Söhne), Ramp (Lausanne), Balance (Suisse), Stoa (Neue Montreal), Willow (Oracle), Parallel (Gerstner), Zomma (Archivo) |
| Serif display | Domaine Display (Klim) · PP Editorial New (Pangram Pangram) | Besley · Newsreader · Source Serif 4 · EB Garamond | Resend (Domaine), Balance (Editorial New), Char (Besley) |
| Mono | Berkeley Mono (U.S. Graphics) | JetBrains Mono · IBM Plex Mono · Commit Mono · Geist Mono (izleme) | Linear, Cursor, Interfere (Berkeley); Panta, Marengo, AgentMail (JetBrains); Arga, Zomma (Plex Mono); Mastra (Commit) |

**Ücretsiz örnek eşleşmeler**
- Tarif 1: Hanken Grotesk ya da Schibsted Grotesk (tek aile)
- Tarif 2: Archivo + IBM Plex Mono (Zomma'nın eşleşmesi) · Instrument Sans + JetBrains Mono
- Tarif 3: Newsreader + Hanken Grotesk · Besley + Schibsted Grotesk

**Rotasyon kuralı:** Listenin ilk satırını varsayılan yapma. Her projede marka karakterine göre seç ve gerekçesini yaz. Bütün agent çıktıları aynı ücretsiz fontu seçerse o font da bir sonraki "Inter" olur.

---

## 5. Tipografi kuralları

1. **Sentence case.** Title Case başlık yasak (Traceforce, Chronicle, Marengo'da görüldü).
2. **Büyük harf yalnızca mono metaveride:** tracking 0…+0.04em, bir bölgede tek satır. Sans-serif tracked caps eyebrow yasak.
3. **Başlık vurgusu tek kelime:** aksan renginde (CTA ya da B nesnesiyle aynı renk) ya da aynı ailenin italik kesiminde. Örnekler: Cua'da "supercomputer" (tuşlarla aynı mavi), Traycer'da "<Nerve Center/>", Casey'de "has your back", Panta'da italik "haul".
4. **Kelime dönüşü (rotating word) yasak.** Başlık ilk anda eksik görünür.
5. **Sayılar kesin:** "8,526,902 task runs" (HUD), "1.0025014%" (Ramp). Kaynağı olmayan "10K+" yazma. Değişen sayılarda `font-variant-numeric: tabular-nums`.
6. **Yasak efektler:** gradient metin, text-shadow glow, outline (stroke) metin.
7. **Alt çizgi ritim aracı olabilir** (witharc.co): `text-decoration-thickness: 1px; text-underline-offset: 0.2em`.
8. **Kopya kuralları (galeriden):** başlık 3–8 kelime ("Time is money. Save both."; "Find the coin. Land the trade."; "Build AI agents"). Somut fiil ("haul", "hand off"). En fazla 2 cümle.

---

## 6. Renk kuralları

### 6.1 Yapı
Her palet 4 ana token ve 2 yardımcı tokendan oluşur: `--bg`, `--fg`, `--fg-muted`, `--accent` + `--line`, `--accent-fg` (bkz. `swiss-system.md` §5).

### 6.2 Tek doygun renk = tek eylem
- **Doygun renk** = HSL doygunluğu > %35 **ve** RGB kanal farkı (maks − min) ≥ 40.
- First screen'de en fazla 1 doygun renk olur ve o renk birincil CTA'dadır.
- İstisnalar (aynı renk olmak şartıyla): B şablonundaki nesne; başlıkta tek bir kelime.
- Galeriden: Ramp lime, Parallel turuncu #FB631B, ProvenMetal kırmızı #FF0021, Browser Use turuncu #FE750E, Asimov camgöbeği #26BECF, Panta orman yeşili #0A3F2F.
- İki aksan rengi hiyerarşiyi böler (Mastra: turuncu şerit + yeşil kelime; Casey: yeşil + pembe ikincil buton).

### 6.3 Sıcak nötr zemin
- **Nötr** = RGB kanal farkı (maks − min) ≤ 12.
- **Sıcak** = R ≥ G ≥ B.
- Açık zemin örnekleri: #F9F7F2 (Panta), #F2F0E7 (Kernel), #F2EFE8 (witharc), #FBFAF7 (Zomma).
- Koyu zemin örnekleri: #161310 (Marengo), #14120B (Cursor), #0A0A0A.
- Saf #FFFFFF ve #000000 yalnızca tamamen monokrom bir sistemde kullanılır (Vercel, Resend, B&B).
- Soğuk nötr (B > R) yalnızca marka soğuksa: Arga #070C0E, Asimov #0D1117.

### 6.4 Metin
- Açık temada `--fg`: #111 ile #25221D arası (Willow #25221D, Sim #1A1A1A). Saf #000 kullanma.
- Koyu temada `--fg`: #EDEDED–#F7F8F8 (Vercel #EDEDED, Linear #F7F8F8) ya da krem #F1E9DC (Marengo).
- `--fg-muted`: `--fg` %55–65 opaklık (Ramp, Willow %60) ya da sabit gri (Linear #8A8F98).

### 6.5 Kontrast
- Gövde metni ≥ **4.5:1**; büyük metin (≥ 24px ya da ≥ 19px 600+) ≥ **3:1**.
- Ölçülen riskler:
  - tash: orta gri #8A8A8A zemin üzerinde beyaz = 3.45:1 → gövde için yetersiz.
  - Parallel: beyaz üzerinde #858483 = 3.73:1 → 26px'te geçer, gövdede kalır.
  - Turuncu #FB631B üzerinde beyaz metin = 3.04:1, siyah metin = 6.9:1 → turuncu/sarı/lime aksanlarda koyu metin kullan.
  - Kırmızı #FF0021 üzerinde beyaz = 3.98:1 → 13px buton etiketinde AA'yı geçmez.
- Fotoğraf üzerindeki metinde kontrastı metnin altındaki en açık bölgeye göre ölç.

### 6.6 Yasak renk kullanımları
| Kullanım | Ölçülebilir tanım |
|---|---|
| Mor/indigo | Gradient'te, glow'da ya da CTA dolgusunda ton 230–290°, HSL doygunluğu > %35 (Tailwind indigo-500 239°, violet-500 258°, purple-500 271° bu aralıkta) |
| Gradient CTA | Butonda `background-image: *-gradient` (Hyperspell, Unisson) |
| Glow | Ürünün ya da başlığın arkasında radial gradient / blur, tonu fark etmez (Traceforce mor, Waybill ve Axiom mavi) |
| Gradient metin | `background-clip: text` + gradient |
| Pastel mesh/blur zemin | Bulanık çok renkli zemin. İzleme: Zomma'da sınırda (düşük doygunluk, mor değil) |
| Çoklu aksan | First screen'de 2+ doygun ton |

### 6.7 Aksan nereden seçilir
1. Logo ya da marka rengi (Raycast kırmızısı logodan gelir).
2. Ürünün kendisi ya da B şablonu nesnesi (AgentMail turuncu zarf).
3. Sektörün fiziksel dünyası: sanayi = sinyal kırmızısı/turuncu (ProvenMetal), finans/sigorta = koyu yeşil (Panta, Casey), altyapı = renksiz/krem (Marengo).
4. Hiçbiri yoksa: renksiz sistem (CTA = `--fg`), Kernel ve Vercel gibi.

"AI mavisi-moru" (230–290°) bu listeden hiçbir yoldan çıkmaz.

### 6.8 Marka rengi mor ya da indigo ise
Kullan, ama yalnızca düz `--accent` olarak (CTA). Gradient, glow ve zemin yıkaması yasak. Zemin sıcak nötr kalır. DENETİM'de "mor/indigo — marka rengi" gerekçesini yaz. Stripe'ın mor gradient'i yıllardır sahiplenilmiş bir marka varlığıdır; referans olarak okunur, taklit edilmez.

---

## 7. Ölçülmüş paletler

| Palet | `--bg` | `--fg` | `--fg-muted` | `--accent` | Kaynak |
|---|---|---|---|---|---|
| Sıcak kağıt + orman yeşili | #F9F7F2 | #0A1A14 | #586261 | #0A3F2F | Panta |
| Krem + kömür (renksiz) | #F2F0E7 | #212225 | fg %60 | = fg | Kernel |
| Beyaz + lime | #FFFFFF | #0C0A08 | fg %60 | #EFF02A (koyu metinle) | Ramp |
| Beyaz + turuncu | #FFFFFF | #181818 | #858483 (≥ 24px) | #FB631B (koyu metinle) | Parallel |
| Sıcak siyah + krem | #161310 | #F1E9DC | #B9AEA0 | = fg (krem) | Marengo |
| Siyah monokrom | #000000 | #EDEDED | #A1A1A1 | beyaz | Vercel |
| Koyu + sinyal kırmızısı | #0A0A0A | #FFFFFF | fg %70 | #FF0021 (≥ 14px 500) | ProvenMetal |
| Mavi-siyah + çelik | #070C0E | #F1F7FA | fg %70 | #A4C1D5 | Arga Labs |
| Sıcak siyah, aksansız | #14120B | #EDECEC | fg %55 | = fg | Cursor |

Ramp'in renkleri Lab'dan hex'e çevrildi (yaklaşık değerler).

---

## 8. Kontrol listesi

- [ ] En fazla 2 aile; computed style'da yedek font yok.
- [ ] Yasak font yok; izleme listesindeyse gerekçe yazıldı.
- [ ] Tarif seçildi ve marka karakterine bağlı gerekçesi yazıldı.
- [ ] Serif yalnızca ≥ 42px; büyük harf yalnızca mono metaveride.
- [ ] Sentence case; kelime dönüşü ve gradient metin yok.
- [ ] Zemin nötr (kanal farkı ≤ 12); saf #FFF/#000 yalnızca monokrom sistemde.
- [ ] Tek doygun renk, yalnızca birincil CTA'da (+ izinli istisna).
- [ ] Mor/indigo, gradient CTA, glow yok.
- [ ] Gövde ≥ 4.5:1, büyük metin ≥ 3:1; aksan üzerindeki metin ölçüldü.
