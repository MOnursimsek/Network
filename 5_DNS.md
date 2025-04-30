# **DNS Nedir?**

**DNS (Domain Name System)**, internet üzerindeki alan adlarını (domain name) IP adreslerine çeviren, yani insanların anlayabileceği dil ile makinelerin anlayabileceği dili birbirine dönüştüren dağıtık bir veritabanı sistemidir.

Örnek:  
Bir web sitesine `www.google.com` yazarak eriştiğinizde, bu alan adı aslında arka planda bir IP adresine (örneğin, `142.250.190.68`) çevrilir. Bu çeviriyi yapan sistem DNS’tir.

**Temel amaçları şunlardır:**
- Alan adlarını IP adreslerine dönüştürmek (Name Resolution)
- Dağıtık bir veritabanı yapısı ile hiyerarşik olarak çalışmak
- Servisleri (web, e-posta, vs.) doğru sunuculara yönlendirmek

## **DNS Neden Gereklidir?**

1. **İnsanların IP adreslerini hatırlaması zordur:**  
   IP adresleri sayısal ifadelerdir ve özellikle IPv6 ile çok daha karmaşık hale gelmiştir (`2001:4860:4860::8888` gibi). Alan adları ise hatırlanabilir ve anlamlıdır.

2. **İnternetteki iletişimin temelini oluşturur:**  
   DNS olmadan, kullanıcıların bir web sitesine erişebilmesi için IP adresini ezberleyip tarayıcıya yazması gerekir.

3. **Hizmetlerin yönlendirilmesi gerekir:**  
   E-posta, FTP gibi hizmetlerin ilgili sunuculara yönlendirilmesi DNS kayıtları sayesinde yapılır.

4. **Kolaylık ve esneklik sağlar:**  
   Bir web sitesinin IP adresi değişse bile, DNS kaydı güncellendiğinde kullanıcılar aynı alan adını kullanarak yeni IP adresine ulaşabilir.

##  **DNS Bileşenleri Ayrıntılı Açıklama**

### 1.  **DNS Resolver (Çözücü / Recursive Resolver)**

####  Görevi:
Kullanıcının yaptığı alan adı sorgusunu alır ve gerekli IP adresini bulmak için DNS sunucularına sırayla sorgu gönderir. Kullanıcıyla DNS sunucuları arasındaki köprü gibidir.

####  İşleyiş:
- Tarayıcıya `www.example.com` yazıldığında ilk çalışan bileşendir.
- Eğer daha önce yapılmış bir sorgu varsa **önbellekten (cache)** IP adresini döner.
- Önbellekte yoksa **root → TLD → yetkili DNS sunucularına** kadar sırayla sorgu gönderir.

####  Not:
Resolver, genellikle internet servis sağlayıcınızın (ISP) DNS sunucusunda çalışır. Google DNS (`8.8.8.8`) veya Cloudflare DNS (`1.1.1.1`) gibi genel DNS çözücüleri de kullanılabilir.

### 2.  **Root Name Servers (Kök DNS Sunucuları)**

####  Görevi:
İnternetin DNS hiyerarşisinin en üstündeki sunuculardır. TLD (üst seviye alan adı) sunucularına yönlendirme yapar.

####  Özellikleri:
- Dünya genelinde **13 adet kök DNS sunucu grubu** vardır. Her biri harflerle (`A` ila `M`) temsil edilir.
- Gerçek sayıları 13 değil, **çok sayıda aynalanmış (anycast) sunucu** üzerinden çalışırlar.
- Root sunucular alan adlarının IP adresini **bilmez**, sadece ilgili TLD sunucusuna yönlendirir.

####  Örnek:
`www.example.com` → Root sunucu “.com” TLD sunucusuna yönlendirir.

### 3.  **TLD Name Servers (Üst Seviye Alan Adı Sunucuları)**

####  Görevi:
Belirli bir alan adı uzantısı (TLD) altındaki alan adlarını yönetir. Örneğin:
- `.com`, `.net`, `.org` → global TLD
- `.tr`, `.uk`, `.de` → ülkeye özel TLD (ccTLD)

####  İşleyiş:
Root sunucuların yönlendirmesiyle devreye girer ve sorgulanan alan adı için **yetkili DNS sunucusunun adresini verir.**

####  Örnek:
`.com` TLD sunucusu, `example.com` alan adının yetkili sunucusunun IP adresini verir.

