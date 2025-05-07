# **Kablosuz LAN (WLAN)**
**Kablosuz Yerel Alan Ağı (Wireless Local Area Network - WLAN)**, cihazların bir erişim noktası (Access Point - AP) üzerinden radyo dalgaları ile iletişim kurduğu bir yerel ağ türüdür. Geleneksel LAN’lardan farklı olarak fiziksel kablolara ihtiyaç duymaz. WLAN'lar, özellikle mobil cihazların yaygınlaşmasıyla birlikte evlerden işletmelere kadar birçok alanda kullanılmaktadır.

Avantajları:

* Kolay kurulum ve esneklik
* Mobilite (kabloya bağlı kalmadan hareket özgürlüğü)
* Genişleme kolaylığı (ekstra kablo çekmeden cihaz ekleme)

Dezavantajları:

* Güvenlik tehditlerine daha açık (örneğin: yetkisiz erişim, şifre kırma)
* Parazit ve sinyal engellerine duyarlı
* Kablosuz ağlar genellikle kablolu ağlara göre daha düşük hız ve daha yüksek gecikme sunabilir

## Kablosuz Ağ Türleri

Kablosuz ağlar kullanım alanlarına ve ölçeklerine göre çeşitli türlere ayrılır. En yaygın kablosuz ağ türleri şunlardır:

### 1. **WPAN (Wireless Personal Area Network) – Kablosuz Kişisel Alan Ağı**

* **Kapsam**: Genellikle 10 metreye kadar
* **Teknolojiler**: Bluetooth, ZigBee, IR (Kızılötesi)
* **Kullanım Alanı**: Cihazlar arası kısa mesafeli iletişim (örneğin: kulaklık – telefon bağlantısı)

### 2. **WLAN (Wireless Local Area Network) – Kablosuz Yerel Alan Ağı**

* **Kapsam**: Ofis, ev, okul gibi küçük/mid ölçekli alanlar
* **Teknolojiler**: IEEE 802.11 a/b/g/n/ac/ax (Wi-Fi)
* **Kullanım Alanı**: Bilgisayar, telefon ve diğer cihazların aynı ağ üzerinden internete erişmesini sağlamak

### 3. **WMAN (Wireless Metropolitan Area Network) – Kablosuz Metropol Alan Ağı**

* **Kapsam**: Bir şehir veya büyük kampüs
* **Teknolojiler**: WiMAX (IEEE 802.16), LTE
* **Kullanım Alanı**: Geniş bir alana yayılmış kullanıcıları kablosuz olarak bağlamak

### 4. **WWAN (Wireless Wide Area Network) – Kablosuz Geniş Alan Ağı**

* **Kapsam**: Ülke geneli veya küresel
* **Teknolojiler**: 3G, 4G, 5G, uydu iletişimi
* **Kullanım Alanı**: Cep telefonları ve mobil cihazlar için geniş kapsamlı internet erişimi

## Kablosuz Teknolojiler

Kablosuz ağlarda veri iletimini sağlayan teknolojiler farklı ihtiyaçlara göre çeşitlenmiştir. İşte yaygın kablosuz teknolojiler:

### 1. **Wi-Fi (IEEE 802.11)**

* **Açıklama**: WLAN’ın temelini oluşturan teknolojidir.
* **Sürümleri**:

  * 802.11a/b/g/n/ac/ax (Wi-Fi 6), 802.11be (Wi-Fi 7)
* **Frekanslar**: 2.4 GHz, 5 GHz, 6 GHz
* **Kullanım**: Ev, ofis, okul, kamu alanları

### 2. **Bluetooth**

* **Açıklama**: Düşük enerji tüketimli, kısa mesafeli cihaz iletişim protokolüdür.
* **Sürümler**: Bluetooth 4.0, 5.0, 5.3 vb.
* **Kullanım**: Kulaklık, klavye, fare, telefon veri paylaşımı

### 3. **NFC (Near Field Communication)**

* **Açıklama**: Çok kısa mesafede (yaklaşık 4 cm) iletişim kuran bir teknolojidir.
* **Kullanım**: Temassız ödeme sistemleri, erişim kartları

### 4. **ZigBee ve Z-Wave**

* **Açıklama**: IoT ve ev otomasyonu için kullanılan düşük enerji tüketimli protokoller
* **Kullanım**: Akıllı ev sistemleri (ışık, güvenlik, sensör)

### 5. **Infrared (IR)**

* **Açıklama**: Kızılötesi ışık ile veri aktarımı sağlar; doğrusal görüş gerektirir.
* **Kullanım**: Eski uzaktan kumandalar, bazı mobil veri transferleri

### 6. **Cellular (Mobil Ağlar)**

* **Teknolojiler**: 2G, 3G, 4G, 5G, LTE
* **Kullanım**: Mobil internet, telefon görüşmesi, mobil veri

### 7. **WiMAX (Worldwide Interoperability for Microwave Access)**

* **Açıklama**: Geniş alanlara yüksek hızlı internet erişimi sunar (IEEE 802.16)
* **Kullanım**: Kırsal internet, metro ağları


## WLAN Mimarisi: Temel Bileşenler ve Çalışma Yapısı

Bir **Kablosuz Yerel Alan Ağı (WLAN)**, çeşitli donanım ve yazılım bileşenlerinin birlikte çalışmasıyla cihazların kablosuz olarak iletişim kurmasına olanak tanır. WLAN mimarisi, kablosuz istemcilerin ağa bağlanmasını ve ağ hizmetlerinden (internet, dosya paylaşımı, yazıcı erişimi vb.) yararlanmasını sağlar.

### 1. Access Point (AP) – Erişim Noktası

**Access Point (AP)**, kablosuz istemcilerin kablolu bir ağa bağlanabilmesini sağlayan köprü (bridge) görevi gören cihazdır. Bir anlamda, AP kablosuz cihazlar ile LAN arasında bir “geçit”tir.

#### Görevleri:

* Kablosuz istemcilerden gelen radyo sinyallerini alır ve bunları Ethernet kablosu üzerinden iletir.
* Aynı zamanda geleneksel Ethernet verisini kablosuz sinyale çevirir ve istemcilere iletir.
* Cihazlara IP adresi verilmesini doğrudan sağlamaz (bunu DHCP sunucusu yapar), ancak bu iletişimi yönlendirir.

#### Türleri:

* **Bağımsız (Autonomous) AP**: Kendi başına çalışan, yönetimi yerel yapılan AP’lerdir. Genellikle küçük ağlarda kullanılır.
* **Hafif (Lightweight) AP**: Yönetim yeteneklerinin çoğunu bir WLC’ye devreden, sadece radyo iletişimi yapan AP türüdür. Kurumsal ağlarda tercih edilir.

### 2. Kablosuz İstemciler (Wireless Clients)

Kablosuz istemciler, WLAN’a bağlanarak ağ üzerindeki kaynaklara erişen cihazlardır. Her istemci bir kablosuz ağ adaptörüne sahip olmalıdır.

#### Örnek Kablosuz İstemciler:

* Laptop, masaüstü bilgisayar (Wi-Fi adaptörüyle)
* Akıllı telefon, tablet
* Yazıcılar
* Güvenlik kameraları
* IoT cihazları (akıllı prizler, sensörler vb.)

### 3.  **Wireless LAN Controller (WLC) – Kablosuz LAN Denetleyicisi**

**WLC**, birden çok Access Point’in merkezi olarak yönetildiği cihazdır. Kurumsal ağlarda çok sayıda AP’nin yapılandırılması, güvenliği ve izlenmesi için kullanılır.

#### Temel Görevleri:

* Hafif AP’lerin tüm yapılandırma, güvenlik ve yazılım güncellemelerini merkezi olarak sağlar.
* AP’lerin frekans, kanal ve çıkış gücü gibi ayarlarını dinamik olarak yönetir.
* Kablosuz istemcilerin kimlik doğrulama sürecini yönetir.
* VLAN ataması, ACL uygulaması ve QoS gibi gelişmiş işlemleri kontrol eder.
* Mobil istemcilerin roaming işlemini hızlı ve kesintisiz hale getirir.

## IEEE 802.11 Standartları ve Gelişimi

**IEEE 802.11**, kablosuz yerel alan ağları (WLAN) için tanımlanmış teknik bir standart ailesidir. Bu standartlar, cihazların radyo frekansı üzerinden nasıl iletişim kuracağını, veri iletim hızlarını, frekans bantlarını, modülasyon tekniklerini ve güvenlik yöntemlerini belirler.

Standartlar **IEEE (Institute of Electrical and Electronics Engineers)** tarafından tanımlanır ve geliştirilir. İlk olarak 1997 yılında yayımlanan temel 802.11 standardı zamanla yeni protokollerle güncellenmiş, daha hızlı, daha güvenli ve daha kararlı hale gelmiştir.



### 🔹 **IEEE 802.11 (1997) – Temel Standart**

* **Frekans Bandı**: 2.4 GHz
* **Maksimum Hız**: 2 Mbps
* **Modülasyon**: FHSS (Frequency Hopping Spread Spectrum), DSSS (Direct Sequence Spread Spectrum)
* **Not**: İlk çıkan sürüm olup düşük hızdan ve kararsızlıktan dolayı sınırlı kullanım gördü.

### 🔹 **IEEE 802.11b (1999)**

* **Frekans Bandı**: 2.4 GHz
* **Maksimum Hız**: 11 Mbps
* **Modülasyon**: DSSS, CCK (Complementary Code Keying)
* **Gelişme**: İlk yaygın kablosuz standardıdır; WLAN’ın ticari olarak yaygınlaşmasını sağlamıştır.
* **Sorunlar**: 2.4 GHz bandı kalabalık olduğundan parazit ve sinyal çakışması yaşanır.

### 🔹 **IEEE 802.11a (1999)**

* **Frekans Bandı**: 5 GHz
* **Maksimum Hız**: 54 Mbps
* **Modülasyon**: OFDM (Orthogonal Frequency Division Multiplexing)
* **Avantaj**: Daha az parazit; daha fazla kanal
* **Sınırlama**: Daha kısa menzil; cihaz uyumluluğu sınırlıydı

### 🔹 **IEEE 802.11g (2003)**

* **Frekans Bandı**: 2.4 GHz
* **Maksimum Hız**: 54 Mbps
* **Modülasyon**: OFDM (802.11a ile aynı), geriye dönük 802.11b uyumu
* **Avantaj**: 802.11b cihazlarla uyumlu, ama daha yüksek hız
* **Sorunlar**: 2.4 GHz bandının kalabalıklığı devam etti

### 🔹 **IEEE 802.11n (2009) – Wi-Fi 4**

* **Frekans Bantları**: 2.4 GHz ve 5 GHz (çift bant desteği)
* **Maksimum Hız**: 600 Mbps’ye kadar (teorik)
* **Teknolojiler**:

  * **MIMO (Multiple Input Multiple Output)**: Birden çok anten ile veri paralel iletilir
  * **Channel Bonding**: 20 MHz yerine 40 MHz kanal genişliği
