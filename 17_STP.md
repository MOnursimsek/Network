# **STP**

## **STP Nedir ve Neden Kullanılır?**

**STP (Spanning Tree Protocol)**, IEEE 802.1D standardı ile tanımlanan bir ağ protokolüdür ve Ethernet ağlarında **döngüleri (loop)** önlemek amacıyla kullanılır. Anahtarlama (switching) ortamlarında, özellikle yedekli bağlantılarla tasarlanmış ağlarda, döngüler meydana gelebilir. Bu döngüler, Ethernet çerçevelerinin sonsuz döngüye girerek ağ trafiğini tıkamasına ve cihazların düzgün çalışamamasına neden olur.

**STP'nin kullanım amacı şunlardır:**

* **Layer 2 döngülerini önlemek:** Anahtarlama ortamlarında oluşan döngüleri tespit ederek onları devre dışı bırakır.
* **Ağın kararlılığını sağlamak:** Belirli bağlantıları yedekte tutarak birincil bağlantı başarısız olduğunda alternatif yol sağlar.
* **Broadcast Storm’ları önlemek:** Ağda sürekli yayılan broadcast mesajlarının kontrolsüz yayılmasını engeller.
* **MAC adres tablosu kararsızlığını önlemek:** Döngü nedeniyle aynı MAC adresinin birden fazla porttan öğrenilmesini ve bu nedenle tabloda sürekli değişiklik olmasını engeller.

**Özetle**, STP, yedekli bağlantıların olduğu ağlarda **aktif bağlantıların bir kısmını geçici olarak devre dışı bırakarak** ağın döngüsüz bir ağaç (spanning tree) yapısına dönüşmesini sağlar. Bu sayede hem yedeklilik korunur hem de ağ çökmesi engellenir.



## **STP Çalışma Prensipleri**

STP’nin temel çalışma prensibi, Layer 2 seviyesinde tüm switch’leri birbirine bağlayan **döngüsüz bir mantıksal ağaç yapısı** (spanning tree) oluşturmaktır. Bu süreç aşağıdaki adımlarla gerçekleşir:

1. **Bridge ID Belirlenir ve Root Bridge Seçilir:**

   * Her switch, kendine ait **Bridge ID** bilgisine sahiptir (Bridge ID = Priority + MAC Address).
   * Tüm switch’ler kendi Bridge ID bilgilerini ağda duyurur.
   * En düşük Bridge ID’ye sahip olan switch **Root Bridge** olarak seçilir.

2. **Yolların Maliyetleri Hesaplanır:**

   * Root Bridge’e ulaşan her yolun bir maliyeti (cost) vardır.
   * Maliyet, port hızı ile ters orantılıdır (örneğin: 100 Mbps = 19 cost, 1 Gbps = 4 cost).
   * Her switch, Root Bridge’e olan **en düşük maliyetli yolu** hesaplar.

3. **Rollerin Belirlenmesi:**

   * Her switch, Root Bridge’e ulaşan en kısa yoldaki portunu **Root Port (RP)** olarak belirler.
   * Her ağ segmenti (link) için Root Bridge’e en kısa yoldan ulaşabilen switch’in portu **Designated Port (DP)** olarak belirlenir.
   * Diğer bağlantılar **Blocking** duruma geçirilir.

4. **Döngü Oluşturabilecek Bağlantılar Devre Dışı Bırakılır:**

   * Döngüye neden olabilecek portlar **Blocking** duruma geçirilerek yalnızca bir aktif yol bırakılır.
   * Böylece yalnızca bir yol üzerinden veri iletimi yapılır, yedek yollar ise yedekte bekler.

5. **Ağda Değişiklik Olursa Spanning Tree Yeniden Hesaplanır:**

   * Bir bağlantı kesilirse veya yeni bir switch ağa eklenirse, STP süreci yeniden başlatılır ve yeni bir ağaç yapısı oluşturulur.

**STP Zamanlayıcıları:**

* **Hello Timer (Varsayılan: 2s):** Root Bridge’in BPDU paketlerini gönderme sıklığı.
* **Forward Delay (Varsayılan: 15s):** Portların Listening ve Learning durumunda kalma süresi.
* **Max Age (Varsayılan: 20s):** BPDU bilgisinin geçerlilik süresi.



## **STP Bileşenleri ve Temel Kavramlar**

STP'nin çalışmasını sağlayan temel bileşenler ve kavramlar şunlardır:

#### 1. **Bridge ID (BID)**

* Her switch’in kimliğini belirler.
* 2 bileşenden oluşur: **Bridge Priority (varsayılan 32768)** + **MAC Adresi**.
* Root Bridge seçimi bu bilgiye göre yapılır.

#### 2. **BPDU (Bridge Protocol Data Unit)**

* Switch’ler arasında STP bilgilerini taşımak için kullanılan kontrol mesajlarıdır.
* Switch’ler BPDU göndererek Root Bridge belirlemesi ve ağ topolojisini yönetir.

#### 3. **Root Bridge**

* Tüm ağın merkezinde yer alan switch’tir.
* Tüm switch’ler bu cihaza olan en kısa yolu hesaplayarak port rollerini belirler.

#### 4. **Root Port (RP)**

* Root Bridge’e en kısa yol üzerinden ulaşmayı sağlayan her switch’teki porttur.
* Sadece Root Bridge bu porta sahip değildir (çünkü o zaten merkezdedir).

#### 5. **Designated Port (DP)**

* Her segmentte Root Bridge’e en kısa yoldan bağlantı sağlayan porttur.
* Ağdaki veri trafiği bu port üzerinden akar.

#### 6. **Blocked Port**

* Döngüye neden olabilecek porttur ve aktif olarak veri iletimi yapmaz.
* Ancak ağda bir arıza olursa, yedek yol olarak devreye girebilir.

#### 7. **STP Port Durumları**

1. **Blocking:** Port veri iletmez, sadece BPDU dinler.
2. **Listening:** BPDU dinler, MAC adresi öğrenmez.
3. **Learning:** BPDU dinler, MAC adresi öğrenir ama veri iletmez.
4. **Forwarding:** Veri iletir ve MAC adresi öğrenir.
5. **Disabled:** Port manuel olarak kapatılmıştır.

#### 8. **STP Maliyetleri (Path Cost)**

* Root Bridge’e giden yolun toplam maliyetidir.
* Hız arttıkça maliyet azalır:

  * 10 Mbps → Cost: 100
  * 100 Mbps → Cost: 19
  * 1 Gbps → Cost: 4
  * 10 Gbps → Cost: 2


## **STP Port Rolleri (Root, Designated, Blocked vb.)**

Spanning Tree Protocol (STP), Layer 2 ağlarda döngüleri önlemek için ağdaki her switch portuna belirli bir **rol** atar. Bu roller, topolojide hangi portların veri ileteceğini, hangilerinin yedekte bekleyeceğini belirler. Her rolün ağdaki işlevi farklıdır:

#### 1. **Root Port (RP)**

* Bir switch’in Root Bridge’e giden **en kısa yoluna ait port**tur.
* Her switch’te **yalnızca bir adet** Root Port bulunur.
* Root Bridge’in kendisinde **Root Port yoktur** (çünkü kendisi merkezdir).
* Root Port veri iletimi için **aktif (forwarding)** durumdadır.

