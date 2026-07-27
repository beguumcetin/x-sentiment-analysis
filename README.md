# X Sentiment Analizi

İstanbul Ticaret Odası (İTO) staj projesi kapsamında, İstanbul'a yönelik tweetlerin **turizm**, **ulaşım** ve **enflasyon** konularında duygu analizi (sentiment analysis).

## Özet

- **Veri:** 571 tweet (orijinal veri seti: 367 + pilot veri seti: 204), spam/reklam/alakasız içerik temizliği yapılmış
- **Model karşılaştırması:** savasy, saribasmetehan ve TurkishBERTweet modelleri 208 satırlık elle etiketlenmiş gold-standard veri üzerinde karşılaştırıldı
- **Fine-tuning:** savasy modeli, LoRA yöntemiyle gold-standard veriyle yeniden eğitildi

| Metrik | Fine-tuning Öncesi | Fine-tuning Sonrası |
|---|---|---|
| Genel doğruluk | %61.5 | %81 |
| Negatif yakalama | %86.6 | %90 |
| Nötr yakalama | %23.9 | %62 |
| Pozitif yakalama | %63.6 | %89 |

Detaylı analiz ve grafikler için: **[dashboard.html](dashboard.html)** (tarayıcıda açılabilir, internet gerektirmez)

## Klasör Yapısı

```
İTO_sentiment_analysisV2.ipynb   ana çalışma notebook'u
dashboard.html                    interaktif sonuç dashboard'u
veri/                             ham/kaynak veriler
ciktilar/                         üretilen tüm sonuç dosyaları
model/                            fine-tune edilmiş LoRA adaptörü ve ön işleme modülü
eski_denemeler/                   bırakılan alternatif model denemesi (referans amaçlı)
```

## Kullanılan Yöntemler

- Regex tabanlı spam/reklam/alakasız içerik temizliği
- Türkçe'ye özel ön işleme (İ/ı karakter sorunu, stopword temizliği)
- Kinaye/ironi şüphesi tespiti
- BERT tabanlı sentiment sınıflandırma (savasy/bert-base-turkish-sentiment-cased)
- LoRA (Low-Rank Adaptation) ile parametre-verimli fine-tuning

---
Begüm Çetin — Staj Görevi
