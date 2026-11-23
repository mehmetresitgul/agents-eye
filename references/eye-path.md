# Göz Yolu (eye-path)

Koddan önce gözün hangi sırayla nereye gideceğine karar vermek için kullanılır. Bu dosyadaki ölçüler 23 Kasım 2026'da 1440×900'de, sayfaların DOM'undan okundu.

## İçindekiler
1. Tanımlar ve dikkat sürücüleri
2. Şablon seçimi (karar ağacı)
3. Şablonlar A–E
4. Ön-kod bloğu (kilitli format)
5. Rakip öğeler ve bastırma
6. Doğrulama testleri
7. Bölüm seviyesinde göz yolu
8. Uygulama ekranları

---

## 1. Tanımlar ve dikkat sürücüleri

- **1. bakış:** Kullanıcının ilk yarım saniyede kilitlendiği öğe. First screen'de yalnızca bir tane olur.
- **2. bakış:** 1. bakışı açıklayan ya da kanıtlayan öğe.
- **3. bakış:** Birincil eylem (CTA). CTA en geç 3. sırada okunmalı. Corvera'da testimonial CTA'nın önüne geçtiği için eylem 4. sıraya düşüyor; bu bir ihlal.

**Dikkati belirleyen sürücüler (güçlüden zayıfa):**

| # | Sürücü | Ölçü | Galeriden örnek |
|---|---|---|---|
| 1 | Boyut × kontrast | Alan büyük ve zeminle kontrastı en yüksek | Stoa 115px başlık, Panta 120px |
| 2 | Doygunluk | Nötr sayfadaki tek doygun öğe | AgentMail'in turuncu zarfı, Ramp'in lime CTA'sı |
| 3 | İzolasyon | Çevresindeki boş alan | Cursor: 26px başlık, etrafı boş olduğu için 1. bakış |
| 4 | Konum | Sol üst (F başlangıcı), Z yolunun uçları | Linear, Sim, Willow: sol üst başlık |
| 5 | Fotoğrafik nesne / yüz | Gerçek nesne, insan yüzü | tash'ın kartı, Granola'daki görüntülü görüşme küçük resimleri |
| 6 | Hareket | Ticker, animasyon, kelime dönüşü | Stoa ticker'ı (kontrollü), Corvera kelime animasyonu (kontrolsüz) |

Hareket (6) en zayıf sıradadır ama 1. bakışı en kolay çalan da odur. Animasyon varsa ön-kod bloğunda "Rakip" satırına yaz.

---

## 2. Şablon seçimi (karar ağacı)

Soruları sırayla sor; ilk "evet"te dur.

1. Ürünün gerçek arayüzü gösterilebiliyor ve bakınca anlaşılıyor mu? → **A**
2. Ürün soyut (API, altyapı, servis) ama tek bir nesneyle (zarf, kart, tuş, çizim) anlatılabiliyor mu ya da markanın sahiplenilmiş bir imza öğesi (wordmark, logo formu, geometrik modül) var mı? → **B**
3. Markaya özgü, bir fikir anlatan fotoğraf var mı (stok ya da AI render değil)? → **C**
4. Mesaj tek cümlede güçlü ve somut mu, ürün henüz gösterilemiyor mu? → **D**
5. Marka kişiliği metinle taşınıyor mu (stüdyo, ajans, araştırma, kişisel)? → **E**
6. Hiçbiri değilse → **A** (ürün yoksa ürünün çıktısını göster: rapor, mesaj, sonuç).

---

## 3. Şablonlar A–E

Izgara terimleri `swiss-system.md` §4'e göredir: 1440'ta 12 kolon, kolon ≈ 86px, gutter 24px, kenar 72px.

### A — Bölünmüş hero
**Göz yolu:** 1 başlık → 2 ürün ekranı → 3 birincil CTA

**Varyant A1 (yan yana):** Metin kolon 1–5/6, ürün kolon 6/7–12. φ bölünmesi: 12 ÷ φ ≈ 7.4 → 7 + 5.
**Varyant A2 (üst/alt):** Üst bantta başlık kolon 1–6, açıklama + CTA kolon 8–12'de başlığın taban çizgisine hizalı (split header). Alt bantta tam genişlikte ürün ekranı, başlığın 48–96px altında.

**Kurallar**
- Ürün ekranı gerçek içerikli olmalı, lorem ipsum olmamalı.
- Ürün ekranı başlıktan daha düşük kontrastlı olmalı (%60–80 opaklık, gri doku zemin ya da düşük kontrastlı çerçeve).
- Başlık ile ürün ekranı arasına başka öğe girmez (logo şeridi, rozet, ikinci başlık).
- A1'de CTA, gövdenin 24–32px altında. A2'de CTA sağ kolonda, başlık tabanı hizasında.