Örnek: Eğer bir switch’in Root Bridge’e giden iki bağlantısı varsa, STP her iki yolun **maliyetini (path cost)** karşılaştırır ve daha düşük maliyetli olan bağlantıyı Root Port olarak belirler.


#### 2. **Designated Port (DP)**

* Her ağ segmentinde (örneğin iki switch arasındaki bağlantı gibi) **Root Bridge’e en kısa yol üzerinden ulaşımı sağlayan porttur**.
* Segment başına **yalnızca bir Designated Port** bulunur.
* Designated Port her zaman **veri iletir (forwarding)** durumundadır.

Aynı segmentteki iki port da Root Bridge’e ulaşıyorsa, STP karşılaştırma yapar ve **daha düşük Bridge ID’ye sahip olan switch’in portunu Designated Port** olarak seçer.


#### 3. **Blocked Port**

* Ağda döngü oluşmasını engellemek amacıyla **aktif olarak kullanılmayan** porttur.
* BPDU dinleyebilir ama veri iletimi yapmaz.
* Yalnızca **yedek yol** olarak bekler.
* Durumu **blocking**’dir; gerektiğinde forwarding durumuna geçebilir.

Örnek: Üç switch’in birbirine üçgen şeklinde bağlandığı bir yapıda, döngüyü engellemek için bir bağlantıdaki port **blocked** durumuna geçirilir.



#### 4. **Alternate Port (RSTP ile birlikte gelir)**

* RSTP (Rapid STP) protokolünde tanımlanmıştır.
* Root Port’a alternatif olan porttur.
* Root Port’un devre dışı kalması durumunda hemen aktif olabilir.
* Blocking benzeri bir durumdadır ama hızlı geçiş sağlar.



#### 5. **Disabled Port**

* Bu port STP tarafından değil, kullanıcı tarafından manuel olarak **devre dışı bırakılmıştır**.
* Hiçbir STP rolü yoktur, veri iletimi ve BPDU alışverişi yapılmaz.


#### 🔁 Port Rolleri ve Durumları Arasındaki İlişki:

| Port Rolü       | Port Durumu | Açıklama                        |
| --------------- | ----------- | ------------------------------- |
| Root Port       | Forwarding  | Root Bridge’e en kısa yol       |
| Designated Port | Forwarding  | Segmentteki en iyi yol          |
| Blocked Port    | Blocking    | Döngü önlemek için devre dışı   |
| Alternate Port  | Discarding  | RSTP yedeği                     |
| Disabled Port   | Disabled    | Kullanıcı tarafından kapatılmış |



## **Bridge ID ve Root Bridge Seçimi**

#### **Bridge ID (BID) Nedir?**

Bridge ID, her switch’in STP içinde tanımlanabilmesi için kullanılan **benzersiz kimlik numarasıdır**. Bridge ID şu iki bileşenden oluşur:

1. **Bridge Priority (Öncelik):**

   * 0 ile 65535 arasında bir değerdir (varsayılan: 32768).
   * Kullanıcı tarafından ayarlanabilir.
2. **MAC Address:**

   * Switch’in en düşük MAC adresi kullanılır.
   * Otomatik olarak atanır.

**Bridge ID = Bridge Priority + MAC Address**

STP’de karşılaştırma yapılırken önce **Bridge Priority** değerlendirilir. Eşitse, **MAC Address** dikkate alınır. En küçük değerli Bridge ID, Root Bridge olarak seçilir.


#### **Root Bridge Seçimi Nasıl Yapılır?**

STP başlatıldığında tüm switch’ler kendilerini Root Bridge olarak varsayar ve BPDU mesajları göndererek Bridge ID bilgilerini duyurur. Aşağıdaki süreç izlenir:

1. Tüm switch’ler **BPDU mesajı gönderir**.
2. Switch’ler, aldıkları BPDU’lardaki Bridge ID bilgileri ile kendi ID’lerini karşılaştırır.
3. En küçük Bridge ID’ye sahip switch **Root Bridge** olur.
4. Diğer tüm switch’ler kendilerini Root Bridge’e bağlı olarak yapılandırır ve port rollerini belirler.

**Bridge ID Karşılaştırma Örneği:**

| Switch | Priority | MAC Address       | Bridge ID               |
| ------ | -------- | ----------------- | ----------------------- |
| SW1    | 32768    | 00-11-22-33-44-01 | 32768.00-11-22-33-44-01 |
| SW2    | 32768    | 00-11-22-33-44-02 | 32768.00-11-22-33-44-02 |

Bu durumda SW1’in MAC adresi daha küçük olduğu için Root Bridge olarak seçilir.



#### **Bridge Priority Ayarlamak:**

Yönetici, belirli bir switch’in Root Bridge olmasını istiyorsa **Bridge Priority** değerini düşürebilir:

```bash
Switch(config)# spanning-tree vlan 1 priority 4096
```

Daha düşük değer verildiğinde, bu switch Root Bridge olmaya daha uygun hale gelir.

## **BPDU Nedir ve Nasıl Çalışır?**

**BPDU (Bridge Protocol Data Unit)**, Spanning Tree Protocol (STP) tarafından kullanılan özel kontrol mesajlarıdır. Ethernet ağındaki switch’ler, **STP topolojisini oluşturmak ve güncel tutmak** için BPDU mesajlarını birbirleriyle paylaşır. Bu mesajlar sayesinde switch’ler birbirlerinin varlığından haberdar olur, Root Bridge’i belirler ve döngüleri önleyecek şekilde port rollerini (Root, Designated, Blocked) yapılandırır.



### **BPDU Nedir?**

* **BPDU**, IEEE 802.1D standardında tanımlanmıştır.
* Sadece switch’ler (bridge’ler) tarafından oluşturulur ve iletilir.
* BPDU’lar genellikle switch’lerin **aktif portları üzerinden** yayılır.
* İki ana BPDU türü vardır:

  1. **Configuration BPDU:** STP’nin normal çalışması sırasında kullanılır.
  2. **Topology Change Notification (TCN) BPDU:** Ağ topolojisi değiştiğinde (örneğin bir bağlantı koptuğunda veya switch eklendiğinde) gönderilir.

###  **BPDU Nasıl Çalışır?**

STP çalışmaya başladığında her switch aşağıdaki şekilde BPDU’ları kullanır:

#### 1. **Başlangıçta Her Switch Kendisini Root Sanır**

* Tüm switch’ler kendilerini Root Bridge olarak varsayarak **kendi BPDU’larını gönderir**.
* BPDU’ların içinde şunlar yer alır:

  * Bridge ID (Priority + MAC)
  * Root Bridge ID (ilk başta kendi Bridge ID’sini yazar)
  * Root Path Cost (Root’a olan maliyet; başlangıçta 0)
  * Sender Bridge ID
  * Sender Port ID
  * Timer bilgileri (Hello, Max Age, Forward Delay)

#### 2. **En Küçük Bridge ID’ye Sahip BPDU Kazanır**

* Switch’ler diğer switch’lerden aldıkları BPDU’ları kendi BPDU’larıyla karşılaştırır.
* Daha **küçük Root Bridge ID**’ye sahip olan BPDU **"daha iyi"** kabul edilir.
* Switch, daha iyi bir BPDU alırsa, artık Root Bridge olmadığını anlar ve o BPDU’yu **iletmeye başlar** (yeniden yazarak).

