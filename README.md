 Projenin Amacı
Bu proje kapsamında, ABD Orman Servisi tarafından sağlanan bir çevresel veri seti (Forest CoverType) kullanılarak, arazilerin hangi orman türüyle kaplı olduğunu tahmin eden bir Random Forest sınıflandırma modeli geliştirildi.

Veri setinde her satır bir araziyi, her sütun ise bu arazinin bir özelliğini temsil ediyor: örneğin yüksekliği, eğimi, toprak tipi, suya uzaklığı gibi. Biz bu sayısal verilere bakarak "Bu arazi hangi orman türüne aittir?" sorusuna cevap vermek istedik.

🧠 Kullanılan Yöntem: Random Forest
Random Forest, adından da anlaşılacağı gibi, birçok karar ağacından oluşan bir ormandır.

Her ağaç:

Verinin rastgele bir alt kümesiyle eğitilir.

Rastgele bazı özellikleri kullanır (örneğin sadece 10 tanesini görür).

Kendi başına tahmin yapar (örneğin “bence bu bir Ladin ormanı” der).

Forest yani orman:

Bütün ağaçların oylarını toplar.

En çok oyu alan sınıfı tahmin olarak kabul eder.

Bu sistem:

Tek bir karar ağacına göre çok daha güvenilir ve sağlam olur.

Hataları azaltır.

Aşırı öğrenmeyi (overfitting) engeller.

📂 Veri Seti – covtype.csv
Veri setinde toplam 55 sütun (özellik) ve binlerce satır vardır. Özellikler şunlardan oluşur:

Sayısal Özellikler: Rakım, eğim, güneşlenme miktarı, mesafeler (yol, nehir, yangın noktası).

Binary Özellikler: 40 farklı toprak tipi ve 4 vahşi alan bölgesi (hepsi 1-0 ile işaretlenmiş).

Hedef Değişken (Target): Cover_Type (1 ile 7 arasında sınıflar)

Her sınıf farklı bir ağaç türünü temsil eder. Örneğin:

1 → Spruce/Fir

2 → Lodgepole Pine

3 → Ponderosa Pine

...

7 → Krummholz

⚖️ Dengesizlik Problemi ve Çözüm
Veri seti bazı orman türlerinden çok, bazı türlerden az örnek içeriyordu. Bu dengesizlik, modelin azınlık sınıfları öğrenmesini zorlaştırabilir.

Çözüm: Her sınıftan eşit sayıda örnek aldık → Dengeli bir eğitim seti oluşturduk. Bu sayede her sınıfa adil davranıldı.

📈 Model Sonuçları – Ne Kadar Başarılıyız?
Modelimizin doğruluğu %85.78. Bu, her 100 tahminden yaklaşık 86’sının doğru yapıldığını gösterir. Çok sayıda sınıf olduğunu düşünürsek bu gayet iyi bir sonuç.

📊 Confusion Matrix Yorumu:
Aşağıdaki grafikte modelin tahmin performansı gösteriliyor:

Satırlar: Gerçek sınıf (doğru olan)

Sütunlar: Modelin tahmini

Kutu içindeki sayı: Kaç örnek o sınıfa tahmin edildi

🟦 Koyu mavi renk = doğru tahminler
⬜ Açık renk = karışıklık (yanlış sınıfa atanmış örnekler)

🔍 Detaylı Yorumlar:
Sınıf 7 (Krummholz) için mükemmel başarı: 550 örnekten 545’i doğru tahmin edilmiş! 🔥

Sınıf 6 (Douglas-fir) de oldukça başarılı: 518 doğru, sadece 32 hata.

Sınıf 2 (Lodgepole Pine) karışıklık yaşamış: 360 doğru ama 109 örnek yanlışlıkla sınıf 1’e gitmiş.

Sınıf 5 ve 4 arasında da çapraz karışıklıklar gözlemleniyor.

👉 Bu karışıklıklar genelde benzer ekosistemlerde bulunan türlerin verilerinin örtüşmesinden kaynaklanır.

🧮 Precision – Recall – F1 Skorları
Precision: “Model bir örneğe ‘sınıf A’ dediğinde, gerçekten sınıf A mıydı?”

