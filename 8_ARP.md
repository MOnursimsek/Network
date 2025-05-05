# **ARP Protokol**

##  ARP Nedir?

ARP (Address Resolution Protocol), **ağ katmanındaki (Layer 3) IP adreslerini**, **veri bağlantı katmanındaki (Layer 2) MAC adreslerine çevirmek** için kullanılan bir protokoldür. 1982 yılında tanımlanmış olan bu protokol, günümüzde hâlâ **IPv4** ağlarının ayrılmaz bir parçasıdır.

Her cihaz (bilgisayar, router, yazıcı, vb.), ağa bağlandığında hem bir IP adresine hem de bir MAC adresine sahiptir. IP adresi, ağlar arası yönlendirmede kullanılırken, MAC adresi fiziksel cihaz kimliği olarak veri çerçevelerinin doğru adrese ulaşmasında kullanılır. IP adresi ağ düzeyinde mantıksal, MAC adresi ise fiziksel ve donanım düzeyinde sabittir.

Bilgisayar, ağ üzerinde başka bir IP adresine veri göndermek istediğinde, hedef cihazın MAC adresini bilmek zorundadır. İşte bu aşamada ARP devreye girerek IP ile MAC adresini eşleştirir.

> ARP, **sadece aynı yerel ağ (subnet) içindeki cihazlar arasında** çalışır. Farklı alt ağlara erişim gerekiyorsa, ARP sorgusu yönlendiriciye (gateway) yapılır.


##  ARP Nasıl Çalışır?


ARP, **IP adresine karşılık gelen MAC adresini bulmak** için bir sorgu/yanıt (request/reply) mekanizmasıyla çalışır. Bu süreç şu adımlarla gerçekleşir:

### 1.  ARP İsteği (Request) Gönderilir

Gönderen cihaz (örneğin PC1), hedef IP adresinin MAC adresini bilmediğinde, ağda **broadcast (yayın)** şeklinde bir ARP isteği gönderir:

```
"192.168.1.5 IP adresine sahip cihazın MAC adresi nedir?"
```

* Bu istek, `FF:FF:FF:FF:FF:FF` MAC adresine gönderilir (yani tüm cihazlara).
* Ethernet çerçevesi bu şekilde tüm ağa iletilir.
* Bu istekte şunlar yer alır:

  * Gönderenin IP ve MAC adresi
  * Hedef IP adresi (henüz MAC adresi bilinmiyor)

### 2.  ARP Yanıtı (Reply) Alınır

Eğer bu isteği alan cihazlardan biri (örneğin IP’si 192.168.1.5 olan PC2) kendi IP adresiyle eşleşme görürse, doğrudan **unicast** olarak yanıt verir:

```
"Ben 192.168.1.5'im. MAC adresim: AA:BB:CC:DD:EE:FF"
```

* Bu yanıt sadece sorguyu gönderen cihaza gider.
* Artık PC1, PC2'nin MAC adresini öğrenmiş olur.


### 3.  ARP Önbelleğine (Cache) Kayıt

Cihaz, gelen ARP yanıtındaki IP–MAC eşleşmesini **kendi önbelleğine (ARP Cache)** kaydeder. Bu sayede aynı IP’ye tekrar veri gönderileceği zaman ARP sorgusu tekrar gönderilmez.

* Örneğin, `192.168.1.5 → AA:BB:CC:DD:EE:FF` kaydı eklenir.
* Bu kayıtlar genellikle birkaç dakika (genelde 2-4 dakika) tutulur ve sonra silinir.

Linux’ta: `ip neigh` veya `arp -n` komutlarıyla görülebilir.
Windows’ta: `arp -a` komutuyla görüntülenir.


### 4.  Veri Gönderimi Gerçekleşir

Artık cihaz, hedefin MAC adresini bildiği için, Ethernet çerçevesini doğru MAC adresine yönlendirerek veri gönderimini gerçekleştirir.


##  ARP Tablosu (Cache) 

###  ARP Tablosu Nedir?

**ARP tablosu (veya ARP cache)**, bir ağ cihazının öğrendiği IP adresi ile buna karşılık gelen MAC adresi eşleşmelerini geçici olarak tuttuğu bir veritabanıdır. Bu sayede her paket gönderiminde ARP sorgusu yapılmaz; sistem, önceden öğrendiği MAC adreslerini tablodan alarak zaman ve kaynak tasarrufu sağlar.

