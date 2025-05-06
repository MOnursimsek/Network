# **DHCP**

## DHCP Nedir?

**DHCP (Dynamic Host Configuration Protocol)**, bir ağ üzerindeki istemcilere otomatik olarak IP adresi ve diğer ağ yapılandırma bilgilerini atayan bir protokoldür. DHCP, istemcilerin manuel olarak yapılandırılmasına gerek kalmadan ağa katılmasını sağlar. Bu protokol, hem küçük hem de büyük ölçekli ağlarda yönetimi kolaylaştırmak ve adres atamalarında insan hatasını azaltmak için kullanılır.

DHCP, istemci-sunucu modeliyle çalışır. Ağda bir **DHCP sunucusu**, istemciler tarafından yapılan IP adresi ve yapılandırma isteğine karşılık olarak geçici veya kalıcı olarak bir IP adresi atar. Ayrıca ağ geçidi (gateway), DNS sunucusu, alt ağ maskesi (subnet mask) gibi önemli bilgileri de otomatik olarak sağlar. İstemci bu bilgileri aldıktan sonra ağa sorunsuz bir şekilde bağlanabilir.


## DHCP'nin Amacı ve Önemi

DHCP’nin temel amacı, IP adreslerinin ve diğer ağ yapılandırmalarının **otomatik ve merkezi bir şekilde yönetilmesini** sağlamaktır. Özellikle kullanıcı sayısının fazla olduğu ağlarda IP adreslerini manuel olarak vermek oldukça zahmetli ve hataya açık bir işlemdir. DHCP, bu işlemleri otomatikleştirerek hem zaman kazandırır hem de hataları en aza indirir.

**DHCP'nin başlıca önemi şu şekilde özetlenebilir:**

* **Otomasyon ve Kolaylık:** Ağ yöneticileri IP adreslerini tek tek yapılandırmak zorunda kalmaz. DHCP, bu süreci otomatik hale getirerek zamandan tasarruf sağlar.
* **Merkezi Yönetim:** IP adresi havuzlarının merkezi olarak yönetilmesini mümkün kılar. Böylece hangi IP adresinin hangi cihaza atandığı takip edilebilir.
* **Hata Azaltma:** Manuel yapılandırma sırasında oluşabilecek IP çakışması, yanlış alt ağ maskesi ya da ağ geçidi gibi hataların önüne geçilir.
* **Dinamik Atama:** Cihazlar ağa bağlandıklarında otomatik olarak geçici (lease süresiyle sınırlı) IP adresleri alabilir. Bu, özellikle misafir ağları veya mobil cihazlar için idealdir.
* **Verimlilik:** Ağ kaynaklarının daha etkin kullanılmasını sağlar. Kullanılmayan IP adresleri yeniden kullanılabilir hale gelir.
* **Taşınabilirlik:** Bir cihaz farklı bir ağa bağlandığında DHCP sayesinde yeniden manuel yapılandırmaya gerek kalmaz.

Sonuç olarak, DHCP hem kullanıcı deneyimini iyileştiren hem de ağ yöneticilerinin işini kolaylaştıran kritik bir ağ servisidir.

## DHCP Nasıl Çalışır? (DHCP İşlem Adımları: DORA)

DHCP, istemci ile DHCP sunucusu arasında dört temel adımdan oluşan bir iletişim süreciyle çalışır. Bu işlem sıklıkla **DORA** kısaltmasıyla ifade edilir. DORA, aşağıdaki adımların baş harflerinden oluşur:

1. **Discover (Keşif)**
2. **Offer (Teklif)**
3. **Request (İstek)**
4. **Acknowledgment (Onay)**

Bu adımlar sayesinde istemci, ağdan geçici veya kalıcı olarak bir IP adresi ve diğer yapılandırma bilgilerini alır. Süreç genellikle birkaç saniye içinde tamamlanır ve otomatik olarak gerçekleşir.


### DHCP İletişim Süreci (Discover, Offer, Request, Acknowledgment)

#### 1. **Discover (Keşif)**

Bu ilk adımda, ağa yeni katılan istemci cihaz henüz IP adresine sahip değildir. Bu nedenle DHCP sunucusunu bulmak için **broadcast (yayın)** tipi bir mesaj gönderir. Bu mesaj tüm ağa gönderilir ve "Bir DHCP sunucusu var mı?" anlamına gelir.

* Bu paket IP seviyesinde `0.0.0.0` adresinden `255.255.255.255` hedef adresine gönderilir.
* Amaç, DHCP sunucularının kendisini fark etmesini sağlamaktır.

