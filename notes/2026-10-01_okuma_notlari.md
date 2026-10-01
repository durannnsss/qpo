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
Tam metin okundu: arXiv:2306.04055v1 (preprint, 8 Haziran 2023; MNRAS'ta yayımlanan sürümden
küçük farklar olabilir). Ayrıca açık kod deposu incelendi (github.com/thissop/QPOML, son commit
2023-02-12; makalede kullanılan sürümle aynı olmayabilir).

- [makale §2.1] GRS 1915+105: RXTE/PCA; Zhang+2020'nin 625 zamanlama gözleminden 554'ünün eşleşen
  enerji spektrumu var. PDS: 128 s aralıklar, 1/128 s çözünürlük, Leahy normalize, Poisson çıkarılmış.
  Sadece QPO'lu gözlemler kullanılmış (yalnız regresyon, sadece temel QPO).
- [makale §2.2, §3.2] MAXI J1535−571: NICER. QPO tespiti: iki sıfır-merkezli Lorentzian + 1–20 Hz'de
  268 frekansta üçüncü Lorentzian taraması, AIC eşiği, **son kabul görsel inceleme ile**.
  68 gözlemde temel+harmonik, 14 gözlemde yalnız temel, 188 gözlemde QPO yok.
- [makale §3.2] Anlamlılık kriteri (GRS 1915+105): güç integrali / 1σ hata > 3 *veya* Q > 2.
- [makale §4.2] Girdiler: (a) mühendislik özellikleri: net sayım hızı, sertlik oranı, Γ, nthcomp
  normalizasyonu, iç disk sıcaklığı, diskbb normalizasyonu; (b) 0.5–10 keV'de 0.5 keV'lik 19 kanal
  (yalnız NICER; RXTE'de kazanç kayması nedeniyle ham spektrum kullanılmamış). Çıktı: frekansa göre
  sıralı (ν, FWHM, normalizasyon) vektörü, eksik QPO = 0, diğerleri min-max ile [0.1, 1].
- [makale §4.3, dipnot 3] %90/%10 ayrım + 5 kez tekrarlanan 10-katlı **rastgele** (MAXI J1535 için
  tabakalı) çapraz doğrulama. Min-max ölçekleme ayrımdan önce yapılmış; yazarlar bunu XSPEC
  parametre sınırlarının sabit olmasıyla gerekçelendiriyor.
- [makale §5] Regresyonda extra trees > random forest > decision tree > doğrusal. MAXI J1535 için
  var/yok sınıflandırması "oldukça kolay"; lojistik regresyon random forest kadar iyi.
  Ham spektrum girdisi, mühendislik özelliklerinden belirgin biçimde kötü.
- [makale §6] Yazarların önerileri: (i) Corral-Santana+2016 ölçeğinde standart bir QPO + spektral
  veri tabanı (RXTE arşivi bunun için değerli), (ii) NS LFQPO ve kHz QPO'ları içeren takip çalışması,
  (iii) çok kaynaklı analiz için **tek aletten, aynı şekilde yeniden işlenmiş** veri (§6.2: farklı
  aletler ve farklı QPO tanımlama yöntemleri karıştırılırsa bunu bir tür veri sızıntısı sayıyorlar),
  (iv) dışarıda tutulan patlamalarda (outburst) test. Bu, hocanın e-postasındaki yönle örtüşüyor.
- [makale §6] **Yenilik riski:** yazarlar NS takip çalışması planlıyor. Yayımlanıp yayımlanmadığını
  ADS'de kontrol etmeliyiz (bu konteynerden arXiv/ADS erişimi yok). [doğrulanmadı]
- [kod] `qpos_per_obs` hesabında `i != 0.1` koşulu dolgu değeri 0 iken gözlem başına QPO sayısını
  doğru saymıyor gibi görünüyor (tabakalama için). Makaledeki sürümde durum farklı olabilir. [doğrulanmadı]
- [bizim] Başlık notu: QPOML'de QPO, PDS fitiyle tespit ediliyor; ML modeli onu enerji spektrumundan
  *tahmin* ediyor. "ML ile tespit" ifadesi ölçülen şeyi abartıyor.

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

## 7. Başvuru formu için başlık önerileri (2026-10-01)
Formdaki tek alan: "Bitirme Çalışmasının Konusu" (uzunluk sınırı belirtilmemiş).
Başlık bir şemsiye; araştırma sorusu ayrıca ve dar tanımlanacak.

Olası çalışmalar: (1) 4U 1636−53 kHz QPO + QPOML; (2) yalnız işlenmiş katalog; (3) mHz QPO;
(4) pulsar QPO'ları (çoğu HMXB); (5) NS+BH kaynaklar arası genelleme (QPOML §6); (6) yöntem geliştirme.

| Başlık | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| A. X-ışını Çift Sistemlerinde Yarı-Periyodik Salınımların Arşiv Verileri ve Makine Öğrenmesi ile İncelenmesi (önerilen) | ✓ | ~ | ✓ | ✓ | ✓ | ✓ |
| B. X-ışını Çift Sistemlerinde Yarı-Periyodik Salınımların Veri Odaklı İncelenmesi | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| C. Nötron Yıldızlı X-ışını Çift Sistemlerinde ... (A'nın NS'ye daraltılmışı) | ✓ | ~ | ✓ | ✓ | ✗ | ✓ |
| QPOML tarzı: NS LMXB'lerde QPO'ların ML ile Tespiti ve Karakterizasyonu | ✓ | ✗ | ✓ | ✗ | ✗ | ~ |

~ = ML hiç kullanılmazsa başlık hafif abartılı kalır.
İngilizce: A. "Investigation of Quasi-Periodic Oscillations in X-ray Binaries Using Archival Data and
Machine Learning"; B. "A Data-Driven Investigation of Quasi-Periodic Oscillations in X-ray Binaries".
Hocaya teyit ettirilecek: terim tercihi (X-ışını/X-ışın çiftleri, yarı-periyodik salınım) ve başlığın
sonradan değiştirilip değiştirilemeyeceği (İTÜ kuralını bilmiyorum).
