# 2. EOF Seçenekleri: Ethereum'un Gelecek Mimarisi

## EOF Fusaka Seçenekleri: Ethereum'un Gelecek Mimarisi

EVM Nesne Formatı (EOF), Ethereum topluluğu içinde süregelen bir tartışmaya neden olmuştur. Bu format, Ethereum Sanal Makinesi'nin (EVM) yapısını modernize etmeyi ve gelecekteki protokol güncellemelerini mümkün kılmayı amaçlamaktadır. All-Core-Devs Execution çağrısı (ACDE) kolaylaştırıcısı Tim Beiko'nun isteği üzerine hazırlanan bu belge, EOF ile nasıl ilerleyeceğimize dair dört net seçenek sunmaktadır:

- **(A) - Tam EOF**: Önerilen tüm özelliklere sahip kapsamlı revizyon
- **(B) - Minimal EOF**: Shanghai dönemindeki öneriye dayalı yalın versiyon  
- **(C) - Temel EOF**: Özellikleri ve uygulanabilirliği dengeleyen orta yol
- **(D) - İç Gözlem EOF**: Gas İç Gözlem temasını kaldıran modifiye edilmiş yaklaşım

---

## Dört Farklı EOF Seçeneğinin Detaylı Analizi

### (A) - Tam EOF (Complete EOF): Kapsamlı Modernizasyon

Bu seçenek, Ethereum Virtual Machine (EVM) mimarisinde köklü bir dönüşüm hedefler ve mevcut "Osaka" meta spesifikasyonunda tanımlanan tüm yenilikleri içerir. Tam EOF, Ethereum'un gelecekteki ölçeklenebilirlik, güvenlik ve geliştirici deneyimi hedeflerine ulaşabilmesi için tasarlanmıştır.

#### Tam EOF'un Tasarım Felsefesi ve Gelişim Süreci

Tam EOF, Ethereum topluluğunun önde gelen isimlerinden gelen çeşitli geri bildirimlerin ve taleplerin birleşiminden doğmuştur. Ethereum'un kurucusu Vitalik Buterin'in kod iç gözlemini (contract introspection) yasaklama önerisi, Vyper programlama dili ekibinin EXCHANGE stack operasyonu talebi ve Solidity ekibinin JUMPF ile tail call (fonksiyonun sonundan başka bir fonksiyona atlama) desteği gibi istekler, bu seçeneğin şekillenmesinde belirleyici olmuştur.

#### eof-devnet-0 Kapsamındaki EIP'ler ve Açıklamaları

**Temel Yapısal EIP'ler**

- **EIP-3540: EOF - EVM Object Format v1**
    - *Açıklama:* Ethereum Virtual Machine (EVM) için yeni bir nesne formatı (EOF) tanımlar. Bu format, akıllı kontratların kod ve veri bölümlerini birbirinden ayırır.
    - *Faydası:* Kod ve veri karışıklığını önler, saldırı yüzeyini azaltır, derleyicilerin ve analiz araçlarının daha güvenli kontratlar üretmesini sağlar.

- **EIP-3670: EOF - Code Validation**
    - *Açıklama:* Akıllı kontrat kodunun deploy (ağa yükleme) aşamasında otomatik olarak doğrulanmasını zorunlu kılar.
    - *Faydası:* Hatalı veya potansiyel olarak tehlikeli kontratların ağa yüklenmesini engeller, güvenliği artırır.

- **EIP-4200: EOF - Static Relative Jumps**
    - *Açıklama:* Geleneksel EVM'de kullanılan dinamik atlama komutları (JUMP, JUMPI) yerine, statik ve göreceli atlama komutları getirir.
    - *Faydası:* Kodun analizini ve doğrulanmasını kolaylaştırır, JUMPDEST gibi işaretçilerin gerekliliğini ortadan kaldırarak kod boyutunu küçültür.

**Gelişmiş Fonksiyonalite EIP'leri**

- **EIP-4750: EOF - Functions**
    - *Açıklama:* Akıllı kontratlarda fonksiyonel programlama desteği sağlar. Her fonksiyonun giriş ve çıkış parametreleri ile stack üzerindeki etkisi açıkça belirtilir.
    - *Faydası:* Kodun okunabilirliğini ve bakımını kolaylaştırır, daha büyük ve karmaşık uygulamaların güvenli şekilde geliştirilmesini sağlar.

- **EIP-5450: EOF - Stack Validation**
    - *Açıklama:* Stack (yığın) üzerinde yapılan işlemlerin doğruluğunu, kod deploy edilirken kontrol eder.
    - *Faydası:* Çalışma zamanında ortaya çıkabilecek kritik hataları önceden engeller, kontratların daha güvenli olmasını sağlar.

---

### (B) - Minimal EOF: Sadelik ve Uyumluluk Önceliği