### 4.  **Authoritative DNS Servers (Yetkili DNS Sunucuları)**

####  Görevi:
Belirli bir alan adına ait **nihai DNS kayıtlarını (IP adresi, e-posta sunucusu, vs.)** tutar. En doğru ve güncel bilgileri sağlar.

####  Özellikleri:
- Bu sunucular alan adının sahibi tarafından veya barındırma (hosting) firması tarafından yönetilir.
- Cevap verdikleri bilgiler **kesindir**, diğer DNS sunucuları sadece yönlendirme yapar.

####  Örnek Kayıtlar:
- `A`: `www.example.com → 192.0.2.1`
- `MX`: `mail.example.com`
- `CNAME`: `blog.example.com → blogs.google.com`

### 5. **DNS Kayıt Türleri (DNS Records)**

Yetkili sunucularda tutulan kayıt türleri, alan adının farklı işlevlerde kullanılmasını sağlar:

| **Kayıt Türü** | **Açıklama** |
|----------------|--------------|
| **A (Address)** | Alan adını IPv4 adresine çevirir. Örnek: `example.com → 192.0.2.1` |
| **AAAA** | Alan adını IPv6 adresine çevirir. |
| **MX (Mail Exchange)** | E-posta sunucusunun adresini belirtir. |
| **CNAME (Canonical Name)** | Bir alan adını başka bir alan adına yönlendirir. Örn: `shop.example.com → store.example.net` |
| **NS (Name Server)** | Alan adının hangi yetkili sunucular tarafından yönetildiğini belirtir. |
| **TXT (Text)** | SPF, DKIM gibi doğrulama verilerini veya özel metinleri içerir. |
| **SOA (Start of Authority)** | Alan adının DNS bölgesine (zone) ait yetki ve zamanlama bilgilerini içerir. |

### 6.**Cache (Önbellek)**

####  Görevi:
Yapılan sorguların sonuçlarını belirli bir süre saklayarak, aynı alan adı için tekrar sorgu yapıldığında daha hızlı sonuç döndürülmesini sağlar.

####  TTL (Time To Live):
- Her DNS kaydının **TTL süresi** vardır.
- Bu süre dolana kadar sonuç önbellekte kalır.
- TTL süresi düşükse daha güncel bilgiler alınır ama daha fazla sorgu olur.

## **DNS Sorgu Türleri (Types of DNS Queries)**

DNS istemcisi, bir alan adının IP adresini öğrenmek için DNS sunucularına farklı türde sorgular gönderebilir. Üç temel DNS sorgu türü vardır:

### A. **Recursive Query (Yinelemeli Sorgu)**  
İstemci (genellikle bir DNS resolver), **kesin cevabı** almak ister.  
DNS sunucusu:
- Ya doğru cevabı döner,
- Ya da hata mesajı döner (bulamıyorsa).  
Sorumluluk tamamen sunucudadır.

**Özellik:**  
DNS sunucusu cevabı almak için başka sunucularla iletişime geçmek zorundadır. Kullanıcıdan sadece bir sorgu gelir, gerisini sunucu yapar.

### **Iterative Query (Yinelemeli Olmayan Sorgu)**  
DNS sunucusu, cevabı **doğrudan bilmiyorsa**, yalnızca bir sonraki adresteki DNS sunucusunun IP'sini verir.

**Özellik:**  
Her adımda istemcinin kendisi başka DNS sunucularına sorgu gönderir. Daha çok DNS sunucuları arasında kullanılır.

### **Non-Recursive Query (Önbellek Sorgusu)**  
Sunucu, önbelleğinde tuttuğu kayıtla hızlı bir cevap döner.  
Yeni sorgu zinciri başlatılmaz.  
Bu sorgu, daha önce çözülmüş bir domain’in önbellekte tutulması durumunda yapılır.


## **DNS Çözümleme Süreci – Step-by-Step**

`www.example.com` yazıldığında neler olur?

### **Adım 1:** Kullanıcı Tarayıcıya Alan Adı Girer  
Tarayıcı DNS çözümleyiciye (`resolver`) başvurur.

### **Adım 2:** Yerel Önbellek Kontrolü  
Tarayıcı veya işletim sistemi daha önce aynı sorguyu yaptıysa, çözümleme **önbellekten** yapılabilir.