#### 2. **Offer (Teklif)**

Ağda bulunan DHCP sunucusu, Discover mesajını aldıktan sonra istemciye bir **IP adresi önerisi** içeren **DHCP Offer** mesajını gönderir. Bu mesajda:

* Teklif edilen IP adresi
* Alt ağ maskesi (subnet mask)
* Varsayılan ağ geçidi (default gateway)
* DNS sunucusu adresleri
* IP adresinin kiralama süresi (lease time)
  gibi bilgiler yer alır.

DHCP sunucusu bu teklifi de **broadcast** olarak gönderir, çünkü istemcinin henüz atanmış bir IP adresi yoktur.

#### 3. **Request (İstek)**

İstemci, birden fazla DHCP sunucusundan teklif almış olabilir. Bu adımda istemci, seçtiği sunucunun teklifini kabul ettiğini belirtmek için bir **DHCP Request** mesajı gönderir.
Bu mesajda, istemci:

* Teklif edilen IP adresini talep ettiğini belirtir.
* Hangi DHCP sunucusunu seçtiğini bildirir.

Bu mesaj da yine **broadcast** olarak gönderilir. Böylece diğer sunucular, tekliflerinin reddedildiğini anlar ve kaynaklarını serbest bırakır.

#### 4. **Acknowledgment (Onay)**

Son adımda seçilen DHCP sunucusu, istemcinin isteğini onaylamak için **DHCP Acknowledgment (ACK)** mesajı gönderir. Bu mesajda:

* IP adresi ataması onaylanır.
* Diğer yapılandırma parametreleri (subnet, gateway, DNS vb.) tekrarlanır.

Bu aşamadan sonra istemci artık IP adresini kullanmaya başlayabilir ve ağ üzerinde iletişim kurabilir.

Bu dört adım sayesinde IP adresleri dinamik ve otomatik bir şekilde atanır. DORA süreci, ağ yönetimini kolaylaştıran en önemli mekanizmalardan biridir.

## DHCP Paket Yapısı

DHCP, **UDP protokolü üzerinden çalışan** bir uygulama katmanı protokolüdür ve temel olarak **BOOTP (Bootstrap Protocol)** üzerine inşa edilmiştir. DHCP paketleri, BOOTP mesaj yapısını kullanır ve üzerine bazı ek alanlar eklenmiştir.

Bir DHCP paketinin genel yapısı aşağıdaki alanlardan oluşur:

| Alan Adı    | Uzunluk (Bayt) | Açıklama                                                      |
| ----------- | -------------- | ------------------------------------------------------------- |
| **op**      | 1              | Mesaj tipi: 1 = İstemci (request), 2 = Sunucu (reply)         |
| **htype**   | 1              | Donanım tipi: 1 = Ethernet                                    |
| **hlen**    | 1              | Donanım adresi uzunluğu (örneğin Ethernet için 6)             |
| **hops**    | 1              | Yönlendirici sayacı; genellikle 0 olarak ayarlanır            |
| **xid**     | 4              | İşlem kimliği (Transaction ID); istemci tarafından belirlenir |
| **secs**    | 2              | İstemcinin DHCP sürecine başladığından beri geçen süre        |
| **flags**   | 2              | Yayın (broadcast) bayrağı                                     |
| **ciaddr**  | 4              | İstemcinin mevcut IP adresi (yenileme sırasında kullanılır)   |
| **yiaddr**  | 4              | Sunucunun istemciye teklif ettiği IP adresi                   |
| **siaddr**  | 4              | Seçilen DHCP sunucusunun IP adresi                            |
| **giaddr**  | 4              | DHCP relay ajanının IP adresi                                 |
| **chaddr**  | 16             | İstemcinin donanım (MAC) adresi                               |
| **sname**   | 64             | Opsiyonel sunucu adı                                          |
| **file**    | 128            | Başlatılacak dosyanın adı (TFTP için)                         |
| **options** | Değişken       | DHCP seçenekleri (örn: mesaj türü, alt ağ maskesi, DNS, vs.)  |

**Options alanı**, DHCP’nin esnekliğini sağlayan en önemli kısımdır. Örneğin:

* `Option 53`: DHCP mesaj türünü belirtir (Discover, Offer, vs.)
* `Option 1`: Subnet maskesi
* `Option 3`: Varsayılan ağ geçidi
* `Option 6`: DNS sunucuları
* `Option 51`: Lease süresi


## DHCP Mesaj Türleri