**Tipik hatalar:** Ürünün arkasına glow koymak; ürün ekranının başlıktan parlak olması; mock'un sahte veri taşıması.

**Referanslar**
- **Linear** (A2): display 64/510/-0.022em/1.0; ürün ekranı başlığın hemen altından başlıyor; first screen'de 3 öğe.
- **Sim** (A2): display 64/400/-0.025em; açıklama + CTA sağ kolonda başlık tabanı hizasında; ürün gri mermer dokuyla geri itilmiş.
- **Willow** (A1): display 60/400/-0.02em; başlık → gövde 24px, gövde → CTA 24px; kare CTA 48px.
- Ek: Interfere, Arga Labs, Spaceflow, Ramp.

### B — Nesne/imza-önce
**Göz yolu:** 1 nesne/imza öğe → 2 başlık → 3 CTA

**Düzen:** Nesne merkezde ya da sağda (kolon 6–12), first screen alanının %25–45'ini kaplar. Başlık sol üstte (kolon 1–5) ya da nesnenin üstünde solda durur.

**Kurallar**
- Nesne sayfadaki tek doygun ya da tek fotoğrafik öğedir.
- Nesne markanın adından, logosundan ya da ürün metaforundan türemeli: zarf = e-posta API'si, kart = kart yatırımı, tuş = bilgisayar, halftone = altyapı/baskı.
- Başlık 2. bakışta olduğu için sakin kalır: 400–500 ağırlık, nötr renk.
- Nesneyle başlık arasında tek bir renk bağı kurulabilir (başlıkta tek kelime, nesneyle aynı renkte).

**Tipik hatalar:** Soyut blob, küre, parıltılı 3D şekil; iki nesnenin yarışması; nesnenin dekoratif kalıp ürünü anlatmaması.

**Referanslar**
- **AgentMail:** turuncu zarf merkezde; başlık solda, slogan sağda (asimetrik üçlü); tek aksan turuncu.
- **tash:** derecelendirilmiş kart orta kolonda; görünür kolon çizgileri; renk yalnızca nesnede.
- **Kernel:** kırpılmış dev wordmark; başlık 64/300 ve küçük harf; köşesiz CTA.
- Ek: Marengo (halftone), Casey (geometrik modül), Vercel (logo), Raycast (logodan türeyen ışık).

### C — Fotoğraf-anlatı
Ortalamaya izin veren tek şablon budur.

**Göz yolu:** 1 fotoğrafın odak noktası → 2 başlık → 3 CTA

**Düzen:** Tam bleed fotoğraf. Metin fotoğrafın en sakin bölgesine yerleşir: ortalanmış üst (Mercury) ya da sol alt çeyrek (Balance). Metin bloğu en fazla 4 öğedir (başlık, lead, CTA, ikincil link).

**Kurallar**
- Fotoğraf markaya özgü bir fikir taşımalı: dağdaki masa = ofisten özgürlük; sütunlar = Stoa.
- Metnin altındaki fotoğraf bölgesi sakin olmalı. Gerekirse düz siyah overlay (%10–25) kullan, gradient değil.
- Ultra ince (200–300) font kullanıyorsan display ≥ 64px olmalı ve kontrast ≥ 3:1.

**Tipik hatalar:** Stok "ekip toplantısı" fotoğrafı ya da AI render; metnin fotoğrafın kalabalık bölgesine düşmesi; fotoğraf + glow.

**Referanslar**
- **Mercury:** masa odak noktası; başlık 49px/480 ortalanmış üstte; ara ağırlıklar 360/420/480.
- **Balance:** gökyüzü; başlık 72/200 serif, sol alt çeyrekte.
- **Stoa:** sütun fotoğrafı + 115px tek satır başlık (C ile D arasında).

### D — Tipografi-önce (poster)
**Göz yolu:** 1 dev başlık → 2 başlık içi vurgu ya da lead → 3 CTA

**Düzen:** Başlık 7–12 kolon genişliğinde, 2–4 satır, ≥ 86px ya da display/body oranı ≥ 4.3. First screen'de başlık dışında en fazla 3 öğe olur.

**Kurallar**
- Leading 0.94–1.0, tracking -0.03/-0.05em.
- Tek tipografik sürpriz serbest: bir kelime italik ya da aksan renginde. **Yeni font eklenmez.** Panta bunu üçüncü bir fontla yapıyor; agent aynı etkiyi 2 font içinde italik ya da renkle kurar.
- Kelime dönüşü (rotating word) yasak: başlık ilk anda eksik görünüyor (Stoa'da "The market behind", Corvera'da "intel→agent").

**Tipik hatalar:** 700 ağırlık; gradient metin; başlığın 5+ satıra kırılıp CTA'yı ekran dışına itmesi.