* **Avantaj**: Daha yüksek hız, daha geniş kapsama alanı, daha kararlı bağlantı

### 🔹 **IEEE 802.11ac (2013) – Wi-Fi 5**

* **Frekans Bandı**: 5 GHz (yalnızca)
* **Maksimum Hız**: 1.3 Gbps (Wave 1), 3.5 Gbps’ye kadar (Wave 2)
* **Teknolojiler**:

  * Geliştirilmiş MIMO
  * **MU-MIMO (Multi-User MIMO)**: Aynı anda birden fazla cihaza veri iletimi
  * **Beamforming**: Sinyalin yönlendirilmesi
* **Avantaj**: Yüksek yoğunluklu ortamlarda daha yüksek performans

### 🔹 **IEEE 802.11ax (2019) – Wi-Fi 6**

* **Frekans Bantları**: 2.4 GHz ve 5 GHz
* **Maksimum Hız**: 9.6 Gbps (teorik)
* **Teknolojiler**:

  * **OFDMA (Orthogonal Frequency Division Multiple Access)**: Verimliliği artırır
  * **Gelişmiş MU-MIMO**: Yüksek cihaz sayısına destek
  * **Target Wake Time (TWT)**: Enerji verimliliği
* **Avantaj**: Kalabalık ortamlarda düşük gecikme, yüksek verim

### 🔹 **IEEE 802.11ax (2021+) – Wi-Fi 6E**

* **Frekans Bandı**: **6 GHz**
* **Yenilik**:

  * Daha fazla kanal (geniş bant genişliği)
  * Daha düşük parazit
  * Wi-Fi 6'nın tüm özelliklerini daha verimli ortamda kullanma
* **Sınırlama**: Yeni donanım gerektirir (Wi-Fi 6E destekli cihazlar)

### 🔹 **IEEE 802.11be (Beklenen: 2024+) – Wi-Fi 7**

* **Frekans Bantları**: 2.4 GHz, 5 GHz, 6 GHz
* **Maksimum Hız**: 46 Gbps (teorik)
* **Teknolojiler**:

  * **320 MHz Kanal Genişliği**
  * **16x16 MU-MIMO**
  * **Multi-Link Operation (MLO)**: Aynı anda birden çok bandı kullanma
* **Hedef**: AR/VR, 8K video, ultra düşük gecikmeli uygulamalar

### Özet Tablosu:

| Standart      | Yıl   | Frekans     | Maks. Hız    | Teknoloji / Özellik   |
| ------------- | ----- | ----------- | ------------ | --------------------- |
| 802.11        | 1997  | 2.4 GHz     | 2 Mbps       | DSSS/FHSS             |
| 802.11b       | 1999  | 2.4 GHz     | 11 Mbps      | CCK                   |
| 802.11a       | 1999  | 5 GHz       | 54 Mbps      | OFDM                  |
| 802.11g       | 2003  | 2.4 GHz     | 54 Mbps      | OFDM, uyumluluk       |
| 802.11n       | 2009  | 2.4/5 GHz   | 600 Mbps     | MIMO, Channel Bonding |
| 802.11ac      | 2013  | 5 GHz       | 1.3–3.5 Gbps | MU-MIMO, Beamforming  |
| 802.11ax      | 2019  | 2.4/5 GHz   | 9.6 Gbps     | OFDMA, TWT, MU-MIMO   |
| 802.11ax (6E) | 2021  | 6 GHz       | 9.6 Gbps     | Daha fazla kanal      |
| 802.11be      | 2024+ | 2.4/5/6 GHz | 46 Gbps      | Wi-Fi 7, MLO          |

## WLAN Modları ve Topolojileri

WLAN (Wireless Local Area Network), kullanıcıların kablo kullanmadan ağ kaynaklarına erişmesini sağlar. Ancak kablosuz cihazların nasıl bağlandığı, ağda nasıl iletişim kurduğu ve ağın yapısal düzeni; kullanılan **WLAN modu** ve **topolojisi** ile belirlenir. Bu yapı, ağın kurulum şeklini, yönetim modelini ve performansını doğrudan etkiler.

### WLAN Modları

WLAN’de cihazların birbirleriyle nasıl haberleştiği, seçilen **çalışma modu** ile tanımlanır. Başlıca modlar şunlardır:

### 1. **Infrastructure Mode (Altyapı Modu)**

Bu modda, tüm kablosuz istemciler **Access Point (AP)** üzerinden haberleşir. Modern WLAN’ların büyük çoğunluğu bu modda çalışır.

* **İletişim**: Cihazlar direkt birbirleriyle değil, AP aracılığıyla haberleşir.
* **Bileşenler**: AP, kablosuz istemciler, opsiyonel olarak WLC (Wireless LAN Controller)
* **Avantajlar**:

  * Merkezileştirilmiş yönetim
  * Güvenlik politikaları kolay uygulanabilir
  * Geniş kapsama alanı (birden fazla AP ile)
  * Roaming (gezici cihazlar AP’ler arasında geçiş yapabilir)
* **Kullanım Alanları**: Kurumsal ağlar, okullar, havaalanları, AVM'ler

**Topoloji**:

```
[İstemci] <---> [AP] <---> [Router/Switch]
```

### 2. **Ad-Hoc Mode (Peer-to-Peer / IBSS Mode)**

Bu modda kablosuz cihazlar **doğrudan** birbirine bağlanır; herhangi bir AP’ye gerek yoktur.

* **İletişim**: Cihazlar arasında doğrudan (peer-to-peer)
* **Avantajlar**:

  * Basit kurulum
  * Küçük ve geçici ağlar için uygun
* **Dezavantajlar**:

  * Kapsama alanı sınırlı
  * Merkezi güvenlik yönetimi yapılamaz
  * Roaming desteği yok
* **Kullanım Alanları**: Geçici dosya paylaşımları, taşınabilir cihazlar arası bağlantılar

**Topoloji**:

```
[İstemci] <-----> [İstemci]
```

### 3. **Mesh Mode (Wireless Mesh Network)**

Bu modda AP’ler hem istemcilere hizmet verir hem de birbirleriyle kablosuz olarak haberleşir. Her AP, diğer AP’lerle kablosuz bağlantı kurarak **çok noktalı bir ağ** yapısı oluşturur.

* **İletişim**: AP’ler birbirine kablosuz olarak bağlı; merkezi AP gerekmez
* **Avantajlar**:

  * Kapsama alanı esnek şekilde genişletilebilir
  * Tek bir noktaya kablo çekmeye gerek kalmadan geniş ağlar kurulabilir
  * Yedeklilik ve oto-iyileştirme desteği
* **Dezavantajlar**:

  * Konfigürasyonu karmaşıktır
  * Her mesh noktası, bant genişliğini paylaşır (performans kaybı olabilir)
* **Kullanım Alanları**: Şehir ağı projeleri, büyük kampüsler, afet bölgeleri

**Topoloji**:

```
[Mesh AP] <---> [Mesh AP] <---> [Mesh AP]
          \                        /
           \---> [İstemci] <-----/
```

### 4. **Repeater / Extender Mode**

Bu modda bir cihaz, mevcut bir WLAN sinyalini **genişletmek** amacıyla kullanılır. Repeater cihazı, orijinal AP’den aldığı sinyali yeniden yayınlar.

* **İletişim**: Repeater, hem istemcilerle hem ana AP ile iletişim kurar
* **Avantajlar**:

  * Sinyal ölü noktalarını kapsar
  * Kablo ihtiyacı olmadan kapsama alanı genişletilir
* **Dezavantajlar**:

  * Bant genişliği ikiye bölünür (performans düşebilir)
  * Gelişmiş güvenlik konfigürasyonları zordur
* **Kullanım Alanları**: Ev ağları, küçük ofisler

**Topoloji**:

```
[AP] <---> [Repeater] <---> [İstemci]
```

### WLAN Topolojileri

WLAN ağları farklı **topoloji yapılarında** organize edilebilir. Bu yapılar ağın tasarımını, yayılmasını ve yönetimini belirler:

| Topoloji Türü           | Açıklama                                                                                                 |
| ----------------------- | -------------------------------------------------------------------------------------------------------- |
| **Star (Yıldız)**       | En yaygın yapıdır. Tüm cihazlar bir AP’ye bağlıdır. Altyapı modunu kullanır.                             |
| **Mesh (Ağ)**           | AP’ler birbirine kablosuz bağlıdır, istemciler bu AP’lere bağlanır. Merkezi yapı gerekmez.               |
| **Point-to-Point**      | İki AP arasında doğrudan bağlantı kurulur. Genellikle iki bina arası kablosuz köprüleme için kullanılır. |
| **Point-to-Multipoint** | Bir AP, birden çok uzak AP’ye bağlantı sağlar. Merkezden çok noktaya yayın yapılır.                      |

## Frekans Bantları, Kanal Planlaması

WLAN ağlarının güvenilir, verimli ve kararlı çalışabilmesi için RF (radyo frekansı) spektrumu üzerinde etkili bir **frekans ve kanal yönetimi** yapılmalıdır. Kablosuz cihazlar aynı ortamda birbirleriyle paylaşım yaptıkları için **girişim (interference)** problemi yaşanabilir. Bunu minimize etmek için frekans, kanal ve RF tasarımı profesyonelce planlanmalıdır.

### Frekans Bantları

WLAN cihazları, IEEE 802.11 standartlarına uygun olarak üç temel frekans bandında çalışır:

#### A. 2.4 GHz Bandı