DHCP protokolü içinde kullanılan çeşitli mesaj türleri vardır. Bu mesajlar, istemci ve sunucu arasında haberleşmeyi sağlar. En yaygın kullanılan mesaj türleri şunlardır:

| Mesaj Türü       | Açıklama                                                                                                                  |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **DHCPDISCOVER** | İstemcinin ağ üzerindeki DHCP sunucularını aradığı ilk mesajdır.                                                          |
| **DHCPOFFER**    | DHCP sunucusunun istemciye IP adresi ve yapılandırma bilgisi teklif ettiği yanıttır.                                      |
| **DHCPREQUEST**  | İstemcinin teklif edilen IP adresini kabul ettiğini belirttiği mesajdır.                                                  |
| **DHCPACK**      | DHCP sunucusunun IP adresi atamasını onayladığı mesajdır.                                                                 |
| **DHCPNAK**      | Sunucunun istemcinin isteğini reddettiği durumlarda gönderilir (örneğin geçersiz IP).                                     |
| **DHCPDECLINE**  | İstemcinin teklif edilen IP adresini başka bir cihazın kullandığını fark edip reddetmesi durumunda gönderilir.            |
| **DHCPRELEASE**  | İstemcinin IP adresini serbest bırakmak için DHCP sunucusuna gönderdiği mesajdır.                                         |
| **DHCPINFORM**   | Halihazırda bir IP adresine sahip istemcinin, sadece konfigürasyon bilgilerini talep ettiği mesajdır (IP adresi istemez). |

## DHCP Port Numaraları

DHCP, **UDP (User Datagram Protocol)** üzerinde çalışır ve istemci ile sunucu arasında belirli portlar kullanılır:

| Taraf       | Port Numarası | Açıklama                             |
| ----------- | ------------- | ------------------------------------ |
| **İstemci** | UDP 68        | DHCP istemcisinin dinlediği porttur. |
| **Sunucu**  | UDP 67        | DHCP sunucusunun dinlediği porttur.  |

İstemci, IP adresi olmadığı için gönderdiği mesajları **broadcast** olarak yollar ve bu mesajlar UDP 67 portuna yönelir. Sunucu da yanıtlarını UDP 68 portuna gönderir.

## DHCP Kira Süresi (Lease Time)

**Kira süresi**, DHCP sunucusunun bir istemciye tahsis ettiği IP adresinin ne kadar süreyle geçerli olacağını belirleyen zaman aralığıdır. Bu süre, DHCP sunucusu tarafından ayarlanır ve saniye, dakika, saat ya da gün olarak ifade edilebilir.

#### Kira Süresinin İşleyişi:

* İstemci, IP adresini aldıktan sonra belirli bir süre için bu adresi kullanma hakkına sahip olur.
* Süre bitmeden önce, istemci kira süresini **yenilemek** için sunucuya **DHCP Request** mesajı gönderir.
* Sunucu **DHCP ACK** mesajı ile yanıt verirse, süre uzatılır.
* Eğer istemci belirli bir süre boyunca kira süresini yenileyemezse veya sunucu yanıt vermezse, istemci IP adresini bırakır ve yeniden Discover mesajı göndererek yeni bir IP talep eder.

#### Kira Süresi Ne Kadar Olmalı?

* **Kısa süreli** (örneğin 1 saat): Misafir ağları, sık sık bağlanan cihazlar için.
* **Uzun süreli** (örneğin 7 gün): Ofis bilgisayarları, sabit cihazlar için.

Doğru ayarlanmış kira süresi, IP adresi havuzunun verimli kullanılmasını sağlar.



## DHCP Rezervasyonları (MAC Adresine Göre IP Atama)

**DHCP rezervasyonu**, belirli bir cihazın MAC adresine önceden tanımlanmış bir IP adresinin sürekli olarak atanmasıdır. Bu yöntemle, cihaz her ağa bağlandığında aynı IP adresini alır.

#### Nasıl Çalışır?

* DHCP sunucusuna, belirli bir MAC adresi ile eşleştirilecek sabit bir IP adresi tanımlanır.
* İlgili istemci ağa her bağlandığında, sunucu bu MAC adresini tanır ve tanımlı IP adresini gönderir.
* Cihaz otomatik yapılandırma avantajını korur, ama sabit IP adresiyle çalışır.

#### Ne Zaman Kullanılır?

* Yazıcılar
* Dosya sunucuları
* Güvenlik kameraları
* Ağ cihazları (yönlendirici, switch vb.)
* Port yönlendirme veya güvenlik duvarı kurallarıyla IP bazlı işlem yapan sistemlerde

