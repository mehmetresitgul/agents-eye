---
name: agents-eye
description: Web arayüzü, landing page, hero, marketing sitesi, ürün/SaaS/startup sayfası, portfolyo veya herhangi bir UI ekranı tasarlarken, kodlarken (HTML/CSS/React/Tailwind), yeniden tasarlarken ya da eleştirirken kullan. Koddan önce göz yolu (1-2-3 odak) analizini zorunlu kılar; Swiss ızgara, φ tabanlı tip skalası, 8px boşluk, en fazla 2 font ve ölçülebilir anti-AI yasakları (Inter/Poppins/Montserrat, mor-indigo gradient, 3 eşit kart, tracked caps, ortalanmış generic hero, sahte sosyal kanıt) uygular; 48 ölçülmüş YC, stüdyo ve altın standart referansından kural çıkarır. Kullanıcı "landing yap", "hero tasarla", "site yap", "daha az AI gibi dursun", "YC tarzı", "Linear/Vercel/Stripe gibi", "redesign", "landing page", "website", "make it look designed" dediğinde ya da görsel bir sayfa üretilecekse, açıkça istenmese bile tetikle.
license: MIT
---

# agents-eye

AI üretimi arayüzlerin sorunu çoğunlukla çirkinlik değil, **karar yokluğu**: varsayılan font, varsayılan ortalanmış iskelet, varsayılan mor, her yerde aynı yumuşak köşe. Bu skill her varsayılanı ölçülebilir bir karara çevirir. Sıra hep aynıdır: önce gözün nereye gideceğine karar ver, sonra ölçülmüş bir sistemle uygula, en son ölç.

Hedef ton: YC/SF. Net, geri çekilmiş, ürün odaklı; ama içinde hiç "AI vibe" yok.

---

## Protokol

Adımları sırayla uygula. Bir adımı atlamak, sonrakileri anlamsızlaştırır.

### 1. Göz yolu şablonunu seç (A–E)
`references/eye-path.md` dosyasını oku ve karar ağacıyla şablonu seç:

| Şablon | Ne zaman | Özet |
|---|---|---|
| **A** Bölünmüş hero | Ürün arayüzü gösterilebiliyor | Sol başlık → ürün ekranı → CTA |
| **B** Nesne/imza-önce | Ürün soyut ama tek nesneyle anlatılabiliyor ya da marka imza öğesi var | Nesne → başlık → CTA |
| **C** Fotoğraf-anlatı | Markaya özgü, hikaye anlatan bir fotoğraf var | Fotoğraf → başlık → CTA (ortalamaya izin veren tek şablon) |
| **D** Tipografi-önce | Mesaj tek cümlede güçlü, ürün henüz gösterilemiyor | Dev başlık → vurgu/lead → CTA |
| **E** Sistem/editoryal | Kişilik metinle taşınıyor (stüdyo, araştırma) | Tek punto, hiyerarşi sıra ve opaklıkla |

Emin değilsen **A** seç; en güvenlisi o.

### 2. Ön-kod bloğunu yaz
Şablonun 2 referansını seç, her birinden **3 ölçülebilir kural** çıkar ve bloğu doldur. Format kilitlidir (ayrıntı: `references/eye-path.md` §4):

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

"Neden" satırına "dikkat çekici" gibi bir sıfat yazma, sayı yaz ("64px, sayfadaki en büyük ve en koyu kütle, sol üst"). Sayı yazamıyorsan karar henüz verilmemiş demektir.

### 3. Sistem kurallarını uygula
- `references/swiss-system.md`: φ tip skalası, 8px boşluk, 1440 ızgarası, renk ve radius tokenları.
- `references/type-and-color.md`: en fazla 2 font, üç font tarifi, yasak ve önerilen fontlar, renk kuralları.

Kodlamadan önce kısa bir SİSTEM bloğu yaz:

```
SİSTEM
Fontlar: [font 1] (rol) + [font 2] (rol) — tarif: [1|2|3] — gerekçe: [marka karakteri]
Display: [px]/[ağırlık]/[tracking em]/[leading] · Body: [px]/[ağırlık]/[leading]
Renk: bg [hex] · fg [hex] · muted [hex/opaklık] · accent [hex] (yalnızca birincil CTA)
Radius: [0|2|4|6] (+ pill yalnızca birincil CTA: evet/hayır)
Izgara: 12 kolon, gutter 24, kenar [px]; başlık [n] kolon
```

### 4. Kodla
Blokları koda birebir çevir. Kodlarken bloktan sapman gerekirse, önce bloğu güncelle; sonra kodu değiştir.

### 5. Denetle
- Tarayıcı varsa: `references/anti-ai.md` §5'teki denetim scriptini 1440×900'de çalıştır.
- Tarayıcı yoksa: `references/anti-ai.md` §6'daki statik denetimi (grep) uygula.
- Ardından `references/eye-path.md` §6'daki 4 doğrulama testini yap (bulanıklık, renk sayısı, CTA mesafesi, öğe sayısı).

Her bayrak için tek satırlık gerekçe yaz ya da düzelt. **Bayrak otomatik ret değildir, gerekçe zorunluluğudur.** Linear da "yasaklı font" bayrağı alır; fark, gerekçesinin olması.

---

## Sert kurallar

Bu kuralların her birinin arkasında galeride ölçülmüş bir neden var. Neden önemli olduklarını bilmek, istisnayı doğru tanımana yardım eder.

