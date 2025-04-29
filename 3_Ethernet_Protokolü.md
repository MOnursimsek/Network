# 📘 Ethernet Protokolü

Ethernet, yerel alan ağı (LAN) teknolojilerinin temel taşıdır ve günümüzde veri iletimi için en yaygın kullanılan ağ protokolüdür. İlk olarak 1973 yılında Xerox PARC tarafından geliştirilmiş ve daha sonra IEEE tarafından **IEEE 802.3** standardı altında resmi hale getirilmiştir. Ethernet, kablolu ağlarda cihazlar arası veri iletişimini tanımlar ve veri iletiminde çerçeve yapısını, adresleme sistemini, hata tespit mekanizmalarını ve medya erişim yöntemlerini içerir.



##  Ethernet'in Temel Özellikleri

| Özellik | Açıklama |
|--------|----------|
| **Standart** | IEEE 802.3 |
| **İletim Türü** | Paket anahtarlamalı, yarı/çift yönlü |
| **Bağlantı Ortamı** | Koaksiyel kablo, UTP/STP kablo, fiber optik |
| **Adresleme** | MAC adresi (48-bit) |
| **Çerçeve Tipi** | Ethernet II, IEEE 802.3 |
| **Erişim Yöntemi** | CSMA/CD (Carrier Sense Multiple Access with Collision Detection) |



##  Ethernet Standartları ve Gelişimi

Ethernet yıllar içinde gelişerek farklı hız ve ortam seçenekleriyle birçok standart ortaya çıkmıştır:

| Standart | Hız | Ortam | Açıklama |
|---------|-----|-------|----------|
| **10BASE-T** | 10 Mbps | UTP | İlk yaygın Ethernet |
| **100BASE-TX (Fast Ethernet)** | 100 Mbps | Cat5 | Daha hızlı veri iletimi |
| **1000BASE-T (Gigabit Ethernet)** | 1 Gbps | Cat5e/Cat6 | Günümüzün standartları arasında |
| **10GBASE-T** | 10 Gbps | Cat6a/Cat7 | Veri merkezlerinde yaygın |
| **100GBASE** | 100 Gbps | Fiber | Büyük veri merkezleri için kullanılır |


##  Ethernet Çerçeve Yapısı

```
| Ön Ekleme | Başlatıcı | Hedef MAC | Kaynak MAC | EtherType |     Veri     |   CRC  |
|-----------|-----------|-----------|------------|-----------|--------------|--------|
| 7 byte    | 1 byte    | 6 byte    | 6 byte     | 2 byte    | 46–1500 byte | 4 byte |
```

### 1. **Preamble (Ön Ekleme)** – 7 byte

- Görevi: Alıcı cihazın sinyale senkronize olmasını sağlar.
- İçeriği: `10101010` bit dizisi tekrarlanır.
- Fiziksel katmana özgü bir sinyalizasyon dizisidir.

### 2. **Start Frame Delimiter (SFD / Başlatıcı)** – 1 byte

- Görevi: Çerçevenin başlangıcını işaret eder.
- Değeri sabittir: `10101011`
- Preamble ile birlikte çalışır: Alıcı "Artık veri başlıyor!" sinyalini bu byte ile alır.



### 3. **Destination MAC Address (Hedef MAC Adresi)** – 6 byte

- Çerçevenin ulaşacağı cihazın MAC adresidir.
- Eğer adres: `FF:FF:FF:FF:FF:FF` ise bu bir **broadcast**'tır (tüm cihazlara gönderilir).
- Multicast veya unicast olabilir.

### 4. **Source MAC Address (Kaynak MAC Adresi)** – 6 byte

- Çerçeveyi gönderen cihazın MAC adresidir.
- Switch'ler MAC adres tablolarını bu alana bakarak oluşturur.

### 5. **EtherType** – 2 byte

- Üst katman protokolünü belirtir.
- Bu alandaki değere göre, Ethernet üstünde taşınan protokol anlaşılır.

#### Yaygın EtherType Değerleri:
| EtherType | Açıklama |
|-----------|----------|
| `0x0800` | IPv4 |
| `0x86DD` | IPv6 |
| `0x0806` | ARP |
| `0x8847` | MPLS |
| `0x8100` | 802.1Q VLAN etiketi (bu durumda başka bir başlık daha eklenir) |


