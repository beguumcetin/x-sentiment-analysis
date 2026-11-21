[English](README.md) | Türkçe

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

## Veri hakkında

Tweet dosyaları burada yayımlanmıyor: X'in geliştirici koşulları tweet içeriğinin yeniden dağıtımını kısıtlıyor ve dosyalarda hesap kimlikleri var. Notebook'taki kayıtlı çıktılar da aynı nedenle temizlendi. Kod, ince ayar yapılmış LoRA adaptörü ve dashboard dahil; notebook'u yeniden çalıştırmak için `veri/` içine kendi tweet toplamanızı koymanız gerekir.

## Klasör Yapısı

```
İTO_sentiment_analysisV2.ipynb   ana çalışma notebook'u
dashboard.html                    interaktif sonuç dashboard'u
veri/                             ham/kaynak veriler (tweet dosyaları bu depoda yok)
ciktilar/                         üretilen sonuç dosyaları (tweet metni içerenler bu depoda yok)
model/                            fine-tune edilmiş LoRA adaptörü ve ön işleme modülü
eski_denemeler/                   bırakılan alternatif model denemesi (referans amaçlı)
```

## Kullanılan Yöntemler

- Regex tabanlı spam/reklam/alakasız içerik temizliği
- Türkçe'ye özel ön işleme (İ/ı karakter sorunu, stopword temizliği)
- Kinaye/ironi şüphesi tespiti
- BERT tabanlı sentiment sınıflandırma (savasy/bert-base-turkish-sentiment-cased)
- LoRA (Low-Rank Adaptation) ile parametre-verimli fine-tuning

## Rakamlarla ilgili not

Tablodaki iki sütun birebir karşılaştırılabilir değil. "Öncesi" rakamları 208 satırlık gold-standard verinin tamamında, "sonrası" rakamları ise bu verinin eğitime girmeyen %20'lik doğrulama kısmında (42 tweet: 20 negatif, 13 nötr, 9 pozitif) ölçüldü. Bu kadar küçük bir örnekte tek bir tweet sınıf başına birkaç puan oynatır; bu yüzden sonuçları kesin bir kazanç olarak değil, yön gösteren bir işaret olarak okumak gerekir. Aynı doğrulama kümesinde taban modelin skorunu ayrıca ölçmek karşılaştırmayı sağlamlaştırırdı.

---
Begüm Çetin — Staj Görevi

## İletişim

Begüm Çetin · begumcetin22@gmail.com · [GitHub](https://github.com/beguumcetin)