###  Tablo Nerede Tutulur?

* Her cihazda (bilgisayar, router, switch) kendi işletim sistemi tarafından bellekte tutulur.
* Tablo geçici (volatile) bellekte saklanır, cihaz yeniden başlatıldığında temizlenir.

###  Tablo Nasıl Oluşur?

* **Dinamik olarak:** Bir ARP sorgusuna gelen yanıt sonucunda otomatik oluşur.
* **Statik olarak:** Kullanıcı veya sistem yöneticisi tarafından manuel olarak girilir ve silinene kadar kalır.


###  ARP Tablosunun Yapısı Örneği:

Linux’ta `ip neigh` çıktısı:

```
192.168.1.1 dev eth0 lladdr 00:11:22:33:44:55 REACHABLE
192.168.1.20 dev eth0 lladdr aa:bb:cc:dd:ee:ff STALE
```

Windows’ta `arp -a` çıktısı:

```
Interface: 192.168.1.10 --- 0x6
  Internet Address      Physical Address      Type
  192.168.1.1           00-11-22-33-44-55     dynamic
  192.168.1.20          aa-bb-cc-dd-ee-ff     dynamic
```

###  Dinamik ARP Kayıtları

* **Nasıl oluşur?**
  Bir ARP isteği sonucunda otomatik olarak oluşur.
* **Avantajları:**
  Kullanıcı müdahalesi gerektirmez; ağ trafiğine göre güncellenir.
* **Dezavantajları:**
  Saldırılara karşı savunmasızdır (örneğin ARP spoofing). Süre dolduğunda silinir.
* **Örnek:**
  Bilgisayarınız ilk kez yazıcıya veri gönderdiğinde, onun MAC adresini öğrenip ARP tablosuna kaydeder.

###  Statik ARP Kayıtları

* **Nasıl oluşur?**
  Sistem yöneticisi tarafından manuel olarak tanımlanır.
* **Avantajları:**
  Güvenlidir; kayıt değişmediği için ARP spoofing gibi saldırılara karşı koruma sağlar.
* **Dezavantajları:**
  Yönetimi zordur; IP değişirse manuel güncellenmesi gerekir.
* **Ne zaman kullanılır?**

  * Kritik sistemlerde (sunucular, routerlar)
  * Güvenlik açısından hassas ortamlarda
  * ARP spoofing’i önlemek için



##  ARP Paket Yapısı

ARP protokolü, donanım (MAC) ve IP adresi bilgilerini içeren sabit formatta bir paket yapısı kullanır. ARP paketleri Ethernet çerçevesi içinde gönderilir.

###  ARP Paketi Ethernet İçinde

| Ethernet Başlığı   | ARP Başlığı |
| ------------------ | ----------- |
| Destination MAC    | Target MAC  |
| Source MAC         | Source MAC  |
| EtherType (0x0806) | ARP Paketi  |


###  ARP Başlık Alanları (28 baytlık yapı)

| Alan              | Uzunluk | Açıklama                                                        |
| ----------------- | ------- | --------------------------------------------------------------- |
| **Hardware Type** | 2 byte  | 1 = Ethernet (IEEE 802.3)                                       |
| **Protocol Type** | 2 byte  | 0x0800 = IPv4                                                   |
| **Hardware Size** | 1 byte  | MAC adresi boyutu (6)                                           |
| **Protocol Size** | 1 byte  | IP adresi boyutu (4)                                            |
| **Opcode**        | 2 byte  | 1 = Request, 2 = Reply                                          |
| **Sender MAC**    | 6 byte  | ARP’yi gönderen cihazın MAC adresi                              |
| **Sender IP**     | 4 byte  | ARP’yi gönderen cihazın IP adresi                               |
| **Target MAC**    | 6 byte  | Hedef cihazın MAC adresi (Request’te genelde 00:00:00:00:00:00) |
| **Target IP**     | 4 byte  | Hedef IP adresi                                                 |


##  Proxy ARP Nedir?



**Proxy ARP**, bir cihazın (genellikle yönlendirici veya güvenlik duvarı), **başka bir cihaz adına ARP yanıtı vermesidir.** Yani IP’si başka bir cihaza ait olan bir ARP isteğine kendi MAC adresini göndererek “benim” der.

