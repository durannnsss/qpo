# Okuma notları ve başlangıç kapsamı — 2026-10-01

Kaynak: Sinem Şaşmaz'ın 2026-10-01 tarihli e-postası ve ekindeki üç makale.
Etiketler: **[makale]** = makalenin bildirdiği, **[kod]** = QPOML açık kodunda gördüğüm,
**[bizim]** = bizim hipotez/önerimiz, **[doğrulanmadı]** = kontrol edilmesi gereken.

## 0. E-postanın söylediği
1. İlk aşama: QPOML yöntemini nötron yıldızlı LMXB'lere uygulamak.
2. Sonra: yöntemi gerekli değişikliklerle "daha zor sistemlere" taşımak (hangi sistemler belirtilmedi).
3. Önce ciddi veri işleme gerekiyor: veri arşivde var ama işlenmemiş. İşlenmiş, açık bir
   katalog tek başına değerli olabilir.
4. Ekteki makaleler "bu sistemler için veri var" örnekleri; ayrı ayrı tez konusu olarak
   sunulmuş değiller.

## 1. QPOML — Kiker, Steiner, Garraffo, Méndez, Zhang (2023, MNRAS 524, 4801)
Tam metni okuyamadım: konteynerden arxiv.org ve academic.oup.com erişimi engelli. Aşağıdakiler
özet düzeyinde (arama sonuçları) ve açık kod deposundan (github.com/thissop/QPOML, son
commit 2023-02-12). **Kod deposu makalede kullanılan sürümle aynı olmayabilir.**

- [makale, özet] Kaynaklar: kara delikli LMXB'ler GRS 1915+105 (RXTE) ve MAXI J1535−571 (NICER).
- [makale, özet] Girdi: yeniden gruplanmış ham enerji spektrumu veya spektral fitten türetilmiş
  özellikler. Çıktı: QPO var/yok (sınıflandırma) ve QPO frekans/genişlik/genlik (regresyon).
  Ağaç tabanlı klasik ML modelleri.
- [makale, özet] Yazarlar NS LFQPO ve kHz QPO'ları da içeren bir takip çalışması yürüttüklerini
  belirtmiş. **Yenilik riski: yayımlanıp yayımlanmadığını ADS'de kontrol etmeliyiz.** [doğrulanmadı]
- [kod] `main.py::load`: min-max ölçekleme train/test ayrımından *önce*, tüm veri üzerinde.
  Ağaçlar için monoton dönüşüm zararsız; doğrusal/kNN modellerde hafif sızıntı.
- [kod] `main.py::evaluate`: `train_test_split` ile gözlem düzeyinde *rastgele* ayrım (varsayılan %10 test).
  Zamanca yakın gözlemler hem train hem test'e düşebilir → zamansal bağımlılık sorusu.
- [kod] Çok çıkışlı regresyon: QPO özellikleri frekansa göre sıralanıp düzleştiriliyor, eksik QPO 0 ile
  dolduruluyor (normalize değerler [0.1, 1] aralığında).
- [kod] `qpos_per_obs` hesabında `i != 0.1` koşulu dolgu değeri 0 iken gözlem başına QPO sayısını
  doğru saymıyor gibi görünüyor (tabakalama için). Makaledeki sürümde durum farklı olabilir. [doğrulanmadı]

## 2. Sanna, Méndez, Belloni, Altamirano (2012, MNRAS 424, 2936) — 4U 1636−53 kHz QPO
- [makale §2] 2010 Mayıs'a kadarki tüm RXTE/PCA gözlemleri: 1280 gözlem, ~3.5 Ms.
- [makale §2] Zamanlama: 125 μs event-mode, 4096 Hz örnekleme (Nyquist 2048 Hz), ~46 keV altı fotonlar,
  16 s'lik Leahy-normalize PDS'ler gözlem başına ortalanmış. Arka plan çıkarımı ve ölü-zaman
  (dead-time) düzeltmesi **yapılmamış**; Poisson seviyesi sabitle fit edilmiş. X-ışını patlamaları çıkarılmış.
- [makale §2] Tespit: 200–1500 Hz'de sabit + 1–2 Lorentzian fiti; anlamlılık = normalizasyon / negatif 1σ
  hata > 3 ve Q = ν/FWHM > 2.
- [makale §2.1] Sonuç: 528/1280 gözlemde kHz QPO; 357 alt, 197 üst kHz QPO; sadece 26 gözlemde ikisi birden.
- [makale §2.1, Şekil 1] **Tek QPO görülen gözlemlerde alt/üst kimliği sert renge (hard colour) göre
  atanmış.** Renkler Crab'a normalize, 3.5–6.0/2.0–3.5 keV (yumuşak) ve 9.7–16.0/6.0–9.7 keV (sert).