Bu yöntem, statik IP yapılandırmasının yönetimsel zorluklarını ortadan kaldırırken aynı kararlılığı sağlar.

## DHCP Seçenekleri (DHCP Options)

DHCP protokolü, istemcilere yalnızca IP adresi değil; aynı zamanda çeşitli ağ yapılandırma bilgilerini de gönderebilmek için **"options" (seçenekler)** alanını kullanır. Bu seçenekler, DHCP paketinin sonundaki **options** bölümünde yer alır ve her biri bir kod numarasıyla tanımlanır.

#### Yaygın Kullanılan DHCP Seçenekleri:

| Kod | Seçenek Adı                  | Açıklama                                        |
| --- | ---------------------------- | ----------------------------------------------- |
| 1   | **Subnet Mask**              | Alt ağ maskesi (örnek: 255.255.255.0)           |
| 3   | **Router (Gateway)**         | Varsayılan ağ geçidi IP adresi                  |
| 6   | **Domain Name Server (DNS)** | DNS sunucularının IP adresleri                  |
| 15  | **Domain Name**              | Varsayılan alan adı (örnek: local)              |
| 51  | **IP Address Lease Time**    | Kira süresi (IP adresinin geçerlilik süresi)    |
| 53  | **DHCP Message Type**        | Paket türünü belirtir (Discover, Offer, vs.)    |
| 54  | **Server Identifier**        | DHCP sunucusunun IP adresi                      |
| 66  | **TFTP Server Name**         | PXE önyükleme yapan cihazlar için TFTP sunucusu |
| 67  | **Bootfile Name**            | Başlatılacak önyükleme dosyası adı              |

#### DHCP Options Nasıl Kullanılır?

* DHCP sunucuları, seçenekleri yapılandırma arayüzü veya CLI üzerinden belirleyerek tüm istemcilere dağıtabilir.
* Örneğin bir istemcinin DNS sunucusunu DHCP ile otomatik alması için Option 6 kullanılır.
* PXE önyükleme için Option 66 ve 67 birlikte kullanılır.

DHCP seçenekleri, ağ yöneticisinin cihazları merkezi olarak yapılandırmasını sağlar ve yönetimi büyük ölçüde kolaylaştırır.

## DHCP Relay Agent (IP Helper)

#### Sorun:

DHCP istemcisi, IP adresi alabilmek için **DHCP Discover** mesajını **broadcast (255.255.255.255)** olarak gönderir. Ancak yönlendiriciler (router), varsayılan olarak **broadcast paketlerini farklı alt ağlara yönlendirmez**.

Bu nedenle, istemcinin bulunduğu ağda doğrudan bir DHCP sunucusu yoksa, DHCP işlemi başarısız olur.

#### Çözüm: **DHCP Relay Agent (IP Helper)**

DHCP Relay Agent, farklı bir ağdaki DHCP sunucusuna broadcast mesajların ulaşmasını sağlayan bir **aracı görevi** görür. Bu görev genellikle yönlendirici (router) tarafından yapılır.

##### İşleyiş:

1. DHCP istemcisi Discover mesajını gönderir (broadcast).
2. Router bu mesajı alır ve kendi IP adresini **relay agent IP (giaddr)** olarak kullanarak **unicast** biçiminde DHCP sunucusuna iletir.
3. DHCP sunucusu, yanıtını yine router’a gönderir.
4. Router, gelen yanıtı istemciye iletir.

#### Cisco Router'da DHCP Relay Ayarı (IP Helper Address):

```bash
interface FastEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 ip helper-address 10.0.0.10   ! DHCP sunucusunun IP adresi
```

#### IP Helper Ne İşe Yarar?

`ip helper-address` komutu, sadece DHCP değil aynı zamanda diğer UDP hizmetlerini de yönlendirebilir (varsayılan olarak UDP 8 servis). Ancak en yaygın kullanımı DHCP içindir.

## DHCPv6: IPv6 için DHCP

DHCPv6, **IPv6** ağları için tasarlanmış olan **Dynamic Host Configuration Protocol**'ün bir versiyonudur. IPv6, IPv4’ün sınırlamalarını aşmak amacıyla geliştirilmiş yeni bir protokol olduğundan, bu yeni protokolle birlikte IP adresi ataması ve diğer ağ yapılandırmalarının yönetilmesi gereklidir. **DHCPv6**, IPv6 adresi ataması yapmak ve IPv6 istemcilerine ağ bilgilerini sağlamak için kullanılan bir protokoldür.