#### 3. **Root Bridge Belirlendikten Sonra BPDU Yayılımı Devam Eder**

* Root Bridge, Configuration BPDU’yu her **Hello Timer (varsayılan 2 saniye)** süresinde gönderir.
* Diğer switch’ler, bu BPDU’ları dinler ve topolojilerini günceller.

#### 4. **Port Rolleri ve Durumları BPDU’lara Göre Belirlenir**

* Hangi portun Root, Designated veya Blocked olacağına, alınan BPDU’lara göre karar verilir.
* BPDU, aynı zamanda switch’in hangi port üzerinden Root Bridge’e daha yakın olduğunu belirlemesine yardımcı olur.

#### 5. **Ağda Değişiklik Olursa TCN BPDU Gönderilir**

* Bir port kapanır/açılır veya switch eklenirse, değişikliği fark eden switch **TCN BPDU** gönderir.
* Bu TCN BPDU, Root Bridge’e kadar iletilir.
* Root Bridge, tüm switch’lere bu değişikliği Configuration BPDU’lar yoluyla bildirir.



### **BPDU İçeriği (Configuration BPDU Formatı)**

| Alan             | Açıklama                                     |
| ---------------- | -------------------------------------------- |
| Protocol ID      | STP için 0x0000                              |
| Version          | STP sürümü (genelde 0x00)                    |
| BPDU Type        | 0x00 (Config BPDU), 0x80 (TCN BPDU)          |
| Flags            | TCN ve Topology Change bitleri               |
| Root Bridge ID   | Root seçilen Bridge’in ID’si                 |
| Root Path Cost   | Root’a giden yolun maliyeti                  |
| Sender Bridge ID | BPDU’yu gönderen switch’in kimliği           |
| Port ID          | Hangi porttan gönderildiği                   |
| Message Age      | BPDU’nun ağda dolaştığı süre                 |
| Max Age          | BPDU’nun geçerlilik süresi (varsayılan 20s)  |
| Hello Time       | Root Bridge’in BPDU gönderme sıklığı         |
| Forward Delay    | Port geçiş gecikmeleri (Listening, Learning) |

## **STP Zamanlayıcıları**

Spanning Tree Protocol (STP), ağda döngüleri önlemek için belirli zamanlayıcılar (timers) kullanır. Bu zamanlayıcılar, BPDU mesajlarının gönderilme sıklığını, topoloji değişikliklerine tepki süresini ve port durum geçiş sürelerini kontrol eder. Üç temel zamanlayıcı vardır: **Hello Time**, **Forward Delay** ve **Max Age**.

### 1. **Hello Time**

#### Tanım:

Hello Time, **Root Bridge’in Configuration BPDU’ları gönderme sıklığını** belirler.

#### Özellikleri:

* Varsayılan değer: **2 saniye**
* Sadece **Root Bridge** tarafından belirlenir ve gönderilir.
* Diğer switch’ler bu değeri Root Bridge’in BPDU’larından alır ve uygular.

#### İşlevi:

* Switch’ler belirli aralıklarla birbirlerine “ben buradayım” mesajı anlamına gelen BPDU’ları gönderir.
* Bu mesajlar sayesinde ağ topolojisinin durumu güncel tutulur.
* Eğer bir switch **Max Age süresi boyunca** BPDU almazsa, Root Bridge’in artık erişilemez olduğunu varsayar.

#### Değiştirme (CLI):

```bash
Switch(config)# spanning-tree vlan 1 hello-time 3
```



### 2. **Max Age**

#### Tanım:

Max Age, bir switch’in aldığı bir BPDU’nun **ne kadar süreyle geçerli** olduğunu belirler.

#### Özellikleri:

* Varsayılan değer: **20 saniye**
* Root Bridge tarafından belirlenir.
* Hello BPDU’ları bu süre boyunca alınmazsa, switch mevcut topolojinin bozulduğuna karar verir.

#### İşlevi:

* Switch, aldığı BPDU mesajını hafızasında tutar ve bir sayaç başlatır.
* Eğer bu sayaç **Max Age süresini aşarsa**, switch BPDU’yu geçersiz sayar.
* Böylece topolojinin değişmiş olabileceğini varsayarak yeniden seçim sürecine başlar (Root Bridge seçimi, port rolleri vs.).

#### Değiştirme (CLI):

```bash
Switch(config)# spanning-tree vlan 1 max-age 25
```


### 3. **Forward Delay**

#### Tanım:

Forward Delay, bir portun STP geçiş durumlarında (Listening → Learning → Forwarding) **her bir aşamada ne kadar süre kalacağını** belirler.

#### Özellikleri:

* Varsayılan değer: **15 saniye**
* Toplamda: 15s (Listening) + 15s (Learning) = **30 saniye gecikme**
* Bu süre içinde port **veri iletimi yapmaz**, yalnızca BPDU mesajlarını işler.

#### İşlevi:

* Ani durum değişikliklerinde döngü oluşmaması için port, hemen forwarding durumuna geçmez.
* İlk olarak **Listening** durumuna geçer ve BPDU’ları dinler.
* Ardından **Learning** durumuna geçerek MAC adreslerini öğrenmeye başlar.
* Ancak bu iki durumda da veri iletimi yapılmaz.
* **Forward Delay**, bu iki adımın her birinde ne kadar kalınacağını belirler.

#### Değiştirme (CLI):

```bash
Switch(config)# spanning-tree vlan 1 forward-time 20
```

## **STP Port Durumları**

Spanning Tree Protocol (STP), ağ döngülerini önlemek için portları belirli **durumlara** (states) geçirerek ağ trafiğini kontrol eder. Her port, ağ topolojisine ve alınan BPDU’lara göre bu durumlar arasında geçiş yapar. Bu geçişler, döngü oluşmadan ağın yeniden yapılandırılmasını sağlar.

STP’de her port şu beş temel **durumdan** birinde bulunur:

### 1. **Blocking (Engelleme Durumu)**

### Tanım:

Port, ağ döngüsü oluşmaması için trafiği **engeller**. Sadece **BPDU mesajlarını dinler**, ancak veri iletimi yapmaz.

### Özellikler:

* MAC adresi öğrenilmez.
* Veri çerçevesi (frame) iletimi yapılmaz.
* Ağda döngü varsa, döngü bu port engellenerek kırılır.
* Ağda değişiklik yoksa port bu durumda kalır.



### 2. **Listening (Dinleme Durumu)**

### Tanım:

Port, olası bir Root ve Designated port seçimi için **BPDU’ları analiz eder**, ancak henüz veri iletimi yapmaz.

### Özellikler:

* MAC adresi öğrenilmez.
* Veri çerçevesi iletimi yapılmaz.
* Port, bu aşamada **seçim süreci** için aktif olarak çalışır.
* Bu durumun süresi **Forward Delay** zamanlayıcısına göre varsayılan olarak **15 saniyedir.**



### 3. **Learning (Öğrenme Durumu)**

### Tanım:

Port artık **MAC adreslerini öğrenmeye başlar**, ama hâlâ veri iletimi yapmaz.

### Özellikler:

* Switch, gelen çerçevelerin kaynak MAC adreslerini MAC adres tablosuna yazar.
* Veri çerçevesi iletimi yapılmaz.
* Bu durum da varsayılan olarak **15 saniye** sürer (**Forward Delay**).



