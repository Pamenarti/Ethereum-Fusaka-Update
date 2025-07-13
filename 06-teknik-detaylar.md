# 06 - Teknik Detaylar ve Açıklamalar

[← 05 - EVM Dönüşüm](./05-evm-donusum.md) | [Ana Sayfa](./README.md) | [07 - Ekonomik Etkiler →](./07-ekonomik-etkiler.md)

---

## Blockchain Jargonlarının Açıklamaları

Fusaka güncellemesi hakkında konuşurken karşılaşılan teknik terimlerin ayrıntılı açıklamaları:

### Temel Blockchain Kavramları

- **Blokzincir (Blockchain):** Merkezi olmayan, dağıtık bir veri tabanı. Her blok, bir önceki bloğun kriptografik özetini (hash) içerir ve zincir şeklinde birbirine bağlanır.
- **Düğüm (Node):** Blokzincir ağında çalışan, işlemleri doğrulayan ve blokları saklayan bilgisayar.
- **Durum (State):** Blokzincirin o anki tüm hesap bakiyeleri, kontrat verileri ve diğer zincir üstü bilgilerin tamamı.
- **Gas:** Ethereum'da işlemlerin gerçekleştirilmesi için ödenen işlem ücretini temsil eden birim.

### Ethereum-Spesifik Terimler

- **Ethereum Virtual Machine (EVM):** Ethereum ağı üzerinde çalışan tüm akıllı kontratların yürütüldüğü sanal makine.
- **Akıllı Kontrat (Smart Contract):** Belirli koşullar gerçekleştiğinde otomatik olarak çalışan, blockchain üzerinde depolanan ve değiştirilemeyen programlar.
- **Opcode (Operation Code):** EVM'in anlayabileceği temel makine talimatları. Her opcode, toplama, veri okuma, atlama gibi belirli bir işlemi gerçekleştirir.
- **Stack (Yığın):** EVM'de işlemlerin geçici olarak tutulduğu, son giren ilk çıkar (LIFO) prensibiyle çalışan veri yapısı.

### Veri Yapıları ve Algoritmalar

- **Merkle Patricia Trie:** Ethereum'un geleneksel olarak kullandığı, verileri organize etmek ve hızlıca doğrulamak için tasarlanmış bir ağaç veri yapısı.
- **Verkle Ağacı:** Merkle Patricia Trie'nin yerini alacak, daha verimli ve küçük kanıtlar üreten yeni nesil bir veri yapısı.
- **Polinomial Commitment:** Birden fazla verinin tek bir özetle temsil edilmesini ve daha sonra bu verilerden herhangi birinin doğrulanabilmesini sağlayan şifreleme yöntemi.
- **Kriptografik Kanıt (Proof):** Bir verinin blokzincirde gerçekten bulunduğunu veya belirli bir değere sahip olduğunu matematiksel olarak ispatlayan veri.

### Ölçeklenebilirlik Çözümleri

- **Layer 2:** Ana blok zincirinin (Layer 1) üzerinde çalışan, ölçeklenebilirlik ve maliyet avantajı sağlayan ek protokoller.
- **Rollup:** Ethereum gibi ana zincirin üzerinde çalışan, işlemleri topluca işleyip özetini ana zincire gönderen ikinci katman çözümleri.
- **Validator (Doğrulayıcı):** Blok zincirinde işlemleri doğrulayan ve yeni blokları oluşturan katılımcılar.
- **Finality (Kesinleşme):** Bir işlemin blok zincirinde geri alınamaz şekilde kalıcı hale gelmesi.

### Geliştirici Araçları ve Teknolojiler

- **Deploy (Yükleme):** Bir akıllı kontratın Ethereum ağına yüklenmesi ve çalışmaya hazır hale getirilmesi işlemi.
- **Debugging (Hata Ayıklama):** Yazılım geliştirme sürecinde, kodda bulunan hataların tespit edilip düzeltilmesi işlemi.
- **Compiler (Derleyici):** Yüksek seviyeli programlama dilinde yazılan kodu, EVM'in anlayabileceği bytecode'a dönüştüren yazılım.
- **JSON-RPC:** Ethereum düğümleriyle iletişim kurmak için kullanılan standart bir protokol.

### Merkeziyetsizlik ve Güvenlik