- [makale §2.2–3] Alt kHz QPO frekansı yüzlerce saniyede onlarca Hz kayabiliyor; gözlem-ortalamalı
  PDS'de QPO'yu yapay olarak genişletiyor.
- [bizim] Önemi: (a) bizim boru hattımız için hazır bir doğrulama hedefi: 528/1280'i ve frekansları
  yeniden üretebiliyor muyuz? (b) Etiket sızıntısı tuzağı: spektrumdan "alt mı üst mü" tahmini kısmen
  etiketleme kuralını (sert renk) geri öğrenir.

## 3. Lyu, Méndez, Zhang, Keek (2015, MNRAS 454, 541) — 4U 1636−53 mHz QPO
- [makale §1] mHz QPO'lar (~7–9 mHz) NS yüzeyinde marjinal kararlı nükleer yanmaya bağlanıyor;
  dar bir parlaklık aralığında görülüyor, tip I patlamadan hemen önce kayboluyor.
- [makale §2, Tablo 1] 4 XMM-Newton EPIC-pn (timing mode) gözlemi + eşzamanlı RXTE. Pile-up var;
  arka plan başka bir kaynağın (GX 339−4) gözleminden alınmış.
- [makale §2.1, Şekil 3–4] QPO frekansı gözlem içinde evriliyor; 1130 s'lik aralıklarda sinüs fiti;
  toplam 14 segment.
- [makale §3.2] QPO frekansı ile kara cisim sıcaklığı arasında anlamlı korelasyon bulunmamış
  (sabit ve kuvvet yasası fitleri, F-testi olasılığı 0.88).
- [bizim] Önemi: farklı fiziksel mekanizma (yüzey yanması vs iç disk dinamiği). QPO tek gözlem içinde
  açılıp kapanıyor → "bir gözlem = bir spektrum = bir QPO etiketi" birimi bozuluyor. Örneklem çok küçük.
  İlk ML adımı için uygun değil.

## 4. Manikantan, Paul, Sharma, Pradhan, Rana (2024, MNRAS 531, 530) — X-ışını pulsarları
- [makale §2.2] 29 pulsarın 99 XMM-Newton/NuSTAR gözlemi; QPO 5 kaynağın 11 gözleminde.
- [makale §2.2] **QPO'lar görsel inceleme ile tanımlanmış**; sonra güç-yasası/Lorentzian + Lorentzian fiti.
  Pulsar spin harmonikleri fitten önce çıkarılmış.
- [makale §3–4, Tablo 7] QPO rms genliği 4 kaynakta enerjiyle artıyor, V 0332+53'te enerji bağımlılığı yok.
- [bizim] Önemi: güçlü manyetik alanlı NS'ler (~10^12 G), manyetosferik modeller (BFM/KFM) — farklı fizik.
  Az pozitif örnek + görsel etiket = ML için zor; büyük olasılıkla e-postadaki "daha zor sistemler"
  aşamasına ait. [doğrulanmadı: hocaya sorulacak]

## 5. Önerilen ilk kapsam [bizim]
Bir kaynak, bir QPO ailesi, bir alet: **4U 1636−53, kHz QPO, RXTE/PCA.**
Gerekçe: büyük örneklem (1280 gözlem), yayımlanmış etiket kümesi (Sanna+2012) ile doğrulama imkânı,
tek alet (kalibrasyon kayması daha az). Hocayla teyit edilecek.

Tez katmanları:
- Asgari tez: tekrarlanabilir boru hattı → gözlem/segment başına PDS + enerji spektrumu/renkler →
  açık tespit kriteri → tespit edilemeyenler için rms üst limitleri içeren katalog → Sanna+2012 ile
  karşılaştırma → basit taban çizgisi (yalnız sert renk) vs QPOML tarzı model, zamana göre gruplanmış doğrulama.
- Yayın düzeyi: enjeksiyon–geri kazanım ile tamlık (completeness) fonksiyonu; 2–3 başka NS atoll kaynağına genişleme.
- Opsiyonel: mHz QPO'lar, pulsarlar, NICER verisi.

## 6. Hocaya sorulacaklar
1. İlk kaynak/alet tercihi: RXTE mi NICER mı? 4U 1636−53 uygun mu?
2. Grubun/işbirlikçilerin hazır indirgeme betikleri var mı (ör. Groningen grubunun RXTE boru hattı)?
3. QPOML yazarlarının NS takip çalışmasından haberdar mı? Çakışma riski.
4. "Daha zor sistemler" ile kastedilen ne (pulsarlar, mHz QPO, düşük sayımlı kaynaklar)?
5. Hesaplama kaynağı ve HEASoft kurulumu.