### 6. **Payload (Veri Alanı)** – 46 ila 1500 byte

- Üst katmanlardan gelen gerçek veridir (IP paketi, ARP verisi vs.).
- Minimum uzunluk: 46 byte. Eğer daha azsa **padding (doldurma bitleri)** eklenir.
- Maksimum uzunluk: 1500 byte (daha fazlası için **Jumbo Frame** gerekebilir).


### 7. **Frame Check Sequence (FCS/CRC)** – 4 byte

- **Hata denetimi** için kullanılır.
- Gönderen cihaz, tüm çerçeve için **CRC (Cyclic Redundancy Check)** hesaplar ve buraya yazar.
- Alıcı cihaz aynı hesaplamayı yapar. Fark varsa çerçeve atılır (**hata tespiti yapılır ama düzeltme yapılmaz**).



###  Ethernet Frame Örneği (IPv4 İçeren)

| Alan | Değer (örnek) |
|------|---------------|
| Hedef MAC | `AA:BB:CC:DD:EE:FF` |
| Kaynak MAC | `11:22:33:44:55:66` |
| EtherType | `0x0800` (IPv4) |
| Veri | IP başlığı + TCP başlığı + veri |
| CRC | 4 byte’lık CRC değeri |


Tabii! Aşağıda **MAC adresleme (Media Access Control Addressing)** hakkında detaylı ve öğretici bir makale bulacaksın. Bu makale, Cisco CCNA düzeyinde hazırlanmış olup ağ temelleriyle ilgilenen herkes için uygundur.


## MAC Adresleme 


###  MAC Adresi Nedir?

**MAC adresi** (Media Access Control Address), bir ağ arabirim kartına (NIC - Network Interface Card) **fiziksel olarak atanmış benzersiz bir tanımlayıcıdır**. Veri bağlantı katmanında (Layer 2) çalışır ve ağdaki cihazların **birbirlerini tanımasını** sağlar.

- **Donanımsal**dır ve genellikle üretici tarafından karta yazılmıştır.
- **Değiştirilemez** olarak bilinir ama bazı işletim sistemlerinde yazılımsal olarak değiştirilebilir (spoofing).


### 2. MAC Adresi Formatı

Bir MAC adresi:

- **48 bit (6 byte)** uzunluğundadır.
- Genellikle **12 hexadecimal karakter** ile ifade edilir.
- 6 grupluk yapıdadır:
  ```
  Örnek: 00:1A:2B:3C:4D:5E
  ```

#### Parçaları:

| Kısım                                        | Uzunluk             | Açıklama                   |
| -------------------------------------------- | ------------------- | -------------------------- |
| **OUI (Organizationally Unique Identifier)** | İlk 24 bit (3 byte) | Üreticiyi tanımlar.        |
| **NIC Specific (Device ID)**                 | Son 24 bit (3 byte) | Cihaza özel seri numarası. |


### MAC Adres Türleri

#### Unicast MAC Adresi:

- Tek bir cihaza yöneliktir.
- MAC adresinin ilk baytının en düşük bitinin (LSB) 0 olması, bunun unicast olduğunu belirtir.
- Örn: `00:1A:2B:3C:4D:5E`

#### Broadcast MAC Adresi:

- Aynı ağdaki **tüm cihazlara gönderim** yapılır.
- Adres: `FF:FF:FF:FF:FF:FF`

#### Multicast MAC Adresi:

- Belirli bir grup cihaz hedeflenir.
- IPv4 için adresler: `01:00:5E:xx:xx:xx`
- Son bit **1** ise multicast olabilir.


## CSMA/CD Mekanizması

**CSMA/CD (Carrier Sense Multiple Access with Collision Detection)**, Ethernet’in eski yarı-duplex ortamlarda çakışmaları önlemek için kullandığı yöntemdir.

### Çalışma Prensibi:
1. Cihaz iletim yapmadan önce ortamı dinler (Carrier Sense).
2. Ortam boşsa iletim yapılır.
3. Çakışma (Collision) olursa algılanır.
4. Tüm cihazlar rastgele süre bekler (Backoff) ve yeniden dener.

