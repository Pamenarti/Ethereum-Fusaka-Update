# 3. PeerDAS Teknolojisi: Veri Erişilebilirliğinde Devrim

## PeerDAS: Peer-to-Peer Data Availability Sampling

PeerDAS (Peer-to-Peer Data Availability Sampling), Ethereum'un ölçeklenebilirlik sorunlarını çözmek için geliştirilmiş yenilikçi bir teknolojik çözümdür. Bu sistem, veri erişilebilirliğini sağlarken aynı zamanda ağın merkeziyetsizliğini koruyor ve doğrulayıcılar (validator) üzerindeki yükü dramatik şekilde azaltıyor.

---

## PeerDAS'ın Temel Çalışma Prensibi

### Geleneksel Sistemin Sınırları

Ethereum'un mevcut sisteminde, her doğrulayıcı tüm veri bloklarını (data blobs) indirmek ve saklamak zorundadır. Bu yaklaşım:

- **Yüksek Bant Genişliği Gereksinimi**: Her doğrulayıcı için GB'larca veri indirme
- **Depolama Maliyetleri**: Sürekli artan veri saklama ihtiyacı
- **Ağ Yoğunluğu**: Aynı verinin binlerce kez kopyalanması
- **Ölçeklenebilirlik Engelı**: Ağ büyüdükçe donanım gereksinimlerinin artması

### PeerDAS Çözümü

PeerDAS, bu sorunları **rastgele örnekleme** (random sampling) ve **erasure coding** (silme kodlama) teknikleriyle çözer:

```
Geleneksel Sistem:    PeerDAS Sistemi:
Node 1: [A][B][C]     Node 1: [A]
Node 2: [A][B][C] →   Node 2: [B]
Node 3: [A][B][C]     Node 3: [C]
Node 4: [A][B][C]     Node 4: [A']
```

---

## Matematiksel Temeli: Erasure Coding Teorisi

### Reed-Solomon Kodlaması

PeerDAS, veri güvenliğini **Reed-Solomon kodlaması** ile sağlar:

- **Orijinal veri**: k adet parçaya bölünür
- **Yedek parçalar**: n-k adet ek parça oluşturulur
- **Toplam parça sayısı**: n parça (n > k)
- **Kurtarma garantisi**: Herhangi k adet parça, orijinal veriyi tamamen geri getirebilir

**Ethereum'da Örnek Parametreler:**
- k = 4096 (orijinal parçalar)
- n = 8192 (toplam parçalar)
- Yedeklilik oranı: %50

### Veri Erişilebilirliği Olasılığı

Bir verinin ağda erişilebilir olma olasılığı:

```
P(available) = 1 - (1 - p)^r
```

**Burada:**
- **p**: Tek bir düğümün veriye erişilebilir olma olasılığı
- **r**: Yedek (redundant) parça sayısı
- **Hedef**: %99.99 erişilebilirlik oranı

---

## Custody Groups: Veri Sorumluluğu Dağıtımı

### Custody Group Sisteminin Çalışması

PeerDAS'ta doğrulayıcılar, **custody groups** (saklama grupları) adı verilen alt gruplara ayrılır:

```
Ethereum Ağı (Örnek: 1,000,000 validator)
├── Custody Group 1 (10,000 validator) → Veri Parçası A
├── Custody Group 2 (10,000 validator) → Veri Parçası B
├── Custody Group 3 (10,000 validator) → Veri Parçası C
└── ... (100 grup toplam)
```

### Custody Sisteminin Avantajları

- **Yük Dağılımı**: Her doğrulayıcı sadece toplam verinin %1'ini saklar
- **Güvenlik**: Birden fazla grup aynı veri parçasını yedekler
- **Esneklik**: Gruplar arası veri paylaşımı mümkün
- **Ölçeklenebilirlik**: Ağ büyüdükçe gruplar yeniden organize edilebilir

---

## Ağ Protokolleri ve Veri Yayılımı

### Yeni Gossip Protokolleri

PeerDAS, veri hücrelerinin (cell) ağda hızlı ve güvenli şekilde yayılması için gelişmiş **gossip protocols** (dedikodu protokolleri) kullanır:

```
Veri Yayılım Süreci:
1. Validator A → Veri parçasını custody group'a gönderir
2. Custody Group → Komşu gruplara yayar
3. Komşu Gruplar → Tüm ağa dağıtır
4. Doğrulama → İhtiyaç halinde parçalar birleştirilir
```

### Bant Genişliği Optimizasyonu

**Geleneksel Sistem:**
- Her doğrulayıcı: O(n) bant genişliği
- Toplam ağ yükü: O(n²)

**PeerDAS Sistemi:**
- Her doğrulayıcı: O(√n) bant genişliği
- Toplam ağ yükü: O(n√n)
- **Sonuç**: %90+ verimlilik artışı

---

## Güvenlik Modeli ve Saldırı Senaryoları

### Data Availability Attacks (Veri Erişilebilirlik Saldırıları)

**Saldırı Türleri:**
1. **Withholding Attack**: Kötü niyetli doğrulayıcılar veri parçalarını saklar
2. **Corruption Attack**: Veri parçaları kasıtlı olarak bozulur
3. **Coordination Attack**: Birden fazla custody group işbirliği yapar

**Savunma Mekanizmaları:**
- **Slashing**: Kötü davranış cezalandırılır
- **Redundancy**: Fazladan veri kopyaları
- **Fraud Proofs**: Yanlış veri tespit sistemi
- **Economic Incentives**: Doğru davranış ödüllendirilir

