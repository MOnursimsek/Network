# **Switch**

## **Switch Nedir?**

**Switch**, OSI modelinin **veri bağlantı (Data Link - Katman 2)** katmanında çalışan, ağ cihazlarını birbirine bağlayan ve veri çerçevelerini (frames) hedef MAC adreslerine göre ileten bir ağ cihazıdır. Gelişmiş modelleri **Katman 3 (Ağ katmanı)** işlevlerini de yerine getirebilir ve yönlendirme yeteneklerine sahip olabilir, ancak temel düzeyde bir switch’in görevi, gelen veri çerçevesini doğru hedefe iletmektir.

Switch’ler bir **LAN (Local Area Network)** içinde cihazların birbirleriyle iletişimini sağlar. Üzerlerinde birden fazla **port (bağlantı noktası)** bulunur ve her bir port, bir ağ cihazına (örneğin bilgisayar, yazıcı, access point) bağlanabilir. Switch, bu cihazlardan gelen veri trafiğini analiz eder ve sadece hedef cihaza yönelik iletim yapar. Bu sayede ağda **çarpışmalar (collision)** azaltılır ve **bant genişliği verimli** kullanılır.

## **Switch’in Çalışma Prensibi**

Switch’in çalışma prensibi, **MAC adreslerine** dayalı veri yönlendirmesidir. Bu işlem birkaç aşamadan oluşur:

1. **Çerçeve Alma (Frame Reception):**
   Switch'e bağlı bir cihaz, başka bir cihaza veri gönderdiğinde, bu veri bir Ethernet çerçevesi (frame) olarak switch'e ulaşır. Çerçevede hem gönderici hem de alıcı MAC adresi bulunur.

2. **MAC Adresini Öğrenme (Learning):**
   Switch, gelen çerçevenin **kaynak (source) MAC adresini** ve bu çerçevenin **geldiği portu** analiz eder. Bu bilgiyi **MAC adres tablosuna (CAM table)** kaydeder. Böylece, o MAC adresine sahip cihazın hangi portta olduğunu öğrenmiş olur.

3. **Tablodan Bakma (Lookup):**
   Switch, çerçevenin **hedef (destination) MAC adresine** bakar ve bu adresin MAC tablosunda olup olmadığını kontrol eder.

4. **İletim Kararı (Forwarding):**

   * **Hedef MAC adresi tablodaysa:** Switch, veriyi sadece ilgili porta iletir (unicast).
   * **Hedef MAC adresi bilinmiyorsa:** Switch, veriyi **tüm portlara** (kaynak port hariç) iletir (flooding). Hedef cihaz cevap verdiğinde, MAC adresi tabloya kaydedilir.

5. **Çerçevenin İletilmesi (Frame Forwarding):**
   Switch, çerçeveyi uygun porta iletir. Bu, ağ trafiğinin yalnızca gerekli cihazlara yönlendirilmesini sağlar.

Switch’ler ayrıca **tam-dupleks (full-duplex)** modda çalışarak aynı anda veri gönderip alabilir, böylece çarpışmaları önler.

## **Switch ile Hub Arasındaki Farklar**