Minimal EOF, Ethereum Virtual Machine (EVM) için önerilen en sade ve uyumlu güncelleme yaklaşımıdır. Bu seçenek, 2022 yılında Şanghay (Shanghai) dönemi için planlanan orijinal vizyona sadık kalır ve yalnızca en temel değişiklikleri içerir.

#### Minimal EOF'un Temel Özellikleri ve Felsefesi

Minimal EOF, karmaşıklığı azaltmak ve mevcut sistemlerle geriye dönük uyumluluğu (backward compatibility) ön planda tutmak için tasarlanmıştır. Bu yaklaşımda, yalnızca en gerekli teknik iyileştirmeler ve güvenlik önlemleri uygulanır.

#### Temel Ethereum İyileştirme Önerileri (EIP'ler)

- **EIP-3540: EOF - EVM Object Format v1** - Kod ve veri bölümlerinin ayrılması
- **EIP-3670: EOF - Code Validation** - Otomatik kod doğrulama
- **EIP-4200: EOF - Static Relative Jumps** - Statik atlama komutları
- **EIP-4750: EOF - Functions** - Fonksiyonel programlama desteği
- **EIP-5450: EOF - Stack Validation** - Yığın doğrulama

#### Yasaklanan Opcode'lar ve Gerekçeleri

**JUMP ve JUMPI (Dinamik Atlamalar)**
- Kodun analiz edilmesini ve doğrulanmasını zorlaştırdığı için yasaklanır
- Statik atlamalar (RJUMP/RJUMPI) ile değiştirilir

**PC (Program Counter)**
- Statik atlamaların kullanılmasıyla gereksiz hale gelir

**SELFDESTRUCT ve CALLCODE**
- Güvenlik açıklarına yol açtığı için yasaklanır
- Modern alternatifler (DELEGATECALL) ile değiştirilir

---

### (C) - Temel EOF (Baseline EOF): Dengeli Modernizasyon

Temel EOF (Ethereum Nesne Formatı), yenilikçi özellikler ile mevcut ekosistemin istikrarı arasında denge kuran, orta yol niteliğinde bir güncelleme seçeneğidir. Bu seçenek, kod iç gözlem (introspection) yasaklarını kaldırarak geliştiricilere daha fazla esneklik sağlar.

#### Temel EOF'un Felsefesi ve Tasarım Yaklaşımı

Temel EOF, Ethereum topluluğunda tartışmalı olan kod ve gas introspection (çalışma zamanında kodun veya gas değerlerinin sorgulanması) yasaklarını ortadan kaldırır. Böylece, mevcut akıllı kontratların ve geliştirici araçlarının yeni formata geçişi kolaylaşır.

#### Temel EOF'un Kapsamlı EIP Listesi

**Temel Yapısal Bileşenler**
- **EIP-3540: EOF - EVM Object Format v1** - Kod ve veri ayrımı
- **EIP-3670: EOF - Code Validation** - Kod doğrulama
- **EIP-4200: EOF - Static Relative Jumps** - Statik atlamalar
- **EIP-4750: EOF - Functions** - Fonksiyonel programlama
- **EIP-5450: EOF - Stack Validation** - Stack doğrulama

**Gelişmiş Özellik Katmanı**
- **EIP-7698: EOF - Creation Transaction** - Gelişmiş kontrat oluşturma
- **EIP-663: SWAPN, DUPN and EXCHANGE Instructions** - Stack manipülasyonu
- **EIP-6206: EOF - JUMPF and Non-Returning Functions** - Tail call optimization
- **EIP-7480: EOF - Data Section Access Instructions** - Veri bölümü erişimi
- **EIP-7620: EOF Contract Creation** - EOF kontrat oluşturma

---

### (D) - İç Gözlem EOF (Introspecting EOF): Pragmatik Evrim

İç Gözlem EOF, Ethereum Virtual Machine (EVM) mimarisinde, Tam EOF (Complete EOF) seçeneğine kıyasla daha esnek ve geliştirici dostu bir yaklaşım sunan bir güncelleme alternatifidir.

#### Temel Felsefe ve Stratejik Yaklaşım

İç Gözlem EOF'un temel amacı, Ethereum ağında çalışan mevcut akıllı kontratların işlevselliğini korurken, sistemin güvenliğini ve öngörülebilirliğini artırmaktır. Bu yaklaşımda, bazı opcode'lar güvenlik ve analiz kolaylığı için yasaklanırken, geliştiricilerin sıklıkla kullandığı EXTCODE* opcode'ları tekrar kullanılabilir hale getirilmiştir.

#### Yasaklanan Opcode'lar ve Gerekçeleri

- **JUMP ve JUMPI**: Dinamik atlamaları engellemek için
- **PC**: Statik kontrol akışıyla gereksiz hale geldiği için
- **SELFDESTRUCT**: Güvenlik riskleri nedeniyle
- **CALLCODE**: Güvenlik ve öngörülebilirlik açısından riskli olduğu için

