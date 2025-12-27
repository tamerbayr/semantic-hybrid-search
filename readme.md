# ⚖️ Hukuk Alanı İçin Hibrit Semantik Arama ve RAG Modülü

> **Ders:** Büyük Dil Modelleri (LLM)  
> **Geliştirici:** Tamer Bayar (220205027)

## 📖 Proje Özeti
Bu çalışma, hukuk gibi hassas ve terminolojiye dayalı alanlarda, **Large Language Model (LLM)** halüsinasyonlarını önlemek ve doğru bilgiye ulaşmak amacıyla geliştirilmiş bir **"Hibrit Retriever"** (Bilgi Getirici) modülüdür.

Geleneksel anahtar kelime aramasının yetersiz kaldığı ve saf vektör aramasının bağlamı kaçırabildiği durumlarda, bu sistem her iki yöntemi **özgün bir hibrit skorlama algoritması** ile birleştirir.

### 🚀 Temel Özellikler
* **Hibrit Arama:** Semantik (vektör) benzerlik ve kelime eşleşmesini birleştiren özel algoritma.
* **Domain Spesifik:** Hukuk terimleri ve soru-cevap çiftleri üzerinde optimize edilmiştir.
* **Yüksek Hız:** FAISS kütüphanesi ile milyonlarca veri içinde milisaniyeler süren arama.
* **Halüsinasyonsuz:** LLM'in metin üretmesine değil, doğrulanmış veritabanından bilgi getirmesine (Retrieval-only) odaklanır.
* **Arayüz:** Gradio tabanlı kullanıcı dostu web arayüzü.

---

## ⚙️ Nasıl Çalışır? (Metodoloji)

Sistem, kullanıcının sorgusunu alıp veritabanındaki en alakalı hukuki cevapları getirmek için **3 aşamalı** bir işlem uygular:

1.  **Vektör Araması (Aday Havuzu):** Kullanıcı sorgusu `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2` modeli ile vektörleştirilir ve FAISS ile en yakın 50 aday getirilir.
2.  **Hibrit Skorlama (Re-Ranking):** Adaylar, aşağıdaki parçalı fonksiyon kullanılarak yeniden puanlanır. Bu, anlamsal olarak yakın ama kritik kelimeleri içermeyen sonuçları filtreler.

### Skorlama Algoritması
Sistemin kalbi olan matematiksel model şu şekildedir:

$$
S_{final} = 
\begin{cases} 
S_{vec} + (\frac{m}{n} \times 0.30) & \text{eğer } m > 0 \\
S_{vec} \times 0.80 & \text{eğer } m = 0 \text{ ve } S_{vec} < 0.40 \\
S_{vec} & \text{diğer durumlarda}
\end{cases}
$$

* **$S_{vec}$:** Kosinüs benzerliği (Vektör skoru).
* **$m$:** Sorgu ve hedef metin arasındaki ortak "temizlenmiş" kelime sayısı.
* **$n$:** Sorgudaki toplam temiz kelime sayısı.
* **Mantık:** Ortak kelime varsa ödüllendir, hem ortak kelime yok hem de benzerlik düşükse cezalandır.

3.  **Filtreleme:** Final skoru **0.45**'in altında olan sonuçlar kullanıcıya gösterilmez.

---

## 🛠️ Kurulum ve Kullanım

Projeyi yerel bilgisayarınızda veya Google Colab'da çalıştırmak için adımları izleyin.

### Gereksinimler
Gerekli kütüphaneleri yükleyin:
```bash
pip install sentence-transformers faiss-cpu gradio stopwords_tr pandas numpy