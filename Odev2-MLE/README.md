# Makine Öğrenmesi Dersi - Ödev 2

### Problem Tanımı [cite: 3-4]
Bu proje, bir ana caddeden geçen araç sayısını Poisson dağılımı kullanarak modellemeyi amaçlar. Temel hedef, trafik yoğunluğunu temsil eden $\lambda$ parametresini Maximum Likelihood Estimation (MLE) yöntemiyle tahmin etmektir.

### Veri Seti [cite: 22]
Analizde kullanılan veri seti, 14 farklı zaman diliminde bir dakikada geçen araç sayılarını içermektedir: 
`[12, 15, 10, 8, 14, 11, 13, 16, 9, 12, 11, 14, 10, 15]`

### Yöntem [cite: 13-14]
1. **Analitik Çözüm:** Poisson olabilirlik fonksiyonunun logaritması alınmış ve türev yoluyla $\hat{\lambda}_{MLE}$ değerinin aritmetik ortalama olduğu kanıtlanmıştır. [cite: 11]
2. **Sayısal Çözüm:** Python `scipy.optimize` kütüphanesi kullanılarak Negatif Log-Likelihood (NLL) fonksiyonu minimize edilmiştir. [cite: 18]

### Sonuçlar ve Tartışma [cite: 35-37]
- **Hesaplanan Lambda ($\lambda$):** ~12.14
- **Model Uyumu:** Poisson PMF grafiği ile veri histogramı karşılaştırıldığında modelin veriye yüksek uyum sağladığı görülmüştür. [cite: 41]
- **Outlier Analizi:** Sisteme eklenen hatalı bir "200" araç verisinin, ortalama tabanlı olan MLE sonucunu ciddi şekilde saptıracağı ve yanlış belediye planlamasına yol açacağı belirlenmiştir. [cite: 44-45]