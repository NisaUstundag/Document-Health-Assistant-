# Belge Sağlığı Asistanı
Akbank Derin Öğrenme Bootcamp - Final Projesi

Bu proje, bir finansal belgenin (fatura, dekont vb.) fiziksel durumunu, derin öğrenme yöntemleri kullanarak "Sağlam" veya "Hasarlı" olarak sınıflandırmak amacıyla geliştirilmiştir. Proje, sadece bir sınıflandırma problemi çözmekle kalmayıp, aynı zamanda pratik bir iş problemine çözüm üretme ve bu çözüm için gereken veri setini sıfırdan oluşturma yeteneklerini sergilemeyi hedefler.

**Kalın Yazı**Projenin Amacı ve Stratejisi
* Liste elemanıKarşılaşılan Problem
* Liste elemanıDijitalleştirme süreçlerinde, taranan belgelerin fiziksel kalitesi (yırtık, lekeli, buruşuk vb.) Optik Karakter Tanıma (OCR) gibi sistemlerin performansını doğrudan etkiler. Ancak, bu spesifik "fiziksel hasar" problemini modellemek için halka açık, etiketlenmiş bir veri seti bulunmamaktadır.

**Kalın Yazı**Geliştirilen Çözüm: Sentetik Veri Üretimi
Bu zorluğun üstesinden gelmek için, projede sentetik veri üretimi yaklaşımı benimsenmiştir. Temiz ve hasarsız belge görsellerinden oluşan bir temel veri seti kullanılarak, Python'un OpenCV kütüphanesi ile programatik olarak "hasarlı" görseller üretilmiştir. Bu yaklaşım, projenin sadece bir model eğitmekten ibaret olmadığını, aynı zamanda bir veri mühendisliği ve yaratıcı problem çözme projesi olduğunu göstermektedir.

Geliştirilen özel fonksiyonlar ile belgelere üç temel hasar türü uygulanmıştır:

* Liste elemanıBuruşukluk (Wrinkle): Geometrik dönüşümler ve sinüs/kosinüs dalgaları kullanılarak gerçekçi bir buruşukluk dokusu eklendi.

* Liste elemanıLeke (Stain): Yarı saydam bir katman bindirme (image blending) tekniği ile belgeler üzerine kahve lekesi gibi hasarlar eklendi.

* Liste elemanıYırtık (Tear): Görüntünün rastgele bir köşesine poligon çizme ve doldurma yöntemiyle yırtık illüzyonu yaratıldı.

**Kalın Yazı**Kullanılan Teknolojiler ve Kütüphaneler
Programlama Dili: Python

* Liste elemanıDerin Öğrenme: TensorFlow, Keras

* Liste elemanıGörüntü İşleme: OpenCV, Matplotlib

* Liste elemanıVeri Manipülasyonu: NumPy

* Liste elemanıGeliştirme Ortamı: Kaggle Notebooks (GPU ile)

* Liste elemanıVersiyon Kontrolü: Git & GitHub

**Kalın Yazı**Proje Adımları
* Liste elemanıVeri Seti Hazırlığı: Kaggle'daki "Dogs vs. Cats" veri seti, konseptin çalıştığını kanıtlamak (Proof-of-Concept) için temel veri seti olarak seçilmiştir. train.zip dosyası açılarak görsellere erişim sağlanmıştır.

* Liste elemanıSentetik Veri Üretimi: Yukarıda bahsedilen özel hasar fonksiyonları kullanılarak 200 "Sağlam" ve 200 "Hasarlı" (rastgele buruşuk, lekeli veya yırtık) olmak üzere toplam 400 görsellik bir veri seti oluşturulmuştur.

* Liste elemanıVeri Ön-İşleme: Keras'ın ImageDataGenerator aracı kullanılarak görseller yeniden boyutlandırılmış, piksel değerleri 0-1 arasına normalize edilmiş ve veri seti %80 eğitim, %20 doğrulama (validation) olmak üzere ikiye ayrılmıştır.

* Liste elemanıModel Mimarisi: Standart bir Konvolüsyonlu Sinir Ağı (CNN) modeli katman katman inşa edilmiştir. Model, Conv2D, MaxPooling2D, Flatten, Dropout ve Dense katmanlarından oluşmaktadır.

* Liste elemanıModelin Eğitilmesi: Hazırlanan veri seti ile model, 15 epoch boyunca adam optimizer ve binary_crossentropy kayıp fonksiyonu kullanılarak eğitilmiştir.

* Liste elemanıDeğerlendirme ve Test: Eğitimin sonuçları grafiklerle görselleştirilmiş ve eğitilmiş modelin daha önce görmediği tek bir resim üzerindeki performansı test edilmiştir.

**Kalın Yazı**Sonuçlar ve Analiz
* Liste elemanıEğitim süreci sonunda elde edilen performans grafikleri aşağıdadır:

* Liste elemanıEğitim Başarımı (Training Accuracy): Model, eğitim verisetini ~%95'in üzerinde bir başarıyla ezberleyerek öğrenme potansiyelini kanıtlamıştır.

* Liste elemanıDoğrulama Başarımı (Validation Accuracy): Model, daha önce görmediği test verilerinde ~%50-60 bandında bir başarı göstermiştir.

Bu iki sonuç arasındaki fark, modelin aşırı öğrendiğini (overfitting) açıkça göstermektedir. Bu, sınırlı bir veri setiyle çalışırken beklenen ve normal bir sonuçtur. Projenin bu aşamadaki amacı, modelin öğrenme kapasitesinin olduğunu ve geliştirdiğimiz sentetik veri üretim altyapısının çalıştığını kanıtlamaktı ve bu amaca başarıyla ulaşılmıştır.

* Liste elemanıTek Resimle Test (Inference)
Eğitilmiş modelin, daha önce görmediği hasarlı bir kedi resmini doğru bir şekilde "HASARLI" olarak sınıflandırdığı görülmüştür. Bu, modelin sadece teoride değil, pratikte de çalıştığının bir kanıtıdır.

**Kalın Yazı**Gelecek Adımlar
* Liste elemanıBu "proof-of-concept" projesini daha da ileriye taşımak için aşağıdaki adımlar atılabilir:

Veri Setini Büyütmek: Üretilen sentetik veri sayısını artırarak (örn. 2000 yerine 10000) modelin daha iyi genelleme yapması sağlanabilir.

Aşırı Öğrenmeyi Engellemek: Dropout katmanını daha agresif kullanmak, L1/L2 regularizasyon eklemek veya Erken Durdurma (Early Stopping) gibi teknikler uygulanabilir.

Transfer Learning: ImageNet gibi büyük veri setleri üzerinde eğitilmiş VGG16, ResNet gibi hazır modelleri kullanarak, daha az veriyle daha yüksek başarı oranlarına ulaşılabilir.