**Referanslar**
- **Panta:** 120/600/-0.035em/0.96; tek kelime italik ve adaçayı yeşili; mono eyebrow.
- **Zomma:** 78/300/-0.03em/1.04; first screen'de 4 öğe; başlık → lead 36px, lead → CTA 48px.
- **Resend:** 96px serif/400, oran 5.3; monokrom.
- Ek: Granola (86px serif, leading 0.93), Browser Use (84px + diyagram).

### E — Sistem/editoryal
**Göz yolu:** 1 ilk satır → 2 ritim öğesi (alt çizgi, liste) → 3 CTA

**Düzen:** Dar nav kolonu (kolon 1–2) + içerik kolonu (kolon 4–9), ya da kenara yaslı tam genişlikte tek cümle. Tek punto (28–50px), çok katman.

**Kurallar**
- Hiyerarşi boyutla değil; sıra, opaklık (%100 / %85 / %70), renk (koyu / gri) ve alt çizgiyle kurulur.
- Boyut farkı en fazla bir φ adımı (ör. 36/26).
- Yalnızca kişiliği metinle taşınan markalarda kullanılır. Ürün sitesinde değer önermesi kaybolur.

**Referanslar**
- **witharc.co:** her şey 32px; ilk satır %85 opaklık + 500 ağırlık, gerisi %70 + 400; altı çizili müşteri isimleri.
- **bakkenbaeck.com:** 50px/500 tek cümle, sol kenar 16px; tek font, tek ağırlık.
- **Parallel:** 36px koyu başlık + 26px gri lead; hiyerarşiyi renk kuruyor.

---

## 4. Ön-kod bloğu (kilitli format)

Format `integration-notes` taslağına iki satır ekler: "Çıkarılan kurallar" (galeri protokolü 3. adım) ve "First screen öğe sayısı" (test 4). Satır sırası ve etiketler değişmez.

```
EYE PATH — [sayfa/ekran adı]
Şablon: [A|B|C|D|E|app] (+varyant) — referans: [ref 1], [ref 2]
Çıkarılan kurallar:
  - [ref 1]: [kural 1]; [kural 2]; [kural 3]
  - [ref 2]: [kural 1]; [kural 2]; [kural 3]
1. bakış: [öğe] — neden: [boyut / kontrast / konum / renk, sayıyla]
2. bakış: [öğe] — neden: [...]
3. bakış: [öğe] — neden: [...]
Rakip: [1. bakışı çalabilecek öğe]
Bastırma: [o öğeyi nasıl geri çektin]
Doygun renk sayısı: [0|1] — [hangi öğe]
First screen öğe sayısı: [n ≤ 6] — [liste]
```

**Yazım kuralları**
- "Neden" satırı en az bir sayı içerir (px, kolon, opaklık, konum yüzdesi).
- "Çıkarılan kurallar" ölçü olmalı, his olmamalı. Doğru: "display 64/400/-0.04em". Yanlış: "temiz ve modern".
- "Rakip" satırı boş bırakılmaz. Rakip yoksa "yok — first screen'de [n] öğe var, hepsi nötr" yaz.

**Doldurulmuş örnek** (kurgusal ürün: "Tally — küçük işletmeler için AI muhasebe")

```
EYE PATH — Tally ana sayfa
Şablon: A (A1) — referans: Willow, Ramp
Çıkarılan kurallar:
  - Willow: display 60/400/-0.02em/1.03; başlık→gövde 24, gövde→CTA 24; kare CTA 48px
  - Ramp: tek font tek ağırlık; tek aksan yalnızca CTA'da; canlı sayaç eyebrow'da
1. bakış: Sol başlık "Kapanışı Tally yapsın." — neden: 64px/400, kolon 1–5, viewport'un %27'sinde, sayfanın en koyu kütlesi
2. bakış: Sağda gerçek mutabakat ekranı — neden: kolon 7–12, %75 opaklık, başlıktan düşük kontrast
3. bakış: "Ücretsiz başla" CTA — neden: tek doygun renk (#1F5C3A), gövdenin 24px altında, 48px yükseklik
Rakip: üst duyuru şeridi
Bastırma: şerit kaldırıldı; duyuru mono 13px olarak footer'a taşındı
Doygun renk sayısı: 1 — birincil CTA
First screen öğe sayısı: 5 — eyebrow sayaç, başlık, gövde, CTA, ürün ekranı
```

---

## 5. Rakip öğeler ve bastırma

