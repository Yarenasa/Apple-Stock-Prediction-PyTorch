# Apple (AAPL) Hisse Senedi Fiyat Tahmini: LSTM ve GRU Karşılaştırması

Bu projede, PyTorch derin öğrenme kütüphanesi kullanılarak Apple Inc. (AAPL) şirketinin geçmiş hisse senedi fiyatları üzerinden geleceğe yönelik zaman serisi tahmini yapılmıştır. Durağan olmayan (non-stationary) ve karmaşık finansal verilerin modellenmesi için geleneksel yöntemler yerine Derin Öğrenme (Deep Learning) mimarileri tercih edilmiştir.

## Proje Adımları ve Metodoloji

1. **Veri Setinin İndirilmesi:** `yfinance` kütüphanesi kullanılarak Apple'ın 2014-2024 yılları arasındaki 10 yıllık günlük kapanış (Close) fiyatları çekilmiştir.
2. **Keşifsel Veri Analizi:** Ham verinin genel trendini incelemek ve modele verilmeden önceki yapısını anlamak için görselleştirmeler yapılmıştır.
3. **Veri Mühendisliği ve Ön İşleme:** Modelin gradyan hesaplamalarında daha stabil çalışabilmesi için tüm veriler `MinMaxScaler` ile -1 ve 1 aralığına normalize edilmiştir. Modelin serisel bağımlılığı öğrenebilmesi için **"Kayan Pencere" (Sliding Window)** tekniği uygulanmış (lookback=20) ve finansal tahminlerde kritik olan veri sızıntısını (data leakage) engellemek adına veri, rastgele değil kronolojik olarak %80 Train, %20 Test şeklinde ayrılmıştır.
4. **Model Mimarilerinin Kurulumu:** PyTorch kullanılarak geçmiş veri dizilerindeki doğrusal olmayan bağıntıları yakalayabilen **LSTM (Uzun Kısa Süreli Hafıza)** ve **GRU (Geçitli Tekrarlayan Birim)** tabanlı iki farklı mimari inşa edilmiştir.
5. **Optuna ile Hiperparametre Optimizasyonu:** Modellerin öğrenme oranı (learning rate) ve gizli katman boyutları (hidden dimension) gibi kritik parametreleri `Optuna` kütüphanesi ile algoritmik olarak optimize edilmiştir.
6. **Sonuçların Karşılaştırılması:** Eğitilen modeller test seti üzerinde denenmiş, yapılan tahminler gerçek fiyat (USD) ölçeğine geri çevrilerek Hata Kareleri Ortalaması (MSE) metrikleri hesaplanmış ve grafiğe dökülmüştür.