### 4. **Forwarding (İletme Durumu)**

###  Tanım:

Port, **normal veri iletimine açık** durumdadır. Hem veri hem de BPDU trafiğini iletir.

###  Özellikler:

* MAC adresi öğrenilir.
* Veri çerçevesi alıp gönderilebilir.
* Bu durumdaki portlar aktif olarak ağı taşır.


### 5. **Disabled (Devre Dışı Durum)**

### Tanım:

Port, **yönetici tarafından manuel olarak kapatılmıştır.** Ne BPDU alır/gönderir, ne de veri iletir.

### Özellikler:

* Yönetimsel olarak `shutdown` komutu ile kapatılır.
* STP tarafından kontrol edilmez.


## **STP Türleri ve Farklılıkları (STP, RSTP, MSTP)**

Ethernet ağlarında döngüleri önlemek için kullanılan Spanning Tree Protocol (STP), zamanla geliştirilmiş farklı sürümlerle karşımıza çıkar. Temel STP yapısına ek olarak **RSTP (Rapid STP)** ve **MSTP (Multiple STP)** gibi daha hızlı ve çoklu VLAN destekli protokoller geliştirilmiştir. Bu bölümde STP türlerini ve aralarındaki farkları ayrıntılı biçimde inceleyelim.


### 1. **STP (Spanning Tree Protocol)**

### Tanım:

* IEEE **802.1D** standardı ile tanımlanmıştır.
* Ağdaki döngüleri önlemek için **tek bir mantıksal yol** oluşturur.
* Her VLAN için **tek bir STP topolojisi** kullanır.

### Özellikleri:

* BPDU (Bridge Protocol Data Unit) mesajlarıyla çalışır.
* **Root Bridge** belirlenir ve port rolleri (Root, Designated, Blocked) atanır.
* Ağda bir değişiklik olduğunda, yeniden seçim süreci **30-50 saniye** sürebilir.

### Port Durumları:

* **Blocking**
* **Listening**
* **Learning**
* **Forwarding**
* **Disabled**

### Avantajlar:

* Basit yapılıdır.
* Döngüleri etkili biçimde engeller.

### Dezavantajlar:

* **Yavaş toparlanma süresi** (convergence) vardır.
* VLAN sayısı arttıkça ölçeklenebilirliği düşer.



### 2. **RSTP (Rapid Spanning Tree Protocol)**

### Tanım:

* IEEE **802.1w** standardıdır.
* STP’nin geliştirilmiş, **daha hızlı** sürümüdür.
* STP ile **geriye dönük uyumludur**.

### Özellikleri:

* Toparlanma süresi **1 saniye civarına** düşürülmüştür.
* BPDU’lar **her port için iki yönlü (point-to-point)** gönderilir.
* Port durumları ve rolleri daha etkin biçimde belirlenir.

### Port Durumları:

* **Discarding** (Blocking + Listening)
* **Learning**
* **Forwarding**

### Port Rolleri:

* **Root Port**
* **Designated Port**
* **Alternate Port** (yedek yol)
* **Backup Port** (aynı segmentteki ikinci yol)

### Avantajlar:

* Çok daha hızlı ağ toparlanması sağlar.
* Karmaşık topolojilerde daha etkilidir.

### Dezavantajlar:

* STP’ye göre biraz daha karmaşık yapıdadır.



### 3. **MSTP (Multiple Spanning Tree Protocol)**

### Tanım:

* IEEE **802.1s** standardıdır.
* VLAN yapılarını destekleyen ve **her VLAN için ayrı STP çalıştırmak yerine,** benzer VLAN’ları **gruplandırarak** ortak bir STP örneği çalıştıran sürümdür.

### Özellikleri:

* VLAN’lar **MST Instance (MSTI)** adı verilen gruplara atanır.
* Her MST Instance için ayrı bir spanning tree oluşturulur.
* Tüm MST yapılandırması ağdaki tüm switch’lerde **aynı olmalıdır** (name, revision number ve VLAN-to-instance mapping).

### Avantajlar:

* Çok sayıda VLAN olan ağlarda **kaynak tasarrufu sağlar.**
* Her VLAN’ın aynı yolu kullanması zorunlu değildir.
* Ağ performansını artırır ve esneklik sağlar.

### Dezavantajlar:

* Yapılandırması daha karmaşıktır.
* Tüm cihazlarda **senkronize yapılandırma** gerektirir.



### STP Türleri Karşılaştırma Tablosu

| Özellik                | STP (802.1D)              | RSTP (802.1w)                       | MSTP (802.1s)                 |
| ---------------------- | ------------------------- | ----------------------------------- | ----------------------------- |
| Toparlanma Süresi      | 30-50 saniye              | \~1 saniye                          | \~1 saniye                    |
| VLAN Desteği           | Sınırlı (tek yapı)        | Sınırlı (tek yapı)                  | Çoklu VLAN için ayrı instance |
| Geriye Dönük Uyumluluk | -                         | STP ile uyumlu                      | RSTP ve STP ile uyumlu        |
| Port Rolleri           | Root, Designated, Blocked | Root, Designated, Alternate, Backup | Aynı RSTP rollerini kullanır  |
| Kullanım Karmaşıklığı  | Düşük                     | Orta                                | Yüksek                        |



## **PVST ve PVST+ (Per VLAN Spanning Tree ve Per VLAN Spanning Tree Plus)**

**PVST** ve **PVST+** terimleri, **Spanning Tree Protocol (STP)**'nin **VLAN tabanlı** yapılandırmalarda kullanıldığı özel türlerdir. Bu protokoller, özellikle **Cisco ağ cihazları** üzerinde VLAN tabanlı ağlarda döngülerin engellenmesini sağlamak için kullanılır. Her iki protokol de aynı temel amacı taşır, ancak **yönetimsel farklar** ve **uyumluluk farklılıkları** bulunur.



### **1. PVST (Per VLAN Spanning Tree)**

**PVST**, her bir **VLAN için ayrı bir Spanning Tree** çalıştırılmasını sağlayan Cisco'nun geliştirdiği bir protokoldür. Yani, her VLAN'ın kendi **STP topolojisi** vardır. Bu protokol, **her VLAN için bağımsız bir Root Bridge** ve **STP topolojisi** oluşturur.

#### **PVST’nin Temel Özellikleri**:

* **Her VLAN için bağımsız bir STP** çalıştırılır. Bu, ağda daha fazla **esneklik** sağlar.
* **VLAN bazlı root bridge seçimi** yapılır. Yani her VLAN için ağdaki en iyi köprü (root bridge) seçilebilir.
* **Yük dengelemesi** sağlar. Farklı VLAN’lar farklı yollar üzerinden veri iletebilir.
* **Her VLAN için ayrı BPDU**'lar iletilir, bu da ağda farklı VLAN'ların birbirinden bağımsız olarak **STP protokolünü çalıştırmasına** olanak tanır.

#### **PVST Avantajları**:

1. **Yük dengelemesi**: Farklı VLAN’lar farklı yolları kullanabilir, bu da ağda daha dengeli bir trafik akışı sağlar.
2. **Her VLAN için ayrı topoloji**: VLAN'lar birbirinden bağımsız olarak yönetilebilir, böylece daha fazla esneklik sağlanır.
3. **Ağ yedekliliği**: Bir VLAN için seçilen yollar arızalanırsa, diğer VLAN'lar etkilenmez.

