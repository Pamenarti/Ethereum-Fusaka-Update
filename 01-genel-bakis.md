# 1. Genel Bakış: Ethereum'un Evrimsel Sıçrayışı

## Ethereum'un Evrimsel Sıçrayışı

Ethereum ağı, 2015'teki lansmanından bu yana sürekli olarak kendini geliştirmeye devam etmektedir. Pectra güncellemesinin ardından gelen Fusaka güncellemesi, Ethereum'un şimdiye kadar yaşadığı en kapsamlı ve dönüştürücü güncellemelerden biri olarak tarihe geçmeye hazırlanıyor. Bu güncelleme, sadece teknik iyileştirmeler değil, aynı zamanda Ethereum ekosisteminin tamamını yeniden şekillendirecek köklü değişiklikler getirmektedir.

Fusaka güncellemesi, iki ana bileşenden oluşmaktadır: Fulu (Consensus Layer - Mutabakat Katmanı) ve Osaka (Execution Layer - Yürütme Katmanı). Bu ikili yapı, Ethereum'un hem ölçeklenebilirlik hem de verimlilik açısından yaşadığı temel sorunlara kapsamlı çözümler sunmayı hedeflemektedir.

---

## Fusaka'nın Ana Bileşenleri ve Teknik Altyapısı

### 1. PeerDAS (Peer-to-Peer Data Availability Sampling): Veri Erişilebilirliğinde Devrim

PeerDAS teknolojisi, Ethereum'un veri işleme yaklaşımında köklü bir değişiklik getirmektedir. Geleneksel sistemde, her doğrulayıcı (validator) tüm veri bloklarını (data blobs) indirmek ve saklamak zorundaydı. Bu durum, ağ üzerinde büyük bir yük oluşturuyor ve ölçeklenebilirlik sorunlarına yol açıyordu.

#### PeerDAS'ın Çalışma Mekanizması:

PeerDAS sistemi, veri erişilebilirlik sorumluluklarını rastgele örnekleme yoluyla dağıtır. Bu yaklaşımda:

- **Parçalı Veri İndirme**: Düğümler, tam veri bloklarını değil, yalnızca küçük veri parçalarını indirirler
- **Rastgele Örnekleme**: Her doğrulayıcı, ağdaki verilerin rastgele bir örneğini alır
- **Dağıtık Doğrulama**: Veri bütünlüğü, merkezi bir otoriteye ihtiyaç duymadan teyit edilir

#### Ölçeklenebilirlik Faydaları:

Bu sistem sayesinde Ethereum, blok başına veri kapasitesini güvenli bir şekilde artırabilir. Bu da Layer 2 rollup'ları için önemli faydalar sağlar:

- **Düşük İşlem Ücretleri**: Rollup'ların veri depolama maliyetleri önemli ölçüde azalır
- **Yüksek Throughput**: Saniye başına işlem kapasitesi dramatik olarak artar
- **Merkeziyetsizliğin Korunması**: Düğüm operatörleri için donanım gereksinimleri makul seviyelerde kalır

---

### 2. Verkle Ağaçları: Durum Yönetiminde Paradigma Değişimi

Verkle ağaçları, Ethereum blokzincirinin mevcut **Merkle Patricia Trie** (MPT) yapısını tamamen değiştiren, blokzincir teknolojisinde çığır açıcı bir gelişmedir. Bu yenilik, blokzincirin **durum verilerini** (yani akıllı kontratların bakiyeleri, depolanan veriler, hesaplar ve diğer zincir üstü bilgileri) nasıl sakladığı ve doğruladığı konusunda köklü bir dönüşüm sağlar.

#### Verkle Ağaçlarının Temel Özellikleri ve Avantajları

**Küçük Kriptografik Kanıtlar (Proof Boyutları)**

Blokzincirlerde, bir hesabın veya kontratın belirli bir durumda olduğunu kanıtlamak için **kriptografik kanıtlar** (proofs) kullanılır. Geleneksel Merkle Patricia Trie yapısında, bu kanıtlar oldukça büyüktür ve çok sayıda veri içerebilir. **Verkle ağaçları** ise, daha gelişmiş bir **polynomial commitment** (çok terimli taahhüt) şeması kullanarak, çok daha küçük ve verimli kanıtlar üretir.

**Stateless Client'lar (Durumsuz İstemciler)**

Verkle ağaçlarının getirdiği en önemli yeniliklerden biri, **stateless client** (durumsuz istemci) konseptidir. Geleneksel olarak, bir Ethereum düğümü (node), tüm blokzincir geçmişini ve mevcut tüm hesap/kontrat durumunu saklamak zorundadır.

**Stateless client** yaklaşımında ise, düğümler tüm durumu saklamak zorunda değildir. Bunun yerine, ihtiyaç duydukları anda, ilgili küçük kanıtları (proofs) kullanarak işlemleri doğrulayabilirler.

