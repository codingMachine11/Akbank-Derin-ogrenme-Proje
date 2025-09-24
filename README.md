# Akbank-Derin-ogrenme-Proje
# 🦙 Alpaca Sınıflandırma Projesi (CNN + Transfer Learning)

## 📌 Giriş

Bu proje, **Global AI Hub Derin Öğrenme Bootcamp** kapsamında gerçekleştirilmiştir.  
Amacımız, Kaggle üzerinde yer alan **Alpaca Dataset Small** veri setini kullanarak **görüntü sınıflandırma** problemi çözmektir. Veri setinde iki sınıf bulunmaktadır:  

- **alpaca** (resimde alpaca bulunan görüntüler)  
- **not alpaca** (resimde alpaca bulunmayan görüntüler)  

Projede öncelikle sıfırdan yazılmış basit bir **Convolutional Neural Network (CNN)** modeli denedik. Ancak küçük veri seti nedeniyle model kısa sürede **overfitting** problemine yakalandı (train doğruluğu artarken validation doğruluğu sabit kaldı). Bu deneyim, overfit’in pratikte nasıl göründüğünü anlamamıza yardımcı oldu.

Sonrasında, gerçek dünyada sık kullanılan bir yaklaşım olan **Transfer Learning** yöntemine geçtik. Burada önceden **ImageNet** üzerinde eğitilmiş **MobileNetV2** modelini kullandık. Modelin taban katmanlarını dondurup sadece tepe katmanını eğittik, ardından son 30 katmanı açarak düşük öğrenme oranı ile **fine-tuning** yaptık. Bu sayede validation ve test doğruluklarını %90’ın üzerine çıkarmayı başardık.

---

## 📊 Metrikler ve Sonuçlar

- **Basit CNN modeli:**  
  - Train doğruluğu: ~%70  
  - Validation doğruluğu: ~%55  
  - Gözlem: Model hızlıca ezberlemeye başladı, genelleme zayıf kaldı.

- **Transfer Learning (MobileNetV2):**  
  - Validation doğruluğu: ~%94  
  - Test doğruluğu: ~%94  
  - Val kaybı düşük ve stabil → model sadece ezberlemiyor, genelleyebiliyor.  
  - Grad-CAM görselleri sayesinde modelin gerçekten **alpaca bölgelerine odaklandığını** gözlemledik.

Bu sonuçlar, küçük veri setlerinde transfer learning’in ne kadar güçlü olduğunu gösteriyor.

---

## 📂 Proje Yapısı

├── README.md # Projenin açıklaması (bu dosya)
├── notebooks/
│ ├── cnn_baseline.ipynb # Basit CNN modeli denemeleri
│ ├── transfer_learning.ipynb # MobileNetV2 ile transfer learning
│ └── evaluation.ipynb # Confusion matrix, yanlış örnekler, Grad-CAM
├── UI/ # (Opsiyonel) Streamlit veya benzeri arayüz için örnek
└── data/ # Veri seti yolu (Kaggle’dan alınır)

---

## 🧩 Ekler

- **Grad-CAM ile yorumlanabilirlik:** Modelin karar verirken resmin hangi bölgelerine baktığını görselleştirdik. Özellikle alpaca kulakları ve yüz bölgesine odaklanması, modelin gerçekten ilgili özellikleri kullandığını gösterdi.  
- **class_weight ile dengeleme:** Sınıflar arasında veri sayısı farklı olduğundan, az olan sınıfın öğrenme sırasında kaybolmaması için class weight kullandık.  
- **Overfitting önlemleri:** Data augmentation, dropout, early stopping ve learning rate azaltma callback’leri kullanıldı.

---

## 🚀 Sonuç ve Gelecek Çalışmalar

Bu proje ile küçük bir veri setinde CNN’lerin sınırlarını, overfitting’in nasıl oluştuğunu ve transfer learning ile nasıl çözülebileceğini deneyimledik.  
**Gelecek çalışmalar için düşündüklerimiz:**

- Daha büyük ve çeşitli bir veri seti toplayarak modeli daha sağlam hale getirmek.  
- Streamlit veya benzeri araçlarla **kullanıcı dostu bir arayüz** eklemek.  
- Modeli **mobil cihazlara uygun TFLite formatına** dönüştürmek.  
- Canlı kamera görüntülerinde (real-time inference) test ederek **gerçek zamanlı kullanım** senaryoları denemek.  

Bootcamp sonrasında da bu repo üzerinde geliştirmelere devam ederek, daha profesyonel bir bilgisayarlı görü projesine dönüştürmeyi hedefliyoruz.

---

## 🔗 Linkler

https://www.kaggle.com/code/perastra/cnn-transfer-learning-projesi-alpaca/edit
---