> Günümüzde kullanılan anahtarlamalı (switched) tam-duplex ağlarda CSMA/CD gerekmez.


### Collision Domain (Çarpışma Alanı) Nedir?

**Collision domain**, çarpışma ihtimalinin olduğu bir ağ segmentidir. Bir çarpışma domain’inde bulunan tüm cihazlar aynı anda veri gönderemez.

- **Hub**: Tek bir collision domain’e sahiptir. Tüm portlar çarpışma paylaşır.
- **Switch**: Her portu ayrı bir collision domain’dir. Yani 24 portlu bir switch, 24 çarpışma alanı oluşturur.
- **Router**: Tüm arayüzleri farklı collision domain’dir.

### Broadcast Domain (Yayın Alanı) Nedir?

**Broadcast domain**, bir yayın paketinin (broadcast) ulaşabileceği cihazların tümünü kapsar. Aynı subnet içinde yer alan cihazlar genelde aynı broadcast domain içindedir.

- **Switch**: Yayın paketlerini tüm portlara iletir (aynı VLAN içindeyse).
- **Router**: Yayın paketlerini **iletmez**, yani broadcast domain’leri sınırlar.
- **VLAN** kullanarak da switch üzerinde broadcast domain’ler ayrılabilir.

## Ağda Kaç Collision ve Broadcast Domain Olduğu Nasıl Anlaşılır?

Örnek:
- 1 adet 24 portlu **hub** → 1 collision domain, 1 broadcast domain
- 1 adet 24 portlu **switch** → 24 collision domain, 1 broadcast domain
- 1 adet **router** → Her port kendi broadcast ve collision domain’idir


## Ethernet’te Kullanılan Bağlantı Ortamları (Medya)


###  1. **Koaksiyel Kablo (Coaxial Cable)**  
- **Eskiden** kullanılan bir kablo türüdür (10BASE5 ve 10BASE2).  
- Ortak bir iletim hattı üzerinde çalışır.  
- Günümüzde **neredeyse tamamen terk edilmiştir**.



###  2. **UTP (Unshielded Twisted Pair)**  
- Günümüzde **en yaygın kullanılan** Ethernet kablosudur.  
- 4 çift bükülmüş bakır tel içerir.  
- **RJ-45** konnektörüyle kullanılır.  
- Cat 5e ve Cat 6 türleri ofislerde çok yaygındır.



###  3. **STP (Shielded Twisted Pair)**  
- UTP'nin daha korumalı versiyonudur.  
- Her tel çifti elektromanyetik parazite karşı **folyo veya örgü ile kaplıdır**.  
- Fabrika gibi girişimin yoğun olduğu yerlerde kullanılır.



###  4. **Fiber Optik Kablo**  
- Veriyi **ışık darbeleriyle** iletir.  
- Çok daha **uzun mesafe** ve **yüksek hız** sunar.  
- **Elektromanyetik girişime karşı tamamen bağışıktır.**

#### İki türü vardır:  
- **Multimode (MMF):** Kısa mesafe, kampüs içi.  
- **Singlemode (SMF):** Uzun mesafe, metro/WAN ağlarında.



###  5. **Kablosuz Ortam (Wireless Ethernet)**  
- Ethernet protokolü kablosuz doğrudan kullanılmaz ama **köprüleme ile desteklenebilir**.  
- Kablosuz ağlar genelde **IEEE 802.11 (Wi-Fi)** kullanır.



###  Özet Tablo

| Medya Türü | Mesafe | Hız | Kullanım |
|------------|--------|-----|----------|
| Koaksiyel  | ~500 m | 10 Mbps | Tarihsel |
| UTP        | 100 m  | 1-10 Gbps | LAN'lar |
| STP        | 100 m  | 1-10 Gbps | Endüstriyel |
| Fiber      | 10+ km | 1-100 Gbps | WAN/LAN |
| Kablosuz   | Değişken | 100 Mbps - 1 Gbps | Geçici/taşınabilir |


## 🔹 Kaynakça
[GeeksforGeeks. (n.d.). *Ethernet Frame Format* ](https://www.geeksforgeeks.org/ethernet-frame-format/)

[Wikipedia Ethernet](https://tr.wikipedia.org/wiki/Ethernet)
