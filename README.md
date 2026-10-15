# LATCH

Düşük kaynaklı cihazlarda yerel muhakemeyi çevrimdışı bilgi paketleri ve canlı web erişimiyle birleştirmeyi inceleyen bir mimari öneri ve deney protokolü.

> **Durum:** Tasarım önerisi. Prototip ölçümü veya deneysel sonuç sunulmuyor; kaynak, gecikme, kalite ve güvenlik eşikleri hedef olarak tanımlanıyor.

## Mimari genel bakış

### LATCH-Web

```mermaid
flowchart LR
    Q["Soru"] --> P["Politika<br/>görev · güncellik · gizlilik"]
    P -->|"Yerel yanıt"| L["Yerel model"] --> LA["Yanıt"]
    P -->|"Bilgi gerekli"| R{"Bilgi yolu"}
    R -->|"Cache"| C["RAM önbelleği"]
    R -->|"Çevrimdışı"| O["Belge paketi<br/>SQLite FTS5 / BM25"]
    R -->|"Güncel bilgi"| W["Sınırlı web araması"]
    C --> E["Bütçeli kanıt paketi"]
    O --> E
    W --> E
    E --> G["Yerel üretici<br/>iddialar + kaynaklar"]
    G --> V["Bağımsız NLI denetimi"]
    V -->|"Destekli"| A["Kaynaklı yanıt"]
    V -->|"Yetersiz / çelişkili"| X["Yanıtı sınırla veya çekimser kal"]
```

### LATCH-Core

```mermaid
flowchart LR
    M["Döngülü küçük model"] --> F["Flash üzerindeki soğuk bellek"] --> B["Eşit kaynak bütçelerinde gecikme ve kaliteyi ölç"]
```

LATCH-Web mevcut bir yerel modeli bilgi kaynakları arasında yöneten ürün hattıdır. LATCH-Core, flash erişim gecikmesini hesaplama sırasında örtme hipotezini sınayan ayrı bir araştırma hattıdır; LATCH-Web’in önkoşulu değildir.

## Makale

[Türkçe makale ve deney protokolü](LATCH_makale.docx)

Makale tarihi: 15 Ekim 2026.
