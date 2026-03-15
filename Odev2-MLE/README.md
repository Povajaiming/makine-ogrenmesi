# MLE ile Akıllı Şehir Planlaması

## Problem Tanımı
Bu çalışmada, bir dakikada geçen araç sayılarının Poisson dağılımına uyduğu varsayılmıştır.
Amaç, Maximum Likelihood Estimation (MLE) yöntemi ile Poisson parametresi olan $\lambda$ değerini tahmin etmektir.

## Veri
Kullanılan trafik verisi:
`[12, 15, 10, 8, 14, 11, 13, 16, 9, 12, 11, 14, 10, 15]`

## Yöntem
Öncelikle Poisson dağılımı için likelihood ve log-likelihood fonksiyonları teorik olarak türetilmiştir.
Ardından negatif log-likelihood fonksiyonu tanımlanarak `scipy.optimize` ile sayısal minimizasyon yapılmıştır.

## Sonuçlar
Analitik çözüm ve sayısal optimizasyon aynı sonucu vermiştir:

- $\lambda \approx 12.142857$

Histogram ve Poisson PMF karşılaştırması modelin verilere makul düzeyde uyduğunu göstermektedir.

## Yorum / Tartışma
Veri setine eklenen 200 değerindeki aykırı gözlem, $\lambda$ tahminini ciddi şekilde yükseltmiştir.
Bu durum, MLE yönteminin aykırı değerlere karşı hassas olduğunu göstermektedir.
Gerçek hayat uygulamalarında veri temizleme ve outlier analizi önemlidir.