### **Adım 3:** Recursive Resolver Devreye Girer  
Resolver sorguyu alır ve root DNS sunucusuna iteratif sorgu gönderir.

### **Adım 4:** Root Sunucu → TLD Sunucusu  
`.com` uzantısı için hangi TLD sunucusunun kullanılması gerektiği bilgisini döner.

### **Adım 5:** TLD Sunucusu → Yetkili DNS Sunucusu  
TLD sunucusu, `example.com` için yetkili sunucunun adresini döner.

### **Adım 6:** Yetkili DNS → IP Adresi  
Yetkili sunucu, `www.example.com` için **A kaydını (IP adresini)** döner.

### **Adım 7:** Cevap Resolver'a → Tarayıcıya  
Çözücü, IP adresini alır, işletim sistemine döner ve tarayıcı sunucuya bağlanır.

### **Adım 8:** Önbelleğe Kaydedilir  
IP bilgisi belirli bir süre önbellekte tutulur (TTL süresince).

## **DNS Güvenliği (DNS Security)**

DNS, internetin temel yapı taşlarından biridir. Ancak tasarlandığı dönemde güvenlik ön planda değildi. Bu yüzden birçok zafiyeti vardır ve saldırılara karşı ek önlemler alınması gerekir.

### 1. **DNS Güvenlik Tehditleri**

#### - **DNS Spoofing / DNS Cache Poisoning**
- Saldırgan, sahte bir DNS cevabını resolver önbelleğine sokar.
- Kullanıcılar sahte IP'ye yönlendirilir (örneğin, sahte bankacılık sitesi).

#### - **DNS Hijacking (Kaçırma)**
- Kullanıcının DNS ayarları değiştirilir (örneğin, kötü amaçlı yazılımla).
- Tüm DNS sorguları saldırganın sunucusuna gider.


#### - **NXDOMAIN Flood**
- Var olmayan alan adları için yoğun sorgular yapılarak DNS çözücü yorulur.

#### - **DNS Amplification (Yansıtmalı Saldırı)**
- Küçük isteklerle büyük DNS cevapları üretilip üçüncü taraf hedefe yönlendirilir.



### 2.  **DNS Güvenliğini Sağlama Yöntemleri**

#### - **DNSSEC (DNS Security Extensions)**
- DNS yanıtlarının dijital olarak **imzalanmasını** sağlar.
- Sahte cevapların tespit edilmesini mümkün kılar.
- **Anahtar kavramlar:**  
  - *RRSIG*: İmzalı kayıt  
  - *DNSKEY*: Anahtar kaydı  
  - *DS*: Delegation Signer (alt alanlar için güvenlik zinciri)

#### - **TLS ve HTTPS Üzerinden DNS (DoT & DoH)**
- DNS verileri şifreli olarak gönderilir:
  - **DoT (DNS over TLS)**: TCP 853 portundan TLS ile iletişim.
  - **DoH (DNS over HTTPS)**: HTTPS protokolü ile 443 portundan.

#### - **Split DNS**
- İç ağ ve dış ağ için farklı DNS sunucuları kullanılır.
- Dahili DNS bilgileri dışarıya sızmaz.

#### -**Rate Limiting ve Firewall Kuralları**
- DNS sunucularını aşırı isteklerden korumak için sorgu limiti ve IP filtreleme yapılır.

#### - **DNS Logging ve İzleme**
- DNS sorguları loglanarak anormal trafik ve tehditler tespit edilebilir.

## Kaynakça

1. [RFC 1034 - DNS Concepts and Facilities](https://datatracker.ietf.org/doc/html/rfc1034)  
2. [RFC 1035 - DNS Implementation and Specification](https://datatracker.ietf.org/doc/html/rfc1035)  
3. [Cloudflare - What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)  
4. [Cloudflare - DNS over HTTPS (DoH)](https://developers.cloudflare.com/fundamentals/privacy/dns-over-https/)  
5. [Cloudflare - DNS Cache Poisoning Explained](https://www.cloudflare.com/learning/dns/dns-cache-poisoning/)  
6. [Cisco - DNS Overview and Configuration](https://www.cisco.com/c/en/us/support/docs/ip/domain-name-system-dns/10120-dns.html)  
7. [Microsoft - DNS Troubleshooting](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/troubleshoot-dns)  
8. **"Computer Networking: A Top-Down Approach" – Kurose & Ross** (Chapter 2 - DNS)

