# Matris Manipülasyonu, Özdeğerler ve Özvektörler

Bu çalışma, 2025-2026 Bahar Dönemi YZM212 Makine Öğrenmesi dersi III. Laboratuvar değerlendirmesi kapsamında hazırlanmıştır.

## 1. Matris Manipülasyonu, Özdeğerler ve Özvektörlerin Makine Öğrenmesi ile İlişkisi

### 1.1 Matris Manipülasyonu Nedir?

Matris manipülasyonu, verilerin matris şeklinde gösterilmesi ve bu matrisler üzerinde toplama, çıkarma, çarpma, transpoz alma, ters alma gibi işlemlerin yapılmasıdır. Makine öğrenmesinde veriler çoğu zaman tablo veya matris yapısında tutulduğu için bu işlemler çok önemlidir. Bir veri kümesinde satırlar genellikle örnekleri, sütunlar ise özellikleri temsil eder. Bu yüzden model eğitimi sırasında yapılan birçok hesap aslında matris işlemlerine dayanır.

### 1.2 Özdeğer ve Özvektör Nedir?

Bir kare matris için, sıfırdan farklı bir vektör doğrusal dönüşümden sonra yönünü kaybetmeden sadece belli bir katsayı ile çarpılıyorsa burada özdeğer ve özvektör kavramı ortaya çıkar. Matematiksel olarak bu durum `A.v = λ.v` şeklinde gösterilir. Burada `λ` özdeğer, `v` ise özvektördür. Özvektör, dönüşümden sonra yönünü koruyan vektörü; özdeğer ise bu vektörün ne kadar ölçeklendiğini gösterir.

### 1.3 Makine Öğrenmesi ile İlişkisi

Makine öğrenmesinde veriler genellikle çok boyutlu olduğu için veriyi anlamak ve daha iyi temsil etmek önemlidir. Özdeğerler ve özvektörler bu noktada bize yardımcı olur. Özellikle veride hangi yönlerin daha baskın olduğunu, varyansın hangi doğrultularda yoğunlaştığını anlamamızı sağlar. Böylece hem veri daha iyi analiz edilir hem de gereksiz boyutlar azaltılabilir.

### 1.4 Kullanıldığı Yöntemler ve Yaklaşımlar

Bu kavramların en bilinen kullanım alanlarından biri PCA yani Principal Component Analysis yöntemidir. PCA’da verinin en önemli yönlerini bulmak amaçlanır. Bunun için veri üzerinden elde edilen yapı üzerinde ayrışım yapılır ve en büyük özdeğerlere karşılık gelen özvektörler seçilir. Bu vektörler verinin en fazla bilgi taşıyan yönlerini gösterir. Böylece veri daha az boyutla temsil edilebilir.

Bir diğer önemli kullanım alanı da spectral embedding ve spectral clustering gibi yöntemlerdir. Bu yöntemlerde veri noktaları arasındaki benzerliklerden bir grafik yapısı kurulur. Daha sonra bu grafiğin Laplasyen matrisi üzerinde işlem yapılarak en anlamlı bileşenler elde edilir. Özellikle klasik yöntemlerin yetersiz kaldığı bazı veri yapılarında bu tür spektral yöntemler daha başarılı sonuç verebilir.

Kısacası matris manipülasyonu, özdeğerler ve özvektörler makine öğrenmesinde sadece teorik kavramlar değildir. Boyut indirgeme, veri analizi, kümelenme ve bazı grafik tabanlı yöntemlerde doğrudan kullanılmaktadır.

### 1.5 Kaynaklar

1. scikit-learn Developers, *PCA — scikit-learn documentation*
2. scikit-learn Developers, *spectral_embedding — scikit-learn documentation*

---

## 2. NumPy `linalg.eig` Fonksiyonunun İncelenmesi

### 2.1 `numpy.linalg.eig` Fonksiyonu Ne Yapar?

`numpy.linalg.eig` fonksiyonu, kare bir matrisin özdeğerlerini ve sağ özvektörlerini hesaplamak için kullanılır. Fonksiyonun girdi olarak kare bir dizi alması gerekir. Çıktı olarak ise iki parçalı bir sonuç döndürür: özdeğerler ve bu özdeğerlere karşılık gelen özvektörler.

### 2.2 Girdi ve Çıktılar

Fonksiyonun girdisi `(M, M)` boyutunda kare bir matristir. Çıktı olarak bir namedtuple döner. Bunun içinde `eigenvalues` ve `eigenvectors` alanları bulunur. Özvektörler sütunlar halinde tutulur. Yani `eigenvectors[:, i]` sütunu, `eigenvalues[i]` değerine karşılık gelen özvektördür.

Dokümantasyonda özdeğerlerin sıralı olmak zorunda olmadığı da belirtilmektedir. Ayrıca gerçek sayılı bir matris verilse bile bazı durumlarda sonuç karmaşık sayı olabilir. Eğer matris gerçek sayılıysa karmaşık özdeğerler eşlenik çiftler halinde gelebilir.

### 2.3 Dokümantasyonun İncelenmesi