### 1. **DHCPv6'nin Temel Özellikleri**

DHCPv6, **IPv6 adres ataması**, **ağ yapılandırması** ve **DNS bilgileri** gibi ağ parametrelerini istemcilere dinamik olarak sağlamak için kullanılır. IPv6, daha fazla adres ve daha karmaşık ağ yapılandırmaları sunduğundan, DHCPv6, IPv4'teki DHCP'nin IPv6'a uyarlanmış halidir.

* **IPv6 Adres Ataması**: DHCPv6, istemcilere dinamik olarak IPv6 adresleri atar.
* **Stateless ve Stateful Modlar**: DHCPv6, istemcilere IP adresi atarken farklı yöntemler kullanabilir. Bu yöntemler **stateful** (durumlu) ve **stateless** (durumsuz) olmak üzere iki ana modda çalışabilir.



### 2. **Stateful ve Stateless Konfigürasyon Modları**

#### a. **Stateful (Durumlu) Konfigürasyon**

Stateful mod, DHCPv6 sunucusunun her bir istemciye bir IPv6 adresi ve diğer ağ yapılandırma bilgilerini (örneğin, DNS sunucusu, ağ geçidi vb.) atadığı moddur. Bu durumda, DHCPv6 sunucusu istemciye IP adresi atar ve bu adresin sürekliliğini izler. Ayrıca, istemciye verilen IP adresi ve diğer parametreler merkezi olarak yönetilir.

* **IP Adresi Ataması**: Sunucu, istemciye belirli bir IP adresi atar.
* **Kira Süresi (Lease Time)**: DHCPv6 sunucusu, atanan IP adresinin geçerlilik süresini belirler.
* **Sunucu Rolü**: DHCPv6 sunucusu, istemcilerin aldığı adresleri ve yapılandırmaları merkezi olarak izler ve yönetir.

#### b. **Stateless (Durumsuz) Konfigürasyon**

Stateless modda, DHCPv6 yalnızca **ekstra yapılandırma bilgileri** sağlar. Yani, istemci, ağda bir IPv6 adresi almak için **Link-Local** adreslerini kullanarak **IPv6 Autoconfiguration (SLAAC)** yöntemini kullanır. DHCPv6 sunucusu ise, istemciler için ek yapılandırma bilgilerini sağlar (örneğin, DNS sunucusu).

* **IPv6 Adresi**: İstemci, kendine otomatik olarak IP adresi atar (SLAAC).
* **Ekstra Yapılandırma Bilgileri**: DHCPv6 sunucusu, istemcilere DNS sunucu adresi gibi ek bilgileri sağlar.
* **Sunucu Rolü**: DHCPv6 sunucusu sadece ağ yapılandırma bilgilerini iletir, IP adresi atama işlemi istemcinin kendi başına yaptığı bir işlemdir.


### 3. **DHCPv6 Mesaj Türleri**

DHCPv6, istemciler ile sunucu arasındaki iletişimi sağlamak için birkaç farklı mesaj türü kullanır. Bu mesajlar, adres ataması, yapılandırma bilgileri ve kira süreleri ile ilgili çeşitli işlemleri kapsar.

#### a. **Sollicit (Soruşturma)**

İstemci, DHCPv6 sunucusunun varlığını sorgulamak için bir **Sollicit** mesajı gönderir. Bu mesaj, DHCPv6 sunucusunun istemciye cevap verip vermediğini anlamak için kullanılır.

#### b. **Advertise (Reklam)**

Sunucu, **Sollicit** mesajına cevap olarak **Advertise** mesajını gönderir. Bu mesajda, sunucu, istemcinin DHCPv6 sunucusuna katılmaya uygun olup olmadığı bilgisini içerir.

#### c. **Request (İstek)**

İstemci, sunucudan IP adresi ve yapılandırma bilgileri almak için bir **Request** mesajı gönderir. Bu mesajda, istemci, adres ve yapılandırma bilgilerini almak için sunucuya taleplerde bulunur.

#### d. **Reply (Cevap)**

Sunucu, istemcinin **Request** mesajına bir **Reply** mesajı ile cevap verir. Bu mesaj, istemcinin talepleri doğrultusunda atanan IPv6 adresi ve diğer ağ yapılandırma bilgilerini içerir.

#### e. **Renew (Yenileme)**

