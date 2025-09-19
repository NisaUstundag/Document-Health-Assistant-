# Belge Sağlığı Asistanı
Akbank Derin Öğrenme Bootcamp - Final Projesi

Bu proje, bir finansal belgenin (fatura, dekont vb.) fiziksel durumunu, derin öğrenme yöntemleri kullanarak "Sağlam" veya "Hasarlı" olarak sınıflandırmak amacıyla geliştirilmiştir. Proje, sadece bir sınıflandırma problemi çözmekle kalmayıp, aynı zamanda pratik bir iş problemine çözüm üretme ve bu çözüm için gereken veri setini sıfırdan oluşturma yeteneklerini sergilemeyi hedefler.

Projenin Amacı ve Stratejisi
Karşılaşılan Problem
Dijitalleştirme süreçlerinde, taranan belgelerin fiziksel kalitesi (yırtık, lekeli, buruşuk vb.) Optik Karakter Tanıma (OCR) gibi sistemlerin performansını doğrudan etkiler. Ancak, bu spesifik "fiziksel hasar" problemini modellemek için halka açık, etiketlenmiş bir veri seti bulunmamaktadır.

Geliştirilen Çözüm: Sentetik Veri Üretimi
Bu zorluğun üstesinden gelmek için, projede sentetik veri üretimi yaklaşımı benimsenmiştir. Temiz ve hasarsız belge görsellerinden oluşan bir temel veri seti kullanılarak, Python'un OpenCV kütüphanesi ile programatik olarak "hasarlı" görseller üretilmiştir. Bu yaklaşım, projenin sadece bir model eğitmekten ibaret olmadığını, aynı zamanda bir veri mühendisliği ve yaratıcı problem çözme projesi olduğunu göstermektedir.

Geliştirilen özel fonksiyonlar ile belgelere üç temel hasar türü uygulanmıştır:

Buruşukluk (Wrinkle): Geometrik dönüşümler ve sinüs/kosinüs dalgaları kullanılarak gerçekçi bir buruşukluk dokusu eklendi.

Leke (Stain): Yarı saydam bir katman bindirme (image blending) tekniği ile belgeler üzerine kahve lekesi gibi hasarlar eklendi.

Yırtık (Tear): Görüntünün rastgele bir köşesine poligon çizme ve doldurma yöntemiyle yırtık illüzyonu yaratıldı.

Kullanılan Teknolojiler ve Kütüphaneler
Programlama Dili: Python

Derin Öğrenme: TensorFlow, Keras

Görüntü İşleme: OpenCV, Matplotlib

Veri Manipülasyonu: NumPy

Geliştirme Ortamı: Kaggle Notebooks (GPU ile)

Versiyon Kontrolü: Git & GitHub

Proje Adımları
Veri Seti Hazırlığı: Kaggle'daki "Dogs vs. Cats" veri seti, konseptin çalıştığını kanıtlamak (Proof-of-Concept) için temel veri seti olarak seçilmiştir. train.zip dosyası açılarak görsellere erişim sağlanmıştır.

Sentetik Veri Üretimi: Yukarıda bahsedilen özel hasar fonksiyonları kullanılarak 200 "Sağlam" ve 200 "Hasarlı" (rastgele buruşuk, lekeli veya yırtık) olmak üzere toplam 400 görsellik bir veri seti oluşturulmuştur.

Veri Ön-İşleme: Keras'ın ImageDataGenerator aracı kullanılarak görseller yeniden boyutlandırılmış, piksel değerleri 0-1 arasına normalize edilmiş ve veri seti %80 eğitim, %20 doğrulama (validation) olmak üzere ikiye ayrılmıştır.

Model Mimarisi: Standart bir Konvolüsyonlu Sinir Ağı (CNN) modeli katman katman inşa edilmiştir. Model, Conv2D, MaxPooling2D, Flatten, Dropout ve Dense katmanlarından oluşmaktadır.

Modelin Eğitilmesi: Hazırlanan veri seti ile model, 15 epoch boyunca adam optimizer ve binary_crossentropy kayıp fonksiyonu kullanılarak eğitilmiştir.

Değerlendirme ve Test: Eğitimin sonuçları grafiklerle görselleştirilmiş ve eğitilmiş modelin daha önce görmediği tek bir resim üzerindeki performansı test edilmiştir.

Sonuçlar ve Analiz
Eğitim süreci sonunda elde edilen performans grafikleri aşağıdadır:

Eğitim Başarımı (Training Accuracy): Model, eğitim verisetini ~%95'in üzerinde bir başarıyla ezberleyerek öğrenme potansiyelini kanıtlamıştır.

Doğrulama Başarımı (Validation Accuracy): Model, daha önce görmediği test verilerinde ~%50-60 bandında bir başarı göstermiştir.

Bu iki sonuç arasındaki fark, modelin aşırı öğrendiğini (overfitting) açıkça göstermektedir. Bu, sınırlı bir veri setiyle çalışırken beklenen ve normal bir sonuçtur. Projenin bu aşamadaki amacı, modelin öğrenme kapasitesinin olduğunu ve geliştirdiğimiz sentetik veri üretim altyapısının çalıştığını kanıtlamaktı ve bu amaca başarıyla ulaşılmıştır.

Tek Resimle Test (Inference)
Eğitilmiş modelin, daha önce görmediği hasarlı bir kedi resmini doğru bir şekilde "HASARLI" olarak sınıflandırdığı görülmüştür. Bu, modelin sadece teoride değil, pratikte de çalıştığının bir kanıtıdır.

Gelecek Adımlar
Bu "proof-of-concept" projesini daha da ileriye taşımak için aşağıdaki adımlar atılabilir:

Veri Setini Büyütmek: Üretilen sentetik veri sayısını artırarak (örn. 2000 yerine 10000) modelin daha iyi genelleme yapması sağlanabilir.

Aşırı Öğrenmeyi Engellemek: Dropout katmanını daha agresif kullanmak, L1/L2 regularizasyon eklemek veya Erken Durdurma (Early Stopping) gibi teknikler uygulanabilir.

Transfer Learning: ImageNet gibi büyük veri setleri üzerinde eğitilmiş VGG16, ResNet gibi hazır modelleri kullanarak, daha az veriyle daha yüksek başarı oranlarına ulaşılabilir.
