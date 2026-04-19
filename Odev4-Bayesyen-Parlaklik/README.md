# YZM212 Makine Öğrenmesi 4. Laboratuvar Ödevi
## Uzak Bir Galaksinin Parlaklık Analizi

## 1. Problem Tanımı
Bu çalışmada, gürültülü gözlem verileri kullanılarak bir gök cisminin gerçek parlaklığı (μ) ve ölçüm belirsizliği (σ) Bayesyen çıkarım ile tahmin edilmiştir. Amaç, sentetik veri üzerinden MCMC yöntemi kullanarak posterior dağılımları elde etmek ve parametre tahminlerini yorumlamaktır.

## 2. Veri
Veri sentetik olarak üretilmiştir.
- true_mu = 150.0
- true_sigma = 10.0
- n_obs = 50

Veri üretiminden sonra elde edilen örnek ortalama 147.7453, örnek standart sapma ise 9.3367 bulunmuştur.

## 3. Yöntem
Bu projede aşağıdaki kütüphaneler kullanılmıştır:
- numpy
- matplotlib
- emcee
- corner

Bayesyen modelde:
- log-likelihood
- log-prior
- log-posterior

tanımlanmış, ardından `emcee.EnsembleSampler` ile MCMC örnekleme yapılmıştır. Sonuçlar trace plot ve corner plot ile görselleştirilmiştir.

## 4. Sonuçlar

| Değişken | Gerçek Değer (Girdi) | Tahmin Edilen (Median) | Alt Sınır (%16) | Üst Sınır (%84) | Mutlak Hata |
|---|---:|---:|---:|---:|---:|
| μ (Parlaklık) | 150.0 | 147.7863 | 146.4261 | 149.0720 | 2.2137 |
| σ (Hata Payı) | 10.0 | 9.4921 | 8.5543 | 10.5313 | 0.5079 |

## 5. Yorum / Tartışma
Bayesyen çıkarım yöntemi, gürültülü veri altında gerçek parametrelere yakın sonuçlar üretmiştir. Parlaklık için elde edilen tahmin gerçek değere yakın olup mutlak hata 2.2137’dir. Hata payı parametresi için tahmin edilen değer 9.4921’dir ve bu da gerçek değer olan 10.0’a oldukça yakındır.

Dar prior deneyi, prior seçiminin sonucu ciddi biçimde etkileyebileceğini göstermiştir. 100-110 aralığında dar prior seçildiğinde μ tahmini 109.4165’e kaymıştır.

Veri miktarı 50’den 5’e düşürüldüğünde posterior dağılım belirgin biçimde genişlemiş, yani belirsizlik artmıştır. Bu durum daha fazla verinin daha güvenilir tahminler ürettiğini göstermektedir.