İstemci, mevcut IP adresini kullanmaya devam edebilmek için **Renew** mesajı gönderir. Bu, mevcut IP adresinin geçerliliğini uzatmak için kullanılır.

### 4. **DHCPv6 ve SLAAC Karşılaştırması**

* **SLAAC (Stateless Address Autoconfiguration)**, IPv6 istemcilerinin ağa bağlandığında kendilerine otomatik olarak bir IPv6 adresi ataması yapmasını sağlar. Bu süreçte, istemci ağın prefix bilgilerini alır ve geçerli bir adres oluşturur.
* **DHCPv6 Stateful**, istemcilere IP adresi atamak ve diğer yapılandırmaları sağlamak için sunucuya dayanır.

SLAAC, istemcilerin kendi adreslerini kendilerinin oluşturmasına olanak verirken, **DHCPv6 Stateful** çözümü daha merkezi bir yapılandırma sunar.



### 5. **DHCPv6 ve IPv6 Autoconfiguration**

IPv6, SLAAC (Stateless Address Autoconfiguration) özelliği ile istemcilerin ağda kendilerine otomatik olarak IP adresi atamalarına olanak tanır. Ancak, bazı durumlarda istemciler ek yapılandırma bilgileri almalıdır. Bu durumda **DHCPv6** devreye girer ve istemcilere ek ağ bilgilerini sağlar (DNS sunucusu, domain adı, vs.). Bu nedenle, **Stateless DHCPv6** ile birlikte SLAAC kullanılarak daha verimli bir yapılandırma elde edilebilir.



## Yönlendiricide DHCPv4 Yapılandırması

**DHCPv4 (Dynamic Host Configuration Protocol for IPv4)**, IPv4 ağlarında cihazlara dinamik olarak IP adresi atamak için kullanılan bir protokoldür. Yönlendiriciler, DHCPv4 sunucusu olarak yapılandırıldığında, ağdaki istemcilere (bilgisayarlar, telefonlar, yazıcılar, vb.) IP adresi atama işlemi otomatik olarak yapılır. DHCPv4'nin yönlendiricide yapılandırılması, IP adres yönetimini merkezi hale getirir ve ağ yöneticilerinin ağdaki IP adreslerinin takibini kolaylaştırır.


### 1. **DHCPv4 Sunucusu Yapılandırması**

Bir Cisco yönlendiricisinde **DHCPv4 sunucusu** yapılandırmak için aşağıdaki adımlar takip edilir.

#### a. **DHCPv4 Havuzu Oluşturma**

DHCPv4 havuzu, ağda dağıtılacak IP adreslerinin belirli bir aralığını tanımlar. İlk olarak, bir DHCP havuzu oluşturulmalıdır.

```
Router(config)# ip dhcp pool [pool_adı]
```

Örnek:

```
Router(config)# ip dhcp pool Ağaç_Ağı
```

Bu komut, "Ağaç\_Ağı" adında bir DHCPv4 havuzu oluşturur.

#### b. **Havuzda Ağ Adresini Belirleme**

DHCPv4 havuzunu oluşturduktan sonra, bu havuzun kullanacağı IP adres aralığını belirlemelisiniz. Bu, cihazlara atanacak IP adreslerinin belirli bir alt ağda yer almasını sağlar.

```
Router(dhcp-config)# network [ağ_adresi] [subnet_mask]
```

Örnek:

```
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
```

Bu, DHCPv4 havuzunun **192.168.1.0/24** ağında IP adresleri atayacağını belirtir.

#### c. **Varsayılan Ağ Geçidi (Gateway) Belirleme**

İstemcilere atanan IP adreslerine, ağ geçidi (default gateway) adresi de sağlanmalıdır. Bu, istemcilerin başka ağlara ulaşabilmesi için gerekli olan yönlendirici adresidir.

```
Router(dhcp-config)# default-router [gateway_adresi]
```

Örnek:

```
Router(dhcp-config)# default-router 192.168.1.1
```

Bu, istemcilere **192.168.1.1** IP adresini ağ geçidi olarak atar.

#### d. **DNS Sunucusu Belirleme**

Ağdaki istemcilere DNS sunucusu adresi sağlamak, ağdaki alan adı çözümlemesi için gereklidir.

```
Router(dhcp-config)# dns-server [dns_sunucu_adresi]
```

Örnek:

```
Router(dhcp-config)# dns-server 8.8.8.8
```

Bu komut, istemcilere **8.8.8.8** DNS sunucu adresini atar.

---

### 2. **DHCPv4 Havuzunda Diğer Ayarların Yapılandırılması**