| Rakip | Neden 1. bakışı çalar | Bastırma |
|---|---|---|
| Duyuru şeridi (en üst) | Doygun renk + sayfanın en üstü | Kaldır ya da nötr tona, 12–13px tek satıra indir. Sim ve Mastra'da başlıktan önce okunuyor. |
| "Backed by YC" / "New" hapı | Başlığın üstünde, çerçeveli, ilk satır | CTA'nın yanına ya da alt şeride 12–13px mono olarak taşı (Asimov, Stoa modeli). |
| Glow / radial gradient | Sayfanın en parlak bölgesi | Kaldır. Ürünü düz zeminde göster (Linear). |
| Logo duvarı | Çok sayıda küçük, yüksek kontrastlı öğe | First screen dışına taşı ya da tek satır, ≤ 24px yükseklik, üstünde ≥ 64px boşluk, etiketsiz bırak. |
| İkinci CTA | Eşit ağırlıklı ikinci buton gözü ikiye böler | Metin linkine ya da çerçeveli butona düşür. |
| Hareket (ticker, kelime dönüşü, sayaç) | Hareket her şeyi geçer | Yalnızca kanıt taşıyorsa (Stoa fiyat ticker'ı) ve başlıkla aynı bölgede değilse kullan. Kelime dönüşü yasak. |
| Çerez banner'ı | Ekranın ortasında modal | Sol altta, küçük, nötr kart. Modal kullanma (Granola'da başlığı kesiyor). |
| Dekoratif doku/desen | Yoğunluk göz çeker | Kenarlarla sınırla (Context.dev'in nokta desenleri), içerik bölgesine sokma. |

---

## 6. Doğrulama testleri

Kod yazıldıktan sonra dört testi uygula ve sonucu DENETİM bloğuna yaz.

### Test 1 — Bulanıklık
1440×900 ekran görüntüsünü yaklaşık 8px bulanıklaştır. Tarayıcıda geçici olarak:
```js
document.documentElement.style.filter = 'blur(8px)'   // geri almak için: ''
```
**Geçer:** Tek bir baskın kütle var ve o kütle 1. bakış öğesi. 2. ve 3. öğeler ayırt edilebiliyor.
**Kalır:** İki ya da daha fazla eşit kütle var; ya da en parlak kütle glow, duyuru şeridi veya dekor.

### Test 2 — Doygun renk sayısı
First screen'deki doygun renkleri say (fotoğraf ve ürün ekranı içerikleri hariç).
- Doygun: HSL doygunluğu > %35 **ve** RGB kanal farkı (maks − min) ≥ 40.
- **Geçer:** 0 ya da 1 (birincil CTA; B şablonunda nesne ya da başlıkta tek kelime aynı renkte olabilir).
- **Kalır:** 2 ya da daha fazla farklı ton (Mastra: turuncu + yeşil; Casey: yeşil + pembe).

### Test 3 — CTA mesafesi
2. bakış öğesinin alt kenarından CTA'nın üst kenarına olan dikey mesafe.
- **Geçer:** A1, D, E şablonlarında ≤ 48px. A2'de CTA sağ kolonda başlık tabanı hizasında. B ve C'de başlık bloğunun içinde.
- **Kalır:** > 48px ve gerekçesiz. Spaceflow'da bu mesafe 262px; CTA bilinçli olarak hero'nun altına itilmiş. Bunu yapacaksan gerekçeyi yaz.

### Test 4 — Öğe sayısı
Nav hariç first screen'deki ayrı öğeleri say. Logo şeridi tek öğe sayılır, buton çifti iki öğe.
- **Geçer:** ≤ 6. (Linear 3, Zomma 4, Willow 5.)
- **Kalır:** ≥ 7. Önce rozet, duyuru, ikinci CTA ve logo duvarını kes.

---

## 7. Bölüm seviyesinde göz yolu

First screen sonrasındaki her bölüm için kurallar aşağıda. Bunlar galeride ölçülmedi; first screen kurallarından türetilmiş önerilerdir.

- Her bölümde tek bir 1. bakış olur: bir başlık + bir kanıt (görsel, sayı ya da ürün ekranı) + en fazla bir eylem.
- 3 eşit kart yerine asimetrik bölünme kullan (8+4, 7+5) ya da bilgi bir listeyse liste olarak yaz.
- Bölüm başlıkları üstünde sans-serif tracked caps eyebrow kullanma. Gerekiyorsa mono, sentence case ya da numara kullan ("01 — Mutabakat").
- Bölümler arası dikey boşluk 96–128px (1440'ta).

---

## 8. Uygulama ekranları

Dashboard ve uygulama ekranlarında A–E yerine `Şablon: app` yaz.
- 1. bakış: ekranın birincil verisi ya da görevi (ör. bugünkü bakiye, açık iş sayısı).
- 2. bakış: o veriyi açıklayan bağlam (trend, filtre, son hareketler).
- 3. bakış: birincil eylem (tek, dolu buton; diğerleri ikincil stil).
- Testler aynı: bulanıklıkta tek kütle, tek doygun renk (durum renkleri hariç: hata, uyarı, başarı), öğe sayısı yerine "birincil eylem sayısı = 1".