### Ağ Bölünmesi (Network Partitioning) Riskleri

**Potansiyel Sorunlar:**
- Custody group izolasyonu
- Veri parçalarına geçici erişim kaybı
- Ağ senkronizasyon sorunları

**Çözüm Stratejileri:**
- Otomatik yeniden dağıtım
- Cross-group veri yedekleme
- Hızlı ağ iyileştirme protokolleri

---

## Performans Metrikleri ve Karşılaştırmalar

### Mevcut Durum vs PeerDAS

| Metrik | Mevcut Sistem | PeerDAS | İyileştirme |
|--------|---------------|---------|-------------|
| **Validator Veri Yükü** | 100% | 1% | 99% azalma |
| **Ağ Bant Genişliği** | O(n²) | O(n√n) | ~90% azalma |
| **Depolama Gereksinimi** | Tam veri | Parçalı veri | 99% azalma |
| **Senkronizasyon Süresi** | Saatler | Dakikalar | 95% iyileştirme |
| **Donanım Maliyeti** | Yüksek | Düşük | 80% azalma |

### Layer 2 Rollup'larına Etki

**Rollup İşlem Maliyetleri:**
- **Öncesi**: $10-50 per rollup batch
- **Sonrası**: $0.10-1.00 per rollup batch
- **Sonuç**: 50-100x maliyet azalması

---

## Uygulama Örnekleri ve Senaryolar

### Senaryo 1: DeFi Uygulaması

**Önceki Durum:**
- Uniswap swap işlemi: $25 gas ücreti
- Günlük işlem hacmi: 100,000 işlem
- Toplam kullanıcı maliyeti: $2.5M/gün

**PeerDAS Sonrası:**
- Uniswap swap işlemi: $0.25 gas ücreti
- Günlük işlem hacmi: 1,000,000 işlem (10x artış)
- Toplam kullanıcı maliyeti: $250K/gün (90% azalma)

### Senaryo 2: NFT Marketplace

**Önceki Durum:**
- NFT mint maliyeti: $50-100
- Günlük mint sayısı: 1,000 NFT
- Sadece büyük koleksiyonlar ekonomik

**PeerDAS Sonrası:**
- NFT mint maliyeti: $0.50-1.00
- Günlük mint sayısı: 100,000 NFT
- Bireysel sanatçılar için erişilebilir

---

## Teknik İmplementasyon Detayları

### Client Güncellemeleri

**Gerekli Değişiklikler:**
```bash
# Consensus Layer (Beacon Chain)
- Custody assignments
- Data availability sampling
- Blob verification

# Execution Layer
- Blob transaction processing
- Data retrieval protocols
- Storage management
```

### Ağ Protokol Güncellemeleri

**Yeni Protocol Messages:**
- `BlobsSidecar`: Veri parçalarını taşır
- `DataColumnsByRange`: Veri sütunları talep eder
- `CustodyColumns`: Saklama sorumluluklarını bildirير

---

## Gelecek Gelişmeler

### Roadmap ve İyileştirmeler

**Kısa Vadeli (2025-2026):**
- Mainnet aktivasyonu
- Client optimizasyonları
- Monitoring ve analytics

**Orta Vadeli (2026-2027):**
- Data availability artışı
- Cross-shard communication
- Advanced fraud proofs

**Uzun Vadeli (2027+):**
- Quantum-resistant updates
- Interchain data availability
- Automated parameter tuning

---

## Blockchain Terimleri ve Jargonlar

### Temel Kavramlar
- **Data Availability**: Veri erişilebilirliği; blokzincir verilerinin ağda mevcut olma durumu
- **Validator**: Blokzincirde işlemleri doğrulayan ve yeni blokları oluşturan katılımcı
- **Sampling**: Örnekleme; büyük veri setinden küçük parçalar alarak analiz yapma
- **Erasure Coding**: Veri kaybını önlemek için fazladan veri parçaları ekleme tekniği

### Teknik Terimler
- **Data Blobs**: Layer 2 çözümlerinin kullandığı büyük veri blokları
- **Custody Group**: Belirli veri parçalarını saklamakla sorumlu doğrulayıcı grubu
- **Gossip Protocol**: Ağdaki düğümlerin veri paylaşımı için kullandığı iletişim protokolü
- **Reed-Solomon**: Hata düzeltme ve veri kurtarma için kullanılan matematiksel algoritma

### Güvenlik Kavramları
- **Slashing**: Kötü davranış gösteren doğrulayıcıların cezalandırılması
- **Fraud Proof**: Yanlış bilgi veya işlemin matematiksel kanıtla tespit edilmesi
- **Withholding Attack**: Veri parçalarının kasıtlı olarak saklanması saldırısı
- **Network Partition**: Ağın farklı kısımlarının birbirinden izole olması

### Performans Metrikleri
- **Throughput**: Birim zamanda işlenebilen işlem sayısı
- **Latency**: Bir işlemin tamamlanması için geçen süre
- **Bandwidth**: Ağ üzerinden birim zamanda aktarılabilen veri miktarı
- **Redundancy**: Veri güvenliği için eklenen fazladan kopya oranı

---

*[← Önceki Bölüm: EOF Seçenekleri](02-eof-secenekleri.md) | [Sonraki Bölüm: Verkle Ağaçları →](04-verkle-agaclari.md)*