Recall: “Gerçekten sınıf A olanları model doğru bulabildi mi?”

F1 Score: Precision ve Recall’un dengeli ortalaması (dengeye bakar).

Genel olarak:

En yüksek F1-skorlar: Sınıf 6 ve 7

En düşük F1-skor: Sınıf 1 ve 2 (karışıklık daha fazla)

Bu da şunu gösteriyor: bazı sınıflar ayırt edilmesi kolay (yüksek doğruluk), bazıları daha benzer ve ayırmak zor (düşük F1).

🧪 Özellik Önem Dereceleri
Random Forest, her özelliğin modelin karar vermesinde ne kadar etkili olduğunu da hesaplayabilir. Biz en önemli 15 özelliği görselleştirdik.

🟨 Örnek dikkat çeken özellikler:

Elevation (Rakım): Açık ara en önemli özellik.

Horizontal Distance to Roadways: İkinci sırada.

Hillshade_3pm / Hillshade_Noon: Güneşlenme miktarı önemliymiş demek ki.

Toprak tipi sütunları da bazı sınıflar için ayırt edici.

📌 Bu analizler sayesinde sadece tahmin yapmakla kalmadık, karar mekanizmasını da anlamış olduk.

✅ Sonuç ve Değerlendirme
Random Forest modeli, karmaşık ve çok sınıflı bir çevresel veri setinde başarılı sonuçlar verdi.

Dengeli örnekleme, modelin adil şekilde öğrenmesini sağladı.

Confusion matrix ile hangi sınıfların karıştığını gözlemledik ve yorumladık.

Özellik önem analizi, modelin neye göre karar verdiğini ortaya koydu.

💬 Neden Random Forest?
Kolay eğitilir, parametre ayarı nispeten basittir.

Overfitting’e dayanıklıdır.

Yüksek doğruluk verir.

Açıklanabilirlik sunar (özellik önem skoru).

NOT: Python kodunda yorum satırlarıyla açıklamalar eklenmiştir. 

Anahtar Kelimeler:

📊 Model / Algoritma Odaklı
Random Forest Sınıflandırıcı

Ensemble Learning Teknikleri

Decision Tree Tabanlı Modeller

Bagging ile Ağaç Tabanlı Öğrenme

Model Performans Karşılaştırması

Feature Importance Analizi

Multi-Class Classification Problem

Explainable Machine Learning

Overfitting'e Dayanıklı Modeller

Parallelized Learning Approach

Model Karar Süreci Görselleştirme

Tree-based ML Algorithms

Interpretability in Random Forest

Scikit-learn Random Forest Model

High-dimensional Data Modeling

🌍 Veri Seti / Uygulama Alanı
Forest Cover Type Dataset

USDA Geo Data Modeling

Coğrafi Bilgi Sistemleri (GIS) ve ML

Ekolojik Sınıflandırma Projesi

Toprak Özelliklerinden Örtü Tipi Tahmini

US Forest Service CoverType Dataset

Real-world Environmental Dataset

Jeofiziksel Veri ile Modelleme

Remote Sensing ve ML Uygulaması

Spatial Feature Classification

Ekosistem Veri Bilimi Projesi

Forest Ecology Prediction with AI

Earth Observation & AI

Raster-like Structured Tabular Data

📈 Değerlendirme ve Sonuçlar
Confusion Matrix Visualization

Class-wise Precision Recall Analysis

Yorumlanabilir Model Çıktıları

Sınıf Karışıklıklarının Analizi

En Başarılı / En Zor Sınıflar

Yüksek Doğruluklu Sınıflandırma

Model Değerlendirme Metodolojisi

Metric-based Performance Insights

Balanced Sampling for Fair Training

Real-life Data Generalization

Detailed Evaluation Report

Performance Metrics Breakdown

📌 Proje Özeti & GitHub-Style Etiketler
#MachineLearning

#RandomForest

#ForestCoverType

#EnvironmentalData

#GeoFeatures

#DataScienceProject

#ScikitLearn

#MultiClassClassification

#MLModelEvaluation

#ExplainableAI

#EnsembleMethods

#FeatureImportance

#ConfusionMatrix

#ModelInterpretability

#EcoML

#ForestML

Sorularınız için ulaşabilirsiniz.:)