1. **Göz yolu analizi yapmadan kod yazma.** Ön-kod bloğu olmayan bir arayüz, varsayılanların toplamıdır. Anti-örneklerin hepsinde 1. bakışın sahibi belirsiz.
2. **Referansları kopyalama; onlardan kural çıkar.** Düzeni, görseli, kopyayı ya da renk paletini birebir alma. Çıkardığın şey ölçü olmalı (boyut, ağırlık, tracking, aralık, renk sayısı). Ramp ve Comp AI aynı fontu kullanıyor; sonucu belirleyen font değil, kurallar.
3. **En fazla 2 font ailesi.** Bir süper ailenin mono üyesi ikinci font sayılır (Geist + Geist Mono = 2). Üçüncü bir vurgu fontu yerine 2 font içinde italik ya da renk kullan.
4. **Yasak fontlar: Inter (tüm varyantları), Poppins, Montserrat.** Linear, Panta ve Kernel Inter'i 510/300 ağırlık ve -0.02/-0.05em tracking ile kurtarıyor; agent bu ince ayarı güvenilir şekilde tutturamadığı için yasak.
5. **Tek doygun renk = tek eylem.** Doygun renk yalnızca birincil CTA'da; istisna olarak B şablonundaki nesnede ya da başlıkta tek bir kelimede, CTA ile aynı renkte kullanılabilir.
6. **Mor/indigo yok.** Gradient'te, glow'da ya da CTA dolgusunda ton 230–290°, HSL doygunluğu %35'in üstündeyse ihlal. Kullanıcının marka rengi morsa yalnızca düz CTA rengi olarak kullan ve bayrağa gerekçe yaz.
7. **Display başlık 400–500 ağırlıkta ve negatif tracking'le.** Güçlü örneklerin çoğunda başlıklar 300–510 ağırlıkta, tracking -0.02/-0.05em. Anti-örneklerde 600–700 ve tracking sıfır ya da pozitif.
8. **Boşluklar 8px katı.** Başlık → lead 16–24px, lead → CTA 24–32px. 22, 25, 28 gibi değerler ızgara dışıdır.
9. **Sahte sosyal kanıt yok.** Yıldız rozeti, isimsiz testimonial, "Trusted by" etiketli gri logo duvarı kullanma. Yerine canlı/kesin sayı ya da gerçek ürün verisi koy.
10. **First screen'de nav hariç en fazla 6 öğe.** Linear 3, Zomma 4 öğe kullanıyor.
11. **Ortalanmış başlık yalnızca C şablonunda ya da 96px üstü tek bir display ifadesinde.** Rozet → ortalanmış başlık → gri metin → iki CTA → glow/logo duvarı iskeleti, galerinin bütün ortalanmış anti-örneklerinde var.
12. **Sentence case.** Title Case başlık ve sans-serif tracked caps etiket yok. Büyük harf yalnızca mono metaveride, satır başına bir kez.

---

## Hangi dosyayı ne zaman oku

| Dosya | Ne zaman |
|---|---|
| `references/eye-path.md` | Her görevde, 1. adımda. Şablon tanımları, ön-kod bloğu, rakip öğeler, doğrulama testleri. |
| `references/swiss-system.md` | 3. adımda. Ölçüler ve tokenlar; hazır CSS başlangıç dosyası §7'de. |
| `references/type-and-color.md` | 3. adımda. Font seçimi ve renk paleti. |
| `references/anti-ai.md` | 5. adımda ve kod yazmadan önce §4'teki öz-kontrolde. |

---

## Çıktı sırası

Kullanıcıya gösterdiğin yanıt bu sırayla ilerler:

1. **EYE PATH** bloğu
2. **SİSTEM** bloğu
3. Kod
4. **DENETİM** bloğu:

```
DENETİM — [sayfa]
Script/statik: [bayrak listesi ya da "0 bayrak"]
Gerekçeler:
  - [bayrak]: [neden bilinçli] — [kural ya da referans]
Testler: bulanıklık [geçti/kaldı] · doygun renk [n] · CTA mesafesi [px] · öğe [n]
```

Denetim bir bayrak ya da başarısız test gösteriyorsa ve gerekçe yazamıyorsan, kodu düzelt ve denetimi tekrarla.

---

## Özel durumlar

**Mevcut bir sayfayı eleştirmek ya da redesign etmek.** Önce sayfanın *mevcut* göz yolunu ön-kod bloğu formatında yaz (rakipler dahil). Denetimi mevcut sayfaya uygula. Ardından en yakın şablonu seç ve düzeltmeleri etki sırasına göre listele: 1. bakışın sahibi → renk → tipografi → boşluk.

**Kullanıcının marka sistemi var.** Kullanıcının kurumsal fontu, logo rengi ya da tasarım sistemi bu skill'in varsayılanlarının önüne geçer. Çakışma varsa (ör. kurumsal font Montserrat), kullan ama DENETİM'de bayrak ve gerekçe olarak yaz. Bunu tipografi ayarıyla dengele (ağırlık 400–500, -0.02em tracking).

**Uygulama/dashboard ekranları.** A–E şablonları marketing first screen'i içindir. Uygulama ekranlarında şablon satırına `app` yaz. 1. bakış ekranın birincil verisi ya da görevi, 2. bakış bağlam, 3. bakış birincil eylem olur. Ön-kod bloğu ve denetim yine zorunlu.

**Bölümler (first screen sonrası).** Her bölümde tek bir 1. bakış olur. 3 eşit kart yerine asimetrik bölünme (8+4, 7+5) ya da liste kullan. Ayrıntı: `references/eye-path.md` §7.

**Kullanıcı açıkça bir yasağı istiyor** (ör. "mor gradient olsun"). Kullanıcının isteği geçerlidir; uygula. DENETİM'de bayrağı göster ve yasağın neden var olduğunu tek satırla belirt.