NumPy dokümantasyonuna göre bu fonksiyon genel kare matrisler için özdeğer ve özvektör hesabı yapmaktadır. Ayrıca bu işlemin arka planda LAPACK’in `_geev` rutinleri kullanılarak gerçekleştirildiği belirtilmektedir. Bu da bize fonksiyonun sadece basit bir Python kodu olmadığını, daha alt seviyede optimize edilmiş sayısal cebir kütüphanelerinden yararlandığını gösterir.

Dokümantasyonda ayrıca yakınsama problemi yaşanırsa `LinAlgError` hatası verilebileceği yazmaktadır. Bu da bazı matrislerde sayısal hesaplamaların her zaman sorunsuz ilerlemeyebileceğini göstermektedir.

### 2.4 Kaynak Kod Mantığı

Kaynak kod incelendiğinde özdeğer ve özvektör sonucunun `EigResult` adlı bir yapı ile döndürüldüğü görülmektedir. Ayrıca yakınsama problemi için `"Eigenvalues did not converge"` şeklinde bir hata mekanizması da tanımlanmıştır. Bu durum, fonksiyonun yalnızca sonuç döndürmekle kalmadığını, hata kontrolü de yaptığını göstermektedir.

Kısaca söylemek gerekirse `numpy.linalg.eig`, kullanıcı açısından tek satırlık kolay bir fonksiyon gibi görünse de arka planda güçlü ve optimize edilmiş bir altyapı kullanmaktadır. Bu yüzden pratik uygulamalarda oldukça kullanışlıdır.

### 2.5 Kaynaklar

1. NumPy Developers, *numpy.linalg.eig — NumPy documentation*
2. NumPy Developers, *numpy/linalg/_linalg.py source code*

---

## 3. Hazır `eig` Fonksiyonu Kullanmadan Özdeğer Hesaplama ve Karşılaştırma

### 3.1 Referans Çalışmanın Özeti

Ödevde verilen GitHub reposunda bir matrisin özdeğerlerini ve özvektörlerini hesaplamaya yönelik bir çalışma bulunmaktadır. Repo açıklamasında genel amaç özdeğer ve özvektör hesabı olarak verilmiştir. Ancak `main.py` dosyasına bakıldığında doğrudan gösterilen ana işlem özdeğer hesabı üzerinedir.

Kod içinde önce karakteristik denklem oluşturulmaktadır. Bunun için `characteristic_equation(matrix)` fonksiyonu ile `A - λI` yapısı kurulmaktadır. Daha sonra determinant tabanlı denklem elde edilmekte ve son aşamada `np.roots(...)` kullanılarak polinomun kökleri bulunup özdeğerler hesaplanmaktadır.

### 3.2 Uygulama Adımları

Bu bölümde referans çalışmaya benzer şekilde ilerlenmiştir. İlk olarak seçilen kare matris için karakteristik denklem mantığı kullanılmıştır. Daha sonra determinanttan gelen polinomun kökleri hesaplanarak özdeğerler elde edilmiştir. Böylece hazır `numpy.linalg.eig` fonksiyonunu doğrudan kullanmadan, daha manuel bir yaklaşımla özdeğer hesabı tekrar uygulanmıştır.

Bu yöntem eğitim açısından faydalıdır çünkü özdeğer hesabının arkasındaki matematiksel mantığı daha açık şekilde göstermektedir. Özellikle karakteristik polinom ile özdeğer arasındaki ilişkiyi görmek açısından yararlıdır.

### 3.3 NumPy ile Karşılaştırma

Aynı matris üzerinde daha sonra `numpy.linalg.eig` fonksiyonu da çalıştırılmıştır. Elde edilen sonuçlar karşılaştırıldığında özdeğerlerin aynı veya çok yakın çıktığı görülmektedir. Küçük farklar varsa bunlar genellikle sayısal gösterim ve yuvarlama farklarından kaynaklanmaktadır.

Burada dikkat çeken nokta şudur: referans repo daha öğretici ve adım adım bir mantık sunarken, NumPy fonksiyonu çok daha kısa ve pratik bir çözüm vermektedir. Ayrıca NumPy aynı anda özvektörleri de döndürmektedir. Bu nedenle eğitim amacıyla manuel yöntem faydalı olsa da gerçek uygulamalarda `numpy.linalg.eig` kullanmak daha mantıklıdır.

### 3.4 Sonuç

Bu ödevde özdeğer ve özvektör kavramlarının makine öğrenmesindeki yeri incelenmiştir. Ayrıca NumPy’nin `linalg.eig` fonksiyonu hem dokümantasyon hem de kaynak kod düzeyinde araştırılmıştır. Son olarak da hazır `eig` fonksiyonu kullanılmadan özdeğer hesabı tekrar uygulanmış ve NumPy sonucu ile karşılaştırılmıştır.

Genel olarak bu çalışma, doğrusal cebir konularının makine öğrenmesi açısından neden önemli olduğunu daha net göstermiştir. Özellikle PCA ve spektral yöntemler gibi alanlarda özdeğer ve özvektörlerin önemli bir yere sahip olduğu görülmüştür. Aynı zamanda NumPy gibi kütüphanelerin bu işlemleri pratikte ne kadar kolaylaştırdığı da anlaşılmıştır.

### 3.5 Kaynaklar

1. Lucas BN, *Eigenvalues-and-Eigenvectors — GitHub repository*
2. Lucas BN, *main.py*
3. NumPy Developers, *numpy.linalg.eig — NumPy documentation*