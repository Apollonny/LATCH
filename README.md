# LATCH

Düşük kaynaklı cihazlarda yerel muhakemeyi çevrimdışı bilgi paketleri ve canlı web erişimiyle birleştirmeyi inceleyen bir mimari öneri ve deney protokolü.

> **Durum:** Tasarım önerisi. Belge prototip ölçümü veya deneysel sonuç sunmuyor; kaynak, gecikme, kalite ve güvenlik eşikleri hedef olarak tanımlanıyor.

## Mimari genel bakış

```mermaid
flowchart LR
    U["Kullanıcı sorusu"] --> P["Politika katmanı<br/>görev · güncellik · gizlilik"]

    P -->|"Dış bilgi gerekmiyor"| LM["Yerel model"]
    LM --> A0["Yanıt"]

    P --> C["RAM önbelleği"]
    C -->|"Geçerli kayıt"| E["Bütçeli kanıt paketi"]
    C -->|"Eksik veya eski kayıt"| R{"Bilgi yolu"}
    R -->|"Çevrimdışı"| O["Lisansı denetlenmiş belge paketi<br/>SQLite FTS5 / BM25"]
    R -->|"Güncel bilgi"| W["Canlı web araması<br/>sınırlı sorgular"]
    O --> E
    W --> E

    E --> G["Yerel üretici model<br/>iddialar + kaynak kimlikleri"]
    G --> V["Bağımsız NLI kanıt denetimi"]
    V -->|"Destekleniyor"| A["Kaynaklarıyla yanıt"]
    V -->|"Yetersiz veya çelişkili"| Q["Yanıtı sınırla, iddiayı çıkar veya çekimser kal"]

    subgraph CORE["LATCH-Core · ayrı araştırma hipotezi"]
        M["Döngülü küçük model"] --> F["Flash üzerindeki soğuk bellek"]
        F --> B["Eşit kaynak bütçelerinde gecikme ve kaliteyi ölç"]
    end

    classDef product fill:#e8f2ff,stroke:#315b8a,color:#13283f
    classDef research fill:#f2edff,stroke:#7050a0,color:#24183a
    class P,C,E,G,V product
    class M,F,B research
```

LATCH-Web, mevcut bir yerel modeli bilgi kaynakları arasında yöneten ürün hattıdır. LATCH-Core ise flash belleğe erişim gecikmesinin hesaplama sırasında örtülüp örtülemeyeceğini sınayan bağımsız bir araştırma hipotezidir; LATCH-Web’in önkoşulu değildir.

## Makale

[Türkçe makale ve deney protokolü](LATCH_makale.docx)

Makale tarihi: 15 Ekim 2026.