#### Kod ve Gas İç Gözlem Politikası

- **Gas İç Gözlem Temasının Kaldırılması**: Geliştiriciler gas ile ilgili bilgilere erişebilir
- **Kod İç Gözlem Temasının Sınırlandırılması**: Yalnızca bellekten yeni kod oluşturma işlemleriyle sınırlandırılmıştır
- **EXTCODE* Opcode'larının Geri Yüklenmesi**: Mevcut kontratların uyumluluğu korunur

---

## Karşılaştırma Tablosu: EIP'lerin EOF Seçeneklerine Göre Dağılımı

| EIP Numarası | Açıklama | Tam EOF | Minimal EOF | Temel EOF | İç Gözlem EOF |
|--------------|----------|---------|-------------|-----------|---------------|
| **EIP-3540** | EVM Object Format v1 | ✅ | ✅ | ✅ | ✅ |
| **EIP-3670** | Code Validation | ✅ | ✅ | ✅ | ✅ |
| **EIP-4200** | Static Relative Jumps | ✅ | ✅ | ✅ | ✅ |
| **EIP-4750** | Functions | ✅ | ✅ | ✅ | ✅ |
| **EIP-5450** | Stack Validation | ✅ | ✅ | ✅ | ✅ |
| **EIP-6206** | JUMPF and Non-Returning Functions | ✅ | ❌ | ✅ | ✅ |
| **EIP-663** | SWAPN, DUPN and EXCHANGE | ✅ | ❌ | ✅ | ✅ |
| **EIP-7480** | Data Section Access | ✅ | ❌ | ✅ | ✅ |
| **EIP-7620** | EOF Contract Creation | ✅ | ❌ | ✅ | ✅ |
| **EIP-7873** | TXCREATE and InitcodeTransaction | ✅ | ❌ | ❌ | ✅ |

---

## Blockchain Terimleri ve Jargonlarının Açıklamaları

### EVM ve EOF Terimleri
- **EVM (Ethereum Virtual Machine)**: Ethereum ağı üzerinde akıllı kontratların çalıştığı sanal makine
- **EOF (Ethereum Object Format)**: Akıllı kontratların kod ve veri bölümlerini ayıran yeni nesil dosya formatı
- **Opcode (Operation Code)**: EVM'in anlayabileceği temel makine talimatları
- **Stack (Yığın)**: EVM'de işlemlerin geçici olarak tutulduğu veri yapısı

### Programlama Kavramları
- **Introspection (İç Gözlem)**: Kodun kendi kendini incelemesi veya analiz etmesi
- **Tail Call**: Bir fonksiyonun sonunda başka bir fonksiyona doğrudan atlama
- **Static Jump**: Derleme zamanında belirlenen sabit atlama noktaları
- **Function**: Kodun modüler ve tekrar kullanılabilir bölümleri

### Güvenlik ve Doğrulama
- **Code Validation**: Kodun doğruluğunun otomatik kontrolü
- **Stack Validation**: Yığın işlemlerinin güvenlik kontrolü
- **Deploy**: Akıllı kontratın Ethereum ağına yüklenmesi
- **Backward Compatibility**: Eski sistemlerle uyumluluğun korunması

---

## Her Seçeneğin Avantajları ve Dezavantajları

### Tam EOF
**Avantajlar:**
- En kapsamlı güvenlik ve performans iyileştirmeleri
- Gelecekteki güncellemeler için sağlam temel
- En yenilikçi özellik seti

**Dezavantajlar:**
- En yüksek karmaşıklık seviyesi
- Mevcut kodlarla en az uyumluluk
- En uzun geliştirme süresi

### Minimal EOF
**Avantajlar:**
- En yüksek geriye dönük uyumluluk
- En düşük geçiş maliyeti
- En hızlı uygulama

**Dezavantajlar:**
- Sınırlı yenilik
- Gelecekteki güncellemeler için kısıtlı temel
- Performans kazanımları sınırlı

### Temel EOF
**Avantajlar:**
- Yenilik ve uyumluluk dengesi
- Makul geçiş maliyeti
- Geliştiriciler için esneklik

**Dezavantajlar:**
- Orta seviye karmaşıklık
- Bazı güvenlik kısıtlamalarından feragat
- Konsensüs zorluğu

### İç Gözlem EOF
**Avantajlar:**
- Mevcut kodlarla yüksek uyumluluk
- Geliştirici dostu yaklaşım
- Pragmatik çözüm

**Dezavantajlar:**
- Bazı güvenlik garantilerinden feragat
- Kontrollü introspection riskleri
- Uzun vadeli mimari kısıtlamalar

---

*[← Önceki Bölüm: Genel Bakış](01-genel-bakis.md) | [Sonraki Bölüm: PeerDAS Teknolojisi →](03-peerdas.md)*