| Özellik                      | **Hub**                                        | **Switch**                                            |
| ---------------------------- | ---------------------------------------------- | ----------------------------------------------------- |
| **Çalışma Katmanı**          | OSI Katman 1 - Fiziksel Katman                 | OSI Katman 2 - Veri Bağlantı Katmanı                  |
| **Veri İletimi**             | Gelen veriyi tüm portlara gönderir (broadcast) | Veriyi sadece hedef cihazın bağlı olduğu porta iletir |
| **MAC Adresi Tabanlı İşlem** | Hayır                                          | Evet (MAC adreslerini öğrenir ve tablo tutar)         |
| **Çarpışma Riski**           | Yüksektir (collision domain aynıdır)           | Çok düşüktür (her port ayrı collision domain'dir)     |
| **Bant Genişliği Kullanımı** | Paylaşımlı bant genişliği                      | Her porta ayrılmış bant genişliği                     |
| **Verimlilik**               | Düşük                                          | Yüksek                                                |
| **Yarı/Tam Dupleks**         | Genellikle yarı-dupleks                        | Tam-dupleks destekler                                 |
| **Fiyat**                    | Daha ucuz                                      | Daha pahalı (ancak daha etkilidir)                    |


## **Switch’lerde MAC Adres Tablosu (CAM Table) ve Öğrenme Süreci**

**CAM (Content Addressable Memory)** tablosu ya da yaygın adıyla **MAC adres tablosu**, switch’in cihazlara ait MAC adreslerini ve bu adreslerin hangi switch portuna ait olduğunu kaydettiği bir veri yapısıdır.

#### **MAC Adres Tablosunun Yapısı:**

| MAC Adresi        | Switch Portu | Yaş/Zaman Damgası |
| ----------------- | ------------ | ----------------- |
| 00:1A:2B:3C:4D:5E | Fa0/1        | 240 saniye        |
| 00:1B:3D:4E:5F:6A | Fa0/3        | 180 saniye        |

> Not: Tablodaki kayıtlar **zamanla silinebilir**. Tipik olarak bir adres 300 saniye (5 dakika) boyunca inaktif kalırsa otomatik olarak silinir.

#### **Öğrenme Süreci (Learning):**

1. Switch, gelen çerçevenin **kaynak MAC adresi** ve **geliş portunu** kontrol eder.
2. Eğer bu adres tabloda yoksa, yeni bir kayıt oluşturur.
3. Eğer adres tabloda varsa ve geliş portu aynıysa, hiçbir şey yapılmaz.
4. Eğer adres tabloda varsa ama geliş portu farklıysa, kayıt **güncellenir**.

#### **Ayrıca Bilinmesi Gerekenler:**

* **Aging Timer:** Her MAC adresi için zaman sayacı başlatılır. Adres belirli bir süre kullanılmazsa tablodan silinir.
* **Static MAC Entries:** Bazı MAC adresleri manuel olarak tabloya kalıcı şekilde eklenebilir. Bu adresler aging süresine tabi değildir.
* **CAM Table Overflow (Taşma):** Ağa çok fazla cihaz bağlanırsa veya MAC spoofing saldırıları olursa CAM tablosu taşabilir. Bu durum güvenlik açığı oluşturur.

## **Switch Türleri (Unmanaged, Managed, Layer 2, Layer 3 Switch’ler)**

#### **1. Unmanaged Switch (Yönetilemeyen Switch):**

* **Tanım:**
  Unmanaged switch’ler temel işlevleri yerine getiren, **kullanıcı yapılandırması gerektirmeyen** “tak ve çalıştır (plug and play)” cihazlardır. Üzerlerinde genellikle **yönetim arayüzü**, VLAN desteği ya da güvenlik özellikleri bulunmaz.

* **Kullanım Alanları:**
  Küçük ofisler, ev ağları veya basit ağ yapılarında tercih edilir. Kurulum kolaylığı ve düşük maliyet avantajı sunar.

* **Avantajları:**

  * Kurulumu ve kullanımı çok kolaydır.
  * Düşük maliyetlidir.
  * Teknik bilgi gerekmez.

* **Dezavantajları:**

  * Trafiği analiz edemez, port yapılandırması yapılmaz.
  * Ağ büyüdükçe yetersiz kalır.
  * Güvenlik özellikleri yoktur.

#### **2. Managed Switch (Yönetilebilir Switch):**

* **Tanım:**
  Ağ yöneticilerinin switch’i yapılandırmasına olanak sağlayan gelişmiş switch türüdür. CLI, web arayüzü, SNMP gibi protokollerle yönetilebilir.

* **Özellikleri:**

  * VLAN desteği
  * QoS (Quality of Service)
  * Güvenlik politikaları (port security, ACL)
  * STP (Spanning Tree Protocol)
  * Port mirroring
  * SNMP, Syslog desteği
  * Uzaktan yönetim (telnet, SSH)

* **Kullanım Alanları:**
  Orta ve büyük ölçekli kurumsal ağlarda kullanılır. Özellikle segmentasyon, izleme ve yönetim gerektiren ağlarda tercih edilir.

#### **3. Layer 2 Switch:**

* **Tanım:**
  OSI’nin **veri bağlantı katmanında** (Layer 2) çalışan, sadece **MAC adreslerine göre** çerçeve iletimi yapan switch’tir.

* **Görevleri:**

  * MAC adresi öğrenme
  * Çerçeve yönlendirme (forwarding)
  * Broadcast, unicast, multicast iletimi
  * VLAN desteği
  * STP gibi Layer 2 protokoller

* **Yönlendirme Yeteneği:**
  Layer 2 switch’ler **IP yönlendirme yapmaz**, sadece Layer 2 düzeyinde işlem yapar. Ancak VLAN’lar arasında yönlendirme gerekiyorsa harici bir router gerekir (Router-on-a-stick).

#### **4. Layer 3 Switch:**

* **Tanım:**
  Hem Layer 2 işlevleri (MAC tabanlı switching) hem de Layer 3 işlevleri (IP yönlendirme) gerçekleştirebilen gelişmiş switch’tir.

* **Özellikleri:**

  * VLAN’lar arası yönlendirme (Inter-VLAN Routing)
  * Statik ve dinamik yönlendirme protokolleri (RIP, OSPF, EIGRP)
  * ACL ve QoS desteği
  * Daha fazla CPU ve bellek kapasitesi
  * Routing table ve MAC table birlikte kullanılır.

* **Kullanım Alanları:**
  Büyük ve kompleks ağlarda, yönlendiricilere ihtiyaç duymadan hızlı yönlendirme işlemleri için tercih edilir.

## **Switch Port Türleri ve Hızları**

#### **1. Port Türleri:**

* **Access Port:**

  * Sadece **tek bir VLAN’a** ait trafiği taşıyan port türüdür.
  * Genellikle son kullanıcı cihazları (PC, yazıcı) bağlanır.
  * Gelen çerçeveye VLAN etiketi eklenmez.

* **Trunk Port:**

  * Birden fazla VLAN’ın trafiğini aynı hat üzerinden taşıyan port türüdür.
  * Switch-switch bağlantılarında veya switch-router bağlantılarında kullanılır.
  * IEEE 802.1Q etiketi ile VLAN bilgisi çerçeveye eklenir.

* **Hybrid Port:**

  * Hem access hem de trunk davranışı gösterebilir.
  * Genellikle özel ağ cihazlarında (örneğin bazı üretici switch’lerde) kullanılır.


#### **2. Hız Türleri:**

| **Hız**                           | **Açıklama**                                                            |
| --------------------------------- | ----------------------------------------------------------------------- |
| **10 Mbps (Ethernet)**            | En eski standart, günümüzde nadiren kullanılır.                         |
| **100 Mbps (Fast Ethernet)**      | Eski ofis ağlarında yaygındı, modern ağlarda yetersiz kalır.            |
| **1 Gbps (Gigabit Ethernet)**     | Günümüzün en yaygın ağ hızı standardıdır.                               |
| **10 Gbps (10-Gigabit Ethernet)** | Veri merkezleri, yüksek bant genişliği gereksinimleri için kullanılır.  |
| **40/100 Gbps ve üzeri**          | Büyük veri merkezlerinde, fiber optik altyapılarla birlikte kullanılır. |

* **Portlar genellikle Otomatik Hız Algılama (Auto-Negotiation)** özelliğine sahiptir.
  Yani cihaz karşısındaki cihaza göre hız ve duplex modunu otomatik belirler.

* **Port Duplex Modları:**

  * **Half Duplex:** Aynı anda sadece tek yönlü veri iletişimi.
  * **Full Duplex:** Aynı anda iki yönlü veri iletişimi (modern switch’lerde yaygın).


## **Switch’lerde Yayın (Broadcast), Çoklu Gönderim (Multicast) ve Tekli Gönderim (Unicast)**

Switch’ler çerçeveleri **hedef MAC adresine göre** üç şekilde iletebilir: **Unicast**, **Multicast**, ve **Broadcast**.

#### **1. Unicast (Tekli Gönderim):**

* **Tanım:**
  Bir cihazdan **belirli tek bir cihaza** veri gönderme işlemidir. Hedef MAC adresi tek bir cihazı ifade eder.

* **Switch Davranışı:**
  Switch, MAC adres tablosuna bakar ve hedef MAC adresine karşılık gelen porta veriyi **yalnızca o porta** yönlendirir.

* **Örnek:**
  Bir bilgisayarın yazıcıya belge göndermesi.

* **Avantaj:**

  * Ağda minimum trafik oluşur.
  * Yüksek verimlilik sağlar.


#### **2. Broadcast (Yayın):**

* **Tanım:**
  Bir cihazın **tüm yerel ağdaki cihazlara** aynı anda veri göndermesidir. Hedef MAC adresi: **FF\:FF\:FF\:FF\:FF\:FF** (broadcast adresi)

* **Switch Davranışı:**
  Switch, çerçeveyi **tüm portlara** gönderir (kaynak port hariç). Bu, aynı VLAN’daki tüm cihazların bu veriyi alacağı anlamına gelir.

* **Örnek:**

  * ARP sorgusu (bir IP adresine karşılık gelen MAC adresini öğrenme).
  * DHCP Discover yayını.

* **Dezavantaj:**

  * Ağda fazla broadcast trafiği varsa performansı düşürebilir.
  * Broadcast storm (yayın fırtınası) riski vardır.


#### **3. Multicast (Çoklu Gönderim):**

* **Tanım:**
  Veri, **belirli bir cihaz grubuna** gönderilir. Hedef MAC adresi özel bir multicast adresidir (örneğin 01:00:5e\:xx\:xx\:xx)

* **Switch Davranışı:**
  Basit switch’ler multicast’i **broadcast gibi** yayabilir.
  Akıllı switch’lerde **IGMP Snooping** özelliği varsa, multicast gruplar izlenir ve sadece ilgili portlara veri gönderilir.

* **Örnek:**
  IP TV yayını, video konferans, grup güncellemeleri.

* **Avantaj:**

  * Unicast’e göre daha az bant genişliği kullanır.
  * Yalnızca ilgili kullanıcılar veri alır.



## **Switch’lerde Döngü Problemi ve Spanning Tree Protocol (STP)**

###  **Switch’lerde Döngü Problemi (Switch Loop)**

#### **1. Döngü Nedir?**

Switch’ler, Layer 2 cihazlar olarak veri çerçevelerini MAC adreslerine göre iletir. Ancak, **birden fazla switch’in fiziksel olarak döngüsel bir şekilde birbirine bağlanması**, yani alternatif yolların olması durumunda, **sonsuz çerçeve döngüsü (switching loop)** oluşabilir.

#### **2. Neden Olur?**

Switch’ler, **MAC adres tablosunu belirli aralıklarla temizler** ve çerçeve alındığında MAC adresi bilinmiyorsa **broadcast yapar**. Döngü durumunda:

* Broadcast çerçeveleri sonsuz döngüye girer.
* Switch’ler sürekli olarak aynı çerçeveleri alıp gönderir.
* MAC tablosu sürekli güncellenir ve kararsız hale gelir.
* CPU ve bant genişliği tükenir.

#### **3. Döngü Probleminin Etkileri:**

* **Broadcast Storm (Yayın Fırtınası):**
  Broadcast trafiği ağda kontrolsüz şekilde yayılır ve tüm bant genişliğini tüketir.

* **MAC Address Table Instability (Kararsız MAC Tablosu):**
  Hedef MAC adresinin hangi porta ait olduğu sürekli değişir, switch yanlış yönlendirmeler yapar.

* **Ağ Çökmesi:**
  Ağa bağlı tüm cihazlar yavaşlar veya bağlantıyı tamamen kaybeder.

#### **4. Döngüye Neden Olan Durumlar:**

* Yanlış yapılan switch bağlantıları (örneğin birden fazla uplink).
* Aynı VLAN’ın birden fazla yol üzerinden dolaşması.
* STP olmayan ağlarda yedek hat kullanımı.


### **Spanning Tree Protocol (STP)**

#### **1. Tanım ve Amacı:**

**Spanning Tree Protocol (STP)**, IEEE **802.1D** standardına göre tanımlanmış bir protokoldür. Amacı:

* Layer 2 ağlarda **döngüleri otomatik olarak algılamak ve önlemek**,
* Yedek yolları **pasif hale getirerek** döngüsüz bir mantıksal ağ topolojisi oluşturmak,
* Ana bağlantı kesilirse yedek yolu **otomatik olarak etkinleştirmektir**.


#### **2. STP’nin Temel Bileşenleri:**

| **Bileşen**                          | **Görevi**                                                                 |
| ------------------------------------ | -------------------------------------------------------------------------- |
| **Bridge ID (BID)**                  | Switch’i benzersiz olarak tanımlar. 2 parça içerir: Bridge Priority + MAC. |
| **Root Bridge**                      | Tüm ağın merkez switch’idir. En düşük Bridge ID'ye sahip switch olur.      |
| **BPDU (Bridge Protocol Data Unit)** | STP mesajlarıdır. Switch'ler bu mesajlarla birbirine STP bilgisi gönderir. |


#### **3. STP Süreci (Adım Adım):**

##### **A. Root Bridge Seçimi:**

* Her switch kendini Root Bridge olarak kabul eder ve BPDU gönderir.
* Switch’ler aldıkları BPDU’ları karşılaştırır.
* **En düşük Bridge ID** değeri olan switch, Root Bridge olur.

##### **B. Her Switch’in Root Port’unu Belirlemesi:**

* Her switch, Root Bridge’e **en kısa yolu sağlayan portu** Root Port olarak seçer.
* Root Port, sadece **bir tane** olur ve Root Bridge’e giden yol olarak kullanılır.

##### **C. Designated Port’ların Belirlenmesi:**

* Her ağ segmentinde, o segmenti Root Bridge’e bağlayan **en iyi yolu sağlayan switch portu** Designated Port olur.
* Segmentte sadece bir Designated Port bulunur.

##### **D. Gereksiz Portlar Blocking Moduna Alınır:**

* Geriye kalan portlar döngüye neden olabileceği için **Blocking** durumuna alınır.
* Bu portlar veri iletmez ama BPDU’ları dinlemeye devam eder.


##  **Switch Konfigürasyonu için Gerekli Temel Cisco IOS Komutları**

Cisco switch’lerde yapılandırma işlemleri CLI (Command Line Interface) üzerinden gerçekleştirilir. Aşağıda temel konfigürasyon komutları kategorilere ayrılarak detaylı şekilde açıklanmıştır:


###  **1. Cihaza Erişim ve Modlar Arası Geçiş**

| Komut                | Açıklama                                               |
| -------------------- | ------------------------------------------------------ |
| `enable`             | Kullanıcı modundan "privileged EXEC" moda geçiş yapar. |
| `configure terminal` | Global yapılandırma moduna geçer.                      |
| `exit`               | Bir üst moda geri döner.                               |
| `end`                | Doğrudan EXEC moduna döner.                            |
| `hostname SW1`       | Switch’in adını "SW1" olarak değiştirir.               |


###  **2. Parola ve Güvenlik Ayarları**

#### **Enable Parolası:**

```bash
enable password cisco
```

> Enable moduna geçişte istenecek düz metin parola (güvenli değildir).

#### **Encrypted Enable Secret:**

```bash
enable secret class
```

> Güvenli, şifrelenmiş enable parolası (öncelikli kullanılır).

#### **Konsol Parolası Ayarı:**

```bash
line console 0
 password cisco
 login
```

#### **VTY (Uzak Erişim) Parolası:**

```bash
line vty 0 4
 password cisco
 login
```

#### **Parolaların Şifrelenmesi:**

```bash
service password-encryption
```

> Düz metinle yazılan parolalar (ör. line, console) şifrelenir (zayıf şifreleme).


###  **3. IP Ayarları (VLAN 1 Arayüzü)**

Cisco switch’lerde doğrudan fiziksel porta IP verilemez. Bunun yerine **VLAN 1 sanal arayüzü (SVI)** yapılandırılır:

```bash
interface vlan 1
 ip address 192.168.1.2 255.255.255.0
 no shutdown
```

> `no shutdown` komutu olmadan arayüz aktif hale gelmez.


###  **4. Port Yapılandırmaları**

#### **Portu Açma/Kapama:**

```bash
interface fastEthernet 0/1
 shutdown
 no shutdown
```

#### **Açıklama Ekleme (Label):**

```bash
description Bilgisayar-1 Baglantisi
```

#### **Statik Hız ve Duplex Ayarı (isteğe bağlı):**

```bash
speed 100
duplex full
```


###  **5. Yapılandırmayı Kaydetme**

#### **Çalışan yapılandırmayı başlatma konfigürasyonuna kaydetme:**

```bash
copy running-config startup-config
```

> Switch yeniden başlatıldığında ayarların kaybolmaması için şarttır.


##  **Packet Tracer ile Basit Switch Yapılandırması**

Cisco Packet Tracer, Cisco cihazlarını simüle etmeye yarayan bir eğitim aracıdır. Aşağıda, **2 bilgisayar ve 1 switch** kullanılarak oluşturulacak **basit bir ağ yapısı** adım adım açıklanmıştır.



###  **Ağ Topolojisi:**

```
[PC0] ---- [Switch] ---- [PC1]
```


###  **Adım 1: Cihazları Ekleme ve Kablolama**

* **1 adet Switch (ör. 2960)**
* **2 adet PC (PC0 ve PC1)**
* Her iki PC’yi de **Switch’in FastEthernet portlarına** bağla.
  (PC0 → Fa0/1, PC1 → Fa0/2)


###  **Adım 2: PC'lere IP Adresi Atama**

* **PC0:**

  * IP: `192.168.1.10`
  * Subnet Mask: `255.255.255.0`
* **PC1:**

  * IP: `192.168.1.20`
  * Subnet Mask: `255.255.255.0`

> Packet Tracer'da PC’ye tıklayıp → "Desktop" sekmesinden → "IP Configuration" kısmına girilir.


### 🔧 **Adım 3: Switch Konfigürasyonu (CLI Üzerinden)**

```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
SW1(config)# interface vlan 1
SW1(config-if)# ip address 192.168.1.1 255.255.255.0
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# line vty 0 4
SW1(config-line)# password cisco
SW1(config-line)# login
SW1(config-line)# exit
SW1(config)# enable secret class
SW1(config)# service password-encryption
SW1(config)# banner motd #Yetkisiz giriş yasaktır!#
SW1(config)# exit
SW1# copy running-config startup-config
```

> Bu konfigürasyon ile switch’e IP atanmış, uzak erişim açılmış ve temel güvenlik önlemleri uygulanmıştır.


### 📶 **Adım 4: Ağ Bağlantı Testi (Ping)**

* PC0’ı aç ve “Command Prompt” kısmından:

```bash
ping 192.168.1.20
```

* Eğer ping başarılıysa:

```bash
Reply from 192.168.1.20: bytes=32 time<1ms TTL=128
```

> Bu, temel bağlantının sağlandığını gösterir.




##  **Switch Portlarının Yapılandırılması**

Cisco switch’lerde her port Layer 2 (veri bağlantı katmanı) üzerinde çalışır. Bu portlar belirli modlara alınarak VLAN'lara atanabilir veya trunk bağlantısı olarak yapılandırılabilir.

###  1. **Port Modları**

| **Mod**               | **Açıklama**                                                              |
| --------------------- | ------------------------------------------------------------------------- |
| **Access Mode**       | Tek bir VLAN’a ait uç cihaz bağlantısı için kullanılır (PC, yazıcı, vb.). |
| **Trunk Mode**        | Birden çok VLAN’ın etiketli (tagged) olarak geçtiği bağlantı türüdür.     |
| **Dynamic Auto**      | Pasif olarak trunk olmayı bekler. Karşı taraf "desirable" ise trunk olur. |
| **Dynamic Desirable** | Aktif olarak trunk olmaya çalışır. Karşı taraf auto ise trunk olur.       |

###  2. **Temel Port Yapılandırma Komutları**

####  **Access Port Olarak Ayarlama:**

```bash
interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
```

> Bu port, VLAN 10’a ait uç cihaza atanır.

####  **Trunk Port Olarak Ayarlama:**

```bash
interface fastEthernet 0/24
switchport mode trunk
switchport trunk allowed vlan 10,20
```

> Bu port, sadece VLAN 10 ve 20’ye ait trafiği taşır.

####  **Portu Etkinleştirme / Devre Dışı Bırakma:**

```bash
shutdown         → Portu kapatır  
no shutdown      → Portu etkinleştirir
```

####  **Açıklama Ekleme:**

```bash
description PC-1 baglantisi
```


##  **VLAN Nedir? ve VLAN Oluşturma (Packet Tracer Uygulaması)**

### 🔹 1. **VLAN Nedir?**

**VLAN (Virtual Local Area Network)**, fiziksel olarak aynı switch’e bağlı cihazların **mantıksal olarak farklı ağlar gibi çalışmasını** sağlayan sanal yapıdır.

####  VLAN’ların Sağladığı Avantajlar:

* Yayın domainlerini sınırlar (broadcast fırtınasını azaltır).
* Güvenlik sağlar (her VLAN ayrı ağ gibi davranır).
* Yönetilebilirlik artar.
* Performans yükselir.

> Örneğin:
> VLAN 10 → Muhasebe
> VLAN 20 → IT
> VLAN 30 → Personel

###  2. **VLAN Oluşturma Komutları:**

```bash
vlan 10
name MUHASEBE
exit

vlan 20
name IT
exit
```

> VLAN’lar sadece tanımlanmakla kalmaz, portlar da atanmalıdır:

```bash
interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
```


###  3. **Packet Tracer Uygulaması (Adım Adım)**

####  **Topoloji:**

* 1 switch
* 4 PC (PC1, PC2, PC3, PC4)
* PC1 ve PC2 → VLAN 10 (Muhasebe)
* PC3 ve PC4 → VLAN 20 (IT)

####  **Adımlar:**

1. Switch’e IP verilmeyecek, çünkü sadece Layer 2 işlemler yapılacak.
2. Aşağıdaki komutlar ile VLAN tanımlanır ve portlar atanır:

```bash
enable
configure terminal

vlan 10
name MUHASEBE
exit

vlan 20
name IT
exit

interface range fa0/1 - 2
switchport mode access
switchport access vlan 10

interface range fa0/3 - 4
switchport mode access
switchport access vlan 20
```

3. Her PC’ye aynı ağdan ama farklı VLAN’dan IP ver:

   * PC1: 192.168.10.1 /24
   * PC2: 192.168.10.2 /24
   * PC3: 192.168.20.1 /24
   * PC4: 192.168.20.2 /24

####  **Sonuç:**

* PC1 ↔ PC2 **birbirine ping atabilir.**
* PC1 ↛ PC3 **birbirine ping atamaz.**


##  **Trunk Port Yapılandırması ve VLAN’lar Arası Haberleşme**

###  1. **Trunk Nedir?**

Trunk bağlantısı, birden fazla VLAN’ın aynı bağlantı üzerinden **etiketli (tagged)** biçimde taşınmasını sağlar. Genellikle **switch–switch veya switch–router** bağlantılarında kullanılır.

###  2. **Trunk Özellikleri:**

* IEEE 802.1Q protokolü ile VLAN etiketleme yapılır.
* Trunk bağlantı üzerinden birden çok VLAN geçebilir.
* Her çerçeveye VLAN ID (etiket) eklenir.
* Native VLAN (varsayılan VLAN) etiketsiz geçer.


###  3. **Trunk Port Yapılandırma (Cisco Komutları):**

```bash
interface fastEthernet 0/24
switchport mode trunk
switchport trunk allowed vlan 10,20
switchport trunk native vlan 99
```

> `native vlan 99`: Etiketsiz çerçevelerin geçtiği VLAN’ı değiştirir. Güvenlik için önerilir.


###  4. **VLAN’lar Arası Haberleşme (Inter-VLAN Routing)**

VLAN’lar farklı broadcast domain’lerdir, bu yüzden kendi aralarında **doğrudan haberleşemezler**. VLAN’lar arası iletişim için şu çözümler gerekir:

####  **1. Router-on-a-Stick (Subinterface Yöntemi):**

* Tek bir router portu kullanılır.
* Her VLAN için alt arayüz (subinterface) tanımlanır.
* Her alt arayüz trunk bağlantıya bağlanır.

```bash
interface GigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

####  **2. Layer 3 Switch Kullanımı:**

* Layer 3 switch’lerde VLAN’lar arası yönlendirme mümkündür.
* Her VLAN için SVI (Switch Virtual Interface) tanımlanır.

```bash
interface vlan 10
ip address 192.168.10.1 255.255.255.0
no shutdown

interface vlan 20
ip address 192.168.20.1 255.255.255.0
no shutdown

ip routing
```

###  **Packet Tracer Örneği (Trunk Bağlantı ve Inter-VLAN Routing)**

* 2 switch, 1 router
* PC1 ve PC2 → VLAN 10
* PC3 ve PC4 → VLAN 20
* Switch–Router bağlantısı trunk
* Router subinterface ile yönlendirme yapıyor
* PC1 ↔ PC3 **ping atabiliyor** (çünkü farklı VLAN’lar arası yönlendirme yapılmış)

## **Switch Üzerinde Port Güvenliği (Port Security) Ayarları**

**Port Security**, switch’e bağlanan cihazların MAC adreslerini sınırlayarak fiziksel erişime karşı güvenlik sağlar. Özellikle uç nokta bağlantılarında, belirli bir MAC adresine sahip olmayan cihazların bağlantısını engellemek için kullanılır.

###  Temel Amaç:

* Belirli bir porta **yalnızca tanımlı MAC adreslerinin** erişmesini sağlamak.
* Farklı bir cihaz bağlandığında **trafik kesilebilir**, **uyarı verilebilir** veya **port kapanabilir**.

###  Adım Adım Port Security Yapılandırması:

#### 1. Port Access Mode’a alınmalı:

```bash
interface fastEthernet 0/1
switchport mode access
```

#### 2. Port Security aktif edilir:

```bash
switchport port-security
```

#### 3. Maksimum MAC adresi sayısı belirlenir (default: 1):

```bash
switchport port-security maximum 1
```

#### 4. Sabit MAC adresi manuel girilebilir:

```bash
switchport port-security mac-address 0011.2233.4455
```

#### 5. Güvenlik ihlali (violation) durumu belirlenir:

```bash
switchport port-security violation shutdown
```

###  Violation Seçenekleri:

| Seçenek      | Açıklama                                                                 |
| ------------ | ------------------------------------------------------------------------ |
| **Protect**  | Tanımsız MAC adreslerini yok sayar, trafik geçirmez ama port açık kalır. |
| **Restrict** | Tanımsız MAC adreslerini engeller ve log oluşturur.                      |
| **Shutdown** | Portu err-disabled durumuna alır, elle açılmalıdır.                      |

#### 6. Ayarları kontrol etmek:

```bash
show port-security interface fastEthernet 0/1
```

#### 7. Port shutdown olduysa açmak:

```bash
interface fastEthernet 0/1
shutdown
no shutdown
```

#### ➤ **Dinamik Öğrenme (Sticky):**

Switch, ilk gelen MAC adresini otomatik olarak tanır ve konfigürasyona ekler.

```bash
switchport port-security mac-address sticky
```

> Kalıcı hale getirmek için “write memory” komutu kullanılır.


####  Sticky MAC Kaydetme Örneği:

```bash
interface fastEthernet 0/3
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation restrict
```

##  **Switch’te Yönetim Erişimi (Konsol, Telnet, SSH Yapılandırması)**

Switch'e uzaktan veya yerel olarak bağlanarak yapılandırma yapılabilir. Konsol fiziksel bağlantı ile yapılırken, Telnet ve SSH uzaktan erişim sağlar.



### **Konsol Erişimi**

Konsol bağlantısı genellikle switch’in "console" portuna fiziksel olarak bağlanarak yapılır. Terminal programları (Putty, TeraTerm, Minicom) kullanılır.

#### Konsol Şifresi Ayarlama:

```bash
line console 0
password cisco
login
```

#### Oturum zaman aşımı ayarı (isteğe bağlı):

```bash
exec-timeout 5 0   → 5 dakika
```


###  **Telnet ile Uzaktan Erişim**

> Telnet şifreli değildir, güvenli ortamda kullanılması önerilir.

#### Gerekli Ayarlar:

1. Switch’e IP adresi ver:

```bash
interface vlan 1
ip address 192.168.1.2 255.255.255.0
no shutdown
```

2. Varsayılan ağ geçidi:

```bash
ip default-gateway 192.168.1.1
```

3. Telnet şifresi ve kullanıcı:

```bash
line vty 0 4
password telnetpass
login
```

> Artık başka bir cihazdan:

```bash
telnet 192.168.1.2
```

###  **SSH ile Güvenli Uzaktan Erişim**

> SSH, şifreli oturum sağlar. Güvenli ortamlarda Telnet yerine tercih edilir.

#### SSH için gerekli yapılandırma:

1. **Alan adı ve hostname ayarla:**

```bash
hostname SW1
ip domain-name ornek.local
```

2. **RSA anahtarı oluştur:**

```bash
crypto key generate rsa
```

> Anahtar boyutu: Minimum 1024 önerilir.

3. **Kullanıcı oluştur ve parola ata:**

```bash
username admin privilege 15 secret admin123
```

4. **VTY hatlarında SSH’ı etkinleştir:**

```bash
line vty 0 4
transport input ssh
login local
```

5. **SSH versiyonunu belirle (önerilir):**

```bash
ip ssh version 2
```

#### SSH ile bağlantı:

```bash
ssh -l admin 192.168.1.2
```

## **Switch Konfigürasyonlarının Yedeklenmesi ve Geri Yüklenmesi**

Switch’lerde yapılan yapılandırmaların yedeklenmesi, sistem arızaları veya donanım değişiklikleri durumunda hızlıca yeniden kurulum yapılabilmesini sağlar. Bu işlem genellikle **TFTP sunucusu** aracılığıyla yapılır.


###  Switch Konfigürasyonları Türleri

| Konfigürasyon Türü | Açıklama                                                                  |
| ------------------ | ------------------------------------------------------------------------- |
| **Running-config** | RAM'de çalışan aktif yapılandırmadır. Switch yeniden başlarsa silinir.    |
| **Startup-config** | NVRAM'de kayıtlı kalıcı konfigürasyondur. Cihaz her açıldığında yüklenir. |

---

###  Konfigürasyonu TFTP Sunucusuna Yedekleme

#### Ön Koşullar:

* TFTP sunucusu çalışır durumda olmalı (aynı ağda veya yönlendirilebilir).
* Switch’in IP adresi atanmış olmalı.
* TFTP sunucusu, yazma izniyle yapılandırılmış olmalı.

####  `startup-config` Yedekleme:

```bash
copy startup-config tftp
```

#### Adımlar:

1. Komut girilir:
   `Destination filename [startup-config]?` → Varsayılan isim ya da özel bir isim girilebilir.

2. IP adresi istenir:
   `Address or name of remote host []? 192.168.1.100`

---

###  2. Konfigürasyonu TFTP'den Switch'e Geri Yükleme

####  `startup-config`’i geri yükleme:

```bash
copy tftp startup-config
```

#### Ardından:

* Switch’i yeniden başlatmak gerekir:

```bash
reload
```

---

###  3. Konfigürasyonu USB’ye Yedekleme (Destekleyen modellerde)

```bash
copy startup-config usbflash0:backup.cfg
```

USB bellekte `backup.cfg` adında dosya oluşur. Geri yükleme için:

```bash
copy usbflash0:backup.cfg startup-config
```

---

###  4. Konfigürasyonu Gösterme ve Kaydetme

#### Geçerli yapılandırmayı göster:

```bash
show running-config
```

#### Geçerli ayarları kalıcı hale getirme:

```bash
copy running-config startup-config
```

veya

```bash
write memory
```


##  **CDP (Cisco Discovery Protocol)**

###  Nedir?

**CDP (Cisco Discovery Protocol)**, Cisco tarafından geliştirilen, OSI modelinin **Veri Bağlantı Katmanı (Layer 2)** üzerinde çalışan **Cisco’ya özel** bir ağ keşif protokolüdür.

Amaç:

* Aynı ağda bulunan **Cisco cihazlarını** (switch, router, IP phone, vs.) otomatik olarak tespit etmek.
* Yönetim ve sorun giderme süreçlerini kolaylaştırmak.


###  CDP Ne İşe Yarar?

* Komşu cihazların:

  * Cihaz türü (Switch, Router, IP Phone, Access Point)
  * Arayüz bilgisi (hangi porta bağlı)
  * Yazılım/IOS sürümü
  * Platform bilgisi
  * IP adresi gibi detaylarını keşfeder.
* Ağ topolojisini anlamada ve dökümante etmede önemli rol oynar.
* IP adresi veya hostname bilgisi olmadan **katman 2 düzeyinde keşif** yapar.


###  CDP Paket Yapısı (Özet)

* **Header** kısmında sürüm, TTL, checksum gibi temel bilgiler yer alır.
* **TLV (Type-Length-Value)** formatında bilgi taşır:

  * Device ID
  * Port ID
  * Capabilities
  * Software Version
  * Management IP Address
  * Platform


###  CDP Zamanlamaları

* CDP mesajları her **60 saniyede bir** gönderilir.
* Komşu zaman aşımı süresi **180 saniye**dir. Bu süre içinde mesaj alınmazsa cihaz “kaybolmuş” sayılır.


###  CDP Komutları

| Komut                       | Açıklama                                        |
| --------------------------- | ----------------------------------------------- |
| `show cdp`                  | Genel CDP durumunu gösterir.                    |
| `show cdp neighbors`        | Komşu cihazların özet bilgilerini verir.        |
| `show cdp neighbors detail` | IP adresi, yazılım sürümü gibi detayları verir. |
| `cdp run`                   | CDP’yi globalde etkinleştirir.                  |
| `no cdp run`                | CDP’yi globalde devre dışı bırakır.             |
| `cdp enable`                | Arayüz üzerinde CDP'yi etkinleştirir.           |
| `no cdp enable`             | Arayüz üzerinde CDP'yi devre dışı bırakır.      |


###  CDP'nin Sınırlamaları

* **Sadece Cisco cihazları** ile çalışır.
* Katman 3 (IP) bağımlı değildir, bu yüzden uzaktaki ağlar görülmez.
* CDP paketleri **şifreli değildir** → güvenlik açığı oluşturabilir.


##  **LLDP (Link Layer Discovery Protocol)**

###  Nedir?

**LLDP (Link Layer Discovery Protocol)**, IEEE 802.1AB standardına sahip, **marka bağımsız**, açık kaynaklı bir ağ keşif protokolüdür. OSI Layer 2 üzerinde çalışır ve CDP’ye benzer şekilde cihaz keşfi sağlar.

Amaç:

* Farklı üreticilere ait ağ cihazları arasında **evrensel keşif** yapılmasını sağlamak.


###  LLDP Ne İşe Yarar?

* Her cihaz, kendine ait bilgileri bağlı olduğu port üzerinden **LLDP reklamı (advertisement)** ile yayınlar.
* Aynı zamanda karşıdan gelen reklamları dinleyerek **komşu cihazların bilgilerini** öğrenir.


###  LLDP ile Paylaşılan Bilgiler

* Cihaz ismi
* Port ismi ve durumu
* MAC adresi
* IP adresi (eğer varsa)
* VLAN bilgisi
* Güç durumu (PoE)
* Medya türü (örneğin fiber, bakır)

###  LLDP Paket Yapısı

* CDP gibi **TLV (Type-Length-Value)** yapısı kullanılır.

* Zorunlu TLV alanları:

  * Chassis ID
  * Port ID
  * Time to Live (TTL)

* Opsiyonel TLV alanları:

  * System Name
  * System Description
  * System Capabilities
  * Management Address


###  LLDP Zamanlamaları

* LLDP mesajları her **30 saniyede bir** gönderilir.
* Varsayılan TTL değeri genelde **120 saniye**dir.


###  LLDP Komutları

| Komut                        | Açıklama                                         |
| ---------------------------- | ------------------------------------------------ |
| `lldp run`                   | LLDP’yi global olarak başlatır.                  |
| `no lldp run`                | LLDP’yi global olarak durdurur.                  |
| `lldp transmit`              | Belirli bir arayüzde LLDP reklamlarını gönderir. |
| `lldp receive`               | Belirli bir arayüzde LLDP mesajlarını alır.      |
| `show lldp`                  | Genel LLDP durumunu gösterir.                    |
| `show lldp neighbors`        | Komşu cihazların bilgilerini listeler.           |
| `show lldp neighbors detail` | Detaylı komşu bilgisi verir.                     |


###  LLDP Avantajları

* Farklı üreticilerle çalışabilir (Cisco, Juniper, HP, Aruba, Mikrotik vs.).
* IP telefonlar ve VoIP sistemlerinde VLAN, ses hizmeti gibi bilgilerin aktarılmasını sağlar.
* CDP’ye göre daha geniş protokol desteği vardır.


###  LLDP'nin Sınırlamaları

* **Varsayılan olarak kapalı** gelir, elle etkinleştirilmelidir.
* CDP kadar Cisco ekosistemine entegre değildir (örneğin IP Phone otomatik yapılandırmaları).



##  CDP (Cisco Discovery Protocol) Yapılandırması

###  CDP Varsayılan Durumu

* **CDP, Cisco cihazlarında varsayılan olarak etkin (enabled)** gelir.
* Tüm aktif arayüzlerde çalışır.
* Cihazlar her **60 saniyede** bir CDP paketi gönderir.

###  Global CDP Yapılandırması

#### CDP’yi Etkinleştirme:

```bash
Switch(config)# cdp run
```

#### CDP’yi Devre Dışı Bırakma:

```bash
Switch(config)# no cdp run
```

Bu komut **tüm cihazda CDP’yi kapatır veya açar.** Bu durumda hiçbir arayüz CDP paketi göndermez.


###  Arayüz Düzeyinde CDP Yapılandırması

#### Belirli bir Arayüzde CDP’yi Etkinleştirme:

```bash
Switch(config)# interface FastEthernet0/1
Switch(config-if)# cdp enable
```

#### Belirli bir Arayüzde CDP’yi Devre Dışı Bırakma:

```bash
Switch(config)# interface FastEthernet0/1
Switch(config-if)# no cdp enable
```

Bu yapılandırma, yalnızca belirtilen arayüz üzerinde CDP’nin çalışmasını kontrol eder.



###  CDP Bilgi Görüntüleme Komutları

| Komut                       | Açıklama                                                                |
| --------------------------- | ----------------------------------------------------------------------- |
| `show cdp`                  | CDP’nin aktif olup olmadığını gösterir.                                 |
| `show cdp interface`        | Hangi arayüzlerde CDP çalıştığını ve istatistikleri gösterir.           |
| `show cdp neighbors`        | Komşu cihazların cihaz adı, portu ve platform bilgilerini listeler.     |
| `show cdp neighbors detail` | Komşu IP adresi, yazılım sürümü, model gibi detaylı bilgileri gösterir. |


###  Örnek CDP Yapılandırması:

```bash
Switch(config)# cdp run
Switch(config)# interface f0/1
Switch(config-if)# no cdp enable
```

Bu yapılandırma ile tüm cihazda CDP etkin olur, ancak `f0/1` portu CDP mesajı göndermez.

##  LLDP (Link Layer Discovery Protocol) Yapılandırması

###  LLDP Varsayılan Durumu

* **LLDP, Cisco cihazlarda varsayılan olarak kapalıdır.**
* Elle etkinleştirilmesi gerekir.


###  Global LLDP Yapılandırması

#### LLDP’yi Global Olarak Etkinleştirme:

```bash
Switch(config)# lldp run
```

#### LLDP’yi Global Olarak Kapatma:

```bash
Switch(config)# no lldp run
```

Bu komutla tüm cihazda LLDP yayını (transmit) ve alımı (receive) aktif hale gelir ya da devre dışı kalır.

###  Arayüz Düzeyinde LLDP Yapılandırması

#### Sadece Yayınlama (Transmit) Etkin:

```bash
Switch(config)# interface g0/1
Switch(config-if)# lldp transmit
Switch(config-if)# no lldp receive
```

#### Sadece Alma (Receive) Etkin:

```bash
Switch(config)# interface g0/1
Switch(config-if)# lldp receive
Switch(config-if)# no lldp transmit
```

#### Hem Yayınlama hem Alma Etkin:

```bash
Switch(config)# interface g0/1
Switch(config-if)# lldp transmit
Switch(config-if)# lldp receive
```

###  LLDP Bilgi Görüntüleme Komutları

| Komut                        | Açıklama                                                                |
| ---------------------------- | ----------------------------------------------------------------------- |
| `show lldp`                  | LLDP’nin cihazda aktif olup olmadığını gösterir.                        |
| `show lldp interface`        | LLDP’nin hangi portlarda çalıştığını listeler.                          |
| `show lldp neighbors`        | LLDP ile keşfedilen komşu cihazların temel bilgilerini gösterir.        |
| `show lldp neighbors detail` | Komşuların ayrıntılı bilgilerini (platform, IP, yazılım, vs.) gösterir. |

###  Örnek LLDP Yapılandırması:

```bash
Switch(config)# lldp run
Switch(config)# interface f0/5
Switch(config-if)# lldp transmit
Switch(config-if)# lldp receive
```

Bu yapılandırma, LLDP’yi global olarak etkinleştirir ve `f0/5` portunda hem gönderim hem de alımı sağlar.


##  CDP ve LLDP Test Senaryosu (Packet Tracer için)

**Topoloji:**
`Switch1 --- FastEthernet0/1 --- Switch2`

### CDP ile Test:

```bash
Switch1(config)# cdp run
Switch2(config)# cdp run

Switch1# show cdp neighbors
```

> Çıktıda Switch2 bilgileri görünmelidir.

### LLDP ile Test:

```bash
Switch1(config)# lldp run
Switch2(config)# lldp run
Switch1(config)# interface f0/1
Switch1(config-if)# lldp transmit
Switch1(config-if)# lldp receive
Switch2(config)# interface f0/1
Switch2(config-if)# lldp transmit
Switch2(config-if)# lldp receive

Switch1# show lldp neighbors
```

> LLDP kullanılarak Switch2 hakkında bilgi edinilmelidir.


##  EtherChannel ile Switch Bağlantılarının Birleştirilmesi

###  EtherChannel Nedir?

**EtherChannel**, birden fazla fiziksel Ethernet bağlantısını **tek bir mantıksal bağlantı** (logical interface) olarak birleştiren teknolojidir. Böylece;

* **Bant genişliği artar** (örneğin 2x1Gbps → 2Gbps)
* **Yedeklilik sağlanır** (bir kablo koparsa bağlantı kesilmez)
* **Yük dengeleme (load balancing)** yapılabilir.
* **Spanning Tree Protocol (STP)**, EtherChannel’ı tek bir bağlantı olarak gördüğü için portları bloklamaz.

###  EtherChannel Özellikleri

| Özellik              | Açıklama                                                   |
| -------------------- | ---------------------------------------------------------- |
| Fiziksel Port Sayısı | Genellikle 2-8 arası port birleştirilebilir                |
| Hız Artışı           | Port sayısı kadar artar (örn. 4x1Gbps = 4Gbps)             |
| STP Uyumluluğu       | Tüm portları tek bağlantı gibi gördüğü için döngü yaratmaz |
| VLAN Uyumluluğu      | Access veya Trunk olarak yapılandırılabilir                |
| Load Balancing       | MAC/IP/port temelli dağılım yapılabilir                    |


###  EtherChannel Türleri

Cisco'da EtherChannel 3 farklı şekilde yapılandırılabilir:

| Tür                                          | Protokol     | Açıklama                                                   |
| -------------------------------------------- | ------------ | ---------------------------------------------------------- |
| **Static (Manual)**                          | Yok          | EtherChannel protokolü kullanılmaz. Sabit yapılandırma.    |
| **PAgP (Port Aggregation Protocol)**         | Cisco'a özel | Otomatik EtherChannel kurulumu için Cisco protokolü.       |
| **LACP (Link Aggregation Control Protocol)** | IEEE 802.3ad | Cisco + diğer marka cihazlarla uyumlu. Endüstri standardı. |


###  Protokol Durumları

####  PAgP:

* `auto`: Pasif mod (karşı taraf "desirable" ise çalışır)
* `desirable`: Aktif mod (karşı taraf "auto"/"desirable" olabilir)

####  LACP:

* `passive`: Pasif mod (karşı taraf "active" ise çalışır)
* `active`: Aktif mod (karşı taraf "active"/"passive" olabilir)

##  EtherChannel Yapılandırması

###  1. Statik (Manual) EtherChannel Yapılandırması

```bash
Switch(config)# interface range f0/1 - 2
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# channel-group 1 mode on
```

> `mode on`: Statik EtherChannel. Karşı taraf da aynı şekilde olmalı.

###  2. PAgP ile EtherChannel (Cisco özel)

```bash
Switch(config)# interface range f0/1 - 2
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# channel-group 1 mode desirable
```

> Diğer tarafta `desirable` veya `auto` olmalı.

###  3. LACP ile EtherChannel (Tavsiye edilen)

```bash
Switch(config)# interface range f0/1 - 2
Switch(config-if-range)# switchport mode trunk
Switch(config-if-range)# channel-group 1 mode active
```

> Diğer switch’te mod `active` veya `passive` olmalıdır.

###  4. Port-Channel Arayüz Yapılandırması

EtherChannel oluşturulduğunda `Port-channel` adında sanal bir arayüz oluşur:

```bash
Switch(config)# interface port-channel 1
Switch(config-if)# description *** SW2 bağlantısı ***
Switch(config-if)# switchport trunk allowed vlan 10,20
```

##  EtherChannel Durumu ve Sorun Giderme

| Komut                            | Açıklama                           |
| -------------------------------- | ---------------------------------- |
| `show etherchannel summary`      | EtherChannel durumu ve mod bilgisi |
| `show etherchannel port-channel` | Port-channel yapılandırması        |
| `show interfaces port-channel 1` | Mantıksal arayüz bilgileri         |
| `show running-config`            | Konfigürasyon doğrulama            |
| `debug pagp` / `debug lacp`      | Paket düzeyinde hata ayıklama      |

##  Packet Tracer: Basit EtherChannel Senaryosu

###  Topoloji:

`Switch1 <===> Switch2`

* `f0/1` ve `f0/2` arası kablolar bağlı

###  Her iki switch için yapılandırma (LACP örneği):

#### Switch1:

```bash
Switch1(config)# interface range f0/1 - 2
Switch1(config-if-range)# switchport mode trunk
Switch1(config-if-range)# channel-group 1 mode active
```

#### Switch2:

```bash
Switch2(config)# interface range f0/1 - 2
Switch2(config-if-range)# switchport mode trunk
Switch2(config-if-range)# channel-group 1 mode active
```

Ardından her iki switch’te:

```bash
Switch# show etherchannel summary
```

> Çıktıda `P` harfi (Port-channel) ve `SU` (Layer 2, in use) gibi durumlar görünecektir.


###  Notlar

* EtherChannel’a dahil olan portlar **aynı hız ve duplex değerine** sahip olmalıdır.
* VLAN konfigürasyonu da uyumlu olmalıdır.
* Her iki uç da aynı EtherChannel protokolünü kullanmalıdır.
* Uyuşmazlık varsa portlar `suspended` olur.


Aşağıda, bu sohbette detaylı olarak incelediğimiz **Switching** konularını kapsayan, **Packet Tracer ile Uygulamalı Senaryolar** başlığı altında **temel**, **orta** ve **gelişmiş düzeyde** örnekler sunulmuştur. Her senaryo, yapılandırma hedefleriyle birlikte açıklanmıştır.



##  Packet Tracer ile Uygulamalı Senaryolar

### (Temel – Orta – Gelişmiş)


###  Senaryo: **Switch Temel Yapılandırması ve VLAN Atamaları**

###  Hedefler:

* Switch hostname değiştirme
* IP yapılandırması
* VLAN oluşturma
* Portlara VLAN atama

###  Topoloji:

* 1 adet Switch
* 2 adet PC (PC0 ve PC1)

###  Yapılandırma Adımları:

1. **Switch Hostname ve IP**

```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
SW1(config)# interface vlan 1
SW1(config-if)# ip address 192.168.1.1 255.255.255.0
SW1(config-if)# no shutdown
```

2. **VLAN Oluşturma ve Atama**

```bash
SW1(config)# vlan 10
SW1(config-vlan)# name HR

SW1(config)# interface fa0/1
SW1(config-if)# switchport access vlan 10

SW1(config)# interface fa0/2
SW1(config-if)# switchport access vlan 10
```

3. **PC’lere IP verilir:**

* PC0: 192.168.1.2
* PC1: 192.168.1.3

###  Beklenen Sonuç:

* PC0 ↔ PC1 iletişim kurar
* Switch erişimi için IP atanmıştır

---

### Senaryo: **Trunk, VLAN’lar Arası İletişim ve Port Security**

###  Hedefler:

* 2 VLAN arası iletişim
* Router-on-a-Stick yapılandırması
* Trunk port ayarları
* Port güvenliği uygulanması

###  Topoloji:

* 2 Switch
* 1 Router
* 4 PC (2 VLAN10, 2 VLAN20)

###  Yapılandırma:

#### VLAN ve Trunk

```bash
SW1(config)# vlan 10
SW1(config)# vlan 20

SW1(config)# interface range fa0/1 - 2
SW1(config-if-range)# switchport access vlan 10

SW1(config)# interface range fa0/3 - 4
SW1(config-if-range)# switchport access vlan 20

SW1(config)# interface fa0/24
SW1(config-if)# switchport mode trunk
```

#### Router (ROAS – Router on a Stick)

```bash
Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0

Router(config)# interface g0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
```

#### Port Security (VLAN10’daki portlara)

```bash
SW1(config)# interface fa0/1
SW1(config-if)# switchport port-security
SW1(config-if)# switchport port-security maximum 1
SW1(config-if)# switchport port-security violation restrict
SW1(config-if)# switchport port-security mac-address sticky
```

###  Beklenen Sonuç:

* VLAN10 ve VLAN20 cihazları **router üzerinden haberleşir**
* Trunk bağlantısı aktiftir
* Port güvenliği ile MAC kısıtlaması uygulanır

---

### Senaryo: **EtherChannel + SSH + Konfigürasyon Yedekleme + CDP/LLDP Keşfi**

###  Hedefler:

* EtherChannel yapılandırma
* Switch yönetimi için SSH erişimi
* Konfigürasyonun yedeklenmesi
* CDP ve LLDP ile komşuların keşfi

###  Topoloji:

* SW1 <==> SW2 (2 bağlantı ile)
* SW1 yönetimi için bir PC (PC-Admin)

###  Yapılandırma:

#### EtherChannel (LACP)

```bash
SW1(config)# interface range fa0/1 - 2
SW1(config-if-range)# switchport mode trunk
SW1(config-if-range)# channel-group 1 mode active

SW2(config)# interface range fa0/1 - 2
SW2(config-if-range)# switchport mode trunk
SW2(config-if-range)# channel-group 1 mode active
```

#### SSH Yapılandırması (SW1)

```bash
SW1(config)# hostname SW1
SW1(config)# ip domain-name example.local
SW1(config)# crypto key generate rsa
SW1(config)# username admin secret 1234
SW1(config)# line vty 0 4
SW1(config-line)# login local
SW1(config-line)# transport input ssh
```

#### Konfigürasyon Yedekleme

```bash
SW1# copy running-config tftp:
Address or name of remote host []? 192.168.1.100
Destination filename [running-config]? SW1_backup.cfg
```

#### CDP ve LLDP

```bash
SW1# show cdp neighbors
SW1(config)# lldp run
SW1# show lldp neighbors
```

###  Beklenen Sonuç:

* SW1 ve SW2 arasında **EtherChannel ile yüksek hızlı bağlantı**
* PC üzerinden SW1’e **SSH ile güvenli erişim**
* Konfigürasyon TFTP sunucusuna yedeklenir
* CDP ve LLDP komutları ile komşu switch’ler görünür

## Kaynakça

1. [Cisco Catalyst Switches - Configuration Guides](https://www.cisco.com/c/en/us/support/switches/catalyst-2960-x-series-switches/products-installation-and-configuration-guides-list.html)
2. [Cisco IOS Command Reference](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/switches/command/reference/swi_book.html)
3. [Cisco Port Security Configuration Guide](https://www.cisco.com/c/en/us/support/docs/lan-switching/port-security/12013-12.html)
4. [Cisco Networking Academy – Switching, Routing, and Wireless Essentials (SRWE)](https://www.netacad.com)
7. [IEEE 802.1D - Spanning Tree Protocol Standard](https://standards.ieee.org/ieee/802.1D/2424/)
8. [IEEE 802.1Q - Virtual LAN Tagging Standard](https://standards.ieee.org/ieee/802.1Q/1036/)
9. [IEEE 802.3ad - Link Aggregation (EtherChannel)](https://standards.ieee.org/ieee/802.3ad/5694/)
10. [IEEE 802.1AB - Link Layer Discovery Protocol (LLDP)](https://standards.ieee.org/ieee/802.1AB/8311/)
14. [NetworkLessons.com – VLAN, STP, EtherChannel Tutorials](https://networklessons.com)
15. [GNS3Vault.com – Packet Tracer and GNS3 Labs](https://gns3vault.com)