#### a. **Kira Süresi (Lease Time) Ayarlama**

DHCPv4, bir IP adresi atandığında, bu adres belirli bir süreyle geçerlidir. Bu süreyi **kira süresi** (lease time) olarak adlandırırız. Kira süresi, DHCPv4 sunucusuna yapılan isteğin geçerlilik süresini belirler.

```
Router(dhcp-config)# lease [gün] [saat] [dakika]
```

Örnek:

```
Router(dhcp-config)# lease 1 12 0
```

Bu, IP adresinin 1 gün, 12 saat geçerli olacağı anlamına gelir.

#### b. **Ağ Dışında IP Adresi Rezervasyonu Yapmak**

Belirli bir cihazın her zaman aynı IP adresini almasını sağlamak için IP adresi rezervasyonu yapılabilir. Bunun için cihazın **MAC adresi** gereklidir.

```
Router(config)# ip dhcp pool [pool_adı]
Router(dhcp-config)# host [ip_adresi] [subnet_mask]
Router(dhcp-config)# hardware-address [mac_adresi]
```

Örnek:

```
Router(dhcp-config)# host 192.168.1.50 255.255.255.0
Router(dhcp-config)# hardware-address 00e0.4c68.8ac3
```

Bu, **192.168.1.50** IP adresini, **00e0.4c68.8ac3** MAC adresine sahip cihaza her zaman atar.

---

### 3. **DHCPv4 Sunucusu İçin IP Adresi Havuzunun Ayarlanması**

Bir yönlendirici üzerinde DHCPv4 yapılandırması yaparken, aynı zamanda bazı IP adreslerinin statik olarak atanması gerekebilir. Örneğin, ağda bazı cihazların her zaman belirli bir IP'yi alması istenebilir. Bu durumda **DHCPv4 rezervasyonları** yapılabilir. Bu, MAC adresi ile IP adresi eşleştirilerek yapılır.

#### a. **DHCPv4'dün Statik IP Ataması (DHCP Rezervasyonu)**

```
Router(config)# ip dhcp pool [pool_adı]
Router(dhcp-config)# host [ip_adresi] [subnet_mask]
Router(dhcp-config)# client-identifier [mac_adresi]
```

Örnek:

```
Router(config)# ip dhcp pool Ağaç_Ağı
Router(dhcp-config)# host 192.168.1.100 255.255.255.0
Router(dhcp-config)# client-identifier 00e0.4c68.8ac3
```

Bu, **192.168.1.100** IP adresini **00e0.4c68.8ac3** MAC adresine sahip cihaza atar.

---

### 4. **DHCPv4 Sunucusunun Aktif Edilmesi**

Yönlendiricide DHCPv4 hizmetini etkinleştirmek için aşağıdaki komut kullanılır:

```
Router(config)# ip dhcp excluded-address [başlangıç_adresi] [bitiş_adresi]
```

Bu komut, DHCPv4 sunucusunun atamaması gereken IP adresi aralığını belirler. Örneğin, yönlendirici IP adresi veya başka bir sabit cihaz için ayrılacak IP'ler dışlanabilir.

Örnek:

```
Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10
```

Bu, **192.168.1.1** ile **192.168.1.10** arasındaki adreslerin DHCP sunucusunun dışında tutulmasını sağlar.

---

### 5. **DHCPv4 Sunucusunun Devre Dışı Bırakılması**

Eğer DHCPv4 sunucusunu devre dışı bırakmak isterseniz, aşağıdaki komutu kullanabilirsiniz:

```
Router(config)# no ip dhcp pool [pool_adı]
```

Örnek:

```
Router(config)# no ip dhcp pool Ağaç_Ağı
```

Bu, belirtilen DHCP havuzunu devre dışı bırakır.


## Yönlendiricide DHCPv6 Yapılandırması

**DHCPv6**, IPv6 ağlarında IP adreslerinin dinamik olarak atanmasını sağlayan bir protokoldür. IPv4'teki DHCP'ye benzer şekilde, DHCPv6 de cihazların IP adreslerini almasını ve ağda doğru yapılandırılmalarını sağlamak için kullanılır. Yönlendiriciler üzerinde DHCPv6 yapılandırması, IPv6 adreslerinin otomatik olarak atanması ve yapılandırılması için gereklidir.

### **Adım 1: DHCPv6 Global Yapılandırma**

İlk olarak, **global ayarları** yapmak gerekir. Bu, DHCPv6'nin etkinleştirilmesi için gerekli olan temel yapılandırmadır.