---

### 3. EOF (Ethereum Object Format): EVM'de Yapısal Dönüşüm

EOF, Ethereum Sanal Makinesi'nin (EVM) mimarisinde köklü bir yeniden yapılanma sağlayan, akıllı kontratların yazımı, dağıtımı ve çalıştırılması süreçlerinde devrim niteliğinde değişiklikler getiren bir güncellemedir.

#### Kod ve Veri Ayrımı

Geleneksel Ethereum Sanal Makinesi'nde (EVM), akıllı kontratların kodu (yürütülebilir talimatlar) ve verisi (sabit bilgiler, lookup tabloları gibi) aynı bölümde, iç içe geçmiş şekilde saklanıyordu. Bu durum, kodun analizini ve güvenliğini zorlaştırıyor, potansiyel güvenlik açıklarına yol açıyordu.

**EOF ile gelen yenilikler:**
- **Kod ve veri bölümleri açıkça ayrılır**: Akıllı kontratın yürütülebilir kodu ile sabit verileri farklı bölümlerde tutulur
- **Daha verimli kod doğrulaması**: Kod ve veri ayrımı sayesinde, kontratın yüklenmesi sırasında kodun geçerliliği ve güvenliği daha kolay ve hızlı şekilde doğrulanabilir
- **Güvenlik açıklarının önlenmesi**: Kodun veriyle karışması sonucu oluşabilecek saldırı yüzeyi daraltılır

---

## Blockchain Terimleri ve Jargonlarının Açıklamaları

### Temel Kavramlar
- **Blockchain (Blokzincir)**: Verilerin merkeziyetsiz, değiştirilemez ve şeffaf şekilde saklandığı dijital defter teknolojisi
- **Validator (Doğrulayıcı)**: Blokzincirde işlemleri doğrulayan ve yeni blokları oluşturan katılımcı
- **Node (Düğüm)**: Ethereum ağında işlemleri doğrulayan ve blokları saklayan bilgisayar
- **Smart Contract (Akıllı Kontrat)**: Belirli koşullar gerçekleştiğinde otomatik olarak çalışan, blockchain üzerinde depolanan programlar

### Teknik Terimler
- **Data Blobs**: Blokzincire eklenen büyük veri blokları, genellikle Layer 2 çözümlerinde kullanılır
- **Layer 2**: Ana blokzincirin üzerinde çalışan, işlemleri daha hızlı ve ucuz şekilde işleyen ek protokoller
- **Rollup**: Layer 2 çözümlerinin bir türü; işlemleri ana zincir dışında toplar ve özetini ana zincire gönderir
- **Gas**: Ethereum'da işlemlerin gerçekleştirilmesi için ödenen işlem ücretini temsil eden birim
- **Throughput**: Bir ağın belirli bir zaman diliminde işleyebileceği işlem sayısı

### Veri Yapıları
- **Merkle Patricia Trie**: Ethereum'un geleneksel veri saklama yapısı
- **Verkle Tree**: Yeni nesil, daha verimli veri saklama yapısı
- **Polynomial Commitment**: Birden fazla verinin tek bir özetle temsil edilmesini sağlayan şifreleme yöntemi
- **Proof (Kanıt)**: Bir verinin doğruluğunu matematiksel olarak ispatlayan veri parçası

---

## Fusaka'nın Beklenen Etkileri

### Kısa Vadeli Etkiler (2025-2026)
- **İşlem Ücretlerinde Dramatik Azalma**: $50-200'den $0.01-0.10'a düşüş
- **DeFi Erişilebilirliğinin Artması**: Küçük yatırımcılar için kapıların açılması
- **NFT Üretiminin Demokratikleşmesi**: Düşük maliyetli NFT oluşturma imkanı

### Uzun Vadeli Etkiler (2027+)
- **Kurumsal Benimsemenin Hızlanması**: Fortune 500 şirketlerinin blokzincir entegrasyonu
- **Yeni Uygulama Kategorileri**: Gerçek zamanlı uygulamalar, mikro-ödemeler
- **Küresel Ekonomik Katılım**: Finansal sistemlerin demokratikleşmesi

---

## Sonraki Adımlar

Bu genel bakışın ardından, aşağıdaki bölümlerde Fusaka'nın her bir bileşenini derinlemesine inceleyeceğiz:

1. **[EOF Seçenekleri](02-eof-secenekleri.md)** - Dört farklı teknik yaklaşım
2. **[PeerDAS Detayları](03-peerdas.md)** - Veri erişilebilirliği teknolojisi
3. **[Verkle Ağaçları](04-verkle-agaclari.md)** - Durum yönetimi devrimi

---

*[Sonraki Bölüm: EOF Seçenekleri →](02-eof-secenekleri.md)*
