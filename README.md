# Hybrid Semantic Retriever

Bu proje, anlamsal benzerlik ile kelime bazlı eşleşmeyi birleştiren,
hibrit bir bilgi erişim sistemi sunmaktadır. Amaç, özellikle
anlamsal hassasiyetin yüksek olduğu alanlarda daha doğru ve güvenilir
arama sonuçları elde etmektir.

---

## Projenin Amacı

Geleneksel kelime tabanlı arama yöntemleri, farklı ifade biçimlerinde aynı
anlama gelen sorguları yakalamakta yetersiz kalabilmektedir.
Yalnızca vektör benzerliğine dayalı anlamsal arama yöntemleri, anlamsal olarak
yakın fakat istenmeyen sonuçlar üretebilmektedir.

Bu proje:
- Metinleri gömme (embedding) vektörlerine dönüştürerek anlamsal benzerliği
  hesaplar
- Elde edilen aday sonuçları, kelime eşleşmesine göre hesaplanan kurallarla
  yeniden sıralar
- Düşük güvenilirlikli sonuçları eler
- 
---

## İçerik

- **Proje Dokümanı**
  - `makale.pdf`  
    Projenin amacı, metodolojisi, kullanılan araçlar ve değerlendirme
    sonuçlarını içeren rapor dosyası.

- **Çalıştırılabilir Kod**
  - `semantic-hybrid-search.ipynb`  
    Google Colab üzerinde çalışacak şekilde hazırlanmış, veri yükleme,
    anlamsal arama, hibrit skorlama ve Gradio arayüzünü içeren Jupyter
    defteri.

- **Model ve İndeks Dosyaları**
  - `faiss.index`  
    FAISS kullanılarak oluşturulmuş, kosinüs benzerliğine dayalı vektör indeksi
    (IndexFlatIP).
  - `sorular.pkl`  
    Sistemde arama yapılan soru metinlerini içeren dosya.
  - `cevaplar.pkl`  
    Sorulara karşılık gelen cevapları içeren dosya.

> `.pkl` ve `.index` dosyaları, sistemin çalışması için gereklidir ve
> arayüz başlatılmadan önce colab ortamına yüklenmelidir.

---

## Not

- Proje ders kapsamında geliştirilmiştir.
