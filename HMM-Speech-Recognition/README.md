<<<<<<< HEAD
# makine-ogrenmesi
=======
# HMM ile İzole Kelime Tanıma Projesi

## 1. Problem Tanımı
Bu proje, Gizli Markov Modelleri (HMM) kullanarak ses verilerinden "EV" ve "OKUL" kelimelerini ayırt edebilen basit bir izole kelime tanıma sistemi geliştirmeyi amaçlamaktadır. Ses spektrumundaki değişimler (High ve Low frekanslar) gözlem birimleri olarak kullanılmıştır.

## 2. Veri Seti
Projede kullanılan veriler, ses sinyalinin basitleştirilmiş bir temsili olan iki farklı frekans düzeyinden oluşmaktadır:
- **High (Yüksek Frekans):** Kodlamada `0` indeksi ile temsil edilmiştir.
- **Low (Düşük Frekans):** Kodlamada `1` indeksi ile temsil edilmiştir.
- **Test Verisi:** [High, Low, Low] dizisi kullanılarak modellerin performansı ölçülmüştür.

## 3. Yöntem
Sistem tasarımı iki temel aşamadan oluşmaktadır:
- **Teorik Modelleme:** Her kelime için fonemler gizli durumlar (states) olarak belirlenmiş ve geçiş (transition) ile emisyon (emission) matrisleri el ile hesaplanmıştır.
- **Uygulama:** Python `hmmlearn` kütüphanesi içindeki `MultinomialHMM` sınıfı kullanılarak kelime modelleri oluşturulmuştur. Modeller, test verisini olasılıksal olarak değerlendirmek (score) için Log-Likelihood yöntemini kullanır.

## 4. Sonuçlar
Yapılan testler sonucunda elde edilen Log-Likelihood skorları şu şekildedir:
- **EV Modeli Puanı:** -1.3295
- **OKUL Modeli Puanı:** -2.3025
- **Karar:** EV modelinin puanı daha yüksek (sıfıra daha yakın) olduğu için test verisi başarıyla **"EV"** olarak sınıflandırılmıştır.

## 5. Yorum ve Tartışma
- **Gürültü Etkisi:** Ses verisindeki gürültü emisyon olasılıklarını belirsizleştirerek tanıma doğruluğunu düşürür.
- **Ölçeklenebilirlik:** Binlerce kelimelik geniş sistemlerde HMM yerini, bağlamsal bilgiyi daha iyi yakalayan Derin Öğrenme (RNN, LSTM vb.) mimarilerine bırakmaktadır.
>>>>>>> b74c412 (İlk yükleme: Klasör yapısı ve rapor tamamlandı)
