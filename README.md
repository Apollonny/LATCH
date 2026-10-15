# LATCH

Düşük kaynaklı cihazlarda yerel muhakemeyi çevrimdışı bilgi paketleri ve canlı web erişimiyle birleştirmeyi inceleyen bir mimari öneri ve deney protokolü.

> **Durum:** Tasarım önerisi. Prototip ölçümü veya deneysel sonuç sunulmuyor; kaynak, gecikme, kalite ve güvenlik eşikleri hedef olarak tanımlanıyor.

## Mimari genel bakış

```mermaid
flowchart LR
    Q["Soru"] --> P["Politika<br/>görev · güncellik · gizlilik"]
    P -->|"Yerel"| LM["Yerel model"] --> A0["Yanıt"]
    P -->|"Bilgi gerekli"| S{"Bilgi yolu"}
    S -->|"RAM cache"| C["Önbellek"]
    S -->|"Çevrimdışı"| O["Belge paketi<br/>FTS5 / BM25"]
    S -->|"Güncel"| W["Canlı web<br/>sınırlı arama"]
    C --> E["Kanıt paketi"]
    O --> E
    W --> E
    E --> G["Yerel üretici<br/>iddialar + kaynaklar"]
    G --> V["Bağımsız NLI"]
    V -->|"Destekli"| A["Kaynaklı yanıt"]
    V -->|"Yetersiz"| X["Sınırla / çekimser kal"]

    subgraph CORE["LATCH-Core · ayrı araştırma hipotezi"]
        M["Döngülü küçük model"] --> F["Flash soğuk bellek"] --> B["Gecikme + kalite ölçümü"]
    end
```

LATCH-Web mevcut bir yerel modeli bilgi kaynakları arasında yöneten ürün hattıdır. LATCH-Core flash erişim gecikmesini hesaplama sırasında örtme hipotezini sınar; LATCH-Web’in önkoşulu değildir.

## Makale

[Türkçe makale ve deney protokolü](LATCH_makale.docx)

Makale tarihi: 15 Ekim 2026.