#### **PVST Dezavantajları**:

1. **Kaynak kullanımı**: Her VLAN için ayrı bir STP örneği çalıştığından, ağ cihazlarının **işlemci gücü** ve **bant genişliği** üzerinde ek yük oluşturur.
2. **Ağ karmaşıklığı**: Çok fazla VLAN olan ağlarda, her VLAN için **ayrı STP topolojisinin yönetimi** daha karmaşık hale gelir.


### **2. PVST+ (Per VLAN Spanning Tree Plus)**

**PVST+**, **Cisco** tarafından geliştirilmiş bir **uzantıdır** ve **PVST’nin** daha **gelişmiş versiyonudur**. **PVST+**, **IEEE 802.1Q VLAN trunking** standardı ile uyumlu çalışarak, VLAN'lar arasında trunk bağlantıları üzerinden **STP BPDU'larını iletmek** için daha geniş bir **uyumluluk sağlar**.

#### **PVST+’ın Temel Özellikleri**:

* **802.1Q uyumluluğu** sağlar: **VLAN trunking** ile uyumlu olarak, trunk bağlantıları üzerinden **VLAN bazlı STP BPDU’larını** iletebilir.
* **VLAN trunking** ile STP'nin çalışmasını sağlar. Bir trunk bağlantısı üzerinden birden fazla VLAN için STP BPDU'ları taşınabilir.
* **Daha geniş cihaz uyumluluğu**: **PVST+**, farklı cihazlar arasında daha uyumlu çalışabilir, çünkü IEEE 802.1Q standardına uygun olarak çalışır.
* **VLAN bazlı root bridge seçimi**: Her VLAN için farklı **Root Bridge** seçimi yapılabilir.

#### **PVST+ Avantajları**:

1. **Gelişmiş uyumluluk**: **IEEE 802.1Q** ile uyumludur ve **trunk bağlantıları** üzerinden BPDU iletimi yapabilir. Bu, farklı üreticilerin cihazları arasında uyumlu çalışmayı sağlar.
2. **Ağ yönetimi**: **PVST**'nin sağladığı tüm avantajları sunar, ancak daha geniş uyumluluk ve daha az sınırlama ile birlikte gelir.
3. **Ağ kaynaklarının verimli kullanımı**: VLAN başına **STP topolojisi** oluşturulması sayesinde ağda daha verimli ve dengeli bir trafik akışı sağlanabilir.

#### **PVST+ Dezavantajları**:

1. **Kaynak kullanımı**: Her VLAN için bağımsız bir STP örneği çalıştırılır, bu da işlemci gücü ve bant genişliği üzerinde yük oluşturur.
2. **Karmaşık yönetim**: Çok sayıda VLAN olan ağlarda, her VLAN için ayrı STP topolojisi yönetimi **zorlaşabilir**.



### **PVST ve PVST+ Arasındaki Farklar**

| Özellik                | PVST (Per VLAN Spanning Tree)           | PVST+ (Per VLAN Spanning Tree Plus)                                               |
| ---------------------- | --------------------------------------- | --------------------------------------------------------------------------------- |
| **Uyumluluk**          | Cisco cihazları arasında çalışır        | 802.1Q VLAN trunking ile uyumludur                                                |
| **STP BPDU İletimi**   | Sadece Cisco cihazları arasında çalışır | Trunk bağlantıları üzerinden çalışabilir                                          |
| **VLAN Bazlı STP**     | Her VLAN için bağımsız STP              | Her VLAN için bağımsız STP, ancak trunk bağlantıları üzerinden iletim yapılabilir |
| **Root Bridge Seçimi** | Her VLAN için farklı Root Bridge seçimi | Her VLAN için farklı Root Bridge seçimi                                           |
| **Kullanım Alanı**     | Cisco ağ cihazları arasında sınırlı     | Daha geniş cihaz uyumluluğu ve trunk bağlantılarında kullanılabilir               |



### **PVST ve PVST+ Kullanım Senaryoları**

* **PVST**: Özellikle **Cisco ağ cihazları** ve **VLAN'lar** arasında **basit yapılandırmalar** gerektiğinde kullanılır. **Cisco cihazları** arasında kullanılan ağlarda, PVST sayesinde her VLAN için **bağımsız bir ağ topolojisi** oluşturulabilir.

* **PVST+**: **802.1Q trunking** ile **VLAN'lar arası veri iletimi** yapılması gereken ağlarda kullanılır. **Trunk bağlantıları** üzerinden **farklı VLAN'lar** için STP BPDU’larının taşınması gerektiğinde tercih edilir. Ayrıca, **çoklu üretici cihazları** arasında uyumlu bir STP yapısı sağlamak için **PVST+** kullanılır.


## **PortFast Nedir?**

**PortFast**, **Spanning Tree Protocol (STP)**'nin bir özelliğidir ve bir switch portunun **Forwarding** (iletişim) durumuna hızlıca geçmesini sağlar. Normalde, STP kullanılarak ağda bağlantı kuran her port, ağdaki olası döngüleri engellemek amacıyla **Listening** ve **Learning** durumlarında bekler. Bu bekleme süresi, genellikle 30-50 saniye arasında değişebilir. **PortFast**, bu süreyi atlayarak portu doğrudan **Forwarding** durumuna getirir, böylece cihazlar daha hızlı bir şekilde ağla bağlantı kurar.

**PortFast** genellikle, **end-user cihazları** (PC, IP telefonlar, yazıcılar vb.) için kullanılır. Çünkü bu cihazlar genellikle ağda döngü yaratmazlar ve STP’nin tam olarak çalışmasına gerek yoktur.

### **PortFast Nasıl Çalışır?**

STP'nin normalde kullandığı dört durum şunlardır:

1. **Blocking**: Port, trafiği iletmiyor ve ağdaki döngüleri önlemek için kapalı durumda.
2. **Listening**: Port, ağdaki döngüleri kontrol eder ancak henüz veri iletmez.
3. **Learning**: Port, ağdaki MAC adreslerini öğrenir ancak hala veri iletmez.
4. **Forwarding**: Port, veri iletebilir ve ağ üzerinden trafiği yönlendirebilir.

**PortFast**, yukarıdaki süreçlerde sadece **Listening** ve **Learning** aşamalarını atlar ve portu doğrudan **Forwarding** durumuna getirir. Bu sayede cihazlar hızlıca ağa bağlanabilir.

### **PortFast Nerelerde Kullanılır?**

**PortFast**, genellikle **end-user cihazları** için etkinleştirilir. Bu cihazlar, ağda döngü yaratmadıkları için **STP**'nin geçiş aşamalarını beklemeye gerek yoktur. **PortFast**, ağdaki cihazların bağlanma sürelerini kısaltır ve kullanıcı deneyimini iyileştirir. Ayrıca, **PortFast**, **access port**'larında kullanılır, yani switch’in diğer switch’lere bağlantı sağladığı **trunk portları** üzerinde kullanılmaz.

### **PortFast Nasıl Yapılandırılır?**

**PortFast**'ı yapılandırmak için aşağıdaki adımları takip edebiliriz:

1. **PortFast'ı Tek Bir Portta Etkinleştirme**:
   PortFast'ı belirli bir portta etkinleştirmek için şu komutları kullanabilirsiniz:

   ```
   Switch1(config)# interface fa0/1
   Switch1(config-if)# spanning-tree portfast
   ```

   Bu komut, **fa0/1** portunu **PortFast** moduna geçirir ve bağlantı kurulum süresi hızlanır.

2. **PortFast'ı Varsayılan Olarak Etkinleştirme**:
   Eğer tüm portlarda **PortFast**'ı etkinleştirmek isterseniz, aşağıdaki komutla tüm portlar için varsayılan olarak aktif hale getirebilirsiniz:

   ```
   Switch1(config)# spanning-tree portfast default
   ```

   Bu komut, switch üzerindeki tüm **access port**’larında **PortFast**'ı etkinleştirir.

### **PortFast’ın Avantajları**:

* **Hızlı Bağlantı Kurulumu**: Cihazlar ağa daha hızlı bağlanır çünkü port doğrudan **Forwarding** durumuna geçer.
* **Kullanıcı Deneyimi İyileştirme**: IP telefonlar, PC'ler ve diğer **end-user** cihazları için ağ bağlantısı hızlıca gerçekleşir.
* **Ağ Performansını Artırır**: Gecikme sürelerini ortadan kaldırarak ağın genel performansını artırır.

### **PortFast’ın Dezavantajları**:

* **Döngü Riski**: **PortFast**, portu doğrudan **Forwarding** durumuna getirdiği için, ağdaki **root bridge** veya **designated bridge** cihazlarına yanlışlıkla etkinleştirilirse, ağda döngü oluşabilir.
* **STP Hataları**: **PortFast**, tüm STP geçiş aşamalarını atladığı için ağda beklenmedik sorunlara yol açabilir.

### **PortFast’ın Test Edilmesi**:

**PortFast** etkinleştirilen bir portta cihazı bağladığınızda, ağ bağlantısının hemen kurulması gerekir. Cihaz, IP adresini hızlıca alır ve iletişime başlar. Bu, **STP**’nin normal geçiş sürecinden çok daha hızlıdır.

### **PortFast ve RSTP**:

**Rapid Spanning Tree Protocol (RSTP)**, **STP**'nin daha hızlı bir versiyonudur ve **PortFast**'ı çok daha hızlı bir şekilde uygular. **RSTP** ile birlikte kullanılan **PortFast**, ağda daha hızlı bir şekilde cihazların bağlantı kurmasını sağlar.



## **Packet Tracer STP Yapılandırması Örneği**

**Spanning Tree Protocol (STP)**, ağdaki döngüleri engellemek için kullanılan kritik bir protokoldür. Packet Tracer üzerinde STP yapılandırması, ağda veri iletimini sağlarken döngü oluşumlarını engellemeye yardımcı olur. Bu başlık altında, STP yapılandırmasını adım adım örnek bir ağ topolojisi üzerinde gerçekleştireceğiz. Yapılandırma, **Root Bridge seçimi**, **port rolleri** ve **port durumları** gibi temel bileşenlerin nasıl çalıştığını anlamanızı sağlayacaktır.

### **1. Topoloji Oluşturma ve Bağlantılar**

Öncelikle, bir **Packet Tracer** topolojisi oluşturacağız. Bu topoloji, üç switch ve iki PC içerecek ve bu ağda **STP** yapılandırmasını yapacağız.

#### **Topoloji**

* **Switch1**, **Switch2** ve **Switch3** cihazlarını kullanacağız.
* **PC1** ve **PC2** cihazlarını **Switch1** ve **Switch2**'ye bağlayacağız.
* Switch'ler arasında bağlantılar yaparak ağ topolojisini oluşturacağız.

#### **Bağlantılar**:

* **PC1** → **Switch1**
* **PC2** → **Switch2**
* **Switch1** → **Switch2**
* **Switch2** → **Switch3**
* **Switch3** → **Switch1**

### **2. STP'nin Varsayılan Durumunu Kontrol Etme**

Packet Tracer’da **STP**, varsayılan olarak etkin hale gelir. Bu nedenle, STP'nin etkin olup olmadığını kontrol etmek için aşağıdaki komutu kullanabiliriz.

1. **Switch1**'in komut satırına erişin ve aşağıdaki komutu girin:

   ```
   Switch1# show spanning-tree
   ```

Bu komut, STP'nin aktif olup olmadığını ve hangi **Root Bridge**'in seçildiğini gösterir. İlk olarak **Root Bridge** seçimi otomatik olacak ve **Bridge ID** ile **Root ID**’yi kontrol edebileceksiniz.

### **3. Root Bridge Seçimi Yapma**

STP'de ağın **Root Bridge**'ini belirlemek için her switch'in **Bridge ID** değerinin en düşük olanı **Root Bridge** olarak seçilir. Ancak, ağda **Root Bridge**’i manuel olarak seçmek isteyebilirsiniz.

#### **Root Bridge Seçimi İçin Priority Değeri Ayarlama**

**Switch1**'i Root Bridge olarak seçmek için **priority** değerini değiştirebiliriz. **Priority** değeri, **Bridge ID**'nin bir parçasıdır ve bu değer, **Root Bridge** seçiminde önemli bir rol oynar.

* **Switch1**'i Root Bridge olarak seçmek için:

  ```
  Switch1(config)# spanning-tree vlan 1 priority 24576
  ```

* **Switch2** ve **Switch3**’ün **priority** değerlerini varsayılan olarak bırakacağız. Bu durumda, **Switch1**'in **Root Bridge** olarak seçilmesi sağlanır.

#### **Root Bridge’i Kontrol Etme**

Root Bridge'in kim olduğunu görmek için şu komutu kullanabilirsiniz:

```
Switch1# show spanning-tree
```

Burada, **Root ID** kısmında, **Root Bridge**'in **Bridge ID**’sini görebilirsiniz.



### **4. Port Rolleri ve Durumları**

STP, her portu farklı rollere ayırır. Bu port rolleri ağda veri iletimini sağlar ve döngülerin engellenmesine yardımcı olur. Aşağıda, her portun görevini açıklayacağız:

#### **Port Rolleri**:

* **Root Port**: En kısa yolun bulunduğu port. Root Bridge’e giden yoldur.
* **Designated Port**: Trafiği geçiren port. Her segmentin bir Designated Port'u vardır.
* **Blocked Port**: Döngüleri engellemek için pasif hale getirilen port.

#### **Port Durumları**:

* **Forwarding**: Port, veri iletimi yapabilir.
* **Blocking**: Port, döngüleri engellemek için pasif hale getirilmiştir.
* **Listening**: Port, BPDU'ları dinler, ancak veri iletimi yapmaz.
* **Learning**: Port, MAC adreslerini öğrenir, ancak veri iletimi yapmaz.

#### **Port Durumlarını Görüntüleme**

Port rolleri ve durumlarını görmek için aşağıdaki komutu kullanabilirsiniz:

```
Switch1# show spanning-tree vlan 1
```

Bu komut, port rolleri ve port durumları hakkında bilgi verir. **Root Port** ve **Designated Port**'ler aktifken, **Blocked Port**'ler ağda döngüleri engellemek amacıyla pasif duruma gelir.



### **5. STP Zamanlayıcılarının Ayarlanması**