- **Stateless Client:** Tüm blokzincir durumunu saklamadan, sadece gerekli kanıtlarla işlemleri doğrulayabilen istemci türü.
- **Introspection (İç Gözlem):** Bir akıllı kontratın kendi kodunu veya başka bir kontratın kodunu çalışma zamanında incelemesi veya analiz etmesi işlemi.
- **Merkeziyetsizlik (Decentralization):** Bir ağın veya sistemin kontrolünün tek bir otoriteye bağlı olmadan, birçok katılımcı arasında dağıtılmış olması.

### Web3 ve DApp Ekosistemi

- **DApp (Decentralized Application):** Merkeziyetsiz uygulama; blockchain üzerinde çalışan, merkezi bir sunucuya bağlı olmayan yazılımlar.
- **Web3:** Blockchain ve merkeziyetsiz teknolojilerle çalışan yeni nesil internet uygulamalarını ifade eder.
- **NFT (Non-Fungible Token):** Benzersiz dijital varlıkları temsil eden, blok zincirinde saklanan tokenlar.
- **DeFi (Decentralized Finance):** Merkeziyetsiz finans; geleneksel finansal hizmetlerin blockchain üzerinde sunulması.

### Oracle ve Köprü Teknolojileri

- **Oracle:** Blockchain dışı verileri akıllı kontratlara aktaran sistem.
- **Cross-chain Bridge:** Farklı blockchain ağları arasında varlık transferi sağlayan protokol.
- **Indexing Service:** Blockchain verilerini düzenleyip hızlı erişim sağlayan servisler.

---

## Veri Tekilleştirme ve Sıkıştırma

Verkle ağaçları, Ethereum'un veri saklama ve erişim süreçlerinde devrim niteliğinde değişiklikler getirmektedir:

### Optimize Edilmiş Veri Yapısı

- **Yüksek Dallanma Faktörü:** Her bir düğüm, çok daha fazla çocuğa sahip olabilir, bu da ağaç derinliğini azaltır ve kanıtların daha kısa olmasını sağlar.
- **Veri Tekilleştirme:** Aynı veriler tekrar tekrar saklanmaz, gereksiz veri tekrarları önlenir.
- **Uzun Vadeli Sürdürülebilirlik:** Blokzincirin boyutu daha yavaş büyür, bu da ağın uzun vadede daha sürdürülebilir olmasını sağlar.

### Stateless Client Teknolojisi

Verkle ağaçları ve stateless client teknolojisi, Ethereum'un ölçeklenebilirliğini, merkeziyetsizliğini ve sürdürülebilirliğini büyük ölçüde artıracak. Bu yenilikler sayesinde:

- Blokzincir teknolojisi daha erişilebilir, hızlı ve güvenli hale gelir
- Ağın uzun vadeli büyümesi kontrol altına alınır
- Her seviyeden kullanıcı ve geliştirici için daha iyi deneyim sağlanır

---

## Kod ve Veri Ayrımı

Geleneksel Ethereum Sanal Makinesi'nde (EVM), akıllı kontratların kodu ve verisi aynı bölümde, iç içe geçmiş şekilde saklanıyordu. EOF ile gelen yenilikler:

### Gelişmiş Güvenlik

- **Kod ve veri bölümleri açıkça ayrılır:** Akıllı kontratın yürütülebilir kodu ile sabit verileri farklı bölümlerde tutulur
- **Daha verimli kod doğrulaması:** Kontratın yüklenmesi sırasında kodun geçerliliği ve güvenliği daha kolay doğrulanabilir
- **Güvenlik açıklarının önlenmesi:** Kodun veriyle karışması sonucu oluşabilecek saldırı yüzeyi daraltılır

### Statik Jump'lar ve Fonksiyon Desteği

- **Dinamik jump'lar yasaklanır:** Kodun çalışma zamanında rastgele bir noktaya atlaması engellenir
- **Statik göreceli jump'lar (RJUMP/RJUMPI):** Kodun kontrol akışı daha öngörülebilir ve analiz edilebilir hale gelir
- **Fonksiyon çağrıları ve tail call desteği:** JUMPF komutu ile fonksiyonlar arasında doğrudan atlama yapılabilir
- **Stack doğrulaması:** Yığın üzerinde yapılan işlemlerin doğruluğu otomatik olarak kontrol edilir

---

[← 05 - EVM Dönüşüm](./05-evm-donusum.md) | [Ana Sayfa](./README.md) | [07 - Ekonomik Etkiler →](./07-ekonomik-etkiler.md)