Bu, cihazın yerel ağda olmasa bile, karşı tarafın onu yerelmiş gibi görüp veri gönderebilmesini sağlar.


###  Nasıl Çalışır?

1. Bilgisayar A, 192.168.1.100 adresine paket göndermek ister ama bu adres farklı bir subnettedir.
2. Yönlendirici, bu IP adresinin başka bir alt ağda olduğunu bilir, ama PC bunu bilmez.
3. Bilgisayar A, ARP ile 192.168.1.100’ün MAC’ini sorar.
4. **Yönlendirici cevap verir:** “Bu IP’ye ben sahibim” ve kendi MAC adresini verir.
5. Artık PC, yönlendiricinin MAC adresine veri yollar, o da paketi doğru alt ağa iletir.



##  Gratuitous ARP Nedir?



**Gratuitous ARP (Karşılıksız ARP)**, bir cihazın kendi IP adresi için **kendi MAC adresini içeren bir ARP Request veya Reply** göndermesidir, **karşılık beklenmez.**


###  Ne Zaman Kullanılır?

1. **IP çakışması tespiti**:

   * Cihaz, ağda başka bir cihazın aynı IP’yi kullanıp kullanmadığını kontrol eder.
   * Kendi IP’si için ARP isteği gönderir. Cevap gelirse, bir çakışma vardır.

2. **ARP tablolarını güncelleme**:

   * Yeni IP adresi alındığında veya MAC adresi değiştiğinde diğer cihazların ARP tablolarını güncellemek için gönderilir.

3. **Failover sistemlerde (örnek: HSRP, VRRP)**:

   * Yedek cihaz aktif hâle geçtiğinde, IP adresi artık ona aittir. Gratuitous ARP göndererek ağdaki tüm cihazlara bu durumu bildirir.


## RARP Nedir ?

RARP (Reverse Address Resolution Protocol), bir cihazın **MAC adresini** kullanarak, o cihaza ait **IP adresini** öğrenmek amacıyla kullanılan bir ağ protokolüdür.

### RARP'in Çalışma Prensibi:

1. **İhtiyaç Durumu**: RARP, genellikle **diskless** (hard diski olmayan) istemciler için kullanılır. Bu tür cihazlar, ağ üzerinden çalıştıkları için IP adresine ihtiyaç duyarlar, ancak kendi IP adreslerini bilmezler.

2. **İstemci İsteği**: Cihaz, ağ üzerinden bir RARP isteği gönderir. Bu istek, cihazın **MAC adresini** içerir.

3. **RARP Sunucusu**: RARP isteği, ağda bir **RARP sunucusuna** ulaşır. Sunucu, istemcinin MAC adresini görür ve bu MAC adresine karşılık gelen IP adresini geri gönderir.

4. **IP Adresi Alınır**: RARP sunucusu, istemciye o MAC adresine ait IP adresini yanıt olarak gönderir. İstemci, bu IP adresi ile ağda iletişim kurmaya başlar.

### Kullanım Alanı:

* **Diskless İstemciler**: Hard diski olmayan cihazlar, genellikle ağ üzerinden çalışırken IP adresini almak için RARP kullanır.
* **Eski Ağ Yapıları**: RARP, özellikle eski ağ yapılarında ve diskless istemcilerle çalışan sistemlerde yaygın olarak kullanılmıştır. Ancak günümüzde, **DHCP (Dynamic Host Configuration Protocol)** protokolü bu amaca daha yaygın olarak hizmet etmektedir.


##  ARP Spoofing ve Güvenlik Tehditleri

###  ARP Spoofing Nedir?

**ARP Spoofing (veya ARP Poisoning)**, **ARP tablosunu kandırmak** amacıyla **yanıltıcı ARP mesajları gönderme** tekniğidir. Bu saldırılar, ağdaki cihazları kandırarak yanlış MAC adresi eşleştirmeleri yapar.

###  Nasıl Çalışır?

1. Saldırgan cihaz, ağa **yanlış ARP mesajları** gönderir.
2. Hedef cihaz, gelen yanıltıcı ARP mesajlarını kabul eder ve **yanlış MAC adresini** kendi ARP tablosuna kaydeder.
3. **Saldırgan**, ağda yer alan diğer cihazlarla iletişim kurarak **yönlendirici ya da diğer cihazların trafiklerini ele geçirebilir**.