STP'nin doğru şekilde çalışabilmesi için bazı zamanlayıcıların ayarlanması gerekmektedir. **Hello Time**, **Forward Delay** ve **Max Age** gibi zamanlayıcılar, ağdaki değişikliklere nasıl tepki verileceğini belirler.

#### **Zamanlayıcıları Ayarlamak**

* **Hello Time**: BPDU’ların gönderilme sıklığı.
* **Forward Delay**: Bir portun **Listening** ve **Learning** durumları arasında geçiş süresi.
* **Max Age**: BPDU'ların geçerlilik süresi.

Örnek olarak, zamanlayıcıları aşağıdaki gibi değiştirebilirsiniz:

```
Switch1(config)# spanning-tree vlan 1 hello-time 5
Switch1(config)# spanning-tree vlan 1 forward-delay 20
Switch1(config)# spanning-tree vlan 1 max-age 30
```

Bu komutlar, **Hello Time**'ı 5 saniyeye, **Forward Delay**'i 20 saniyeye ve **Max Age**'i 30 saniyeye ayarlayacaktır.


### **6. STP Konfigürasyonunu Test Etme**

Konfigürasyonu test etmek için, topolojiyi gözlemleyebilirsiniz. Örneğin, ağda bir portu **bloklamak** ve ardından **STP'nin** nasıl tepki verdiğini görmek için, bir bağlantıyı kesebilirsiniz.

#### **Bağlantıyı Kesme ve STP'nin Tepkisini Gözlemleme**:

Bir switch portunu **shutdown** komutuyla kapatarak ağdaki port durumlarını gözlemleyebilirsiniz:

```
Switch1(config)# interface fa0/1
Switch1(config-if)# shutdown
```

Bağlantıyı kapattığınızda, STP’nin yeni bağlantı yolunu hesaplayıp devreye alması beklenir. Bunun sonucunda, **Blocked Port**'in durumu değişir ve ağda döngü oluşumunu engeller.



## **Packet Tracer Uygulaması RSTP**

**Rapid Spanning Tree Protocol (RSTP)**, **STP**’nin geliştirilmiş bir versiyonudur ve ağdaki topolojik değişikliklere daha hızlı tepki vererek ağın daha hızlı toparlanmasını sağlar. Bu başlık altında, **RSTP**’yi Packet Tracer üzerinde yapılandıracak ve ağdaki değişikliklere nasıl hızlı tepki verdiğini gözlemleyeceğiz.

### **1. Topoloji Oluşturma**

Bu uygulama için, daha önce oluşturduğumuz **STP** topolojisini kullanacağız. Ancak, bu sefer **RSTP** kullanacağız. Bu topolojide üç adet **switch** (Switch1, Switch2, Switch3) ve iki adet **PC** (PC1, PC2) yer alacak.

#### **Topoloji**:

* **PC1** → **Switch1**
* **PC2** → **Switch2**
* **Switch1** → **Switch2**
* **Switch2** → **Switch3**
* **Switch3** → **Switch1**

**RSTP** yapılandırmasını uygulamak için önce **STP** yapılandırmamızın RSTP'ye uygun şekilde değişmesini sağlayacağız.

### **2. RSTP Modunu Etkinleştirme**

Packet Tracer’da RSTP’yi etkinleştirmek için **spanning-tree** komutunu kullanarak her switch’te **RSTP** modunu aktif hale getireceğiz. **RSTP**, daha hızlı topluluklar arası geçiş süresi ve daha hızlı ağ toparlanma sağlar.

#### **RSTP Modunu Etkinleştirmek İçin Komutlar**:

Her bir switch'te aşağıdaki komutu giriyoruz:

```
Switch1(config)# spanning-tree mode rapid-pvst
Switch2(config)# spanning-tree mode rapid-pvst
Switch3(config)# spanning-tree mode rapid-pvst
```

Bu komut, her switch'te **Rapid PVST+ (Per VLAN Spanning Tree)** modunu etkinleştirir. Bu mod, her VLAN için ayrı **STP** örneği çalıştırır, dolayısıyla VLAN başına daha hızlı ağ toparlanması sağlar.

### **3. RSTP Zamanlayıcılarının Ayarlanması**

RSTP, STP’den farklı olarak **Hello Time**’i sabit tutar ve **Forward Delay** ve **Max Age** gibi değerleri optimize eder. **RSTP**'nin temel özelliklerinden biri, geçiş sürelerinin **STP'ye** göre çok daha hızlı olmasıdır.

#### **Zamanlayıcıları Ayarlama**:

**RSTP**’de zamanlayıcılar STP’ye göre daha hızlıdır. Yine de, zamanlayıcıları özel ihtiyaçlarınıza göre ayarlayabilirsiniz.

Örneğin:

```
Switch1(config)# spanning-tree vlan 1 hello-time 2
Switch1(config)# spanning-tree vlan 1 forward-delay 15
Switch1(config)# spanning-tree vlan 1 max-age 20
```

Bu komutlar ile **Hello Time**’ı 2 saniye, **Forward Delay**’i 15 saniye ve **Max Age**’i 20 saniye olarak ayarlayabilirsiniz.

### **4. RSTP Port Durumları**

**RSTP**'de portlar daha hızlı geçiş yapar ve geçiş süreçlerini daha kısa sürede tamamlar. **STP**’deki **Listening** ve **Learning** durumları, **RSTP**'de doğrudan **Discarding** ve **Forwarding** olarak basitleştirilmiştir. **RSTP** portları hızlıca **Discarding** ve **Forwarding** arasında geçiş yapar.

#### **Port Durumları**:

* **Discarding**: Port, veri iletimi yapmaz, ancak BPDU’ları dinler.
* **Forwarding**: Port, veri iletimi yapabilir.
* **Learning**: Bu durum **RSTP**’de kullanılmaz. Yalnızca **Forwarding** ve **Discarding** durumları vardır.

Portların durumlarını görmek için şu komutu kullanabilirsiniz:

```
Switch1# show spanning-tree vlan 1
```

Bu komut, her portun hangi durumda olduğunu ve hangi portların aktif olduğunu gösterir.

### **5. Root Bridge Seçimi ve RSTP**

**RSTP**’de Root Bridge seçim süreci **STP**'ye benzer şekilde çalışır. Ancak, **RSTP**’de geçişler daha hızlıdır. Root Bridge seçimi için **Priority** değerini değiştirebilirsiniz.

Örneğin, **Switch1**'i Root Bridge olarak belirlemek için:

```
Switch1(config)# spanning-tree vlan 1 priority 24576
```

Bu komut, **Switch1**’i **Root Bridge** olarak seçecektir.

#### **Root Bridge Seçimini Kontrol Etme**:

```
Switch1# show spanning-tree
```

Bu komutla, Root Bridge’in kim olduğunu ve portların durumlarını kontrol edebilirsiniz.

### **6. RSTP’nin Hızlı Tepkisini Test Etme**

**RSTP**, ağda oluşan değişikliklere çok hızlı tepki verir. Bir port kapanarak bir bağlantı kaybolduğunda, **RSTP** hızlıca yeni bir yol oluşturur. Bu, **STP**’de daha uzun süren bir işlemdir.

#### **Bağlantıyı Kapatma ve RSTP Tepkisini Görme**:

Bir bağlantıyı kapattığınızda, **RSTP** çok hızlı bir şekilde yeni bir köprü yolu oluşturur. **STP**'de bu işlem birkaç saniye sürebilirken, **RSTP**’de bu süre daha kısadır.