**Komutlar:**

1. **Global yapılandırma moduna girin:**

   ```
   Router# configure terminal
   ```

2. **DHCPv6 sunucusunu etkinleştirin:**
   DHCPv6'yi etkinleştirmek için aşağıdaki komutu kullanarak yönlendiricide DHCPv6 sunucusunu başlatın.

   ```
   Router(config)# ipv6 dhcp pool [pool_adı]
   ```

   Burada, **\[pool\_adı]** yapılandırmak istediğiniz havuzun adıdır.

3. **DHCPv6 havuzu yapılandırın:**
   Havuzda kullanılacak IPv6 adresi aralığını belirlemek için şu komutu kullanabilirsiniz:

   ```
   Router(dhcp-config)# address prefix [prefix] [prefix uzunluğu]
   ```

   Örnek:

   ```
   Router(dhcp-config)# address prefix 2001:db8:1::/64
   ```

   Bu, **2001\:db8:1::/64** adres aralığını kullanarak cihazların DHCPv6 üzerinden bu adresi almasını sağlar.

4. **Diğer ayarları yapılandırın:**
   DHCPv6 havuzuna dahil edilmesi gereken diğer seçenekleri belirleyebilirsiniz. Örneğin, **DNS sunucusu** gibi:

   ```
   Router(dhcp-config)# dns-server 2001:db8:1::53
   ```

### **Adım 2: IPv6 Adresinin Yönlendirici Arayüzüne atanması**

DHCPv6 sunucusu, yönlendiricinin arayüzü üzerinden IP adresi atayacaktır. Bunu yapmak için, yönlendirici arayüzünü yapılandırmalısınız.

1. **Yönlendirici arayüzüne IPv6 adresi atayın:**

   ```
   Router(config)# interface [interface_adı]
   Router(config-if)# ipv6 address [ipv6_adresi]/[prefix uzunluğu]
   Router(config-if)# ipv6 enable
   ```

   Örnek:

   ```
   Router(config)# interface g0/1
   Router(config-if)# ipv6 address 2001:db8:1::1/64
   Router(config-if)# ipv6 enable
   ```

   Burada, **g0/1** Ethernet arayüzüne **2001\:db8:1::1/64** IPv6 adresi atanmıştır.

### **Adım 3: Yönlendirici Arayüzünde DHCPv6 Sunucusunu Etkinleştirme**

DHCPv6 sunucusunun, IPv6 adreslerini cihazlara atamasını sağlamak için, ilgili arayüzde DHCPv6 hizmetinin etkinleştirilmesi gerekir.

1. **Arayüzde DHCPv6 yapılandırmasını etkinleştirin:**

   ```
   Router(config-if)# ipv6 dhcp server [pool_adı]
   ```

   Bu komut, belirli bir arayüzde **\[pool\_adı]** havuzunu kullanarak DHCPv6 hizmetini etkinleştirir.

   Örnek:

   ```
   Router(config-if)# ipv6 dhcp server DHCPv6-Pool
   ```

   Bu komut, **DHCPv6-Pool** havuzunu kullanarak IPv6 adres atamalarını başlatacaktır.

### **Adım 4: DHCPv6 ile IP Adresi Almayı Test Etme**

Yapılandırma tamamlandıktan sonra, bir IPv6 istemcisine **DHCPv6** adresi atandığını test etmek gerekir.

1. **İstemci cihazına DHCPv6 adresi aldırmak için, istemcide IPv6 yapılandırmasını başlatın:**
   İstemcinin **IPv6 adres almasını** sağlamak için, istemcinin otomatik olarak DHCPv6 üzerinden IP alacak şekilde yapılandırılması gerekir. Bu genellikle istemcide **Stateless Address Autoconfiguration (SLAAC)** ya da **DHCPv6**'yı etkinleştirmekle yapılır.

2. **Test etmek için, istemcinin IP adresini kontrol edin:**
   İstemci cihazında aşağıdaki komutu çalıştırarak atanmış IPv6 adresini kontrol edebilirsiniz:

   ```
   show ipv6 address
   ```

   Bu komut, istemci cihazına atanmış olan IPv6 adreslerini görüntüler.

## Kaynakça

1. [RFC 2131 – Dynamic Host Configuration Protocol (DHCP)](https://datatracker.ietf.org/doc/html/rfc2131)
2. [RFC 8415 – DHCPv6: Dynamic Host Configuration Protocol for IPv6](https://datatracker.ietf.org/doc/html/rfc8415)