###  ARP Spoofing'in Neden Olduğu Güvenlik Sorunları:

* **IP-MAC Eşleştirmesinin Manipülasyonu:** Ağdaki cihazların doğru IP adresi ve MAC adresi eşleşmeleri bozulur.
* **Ağ Dinleme (Sniffing):** Trafik saldırganın cihazı üzerinden geçebilir, şifreli olmayan veriler ele geçirilebilir.
* **İçerik Değiştirme:** Trafik üzerinden yapılan saldırılar, verilerin değiştirilmesine veya çalınmasına yol açabilir.
* **Denial of Service (DoS):** Saldırganın cihazı, hedef cihazlara veri gönderme işlemlerini engelleyebilir.


## ARP'nin Sınırlamaları ve Alternatifleri 

###  **ARP'nin Sınırlamaları:**

* **IPv6 Desteği Olmaması:** ARP, yalnızca **IPv4** protokolü için geçerlidir ve **IPv6**'da kullanılmaz. IPv6, **ARP'nin** işlevlerini gerçekleştirmek için farklı bir protokol kullanır.
* **Güvenlik Sorunları:** ARP, şeffaf ve basit bir protokoldür. Bu, **ARP Spoofing** gibi saldırılara karşı savunmasızdır. Saldırganlar, ağdaki cihazların IP-MAC eşleşmelerini manipüle edebilir ve **Man-in-the-Middle (MITM)** saldırıları gerçekleştirebilirler.
* **Dinamik Yapı:** ARP tablosundaki bilgiler zamanla eskiyebilir, bu da **IP-MAC eşleşmelerinin geçerliliğini yitirmesi** anlamına gelir. Bu durumda, sürekli olarak yeni ARP talepleri yapılır ve ağ trafiği artar.
* **Şebeke Yoğunluğu:** ARP, **broadcast (yayın)** tabanlı çalışır, bu da ağda her ARP isteği ile birlikte **gerekli olmayan cihazlara** veri gönderilmesine yol açar. Bu, büyük ağlarda **şebeke trafiğini** artırabilir.


### **ARP Alternatifleri (Örneğin, NDP – IPv6 İçin):**

**NDP (Neighbor Discovery Protocol)**, **IPv6**'nın ARP yerine kullanılan protokolüdür ve ARP'nin işlevlerini geliştirmek ve daha güvenli bir alternatif sunmak amacıyla tasarlanmıştır.

#### **NDP (Neighbor Discovery Protocol):**

NDP, **IPv6 ağlarında** **adres çözümleme (Address Resolution)**, **komşu keşfi (Neighbor Discovery)**, **duplikasyon tespiti (Duplicate Address Detection)** gibi işlevler sağlar. NDP, ARP'den daha fazla özellik sunar ve daha güvenlidir.

* **ICMPv6 Temellidir:** NDP, **ICMPv6** mesajları kullanarak çalışır.
* **Neighbor Solicitation (NS) ve Neighbor Advertisement (NA):**

  * **NS** mesajı, **IPv6 adresinden MAC adresine** dönüşüm için kullanılır.
  * **NA** mesajı, **MAC adresine karşılık gelen IPv6 adresini** döndürür.
* **Daha Güvenli ve Etkili:** NDP, **autokonfigürasyon (auto-configuration)** ve **kimlik doğrulama (authentication)** özellikleri sunar. Bu sayede NDP, **ARP Spoofing** gibi saldırılara karşı daha dayanıklıdır.




































































## Kaynakça

1. Tanenbaum, A. S., & Wetherall, D. J. – *Computer Networks* (5th Edition)

2. Kurose, J. F., & Ross, K. W. – *Computer Networking: A Top-Down Approach* (7th Edition)

3. [Cisco – ARP (Address Resolution Protocol) Documentation](https://www.cisco.com/c/en/us/support/docs/ip/address-resolution-protocol-arp/13718-arp.html)

4. [RFC 826 – An Ethernet Address Resolution Protocol](https://datatracker.ietf.org/doc/html/rfc826)

5. [RFC 4861 – Neighbor Discovery for IP version 6 (IPv6)](https://datatracker.ietf.org/doc/html/rfc4861)