1. **Switch1** üzerindeki portu kapatın:

   ```
   Switch1(config)# interface fa0/1
   Switch1(config-if)# shutdown
   ```

2. Bu portu kapattıktan sonra, **RSTP** yeni port yollarını hemen aktif hale getirecektir. Geçiş hızını gözlemleyebilirsiniz.


## **Packet Tracer Uygulaması MSTP**

**Multiple Spanning Tree Protocol (MSTP)**, birden fazla **VLAN** için tek bir **Spanning Tree** ağını oluşturarak ağın yönetimini kolaylaştıran ve performansı artıran bir protokoldür. MSTP, **STP** ve **RSTP**’nin özelliklerini birleştirerek, çoklu VLAN’lar için tek bir **spanning tree**’yi kullanırken aynı zamanda her VLAN için farklı ağ tasarımları oluşturmanıza olanak tanır. Bu başlık altında, **MSTP** yapılandırmasını **Packet Tracer** üzerinde gerçekleştireceğiz ve alan tanımlamalarıyla birlikte nasıl çalıştığını öğreneceğiz.

### **1. Topoloji Oluşturma**

Bu uygulama için daha önceki **STP** ve **RSTP** topolojilerini kullanabiliriz. Bu topolojide **Switch1**, **Switch2**, ve **Switch3**'ü kullanacağız. Ayrıca, her switch için farklı VLAN’lar oluşturacağız ve her VLAN için ayrı **MSTP** instance'ları tanımlayacağız.

#### **Topoloji**:

* **PC1** → **Switch1**
* **PC2** → **Switch2**
* **Switch3** → **Switch1** (Switch1 ile Switch3 arasında yedek bağlantı)
* **Switch1** → **Switch2**
* **Switch2** → **Switch3**

Bu topolojiyi kurarak **MSTP**’yi yapılandıracağız.

### **2. MSTP Modunun Etkinleştirilmesi**

**MSTP**, **Rapid PVST+** ve **STP** gibi diğer spanning tree protokollerinin yerine geçebilir. **MSTP**, her VLAN için ayrı bir **instance** kullanarak ağdaki döngüleri önler ve ağın daha verimli çalışmasını sağlar.

Packet Tracer’da **MSTP** modunu etkinleştirmek için aşağıdaki adımları takip edeceğiz:

#### **MSTP Modunu Etkinleştirme**:

Her switch'te **MSTP**’yi etkinleştireceğiz:

```
Switch1(config)# spanning-tree mode mst
Switch2(config)# spanning-tree mode mst
Switch3(config)# spanning-tree mode mst
```

Bu komutla **Switch1**, **Switch2**, ve **Switch3**’ü **MSTP** moduna geçiriyoruz.

### **3. MSTP Alan Tanımlamaları (MST Instances)**

MSTP, **VLAN’ları** farklı **instance'lar** (örneğin, **VLAN 10**’u **instance 1** olarak) grubunda toplar. Bu sayede her VLAN için farklı **spanning tree** instance’ları oluşturulur.

#### **MSTP Instance Oluşturma ve VLAN’ları Atama**:

Her VLAN'ı bir **instance**'a atayarak, ağda daha esnek ve verimli bir **spanning tree** yapılandırması sağlayacağız. Bu örnekte, **VLAN 10**'u **Instance 1**'e ve **VLAN 20**'yi **Instance 2**'ye atayacağız.

1. **MSTP Instance Yapılandırması**:

   * **Switch1**:

     ```
     Switch1(config)# spanning-tree mst configuration
     Switch1(config-mst)# instance 1 vlan 10
     Switch1(config-mst)# instance 2 vlan 20
     Switch1(config-mst)# exit
     ```
   * **Switch2**:

     ```
     Switch2(config)# spanning-tree mst configuration
     Switch2(config-mst)# instance 1 vlan 10
     Switch2(config-mst)# instance 2 vlan 20
     Switch2(config-mst)# exit
     ```
   * **Switch3**:

     ```
     Switch3(config)# spanning-tree mst configuration
     Switch3(config-mst)# instance 1 vlan 10
     Switch3(config-mst)# instance 2 vlan 20
     Switch3(config-mst)# exit
     ```

Yukarıdaki komutlar, **Switch1**, **Switch2** ve **Switch3**'te **MSTP** instance'ları oluşturur ve **VLAN 10**'u **Instance 1**'e, **VLAN 20**'yi ise **Instance 2**'ye atar.

#### **MSTP Topoloji Durumunu Görüntüleme**:

MSTP'nin doğru şekilde yapılandırıldığını kontrol etmek için aşağıdaki komutu kullanabiliriz:

```
Switch1# show spanning-tree mst
```

Bu komut, her instance’ın durumunu ve hangi VLAN’ların hangi instance’a ait olduğunu gösterecektir.

### **4. MSTP Konfigürasyonu ve Root Bridge Seçimi**

MSTP’de **Root Bridge** seçimi, her **instance** için ayrı yapılır. Bu sayede her VLAN için bağımsız **Root Bridge**’ler seçilebilir. Root Bridge’i seçmek için **priority** değerini değiştirebilirsiniz.

#### **Root Bridge Seçimi**:

* **Switch1**'i **instance 1** için Root Bridge olarak belirlemek için:

  ```
  Switch1(config)# spanning-tree mst 1 priority 24576
  ```
* **Switch2** ve **Switch3**’ü **instance 1**'in Root Bridge’i olarak bırakmak için varsayılan **priority** değerini koruyacağız.

#### **Root Bridge Durumunu Kontrol Etme**:

```
Switch1# show spanning-tree mst
```

Bu komut, **Root Bridge**'in kim olduğunu ve her instance için port durumlarını gösterir.

### **5. MSTP Zamanlayıcılarının Yapılandırılması**

MSTP, **STP** ve **RSTP**'ye benzer zamanlayıcılar kullanır. Ancak, **MSTP**’de **Hello Time**, **Max Age**, ve **Forward Delay** gibi zamanlayıcılar, **instance** bazında özelleştirilebilir.

#### **Zamanlayıcıları Ayarlama**:

Zamanlayıcıları her **instance** için ayrı olarak ayarlayabilirsiniz. Örneğin, **instance 1** için aşağıdaki gibi ayarlamalar yapılabilir:

```
Switch1(config)# spanning-tree mst 1 hello-time 2
Switch1(config)# spanning-tree mst 1 forward-delay 15
Switch1(config)# spanning-tree mst 1 max-age 20
```

Bu komutlar, **instance 1** için zamanlayıcıları ayarlar ve ağdaki geçiş sürelerini optimize eder.

### **6. MSTP’nin Test Edilmesi ve Topolojik Değişiklikler**

MSTP, ağdaki topolojik değişikliklere karşı hızlı tepki verir. Bir portu kapatıp ağın tepki süresini gözlemleyeceğiz.

#### **Bağlantıyı Kapatma ve MSTP Tepkisini Görme**:

* **Switch1**’in portunu kapatmak için:

  ```
  Switch1(config)# interface fa0/1
  Switch1(config-if)# shutdown
  ```
* Bağlantıyı kapattıktan sonra, **MSTP** yeni port yolunu hemen aktif hale getirecektir. Bu geçişin hızını gözlemleyebilirsiniz.