* **Frekans aralığı**: 2.400 MHz – 2.483,5 MHz (toplam 83.5 MHz genişlik)
* **Kanal genişliği**: Her kanal 20 MHz genişliğinde
* **Toplam kanal sayısı**: 14 (ancak Türkiye'de kanal 1–13 kullanılabilir)
* **Çakışmayan kanal sayısı**: Sadece **3** (kanal 1, 6 ve 11)

Kanal aralıkları 5 MHz iken, her kanal 20 MHz genişlik kaplar. Bu da demektir ki:

* Kanal 1 → 2401–2421 MHz
* Kanal 2 → 2406–2426 MHz
* Kanal 3 → 2411–2431 MHz
  … ve bu şekilde **her kanal üst üste biner**.

Bu yüzden **yalnızca 1, 6 ve 11** numaralı kanallar çakışmaz.

#### B. 5 GHz Bandı

* **Frekans aralığı**: 5.150 MHz – 5.825 MHz (ülkelere göre değişebilir)
* **Kanal genişlikleri**: 20 MHz, 40 MHz, 80 MHz ve 160 MHz
* **Çakışmayan kanal sayısı**: 20’den fazla

#### C. 6 GHz Bandı (Wi-Fi 6E ve Wi-Fi 7)

* **Frekans aralığı**: 5.925 MHz – 7.125 MHz
* **Kanal genişlikleri**: 20 / 40 / 80 / 160 MHz
* **Toplam kanal sayısı**: \~60+ (ülkeye göre değişir)

### Kanal Planlaması

Amaç: Kablosuz cihazlar arasında **kanal çakışmalarını** ve **girişimi** minimize etmek

####  A. Kanal Çakışma Türleri:

| Tür                                     | Açıklama                                                                                                   |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Co-Channel Interference (CCI)**       | Aynı kanalın birden fazla AP tarafından kullanılması sonucu, cihazlar sırayla veri gönderir → verim düşer. |
| **Adjacent Channel Interference (ACI)** | Yandaki kanallarla sinyal çakışması olur, bu sinyaller birbirini bozar. 2.4 GHz bandında çok yaygındır.    |

#### 🔸 B. 2.4 GHz Kanal Planlama Stratejisi

* Yalnızca **1, 6, 11** kullanılmalı.
* Aynı kanaldaki AP'ler, fiziksel olarak birbirinden uzak yerleştirilmeli.
* Örnek yerleşim (üçgenleme yöntemi):

  * \[AP1: kanal 1] – \[AP2: kanal 6] – \[AP3: kanal 11]

#### 🔸 C. 5 GHz Kanal Planlama Stratejisi

* Çok sayıda çakışmayan kanal sayesinde esnek yapılandırma mümkün
* DFS ve TPC destekleyen cihazlar tercih edilmeli
* Kullanıcı yoğunluğuna göre 40 MHz / 80 MHz genişlikte kanal kullanılabilir


## SSID, BSSID ve ESSID Kavramları

### 🔹 SSID (Service Set Identifier)

* **Tanım**: Kablosuz ağın "isim" kısmıdır.
* **Görevi**: Ağları birbirinden ayırmak ve istemcilerin bağlanacağı ağı tanımlamak için kullanılır.
* **Özellikleri**:

  * Maksimum 32 karakter uzunluğundadır.
  * Genellikle Access Point’ler tarafından periyodik olarak beacon çerçeveleriyle yayınlanır.
  * Gizlenebilir (ancak bu, güvenlik sağlamaz).
* **Örnek**: Evdeki ağ adı: `EvWifi`, kafe ağı: `CafeNet`

### 🔹 BSSID (Basic Service Set Identifier)

* **Tanım**: Kablosuz ağın fiziksel kimliğini (MAC adresi) tanımlar.
* **Görevi**: SSID aynı olsa bile, Access Point’lerin birbirinden ayrılmasını sağlar.
* **Özellikleri**:

  * Genellikle Access Point’in radyo arabirimine ait MAC adresidir.
  * Her AP'nin her radyo frekansı için farklı bir BSSID’si olabilir.
  * Tek bir SSID altında birden çok BSSID bulunabilir.

> Aynı SSID’ye sahip farklı AP’ler, roaming (dolaşım) için yapılandırıldığında her biri farklı BSSID ile çalışır.

### 🔹 ESSID (Extended SSID)

* **Tanım**: Birden fazla AP’nin aynı SSID ile birleştiği genişletilmiş servis kümesinin adıdır.
* **Görevi**: Kurumsal ortamlarda, tüm AP'lerin aynı SSID'yi yayınladığı birleşik ağ yapısını ifade eder.
* **Özellikleri**:

  * İstemciler, erişim noktaları arasında kesintisiz dolaşım yapabilir.
  * ESSID ≈ SSID (terimsel olarak fark vardır ama günlük kullanımda eşanlamlı kullanılır)

## Kablosuz Güvenlik Protokolleri

Kablosuz ağlar, fiziksel kablo güvenliğinden yoksun olduğu için **şifreleme ve kimlik doğrulama** mekanizmalarına ihtiyaç duyar. Bu mekanizmalar kablosuz güvenlik protokolleriyle sağlanır.

### 🔸 WEP (Wired Equivalent Privacy)

* **İlk çıkan kablosuz güvenlik protokolüdür (1999)**
* **Şifreleme algoritması**: RC4
* **Anahtar yapısı**: 64-bit veya 128-bit (40-bit veya 104-bit kullanıcı anahtarı + 24-bit IV)
* **Zayıflıkları**:

  * IV (Initialization Vector) çok kısa ve tekrar edebilir
  * RC4 artık güvenli değil
  * Şifre kolayca kırılabilir (aircrack-ng gibi araçlarla dakikalar içinde)
* **Sonuç**: **Güvenli değildir, kesinlikle kullanılmamalıdır.**

### 🔸 WPA (Wi-Fi Protected Access)

* **WEP’in geçici halefidir.**
* **Şifreleme**: RC4 + TKIP (Temporal Key Integrity Protocol)
* **İyileştirme**:

  * Her paket için yeni şifreleme anahtarı
  * Anahtar karıştırma (key mixing)
* **Zayıf noktaları**:

  * RC4 kullanımı sürmektedir
  * TKIP günümüz tehditlerine karşı yeterli değildir
* **Sonuç**: WEP’ten daha güvenli, ama artık **zayıf** kabul edilir.

### 🔸 WPA2 (Wi-Fi Protected Access 2)

* **2004'te standartlaştı, uzun süre kurumsal standart oldu.**
* **Şifreleme**: AES (Advanced Encryption Standard) + CCMP (Counter Mode CBC-MAC Protocol)
* **Güçlü yönleri**:

  * Güçlü simetrik şifreleme (AES-CCMP)
  * DoS, spoofing ve veri gizliliğine karşı koruma
* **Saldırı türleri**:

  * KRACK saldırısı (4-yönlü el sıkışma açığı)
* **Kullanım türleri**:

  * WPA2-PSK (ev tipi)
  * WPA2-Enterprise (802.1X / RADIUS)

### 🔸 WPA3 (Wi-Fi Protected Access 3)

* **2018'de tanıtıldı, en güncel protokoldür.**
* **Şifreleme**: AES-CCMP + Gelişmiş SAE (Simultaneous Authentication of Equals)
* **Yenilikler**:

  * Brute-force parola saldırılarına karşı koruma (offline dictionary attack engellenir)
  * **Forward secrecy** desteği
  * WPA3-Enterprise: 192-bit güvenlik seviyesi
* **Zayıf yönü**:

  * Eski cihazlarla uyumsuz olabilir
* **Sonuç**: Günümüzde en güvenli seçenektir.



## RADIUS ve PSK Kavramları

### 🔸 RADIUS (Remote Authentication Dial-In User Service)

* **Merkezi kimlik doğrulama protokolü ve sunucusu**
* **Görevleri**:

  * Kullanıcı adı/parola doğrulama
  * Bağlantı yetkileri atama
  * Bağlantı süresi/log kayıtları tutma
* **Protokol**: UDP 1812 (Authentication) ve 1813 (Accounting)
* **Kurumsal ortamlarda** 802.1X ile birlikte kullanılır



### 🔸 PSK (Pre-Shared Key)

* **Önceden paylaşılan parola ile kimlik doğrulama yöntemi**
* **Kullanım alanı**: Ev, küçük ofis ağları (WPA/WPA2/WPA3-PSK)
* **İşleyiş**:

  * Tüm istemciler aynı şifreyi kullanır
  * Şifre girildikten sonra, 4-way handshake ile güvenli bağlantı kurulur
* **Zayıflıkları**:

  * Aynı şifre birçok kişiyle paylaşıldığında güvenlik düşer
  * Şifre sızarsa tüm ağ riske girer


## 802.11 Frame Yapısı

IEEE 802.11, kablosuz LAN (WLAN) protokolünde veri iletimi, çerçeve yapısı aracılığıyla gerçekleştirilir. 802.11 çerçeveleri, ağdaki cihazlar arasında verinin nasıl iletileceğini ve alınacağını belirleyen temel birimlerdir. Her bir çerçeve, başlık, veri ve denetim bilgileri içerir.

### 1. **Çerçeve Yapısının Genel Görünümü**

Bir 802.11 çerçevesi genellikle üç ana bölümden oluşur:

1. **Başlık (Header)** – Çerçevenin yönetim, adresleme ve kontrol bilgilerini içerir.
2. **Veri (Payload)** – Asıl iletilen veri paketini taşır.
3. **FCS (Frame Check Sequence)** – Hata kontrolü için kullanılan bir alan.

### 2. **Çerçeve Türleri**

802.11 standardı, farklı türde çerçeveler tanımlar. Her bir çerçeve türü, belirli bir işlevi yerine getiren veri iletimini sağlar. Bunlar şunlardır:

1. **Data Frame (Veri Çerçevesi)**: Kullanıcı verilerinin taşındığı çerçevelerdir.
2. **Management Frame (Yönetim Çerçevesi)**: Ağda istemciler ve Access Point’ler arasında ağ yönetim bilgileri taşır (örneğin, bağlantı isteği, ağ taraması).
3. **Control Frame (Kontrol Çerçevesi)**: Verilerin doğru ve verimli bir şekilde iletilmesi için kontrol sinyalleri taşır (örneğin, çerçeve sıralama, hata düzeltme).

### 3. **802.11 Çerçeve Başlık Yapısı**

Bir 802.11 çerçevesinin başlığı genellikle şu bileşenleri içerir:

1. **Frame Control**: Çerçeve türünü ve kontrol bilgilerini belirler. Örneğin:

   * Çerçeve türü (data, management, control)
   * Çerçevenin yönü (gelen, giden)
   * Çerçeve iletim hızı
2. **Duration/ID**: Çerçevenin süresi veya ID'si. Yönetim çerçevelerinde bu alan ağdaki zamanlamayı belirler.
3. **Address 1 (DA - Destination Address)**: Çerçevenin hedef adresi.
4. **Address 2 (SA - Source Address)**: Çerçevenin kaynak adresi.
5. **Address 3**: Genellikle Access Point (AP) adresi ya da, ağda yönlendirici olan cihazın adresidir.
6. **Sequence Control**: Çerçeve sırasını takip etmek ve veri iletimini yönetmek için kullanılır.
7. **Address 4**: Genellikle 802.11e ve sonraki sürümlerde kullanılan ek adres alanıdır (özellikle WLAN'in mesafe büyüdükçe).
8. **QoS Control**: Servis kalitesi (Quality of Service) bilgilerini içerir (Opsiyonel).

### 4. **Veri (Payload)**

* **İçerik**: Veri kısmı, genellikle kullanıcı verisini taşır ve burada ağ protokollerine ait veri paketleri bulunur.
* **Ethernet Çerçevesi**: 802.11 veri çerçevesinin içinde Ethernet çerçevesi de bulunabilir. Örneğin, bir IP paketi ya da TCP/UDP verisi.

### 5. **Frame Check Sequence (FCS)**

* **Hata Kontrolü**: Bu bölüm, iletilen çerçevenin hatasız olup olmadığını denetler. CRC (Cyclic Redundancy Check) algoritmasıyla çerçevenin doğruluğu kontrol edilir.
* **İşleyiş**: Çerçeve alıcıya ulaştığında, FCS alanı kullanılarak bir hata kontrolü yapılır. Eğer hata bulunursa, verinin yeniden iletilmesi istenir.

### 6. **Çerçeve Yapısının Detayları**

Her çerçeve, kullanılan IEEE 802.11 protokolüne ve çerçevenin türüne göre farklılık gösterebilir. Ancak, genellikle temel bir 802.11 çerçevesi aşağıdaki bileşenleri içerir:

| Alan                       | Boyut (bit) | Açıklama                                                                                 |
| -------------------------- | ----------- | ---------------------------------------------------------------------------------------- |
| Frame Control              | 2           | Çerçeve tipi ve kontrol bilgisi                                                          |
| Duration/ID                | 2           | Çerçevenin geçerlilik süresi ya da ID bilgisi                                            |
| Address 1                  | 6           | Hedef adres (Destination Address)                                                        |
| Address 2                  | 6           | Kaynak adres (Source Address)                                                            |
| Address 3                  | 6           | İlgili cihazın adresi (Access Point veya router)                                         |
| Sequence Control           | 2           | Çerçeve sırası ve kontrol bilgisi                                                        |
| Address 4                  | 6           | Opsiyonel bir alan, genellikle dört adresli çerçevelerde kullanılır (802.11e ve sonrası) |
| QoS Control                | 2           | Kalite kontrolü, trafik önceliği gibi bilgileri taşır                                    |
| Payload (Data)             | Değişken    | Asıl veri kısmı (IP paketleri, Ethernet çerçeveleri vs.)                                 |
| FCS (Frame Check Sequence) | 4           | Çerçevenin hata kontrolü, CRC (Cyclic Redundancy Check) ile doğrulama yapılır            |

### 7. **Çerçeve Tipleri ve Kullanım Alanları**

802.11 çerçevelerinin farklı türleri, ağda farklı işlevler için kullanılır:

1. **Data Frame (Veri Çerçevesi)**:

   * İstemci ve AP arasında veri iletimini sağlar.
   * Bu tür çerçeveler, genellikle kullanıcı verisi taşır.

2. **Management Frame (Yönetim Çerçevesi)**:

   * **Beacon Frames**: AP’nin varlığını duyurur.
   * **Association Request/Response**: Bir istemci, bir AP'ye bağlanmak için bu çerçeveyi gönderir.
   * **Disassociation/Deauthentication**: Bağlantıyı sonlandıran çerçevelerdir.

3. **Control Frame (Kontrol Çerçevesi)**:

   * **RTS (Request to Send) & CTS (Clear to Send)**: Çerçeve çakışmalarını engellemek için kullanılır.
   * **ACK (Acknowledgment)**: Veri iletiminin doğru şekilde alındığını onaylar.

## CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance) Protokolü

**CSMA/CA**, kablosuz ağlarda veri iletimini düzenleyen bir protokoldür. Bu protokol, özellikle çakışmaların sık yaşandığı kablosuz ortamda, veri iletimlerini koordine ederek verimli bir ağ iletişimi sağlamayı hedefler. CSMA/CA, IEEE 802.11 (Wi-Fi) standardında kullanılan ana protokollerden biridir ve temel amacı veri iletim çakışmalarını önlemektir.

### **CSMA/CA'nın Çalışma Prensibi**

CSMA/CA, iki ana aşamadan oluşur:

1. **Carrier Sense (Taşıyıcı Algılama)**

   * **Taşıyıcı Algılama** (Carrier Sense), bir cihazın veriyi göndermeden önce, ağ ortamının "boş" olup olmadığını kontrol etmesidir. Cihaz, iletim yapmak istediği frekansı dinler ve bu frekansta başka bir cihaz veri gönderiyorsa, iletim yapılmaz.
   * Bu adım, ağda bir çakışma olasılığını azaltmaya yönelik ilk adımdır. Ancak, **çoklu cihazlar aynı anda veri göndermek istediğinde** sorunlar ortaya çıkabilir.

2. **Collision Avoidance (Çakışma Önleme)**

   * **Çakışma Önleme** (Collision Avoidance), taşıyıcı algılamasının ardından gelir. Burada, bir cihaz veri iletmeye karar verirken, ağdaki diğer cihazlarla çakışma olasılığını önlemek için belirli bir **bekleme süresi** kullanılır.
   * Çakışma olasılığını daha da azaltmak için cihazlar, **backoff (geri sayım) mekanizması** kullanarak rastgele bir süre boyunca bekler. Bu bekleme süresi, ağda farklı cihazların sırasıyla veri iletmesini sağlamak amacıyla rastgele bir değere atanır.

### **CSMA/CA Protokolünün Adımları**

1. **Taşıyıcı Algılama (Carrier Sense)**:

   * Cihaz, ağda başka bir cihazın veri gönderip göndermediğini kontrol eder.
   * Eğer ağ "boş"sa (yani başka bir cihaz veri iletmiyorsa), cihaz veri iletmek için harekete geçer.
   * Eğer ağ "dolu"ysa (yani başka bir cihaz veri iletmekteyse), cihaz veri iletimi için bekler.

2. **RTS/CTS (Request to Send / Clear to Send)**:

   * Eğer cihaz, taşıyıcı algılama sonucunda ağda boş bir kanal bulursa, **RTS (Request to Send)** mesajını gönderir.
   * RTS mesajı, cihazın veri göndermeden önce bu isteği ağdaki diğer cihazlara bildirmesini sağlar.
   * Eğer hedef cihaz veri göndermesine izin veriyorsa, bir **CTS (Clear to Send)** mesajı gönderir.
   * RTS/CTS, özellikle uzun veri paketleri için çakışma olasılığını daha da azaltmaya yardımcı olur. Bu işlem, veri gönderimi öncesinde cihazların birbirlerinin iletimlerinin çakışmasını önlemeye yardımcı olur.

3. **Backoff (Geri Sayım) ve Çakışma Önleme**:

   * Eğer taşıyıcı algılama sırasında kanal doluysa veya RTS/CTS aşaması başarısız olursa, cihaz belirli bir süre boyunca bekler.
   * Cihaz, belirli bir **backoff süresi** boyunca rastgele bir süre boyunca bekler (bu süre, ağda çakışma riskini azaltmaya yardımcı olur).
   * Backoff süresi, **CW (Contention Window)** adı verilen bir değere dayalı olarak hesaplanır. Bu pencere, cihazın rastgele bekleme süresini belirler.
   * Backoff süresi sonunda, cihaz tekrar taşıyıcı algılamaya başlar.

4. **Veri Gönderimi ve Acknowledgment (Onay)**:

   * Eğer cihaz veri iletimi yaparsa, alıcı cihaz, iletimi doğru şekilde aldığını belirten bir **ACK (Acknowledgment)** mesajı gönderir.
   * Bu, veri iletiminin başarılı olduğunun bir göstergesidir. Eğer ACK mesajı alınmazsa, cihaz yeniden iletim için harekete geçer.

### **CSMA/CA'nın Zorlukları ve Kısıtlamaları**

1. **Hidden Node (Gizli Düğüm) Problemi**:

   * **Hidden node** problemi, bir cihazın başka bir cihazın iletimini duyamaması durumudur. Bu, taşıyıcı algılamanın düzgün çalışmaması nedeniyle çakışmalara neden olabilir. Örneğin, bir cihaz başka bir cihazla doğrudan iletişim kurmak istese de, iletimi gizli bir cihaz tarafından engellenebilir.
   * Bu sorunun çözümü için **RTS/CTS** protokolü kullanılır. RTS/CTS, cihazların birbirlerinin iletimlerini duymalarını sağlar ve gizli düğüm probleminin etkisini azaltır.

2. **Çakışmaların Tamamen Önlenememesi**:

   * CSMA/CA, çakışmaları önlemeye çalışırken, kanalın çok meşgul olduğu durumlarda veri iletimi gecikebilir.
   * Ağdaki cihaz sayısı arttıkça, geri sayım süreleri (backoff) artar ve bu da ağdaki genel verimliliği düşürebilir.

3. **Ağdaki Trafiğin Artması ile Backoff Sürelerinin Uzaması**:

   * Ağ yoğunlaştıkça, cihazların bekleme süreleri uzar, bu da veri iletiminin daha uzun süreler almasına ve ağın genel verimliliğinin düşmesine yol açar.
   * Bu sorunun önüne geçebilmek için kanal kapasitesi artırılabilir veya daha gelişmiş protokoller (örneğin, OFDMA) kullanılabilir.

### **CSMA/CA'nın Avantajları**

* **Çakışma Azaltma**: CSMA/CA, çakışma olasılığını önemli ölçüde azaltır, çünkü cihazlar veri iletimine başlamadan önce ağ ortamını dinler.
* **Basitlik ve Verimlilik**: Bu protokol, kablosuz ağlar için nispeten basit ve verimli bir çakışma öncesi mekanizma sunar.
* **Kolay Entegrasyon**: Wi-Fi cihazları ve ağ altyapısı, CSMA/CA protokolünü kullanarak kolayca entegre edilebilir.


## **Kablosuz Cihaz ile Access Point Arasındaki İletişim Aşamaları**

Kablosuz cihazlarla (örneğin, dizüstü bilgisayarlar, akıllı telefonlar veya tabletler) bir **Access Point (AP)** arasındaki iletişim, belirli bir dizi aşamadan geçer. Bu aşamalar, kablosuz ağın doğru şekilde çalışabilmesi için gerekli olan bağlantı ve veri iletimi süreçlerini kapsar. İletişim süreci genellikle aşağıdaki adımlardan oluşur:

### 1. **Tarama (Scanning)**

Kablosuz cihaz, çevresindeki **Access Point**'leri tespit etmek için tarama işlemi başlatır. Bu işlem, cihazın çevresindeki radyo dalgalarını dinleyerek mevcut ağları keşfetmesini sağlar. Tarama işlemi, iki farklı şekilde gerçekleştirilebilir:

* **Pasif Tarama**: Cihaz, çevresindeki AP’lerin yayınladığı sinyalleri bekler. AP’ler belirli aralıklarla **Beacon Frame** adında sinyaller gönderir ve bu sinyaller içinde SSID (Service Set Identifier) ve diğer ağ bilgileri yer alır.

* **Aktif Tarama**: Cihaz, AP’lere belirli bir istek (Probe Request) gönderir. AP’ler, bu isteğe yanıt olarak **Probe Response** gönderir. Bu işlem, cihazın ağları daha hızlı tespit etmesine yardımcı olabilir.

### 2. **Bağlantı Kurma (Association)**

Tarama tamamlandıktan sonra, cihaz en uygun **Access Point**'i seçer ve **Association Request** mesajı gönderir. Bu mesajda cihaz, bağlanmak istediği ağın SSID’si ve diğer bilgileri içerir.

* **Association Request**: Kablosuz cihaz, AP'ye bu mesajı göndererek bağlantı isteğinde bulunur.
* **Association Response**: AP, cihazın bağlantı talebini değerlendirir ve başarılı ise cihazı ağ ile ilişkilendirir. Bu yanıt genellikle **Association ID** (AID) içerir, bu da cihazın ağdaki benzersiz kimliğidir.

Bu aşama, cihazın Access Point ile olan bağlantısının başlangıcıdır ve cihazın AP ile iletişim kurmasına olanak tanır.

### 3. **Kimlik Doğrulama (Authentication)**

Bağlantı isteği yapıldıktan sonra, cihazın **kimlik doğrulama** işlemi yapılır. Bu adımda, cihazın ağdaki geçerli bir kullanıcı olup olmadığı doğrulanır. Kimlik doğrulama işlemi farklı yöntemlerle yapılabilir:

* **Açık Kimlik Doğrulama**: Bu yöntem, genellikle güvenlik gereksinimleri olmayan ağlarda kullanılır. Cihaz, Access Point ile bağlantı kurarken kimlik doğrulama adımı atlanabilir.

* **Şifreli Kimlik Doğrulama (WPA/WPA2/WPA3)**: Güvenli ağlarda, cihazın **WPA (Wi-Fi Protected Access)** veya **WPA2/WPA3** protokollerine göre kimliği doğrulanır. Cihazın doğru şifre (WPA-PSK) veya doğru kimlik bilgileri (802.1X, RADIUS sunucusu) sunması gerekir.

Bağlantı başarılı olursa, cihaz ve AP arasında bir **Authentication Success** mesajı iletildiği görülür.

### 4. **IP Adresi Alımı ve DHCP Süreci**

Kimlik doğrulaması tamamlandıktan sonra, cihazın ağ üzerinden internet erişebilmesi için bir IP adresine ihtiyacı vardır. Bu noktada, **DHCP (Dynamic Host Configuration Protocol)** devreye girer.

* Cihaz, IP adresini almak için **DHCP Discover** mesajı gönderir.
* **DHCP Server** (bu, genellikle ağdaki router veya ayrı bir sunucu olabilir), cihazdan gelen isteği alır ve bir IP adresiyle yanıtlar.
* Cihaz, DHCP server'dan aldığı IP adresini ve diğer ağ yapılandırmalarını (gateway, DNS sunucusu vb.) kullanarak internet erişimini sağlamak için hazır hale gelir.

### 5. **Veri İletimi (Data Transmission)**

Cihaz, AP ile bağlantı kurduktan ve IP adresini aldıktan sonra, artık veri iletimine başlayabilir. Bu aşama, cihazın ağ üzerindeki diğer cihazlarla iletişim kurmasını sağlar. Veri iletimi, genellikle **Data Frames** aracılığıyla yapılır ve şifreleme protokolleri devreye girebilir.

* Cihaz ve AP arasındaki veri iletimi, belirli aralıklarla **Data Frames** olarak paketlenir ve karşılıklı olarak iletilir.
* **Wi-Fi bağlantısındaki sinyal gücü ve bant genişliği**, iletilen verinin hızını ve kalitesini etkileyebilir.
* Güvenlik protokolleri (WPA2 veya WPA3) bu verileri şifreleyerek, ağdaki güvenliği sağlar.

### 6. **Roaming (Geçiş)**

Kablosuz cihazlar, aynı ağda birden fazla **Access Point**'in bulunduğu durumlarda bir AP'den diğerine geçiş yapabilir. Bu, özellikle büyük alanlarda çalışan cihazlar için önemlidir. **Roaming**, cihazın bir Access Point'ten diğerine geçişini ifade eder.

* Roaming süreci, cihazın bağlandığı AP’nin sinyal gücü zayıfladığında veya cihaz başka bir AP'ye daha yakın olduğunda devreye girer.
* Bu geçişin hızlı ve kesintisiz olabilmesi için ağda **Roaming** ayarlarının doğru yapılandırılmış olması gerekir. Örneğin, **802.11r** (Fast BSS Transition) protokolü, cihazların AP’ler arasında hızlı bir şekilde geçiş yapmasını sağlar.

### 7. **Bağlantı Sonlandırma (Disassociation)**

Cihaz, belirli bir süre sonra ağdan ayrılmak isteyebilir veya cihazın kapanması, bağlantının sonlanmasına neden olabilir. Bu noktada, **Disassociation** süreci devreye girer.

* Cihaz, AP'ye **Disassociation Request** mesajı gönderir.
* AP, bu talebi alır ve cihazı ağdan ayırır. Bu işlem, cihazın ağdaki aktif bağlantısının sonlanmasını sağlar.

## CAPWAP (Control and Provisioning of Wireless Access Points) Protokolü

**CAPWAP (Control and Provisioning of Wireless Access Points)**, kablosuz erişim noktaları (AP’ler) ile merkezi bir denetleyici (Wireless LAN Controller - WLC) arasında iletişimi yöneten bir protokoldür. Bu protokol, kablosuz ağları daha verimli ve merkezi bir şekilde yönetmek için geliştirilmiştir. CAPWAP, özellikle büyük ölçekli ağlarda erişim noktalarını merkezi bir kontrol noktasından yönetmeye ve yapılandırmaya olanak tanır.

CAPWAP, **IEEE 802.11** standardında tanımlanan ve **IETF (Internet Engineering Task Force)** tarafından geliştirilmiş bir protokoldür. Bu protokol, erişim noktalarının merkezi bir noktadan yönetilmesine ve tüm yapılandırmalarının tek bir denetleyici üzerinden yapılmasına imkan verir. Bu, özellikle çok sayıda AP bulunan büyük ağlarda önemli bir yönetim kolaylığı sağlar.

### **CAPWAP'ın Çalışma Prensibi**

CAPWAP, AP ile WLC arasındaki iletişimi yönetirken, genel olarak şu adımlar üzerinden çalışır:

1. **AP'nin Bağlanması ve Tanımlanması**:

   * Bir AP, ağda aktif olduğunda, ağdaki merkezi WLC’yi bulmak için DHCP veya başka yöntemlerle WLC'nin IP adresini keşfeder. Bu, CAPWAP keşif sürecini başlatır.
   * AP, WLC'ye bağlanmayı talep eden bir CAPWAP keşif mesajı gönderir. WLC, bu keşif mesajını alır ve AP'nin bağlantısını kabul eder.
   * Bağlantı kurulduktan sonra, WLC AP'ye gerekli yapılandırma bilgilerini gönderir. Bu, IP adresi, SSID, güvenlik ayarları, kanal planlaması gibi parametreleri içerir.

2. **Yapılandırma Transferi ve Yapılandırma**:

   * WLC, tüm AP'lere merkezi bir şekilde yapılandırmalarını gönderir. Bu, ağda tutarlılığı sağlar ve yönetim açısından büyük bir kolaylık sunar. AP'ler, gelen yapılandırmalar doğrultusunda ağ parametrelerini alır ve bağlantı noktalarını buna göre ayarlar.
   * Yapılandırma bilgilerinin merkezi bir noktadan AP'lere dağıtılması, ağ yöneticilerinin tüm erişim noktalarını aynı anda yapılandırabilmesini sağlar.

3. **Veri İletimi ve Tünelleme**:

   * AP, ağ üzerinden gelen verileri toplar ve merkezi WLC’ye iletir. Bu veriler **CAPWAP tüneli** üzerinden iletilir. Tünelleme işlemi, veri paketlerinin şifrelenmesini ve güvenli bir şekilde taşınmasını sağlar.
   * Bu veri iletimi sırasında, AP sadece uç cihazlardan gelen verileri alır ve WLC’ye iletir. WLC, veriyi doğru hedefe yönlendirmekle sorumludur. Bu sayede, tüm yönlendirme ve güvenlik işlemleri WLC tarafından gerçekleştirilir, bu da ağın yönetilmesini ve izlenmesini merkezi hale getirir.

4. **Erişim Noktası Durumu ve İzleme**:

   * AP, çalışma durumunu ve ağ bağlantı durumu hakkında sürekli olarak WLC’ye raporlar gönderir. Bu, ağ yöneticilerinin her bir AP’nin durumunu merkezi bir noktadan takip etmesine olanak tanır.
   * Durum bilgileri, ağdaki olası aksaklıkların tespit edilmesine yardımcı olur. WLC, bu raporları analiz ederek, ağdaki AP'lerin performansını ve sağlığını izler.

5. **Veri Güvenliği ve Kimlik Doğrulama**:

   * CAPWAP, AP ile WLC arasındaki iletişimi şifreler. Bu, ağda gönderilen verilerin güvenliğini sağlar ve ağdaki cihazlar arasında gizliliği korur.
   * WLC, AP'ler ile bağlantıya geçmeden önce kimlik doğrulama ve yetkilendirme işlemleri gerçekleştirir. Bu, ağın yalnızca yetkilendirilmiş AP’ler tarafından yönetilmesini sağlar ve ağ güvenliğini artırır.

### **CAPWAP Çerçevesi (Frame Structure)**

CAPWAP, iletişimde **veri çerçeveleri** kullanır. Bu çerçeveler, WLC ile AP arasında veri iletimini sağlayan temel birimlerdir. CAPWAP çerçeveleri, genellikle **kontrol, veri ve yönetim** olmak üzere üç ana kategoride sınıflandırılabilir.

1. **Kontrol Çerçeveleri**:

   * WLC ile AP arasında yönetimsel mesajlaşmayı sağlar. AP'ler, WLC'ye bağlanma talebi, yapılandırma bilgisi gönderme ve durum raporları gibi işlemleri kontrol çerçeveleri aracılığıyla iletir.

2. **Veri Çerçeveleri**:

   * Kullanıcı verileri, AP’ler üzerinden WLC’ye iletilirken bu çerçeveler kullanılır. Veri çerçeveleri, kullanıcı cihazlarının gönderdiği ve aldığı verilerin taşınmasını sağlar.

3. **Yönetim Çerçeveleri**:

   * AP'ler ve WLC arasındaki yapılandırma değişiklikleri, hata raporları ve durum bilgileri yönetim çerçeveleri ile taşınır. Bu çerçeveler, ağın yönetimini ve izlenmesini kolaylaştırır.

Her çerçeve, **protokol başlıkları, veri yükü ve kontrol bilgilerini** içerir ve her iki cihazın birbirine doğru şekilde veri iletmesini sağlar.

### **CAPWAP Protokolünün Sağladığı Yararlar**

CAPWAP, merkezi ağ yönetimi, güvenlik ve yapılandırma kolaylıkları sağlar. Ancak, protokolün sunduğu başlıca avantajları da şunlardır:

* **Merkezi Yönetim**: Tüm AP'lerin aynı anda ve merkezi bir noktadan yapılandırılması, ağın yönetimini kolaylaştırır.
* **Yüksek Esneklik ve Uyumluluk**: CAPWAP, farklı marka ve modellerdeki AP'lerin aynı ağda kullanılabilmesine olanak tanır.
* **Gelişmiş Güvenlik**: AP ile WLC arasındaki veri şifrelenerek, ağ güvenliği sağlanır. Bu, potansiyel güvenlik açıklarının azaltılmasına yardımcı olur.
* **Ağ İzleme ve Raporlama**: WLC, bağlı AP'lerin durumunu sürekli olarak izler ve performans raporları sunar. Bu da ağın verimli bir şekilde yönetilmesini sağlar.

### Split MAC (Split Media Access Control) Protokolü: Daha Ayrıntılı Açıklama

**Split MAC**, kablosuz ağlarda (özellikle **Wi-Fi** ağlarında) kullanılan bir yöntemdir. Bu yöntem, **Erişim Noktaları (AP'ler)** ve **Kablosuz LAN Denetleyicileri (WLC'ler)** arasındaki iş bölümüyle ilgili bir yapı sağlar. **Media Access Control (MAC)**, ağda veri iletimini yöneten bir katman olup, Split MAC, bu katmanın işlevlerini iki cihaz arasında paylaştırarak daha verimli bir ağ yönetimi ve iletişimi sunar. Split MAC, genellikle **CAPWAP (Control and Provisioning of Wireless Access Points)** protokolü ile ilişkilidir ve büyük ölçekli kablosuz ağlarda yönetim, performans ve güvenlik açısından büyük avantajlar sağlar.

## **Split MAC Mimarisi ve Çalışma Prensibi**

**Split MAC** mimarisinde, **MAC işlemleri** (veri iletimi, çerçeve yönetimi, sinyalizasyon vb.) iki ana bileşen arasında paylaşılır: **Access Point (AP)** ve **Wireless LAN Controller (WLC)**.

1. **Erişim Noktası (AP)**, kablosuz ağda yerel işlemleri ve temel veri iletimini üstlenir. Ancak, daha karmaşık işlevler, ağ yönetimi ve yapılandırma işlemleri gibi daha yüksek seviyeli işlemler **WLC** tarafından yönetilir.

2. **Wireless LAN Controller (WLC)**, AP’ler üzerinde merkezi bir yönetim sağlar. WLC, AP’lerin yapılandırmalarını ve güvenlik politikalarını yönetir. Ayrıca, roaming, trafik yönlendirme, kullanıcı yönetimi ve ağın genel performansının izlenmesi gibi kritik görevleri yerine getirir.

Bu iş bölümü, kablosuz ağın daha verimli ve yönetilebilir olmasına yardımcı olur.

### **AP ve WLC Arasında Yapılan İş Bölümü**

#### 1. **AP'nin Sorumlulukları (Yerel İşlemler)**

AP, Split MAC mimarisinde aşağıdaki işlemleri yerel olarak yönetir:

* **Fiziksel Katman Yönetimi (PHY)**:

  * AP, kablosuz sinyallerin alımı ve yayılmasından sorumludur. Kablosuz cihazlardan gelen veri paketlerini alır ve yayar.
  * Frekans bandını (örneğin 2.4 GHz, 5 GHz) kullanarak veri iletimini gerçekleştirir.
  * Bu, **modülasyon, kodlama, sinyal güç ayarları** gibi fiziksel katman işlevlerini içerir.

* **Medya Erişim Kontrolü (MAC)**:

  * AP, **data frame** (veri çerçevesi) ve **management frame** (yönetim çerçevesi) gibi temel çerçeve türlerini işler. Bu çerçeveleri alır ve iletir.
  * **Çerçeve iletimi**: Kablosuz cihazlardan gelen verileri alır ve belirli bir hedefe iletir.
  * **Çerçeve alımı**: AP, gelen veri çerçevelerini alır ve WLC'ye iletir.

* **Çakışma Tespiti ve İletim (CSMA/CA)**:

  * AP, veri iletiminden önce **Carrier Sense Multiple Access with Collision Avoidance (CSMA/CA)** protokolünü kullanarak çakışmaların önüne geçer.
  * Bu, kablosuz ortamda sinyal çakışmalarını minimize etmek için kullanılır.

* **Fiziksel Katman Ayarları**:

  * AP, kanal ayarlamaları ve frekans yönetimini yaparak, ağdaki performansı optimize eder.
  * Kanal seçimi, **SNR (Signal-to-Noise Ratio)** ve **RSSI (Received Signal Strength Indicator)** gibi parametreler izlenir.

#### 2. **WLC'nin Sorumlulukları (Merkezi İşlemler)**

WLC, daha karmaşık işlemleri ve ağ yönetimi ile ilgili görevleri üstlenir. WLC’nin sorumlulukları şunlardır:

* **Merkezi Yapılandırma Yönetimi**:

  * WLC, tüm AP’ler için merkezi yapılandırma sağlar. Bu, SSID’ler, güvenlik politikaları (WPA, WPA2), IP adresleri ve VLAN yapılandırmalarını içerir.
  * WLC, ağdaki tüm AP'lere yapılandırma gönderir ve böylece her AP'yi merkezileştirilmiş bir yönetimle yönetir.

* **Roaming Yönetimi**:

  * WLC, kablosuz cihazların bir AP'den diğerine geçişi sırasında bağlantıyı kesintisiz hale getirir. Bu özellik, **roaming** olarak adlandırılır.
  * Roaming, cihazların farklı AP’ler arasında geçiş yaparken bağlantının stabil ve sürekli olmasını sağlar.

* **Medya Erişim Kontrolü (MAC) ve İletişim**:

  * WLC, AP’lerin **MAC adresi tablosunu** kontrol eder, istemcilerin kimlik doğrulamasını yapar ve ağdaki cihazlar arasında iletişim yönlendirmelerini sağlar.
  * WLC, veri çerçevelerinin düzgün iletimini sağlar ve yönlendirme işlemlerini merkezi olarak yönetir.

* **Erişim Kontrolü ve Güvenlik**:

  * WLC, **802.1X** kimlik doğrulaması ve şifreleme protokollerini yönetir.
  * AP’lerdeki güvenlik politikalarını kontrol eder ve istemci cihazlarının güvenli bir şekilde ağa bağlanmasını sağlar.

* **Ağ Performans İzleme**:

  * WLC, tüm AP’lerin performansını izler ve merkezileştirilmiş ağ izleme raporları oluşturur.
  * **İzleme, hata tespiti ve ağ durumu** hakkında bilgiler sunar. Bu veriler, ağ yöneticilerine ağın sağlığı hakkında bilgi verir.

* **VLAN ve Trunking Yönetimi**:

  * WLC, AP'ler üzerinden farklı **VLAN’lar** (Virtual LAN) ve **trunking** işlemlerini yönetir. Bu, veri trafiğinin doğru VLAN'lar arasında yönlendirilmesini sağlar.

### **Split MAC'in Teknik Yararları**

**Split MAC** protokolü, kablosuz ağların verimli ve güvenli bir şekilde çalışmasını sağlayan birçok avantaj sunar. İşte bu avantajlar:

1. **Yük Dengelemesi ve Verimlilik**:

   * **Erişim Noktaları (AP’ler)**, düşük seviyeli işlemleri yerel olarak yönettiği için, ağ yöneticisinin merkezi bir cihaz (WLC) üzerinde yükü dengeleyebilmesi sağlanır.
   * Yükün AP'ler ile bölünmesi, **merkezi yönetim yükünü** azaltır ve daha verimli bir ağ yönetimi sağlar.

2. **Gelişmiş Güvenlik**:

   * Merkezi yönetim sayesinde güvenlik politikaları (WPA2, 802.1X) merkezi olarak kontrol edilir. Bu, güvenlik açıklarının azaltılmasına yardımcı olur.
   * WLC, tüm ağ trafiğini izleyerek potansiyel tehditleri erken tespit edebilir.

3. **Yüksek Performans ve Azaltılmış Gecikme**:

   * AP’ler yerel işlemleri gerçekleştirdiğinden, gecikme süresi daha kısa olur ve veri iletimi daha hızlı yapılır.
   * AP'lerin **data forwarding** işlemlerini doğrudan yapması, merkezi işlem yükünü azaltır ve ağdaki veri iletim hızını artırır.

4. **Kolay Yönetim ve Ölçeklenebilirlik**:

   * AP’lerin merkezi yönetimi, ağ yöneticisinin yapılandırmaları hızlıca değiştirmesine olanak tanır.
   * Yeni AP eklemeleri ve ağ genişletmeleri daha kolay hale gelir, çünkü yapılandırmalar merkezi olarak yapılır ve tüm ağ cihazlarına uygulanır.

5. **Esneklik ve Hızlı Adaptasyon**:

   * AP'ler, çevresel koşullara göre (sinyal yoğunluğu, kanal trafiği) adapte olur ve daha verimli bir ağ bağlantısı sağlar.
   * WLC, farklı ağ senaryolarına hızlıca adapte olabilir, ağ yapısındaki değişiklikler kolayca yönetilebilir.

## **Çoklu Erişim Yöntemleri: DSSS, FHSS, OFDM**

Kablosuz iletişimde, aynı frekans bandında birden fazla cihazın veri iletmesi ve alması gerekir. Bu süreçte **çoklu erişim yöntemleri**, cihazların birbirine çakışmadan aynı spektrumda iletişim kurmasını sağlar. **DSSS**, **FHSS**, ve **OFDM** gibi çoklu erişim yöntemleri, bu tür iletimleri yönetmek için farklı teknikler sunar. Her bir yöntem, belirli avantajlar ve kullanım senaryoları ile farklı gereksinimlere hitap eder.

### **DSSS (Direct Sequence Spread Spectrum)**

**DSSS**, **Doğrudan Dizi Yayılım Spektrumu** olarak bilinir ve kablosuz iletişimde kullanılan bir **çoklu erişim yöntemidir**. DSSS, bir sinyalin frekansını genişleterek, çok daha geniş bir spektrumda iletim yapmayı amaçlar. Bu genişleme, veri sinyalinin, belirli bir **"yayılan dizi"** kullanılarak daha geniş bir frekans bandına yayılmasını sağlar.

#### **DSSS’in Temel Prensibi**

* **Spreading Code (Yayılan Dizi)**: DSSS, her bitin iletilmeden önce bir **spreading code** (yayılma kodu) ile genişletilmesini sağlar. Bu kod, sinyali daha geniş bir frekans bandına yayar. Veriler bu yayılma kodları aracılığıyla daha fazla band genişliğine yayılır.
* **Yüksek Güvenlik**: DSSS, sinyali geniş bir spektruma yayarak, daha az parazit etkisiyle daha güvenli iletişim sağlar. Ayrıca, **parazitlerin** (interferans) hedeflenen veriye zarar vermesi daha zordur.
* **Frekans Hızı**: DSSS, daha geniş bir frekans bandını kullanarak, daha yüksek hızlarda veri iletimi yapılmasını sağlar.
* **Veri Kodlaması**: DSSS, iletilen her veri bitini, daha geniş bir bit dizisine dönüştürür. Bu dönüşüm sayesinde, aynı frekans bandı üzerinde birden fazla veri akışı yapılabilir.

#### **Avantajları**

* **Parazitlere Karşı Dayanıklı**: DSSS, sinyalin spektruma yayılması sayesinde parazitlerden (interferans) etkilenme olasılığı azalır.
* **Daha Az Çakışma**: Aynı frekansta daha fazla kullanıcıya olanak sağlar.
* **Gizlilik**: Veriler yayılma kodları sayesinde güvenli iletilir.

#### **Dezavantajları**

* **Bant Genişliği**: DSSS, geniş frekans bandı kullanmak zorunda olduğu için daha fazla bant genişliği gerektirir.
* **Veri Hızı**: Yayılan dizi genişleme nedeniyle, bazen veri hızında düşüş yaşanabilir.

### **2. FHSS (Frequency Hopping Spread Spectrum)**

**FHSS**, **Frekans Atlamalı Yayılım Spektrumu** olarak bilinir ve sinyallerin birden fazla frekans kanalı üzerinden sürekli olarak **atlamasına** dayanan bir iletişim tekniğidir. FHSS, bir cihazın sürekli olarak belirli bir frekans aralığından diğerlerine sıçrayarak iletişim yapmasını sağlar.

#### **FHSS’in Temel Prensibi**

* **Frekans Atlamaları**: Cihaz, veri iletimini **frekanslar arasında sıçrayarak** yapar. Bu atlamalar belirli bir algoritma ile düzenli olarak gerçekleştirilir. Her atlama, belirli bir zaman dilimi boyunca ve önceden belirlenmiş bir sıralama ile yapılır.
* **Zamanlama**: Atlamalar zaman dilimlerine göre yapılır. Yani, her cihaz, **zamanlamayı senkronize** şekilde takip eder.
* **Gizlilik ve Güvenlik**: Atlamalı frekanslar sayesinde, verinin izlenmesi zorlaşır. Ayrıca, eğer bir kanal tıkalıysa, cihaz otomatik olarak diğer frekansa geçer.

#### **Avantajları**

* **Düşük Parazit**: Sürekli frekans atlaması, cihazın tıkalı kanallar veya parazitlerden etkilenmesini azaltır.
* **Gizlilik ve Güvenlik**: Sinyalin hangi frekansta olduğunu tahmin etmek zor olduğundan, daha güvenli bir iletişim sağlar.
* **Karmaşık Ortamlar İçin Uygun**: Çok sayıda cihazın aynı frekansı kullanmak zorunda olduğu ortamlarda parazitlerin etkisi düşer.

#### **Dezavantajları**

* **Düşük Veri Hızı**: Sürekli frekans atlaması nedeniyle, veri iletim hızı düşük olabilir.
* **Verimlilik**: Frekans atlamalı sistem, verimli bir şekilde kullanılabilmesi için daha fazla zaman senkronizasyonu ve koordinasyon gerektirir.

### **3. OFDM (Orthogonal Frequency Division Multiplexing)**

**OFDM**, **Dikdörtgen Frekans Bölmeli Çoklama** olarak bilinir ve günümüz kablosuz iletişim teknolojilerinde sıklıkla kullanılan bir **çoklu erişim yöntemi**dir. OFDM, birden fazla taşıyıcı frekansının paralel olarak kullanıldığı bir teknik olup, her taşıyıcı frekansın birbirine **dik** (orthogonal) olmasını sağlar.

#### **OFDM’in Temel Prensibi**

* **Çoklu Taşıyıcılar**: OFDM, veriyi birden fazla taşıyıcı frekansına böler. Bu taşıyıcılar birbirine paralel bir şekilde çalışır ve her bir taşıyıcı üzerinden düşük hızlı veri iletimi yapılır.
* **Orthogonalite**: OFDM’de taşıyıcılar birbirine dik açıyla yerleştirilir, yani taşıyıcı frekansları birbirine zarar vermez. Bu özelliğe **orthogonalite** denir.
* **Subcarrier (Alt Taşıyıcılar)**: Veriler, her biri düşük hızda çalışan birden fazla alt taşıyıcıya bölünerek iletilir. Bu, daha yüksek veri hızları sağlar çünkü birden fazla taşıyıcı üzerinden paralel veri iletimi yapılır.

#### **Avantajları**

* **Yüksek Veri Hızı**: OFDM, çoklu taşıyıcılar kullanarak yüksek veri iletim hızları sağlar.
* **Gelişmiş Parazit Toleransı**: OFDM, frekans selektivitesi ve parazitlere karşı dayanıklı bir yapı sunar. Bu, özellikle karmaşık ortamlar için avantaj sağlar.
* **Verimli Bant Kullanımı**: Taşıyıcılar arasındaki dik açı sayesinde, spektrum daha verimli bir şekilde kullanılır.

#### **Dezavantajları**

* **Karmaşıklık**: OFDM sistemleri, diğer yöntemlere kıyasla daha karmaşıktır ve bunun yönetimi daha zordur.
* **Düşük Frekanslarda Duyarlılık**: OFDM, düşük frekanslarda daha duyarlıdır ve bu da bazen hatalı veri iletimiyle sonuçlanabilir.


## Kablosuz Ağ Tehditleri ve Saldırı Türleri

### 1.  Eavesdropping (Dinleme)

- Saldırgan, kablosuz trafiği pasif olarak izler.
- Şifrelenmemiş veriler kolayca elde edilebilir.
- **Önlem:** WPA3, VPN, HTTPS kullanımı



### 2.  Evil Twin (Sahte Access Point)

- Gerçek ağa benzer isimde sahte bir AP yayınlanır.
- Kullanıcılar bu sahte AP’ye bağlandıklarında, saldırgan tüm verilerini görebilir.
- **Önlem:** AP sertifikası kontrolü (802.1X), captive portal uyarıları


### 3.  DoS ve Deauthentication Saldırıları

- **Deauth saldırısı:** Kurbanın AP ile olan bağlantısını sürekli kopararak kesintiye neden olur.
- **DoS (Denial of Service):** Ağa sahte trafik göndererek AP’yi veya istemcileri yorar.
- **Önlem:** 802.11w (Management Frame Protection), saldırı tespit sistemleri (WIDS)



### 4.  Man-in-the-Middle (MitM)

- Saldırgan, istemci ile AP arasında aracı olur.
- Tüm trafik üzerinden geçerken manipülasyon yapılabilir.
- **Önlem:** HTTPS, VPN, EAP-TLS


### 5.  Rogue Access Point (Yetkisiz AP)

- İçeriden bir kullanıcı, şirket ağına yetkisiz bir AP bağlayabilir.
- Güvenlik duvarı ve VLAN geçişleri aşılabilir.
- **Önlem:** WIPS (Wireless Intrusion Prevention System), AP MAC filtreleme



### 6.  Brute Force / Dictionary Saldırıları

- Zayıf WPA/WPA2 parolaları hedef alınır.
- Wi-Fi handshake paketleri yakalanıp parola kırılabilir.
- **Önlem:** Karmaşık parolalar, WPA3 geçişi


### 7.  Packet Injection (Paket Enjeksiyonu)

- Saldırgan sahte paketler göndererek ağa müdahale edebilir.
- Örnek: ARP spoofing, DNS poisoning
- **Önlem:** VLAN segmentasyonu, DHCP snooping, dynamic ARP inspection



## Packet Tracer'da Kablosuz LAN (WLAN) Yapılandırması:

Bu örnekte, **Packet Tracer** kullanarak basit bir **Kablosuz LAN (WLAN)** yapılandırması yapacağız. Bu yapılandırma, bir **Access Point (AP)**, **Kablosuz İstemciler** (Wi-Fi cihazları) ve bir **Router** kullanarak yapılacaktır. Bu, temel bir ağda kablosuz bağlantı kurulumu için temel adımları içerecektir.

### **1. Gerekli Cihazların Seçilmesi**

* **1 adet Router**: Ağın yönlendirici cihazı olarak kullanılacak.
* **1 adet Access Point (AP)**: Kablosuz ağ bağlantısı için kullanılacak cihaz.
* **2 adet PC veya Laptop**: Kablosuz ağ cihazları olarak kullanılacak (Wi-Fi özellikli).
* **1 adet Switch**: Router ve Access Point'in birbirine bağlanması için gerekli.

### **2. Cihazların Yerleştirilmesi**

1. **Router**: Router'ı ağın merkezine yerleştirin.
2. **Access Point (AP)**: Access Point’i Router ile bağlantılı olacak şekilde yerleştirin.
3. **Switch**: Switch, Access Point ve Router’ı birbirine bağlayacak.
4. **PC veya Laptop**: İki bilgisayarı, kablosuz ağın bağlanacağı istemciler olarak yerleştirin.

### **3. Router Konfigürasyonu**

Router üzerinde temel ağ yapılandırmasını yapalım.

1. **Router’a Bağlanma**:

   * Packet Tracer’da Router’ı tıklayın ve **CLI** sekmesine geçin.
   * Aşağıdaki komutları kullanarak temel yapılandırmayı yapalım:

```bash
Router> enable
Router# configure terminal
Router(config)# interface gig0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# ip routing
Router(config)# exit
```

Bu adımlar, Router’ın **192.168.1.1** IP adresiyle yapılandırılmasını sağlar.

### **4. Access Point (AP) Yapılandırması**

Access Point'i Router’a bağladıktan sonra kablosuz ağ ayarlarını yapacağız.

1. **Access Point Konfigürasyonu**:

   * Access Point’i seçin ve **Config** sekmesine geçin.
   * **SSID (Service Set Identifier)** ayarını yapın. Bu, ağın ismi olacak.

     * SSID: `MyWLAN`
   * **Security** sekmesinde, **WPA2** şifreleme protokolünü seçin.

     * Şifre: `12345678`
2. **IP Yapılandırması**:

   * Access Point’in IP adresini, Router ile uyumlu olacak şekilde **192.168.1.2** olarak belirleyin.

### **5. Kablosuz İstemcilerin Yapılandırılması**

Kablosuz istemcilerin (PC veya Laptop) Access Point'e bağlanabilmesi için SSID ve şifre bilgileri gereklidir.

1. **PC veya Laptop Yapılandırması**:

   * İlk PC’yi tıklayın, ardından **Desktop** sekmesinden **PC Wireless**’a tıklayın.
   * Bağlanılacak ağ olarak **MyWLAN**’ı seçin.
   * Şifreyi girin: `12345678`
   * IP yapılandırmasını **DHCP** olarak seçin.
2. **İkinci PC için Aynı Adımlar**:

   * Diğer PC için de aynı işlemleri yapın. Aynı SSID ve şifreyi girerek ağınıza bağlanmasını sağlayın.

### **6. Bağlantının Test Edilmesi**

Bağlantıyı test etmek için her iki PC’den de **ping** komutunu kullanarak Router’a ve birbirlerine ping atabilirsiniz.

1. **Ping Komutu**:

   * Birinci PC’nin **Desktop** sekmesinden **Command Prompt**’u açın.
   * Router’a ping atmak için:

```bash
ping 192.168.1.1
```

* Aynı şekilde, diğer PC’den de ping atarak iki cihaz arasındaki bağlantıyı test edebilirsiniz.

### **7. Sonuç**

Bu adımları tamamladıktan sonra, Packet Tracer’daki ağda iki kablosuz istemcinin **Access Point** üzerinden internete bağlandığını ve Router ile iletişim kurabildiğini görmelisiniz. Bu yapılandırma, temel bir WLAN kurulumunu ve yapılandırmasını tamamlamış olacaktır.


## Packet Tracer'da Orta Düzeyde Kablosuz LAN (WLAN) Yapılandırması:

Bu örnekte, **Packet Tracer** kullanarak orta düzeyde bir **Kablosuz LAN (WLAN)** yapılandırması yapacağız. Yapılandırmada **Router**, **Access Point (AP)**, **Switch**, **PC'ler** ve **VLAN yapılandırması** yer alacak. Bu, birden fazla ağ segmentini ayıran ve kablosuz cihazların birbirleriyle güvenli bir şekilde iletişim kurmasını sağlayan bir kurulum olacaktır.

### **Gerekli Cihazlar**

1. **Router**: Kablosuz ağ için yönlendirici cihaz.
2. **Switch**: Ağ cihazlarını birbirine bağlayan anahtar cihaz.
3. **Access Point (AP)**: Kablosuz ağ erişimi sağlayan cihaz.
4. **PC'ler**: Kablosuz ağ istemcileri (Wi-Fi özellikli).
5. **VLAN Yapılandırması**: Kablosuz ağ için VLAN'lar oluşturulacak.

---

### **1. Cihazların Yerleştirilmesi ve Bağlantılar**

1. **Router**: Ağın merkezine yerleştirilir ve kablosuz ağın yönlendirilmesini sağlar.
2. **Access Point (AP)**: Router’a bağlanacak şekilde yerleştirilir.
3. **Switch**: Router ve Access Point arasında veri iletimi için kullanılır.
4. **PC’ler**: PC’ler kablosuz ağ cihazları olarak yerleştirilir ve Access Point’e bağlanacak şekilde yapılandırılır.

---

### **2. Router Yapılandırması**

Router'ı temel ağ yapılandırması için aşağıdaki adımları takip ederek yapılandıralım.

1. **Router’a Bağlanma**:

   * Router’ı tıklayın ve **CLI** sekmesine geçin.
   * Aşağıdaki komutları kullanarak **IP adresi** yapılandırmasını yapalım:

```bash
Router> enable
Router# configure terminal
Router(config)# interface gig0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# ip routing
Router(config)# exit
```

Router, **192.168.1.1** IP adresine sahip olacak ve ağın **IP yönlendirmesini** yapacak.

2. **VLAN Yapılandırması**:

   * Kablosuz ağ istemcilerini farklı VLAN'larda tutmak için VLAN yapılandırmasını yapmamız gerekiyor. Bu VLAN'lar, kablosuz ağ kullanıcılarının bölümlerini ayıracak.
   * **VLAN 10** (Veri Ağcıları) ve **VLAN 20** (Misafir Ağcıları) olarak iki VLAN oluşturacağız.

```bash
Router# configure terminal
Router(config)# vlan 10
Router(config-vlan)# name Data
Router(config-vlan)# exit
Router(config)# vlan 20
Router(config-vlan)# name Guest
Router(config-vlan)# exit
Router(config)# exit
```

---

### **3. Access Point (AP) Yapılandırması**

Access Point üzerinden kablosuz ağ yapılandırmasını yapacağız. Kablosuz ağda farklı VLAN'lar olacak ve her VLAN’ın kendi **SSID**'si olacak.

1. **Access Point Konfigürasyonu**:

   * **SSID 1**: "Data\_Network" (Veri Ağı için)
   * **SSID 2**: "Guest\_Network" (Misafir Ağı için)

2. **SSID ve Güvenlik Ayarları**:

   * AP'yi seçin ve **Config** sekmesine geçin.
   * **SSID 1** ve **SSID 2** için güvenlik ayarlarını yapalım (WPA2, PSK şifreleme).
   * **SSID 1**: `Data_Network`, Şifre: `data123`
   * **SSID 2**: `Guest_Network`, Şifre: `guest123`

3. **IP Yapılandırması**:

   * AP’nin IP adresini **192.168.1.2** olarak belirleyin ve VLAN ayarlarını yapın.

---

### **4. Switch Yapılandırması**

Switch, router ve access point arasında veri iletimini sağlamak için kullanılır.

1. **VLAN Yapılandırması**:

   * Switch'e bağlanarak aşağıdaki komutları kullanarak VLAN'ları yapılandırın:

```bash
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Data
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name Guest
Switch(config-vlan)# exit
```

2. **VLAN’ları Bağlama**:

   * Access Point ve Router arasındaki portları doğru VLAN’lara atayalım.

```bash
Switch(config)# interface range gig0/1 - 2
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit

Switch(config)# interface range gig0/3 - 4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config-if-range)# exit
```

Bu komut, AP'yi farklı VLAN'lara bağlayacaktır.

---

### **5. PC ve Laptop’ların Yapılandırılması**

Her iki PC'nin de kablosuz ağa bağlanabilmesi için ayarları yapalım.

1. **PC 1 (Data Network)**:

   * PC’yi tıklayın ve **Desktop** sekmesinden **PC Wireless**'a tıklayın.
   * **SSID 1** olan **"Data\_Network"**'a bağlanın ve şifreyi girin: `data123`.
   * **IP yapılandırması**: DHCP'yi seçin, böylece IP adresini otomatik olarak alır.

2. **PC 2 (Guest Network)**:

   * Diğer PC’yi tıklayın ve aynı işlemleri takip ederek **SSID 2** olan **"Guest\_Network"**’a bağlanın.
   * Şifreyi girin: `guest123`.
   * **IP yapılandırması**: DHCP’yi seçin, böylece IP adresi otomatik olarak verilecektir.

---

### **6. Bağlantının Test Edilmesi**

Bağlantıyı test etmek için her iki PC’den de **ping** komutunu kullanarak Router’a ve birbirlerine ping atabilirsiniz.

1. **Ping Komutu**:

   * **PC 1** üzerinden **Desktop** sekmesinden **Command Prompt**'u açın.
   * **Router’a ping atmak için**:

```bash
ping 192.168.1.1
```

* Aynı şekilde, **PC 2**'den de Router'a ping atabilirsiniz.

2. **PC’ler Arası Bağlantı Testi**:

   * Her iki PC de aynı ağda olduğu için birbirlerine ping atabilirler. Bunun için **Command Prompt**'u açın ve şu komutu kullanın:

```bash
ping 192.168.1.x
```

Cisco Packet Tracer'da bir **Wireless LAN Controller (WLC)** yapılandırma örneği hazırlayalım. Bu örnek senaryoda bir WLC üzerinden erişim noktaları (Access Point – AP) yönetilecek, istemciler kablosuz ağ üzerinden internete çıkış yapabilecek.


##  WLC Yapılandırması örnek

Kablosuz istemcilerin WLC tarafından kontrol edilen bir Access Point'e bağlanarak DHCP'den IP alması ve internete çıkması.

**Topoloji Bileşenleri:**

* 1 x Wireless LAN Controller (WLC-PT)
* 1 x Switch
* 1 x Router
* 1 x Access Point (Autonomous değil, lightweight mode)
* 1 x Kablosuz PC (Laptop)
* DHCP’yi router verecek.


###  1. Cihazların Bağlantısı

* **Router <-> Switch**: FastEthernet0/0 ↔ FastEthernet0/1
* **WLC <-> Switch**: Port1 ↔ FastEthernet0/2
* **Access Point <-> Switch**: FastEthernet0 ↔ FastEthernet0/3
* **Laptop (Kablosuz PC)**: Kablosuz bağlanacak



###  2. Router Yapılandırması (IP + DHCP)

```plaintext
Router> enable
Router# configure terminal
Router(config)# interface fa0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# ip dhcp pool WIRELESS
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
```



###  3. WLC Yapılandırması

1. **WLC üzerine tıklayın → GUI’ye girin (Web Tarayıcı Açılmazsa CLI ile)**

2. CLI üzerinden IP adresi ve DHCP yapılandırması:

```plaintext
WLC> enable
WLC# configure terminal
WLC(config)# interface vlan 1
WLC(config-interface)# ip address 192.168.1.2 255.255.255.0
WLC(config-interface)# exit

WLC(config)# wlan 1 WirelessNet WirelessSSID
WLC(config-wlan)# vlan 1
WLC(config-wlan)# security wpa akm psk set-key ascii 0 kablosuz123
WLC(config-wlan)# no shutdown
WLC(config-wlan)# exit
```

3. **WLC’ye AP tanıtımı yapılmaz, AP otomatik olarak CAPWAP ile bağlanır.**
   Eğer Access Point lightweight değilse, Packet Tracer’da WLC’ye bağlanmaz.



###  4. Access Point (Lightweight AP) Bağlantısı

* **Switch’e bağlı olmalı**
* IP'yi DHCP ile alır ve WLC’yi bulur.

**AP otomatik olarak WLC’ye bağlanır** (Packet Tracer'da bu otomatik olur, CLI gerekmez).

###  5. Kablosuz PC Yapılandırması

1. Kablosuz Laptop'a tıkla → "Desktop" → "PC Wireless"

2. **SSID**: WirelessSSID
   **Security Mode**: WPA-PSK
   **Password**: kablosuz123

3. DHCP ile IP alacak.
   "Command Prompt" üzerinden `ipconfig` ile kontrol et.


### Test

* Laptop'tan `ping 192.168.1.1` komutu → Başarılı olmalı.
* Laptop’tan `ping 8.8.8.8` veya dış IP → Router NAT yapmadığı için başarısız olur ama iç bağlantı test edilir.


## **Kaynakça**

1. [RFC 5415 – Control And Provisioning of Wireless Access Points (CAPWAP) Protocol Specification](https://datatracker.ietf.org/doc/html/rfc5415)
2. [RFC 4347 – Datagram Transport Layer Security (DTLS)](https://datatracker.ietf.org/doc/html/rfc4347)

3. [Cisco – Wireless LAN Controller Configuration Guide](https://www.cisco.com/c/en/us/td/docs/wireless/controller/8-10/config-guide/b_cg810.html)

4. [IEEE 802.11 Standard ](https://en.wikipedia.org/wiki/IEEE_802.11)

