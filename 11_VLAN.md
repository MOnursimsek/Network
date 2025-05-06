# **VLAN**

## **VLAN Nedir ve Ne Amaçla Kullanılır?**

**VLAN (Virtual Local Area Network)**, fiziksel olarak aynı ağda bulunan cihazları, mantıksal olarak birbirinden ayırarak farklı sanal ağlar oluşturmak için kullanılan bir ağ teknolojisidir. VLAN, özellikle ağda daha iyi yönetim, güvenlik ve performans sağlamak amacıyla kullanılır. Fiziksel ağ topolojisinden bağımsız olarak, ağ segmentleri oluşturulmasına olanak tanır.

#### **VLAN'ın Temel Amacı:**

* **Ağ Bölümlendirme:** VLAN, aynı fiziksel ağ altyapısını kullanan, fakat mantıksal olarak ayrılmış ağ segmentleri oluşturur. Bu, ağın daha verimli yönetilmesini sağlar.
* **Ağ Performansını İyileştirme:** Trafiği sınırlayarak ağ üzerindeki bant genişliğini optimize eder ve çakışmaları azaltır. Örneğin, bir VLAN'ın içinde yer alan cihazlar yalnızca o VLAN içindeki diğer cihazlarla iletişim kurar, bu da ağ trafiğini azaltır.
* **Güvenliği Artırma:** Güvenlik açısından, her VLAN, diğerlerinden izole edilebilir. Bu, ağdaki farklı kullanıcı grupları ve cihazlar arasında erişim kontrolü sağlar. Örneğin, bir VLAN'da bulunan finans departmanı, yalnızca kendine ait verilere erişebilir ve diğer departmanlarla paylaşım yapmaz.
* **Ağ Yönetimini Kolaylaştırma:** VLAN'lar sayesinde ağ yöneticileri, kullanıcıları coğrafi konumlarına veya departmanlarına göre grup haline getirebilir ve grupların yönetimini kolaylaştırabilir.


## **VLAN Kavramı ve Temel Prensipler**

**VLAN**'lar, **mantıksal ağ segmentleri** oluşturur ve genellikle bir veya daha fazla **switch** üzerinden yapılandırılır. Temel prensipler ve önemli kavramlar şunlardır:

#### **1. VLAN ID ve Etiketleme:**

VLAN'lar, her biri benzersiz bir **VLAN ID** (VLAN Kimliği) ile tanımlanır. Bu kimlik, VLAN'ı diğer VLAN'lardan ayıran ve iletişimi düzenleyen sayısal bir değerdir. VLAN ID'si 1 ile 4095 arasında bir değere sahip olabilir, ancak genellikle 1-1005 arası ID'ler kullanıcı VLAN'ları için, 1006-4095 arası ise sistem VLAN'ları için ayrılır.

VLAN ID'leri, ağ cihazları arasında **etiketleme** kullanılarak taşınır. Bu etiketleme, **802.1Q** protokolü tarafından sağlanır ve her Ethernet çerçevesine bir VLAN etiketi eklenir. Bu etiket, verilerin hangi VLAN'a ait olduğunu belirtir.

#### **2. VLAN'lar Arası İletişim:**

VLAN'lar, temelde birbirinden izole edilmiştir, yani bir VLAN içindeki cihazlar, doğrudan başka bir VLAN'daki cihazlarla iletişim kuramazlar. Bu durum, ağda güvenliği artırır ve trafiği optimize eder. Ancak, farklı VLAN'lar arasında iletişim kurmak için bir **router** veya **Layer 3 switch** kullanılır. Bu cihazlar, VLAN'lar arasında yönlendirme (routing) işlemi gerçekleştirir.

#### **3. Switch'lerde VLAN Yapılandırması:**

Bir **switch**, bir VLAN'a ait portları birbirine bağlar. Switch üzerindeki portlara VLAN'lar atanır, ve bu sayede belirli portlara bağlı cihazlar aynı VLAN'a dahil olur. **Access port** (erişim portu) sadece bir VLAN'a hizmet ederken, **trunk port** birden fazla VLAN'ı taşır.

* **Access Port:** Cihazlar yalnızca bir VLAN'a atanır. Genellikle son cihazlar, bilgisayarlar, yazıcılar vb. bağlanırken kullanılır.
* **Trunk Port:** Bu port, birden fazla VLAN'ı taşır ve genellikle switchler arasındaki bağlantılarda kullanılır. **802.1Q** etiketleme kullanılarak farklı VLAN'lar ayrılır.

#### **4. VLAN'ların İzolasyonu:**

Her VLAN, ağdaki diğer VLAN'lardan **mantıksal olarak izole edilir**. Bu, her VLAN'ın yalnızca kendi üyeleriyle iletişim kurmasına olanak tanır. Bu özellik, özellikle güvenlik ve ağ trafiği yönetimi için çok önemlidir.

#### **5. Default VLAN:**

Switch'lerde genellikle **VLAN 1** varsayılan VLAN olarak atanır. Tüm portlar ilk başta **VLAN 1**'e aittir. Ancak, güvenlik ve yönetim amacıyla, varsayılan VLAN değiştirilerek farklı VLAN'lar atanabilir.

#### **6. Dinamik VLAN Yapılandırması:**

VLAN'lar, ağ yöneticileri tarafından manuel olarak yapılandırılabileceği gibi, bazı durumlarda **dinamik VLAN yapılandırması** da yapılabilir. Bu, cihazların bağlı olduğu switch portu veya cihazın **MAC adresine** göre VLAN atamalarının otomatik yapılmasını sağlar.


## **VLAN Türleri (Statik, Dinamik, Genel)**

VLAN’lar; yapılandırılma ve yönetilme şekillerine göre farklı türlere ayrılır. Bu türler ağ yöneticilerine esneklik, güvenlik ve yönetilebilirlik sağlar. Temelde VLAN’lar üç ana kategoride incelenir: **Statik VLAN**, **Dinamik VLAN**, ve **Genel VLAN türleri**.


### **1. Statik VLAN (Port Tabanlı VLAN)**

Statik VLAN, bir switch üzerindeki belirli portlara manuel olarak VLAN ataması yapılarak oluşturulan VLAN türüdür. Her port sadece tek bir VLAN’a ait olur. Bağlı olan cihazın MAC adresine veya diğer özelliklerine bakılmaz; hangi porta bağlıysa o VLAN’a dahil olur.

### **Özellikleri:**

* Switch konfigürasyonları manuel olarak yapılır.
* Port’a hangi cihaz bağlanırsa bağlansın, o portun VLAN’ına dahil olur.
* Kolay yönetilir, öngörülebilirlik sağlar.
* Küçük ve orta ölçekli ağlarda yaygın olarak kullanılır.

### **Avantajları:**

* Kurulumu ve yapılandırması basittir.
* Trafik kontrolü ve güvenlik açısından nettir; çünkü bağlantı port temellidir.
* Hangi cihazın hangi VLAN’da olduğunu fiziksel bağlantıdan anlayabilirsiniz.

### **Dezavantajları:**

* Taşınabilirlik zayıftır. Cihaz farklı bir porta bağlandığında, VLAN ayarının yeniden yapılması gerekir.
* Büyük ağlarda yönetimi zorlaşabilir, zaman alabilir.

---

### **2. Dinamik VLAN (MAC Tabanlı VLAN)**

Dinamik VLAN, switch’e bağlanan cihazların **MAC adreslerine**, **kullanıcı bilgilerine**, ya da **giriş protokollerine** göre otomatik olarak VLAN ataması yapılan türdür. VLAN atamaları **VMPS (VLAN Management Policy Server)** gibi bir merkezi sunucu tarafından gerçekleştirilir.

### **Özellikleri:**

* Kullanıcının hangi porta bağlandığı önemli değildir; kim olduğu önemlidir.
* Switch, cihazın MAC adresine göre VLAN atamasını otomatik yapar.
* VLAN bilgileri bir veritabanı (örneğin MAC-VLAN eşleşmesi) içinde saklanır.
* Genellikle kurumsal yapılarda, mobil kullanıcıların yoğun olduğu sistemlerde tercih edilir.

### **Avantajları:**

* Cihazlar ağa nereden bağlanırsa bağlansın, doğru VLAN’a yönlendirilir.
* Esnek yapı sağlar, kullanıcı taşınabilirliği yüksektir.
* Büyük ağlarda merkezi yönetimle verimlilik sağlar.

### **Dezavantajları:**

* Kurulum ve yapılandırma karmaşıktır.
* VMPS gibi ek altyapı gerektirir.
* Sorun giderme süreci daha zor olabilir.

---

### **3. Genel VLAN Türleri (VLAN Kategorileri ve Kullanım Amaçları)**

 Bu başlık altında, VLAN’lar farklı amaçlara göre sınıflandırılır. Bunlar statik veya dinamik yapılandırmalardan bağımsız olarak, işlevlerine göre çeşitlendirilir:


### **a. Default VLAN (Varsayılan VLAN)**

* Genellikle VLAN 1’dir.
* Tüm switch portları bu VLAN’da başlar.
* Switch yönetimi ve bazı protokoller bu VLAN üzerinden çalışır.
* Güvenlik sebebiyle kullanılmaması tavsiye edilir.

### **b. Management VLAN (Yönetim VLAN’ı)**

* Switch veya yönlendirici gibi cihazların yönetim trafiğini taşır.
* Cihazlara SSH, Telnet veya SNMP gibi yönetim protokolleriyle ulaşılır.
* Genellikle ayrı bir VLAN atanarak ağ trafiğinden izole edilir.
* Örneğin: `VLAN 10 – Management`


### **c. Voice VLAN (Ses VLAN’ı)**

* IP telefonların verilerini taşıyan VLAN türüdür.
* QoS (Quality of Service) önceliğiyle ses trafiği, veri trafiğinden ayrılır.
* Trunk portlarda hem veri hem ses VLAN’ı birlikte taşınabilir.
* Ses gecikmelerini azaltmak için kullanılır.


### **d. Native VLAN**

* 802.1Q trunk bağlantılarında, etiketlenmemiş trafiğin taşındığı VLAN’dır.
* Varsayılan olarak VLAN 1’dir.
* Güvenlik için başka bir VLAN atanması önerilir (örneğin VLAN 999).
* Trunk portlar arasında uyum sağlamak için kullanılır.


### **e. Guest VLAN (Misafir VLAN’ı)**

* Ağa geçici olarak bağlanan kullanıcılar için oluşturulan VLAN’dır.
* Sınırlı internet erişimi verilir; iç ağlara erişim engellenir.
* Güvenliği artırır ve izolasyon sağlar.


## VLAN ID Nedir?

* **VLAN ID**, bir VLAN’ı diğerlerinden ayırmak için kullanılan sayısal bir kimliktir.
* **0 – 4095** arasında değer alabilir; ancak tüm aralık kullanılmaz:

  * **0**: Etiketli ama VLAN ID’siz özel kullanım (Priority Tagging).
  * **1 – 4094**: Kullanıcı tanımlı VLAN'lar.
  * **4095**: Rezerve edilmiş, özel amaçlı.
* En yaygın VLAN ID örnekleri:

  * VLAN 1: Default VLAN (varsayılan).
  * VLAN 10, 20, 30: Kullanıcı VLAN’ları.
  * VLAN 999: Native VLAN olarak güvenlik için önerilir.

## 802.1Q Etiketleme (Tagging) Mantığı

802.1Q, bir Ethernet çerçevesine VLAN bilgisi eklemek için kullanılır. Bu işlem, **"tagging"** olarak adlandırılır. Yani Ethernet çerçevesi içerisine özel bir VLAN etiketi yerleştirilir.

###  **Etiketleme Nerede Kullanılır?**

* **Trunk portlarında** kullanılır; çünkü bu portlardan birden fazla VLAN trafiği geçer.
* Access portlarda etiketleme yapılmaz; çerçeve sadece ait olduğu VLAN’a aittir.


###  **802.1Q VLAN Etiket Yapısı (Ethernet Frame)**

802.1Q standardı, Ethernet çerçevesine **4 baytlık (32 bit)** bir VLAN etiketi ekler. Bu etiket, **Ethernet başlığı ile veri alanı arasına** yerleştirilir.

### Etiketlenmiş bir Ethernet çerçevesi yapısı:

```
[Destination MAC]  
[Source MAC]  
[Tag Protocol Identifier (TPID) - 2 byte: 0x8100]  
[Tag Control Information (TCI) - 2 byte]  
[EtherType / Length]  
[Payload]  
[FCS (Frame Check Sequence)]
```

###  **Tag Control Information (TCI) Alanı:**

Aşağıdaki bilgileri içerir:

| Bit Sayısı | Alan                              | Açıklama                                  |
| ---------- | --------------------------------- | ----------------------------------------- |
| 3 bit      | **Priority (PCP)**                | QoS için öncelik seviyesi (0–7)           |
| 1 bit      | **Drop Eligible Indicator (DEI)** | Trafiğin önemsiz olup olmadığını belirtir |
| 12 bit     | **VLAN ID**                       | 0–4095 arası VLAN kimliği                 |

Örnek: VLAN 10 için bir çerçeveye TCI alanında `0000 0000 0000 1010` (binary) yerleştirilir.

## **VLAN Port Türleri**

VLAN (Virtual Local Area Network) yapılandırmasında, switch üzerindeki portların nasıl davranacağını belirlemek için her bir porta uygun bir **port türü (port mode)** atanır. VLAN port türleri, bir portun hangi VLAN’lara hizmet ettiğini ve çerçevelerin etiketlenip etiketlenmeyeceğini belirler.

Temel olarak VLAN port türleri üçe ayrılır:

### 1. **Access Port**

Access port, yalnızca **tek bir VLAN’a** ait trafiği taşıyan ve bu trafiği **etiketsiz (untagged)** olarak işleyen port türüdür.

### 🔹 Özellikler:

* Sadece **bir VLAN’a** ait olabilir (genellikle bir son kullanıcı VLAN’ı).
* Gelen ve giden trafik **etiketsizdir**.
* Porttan gelen trafik switch içinde ilgili VLAN'a yönlendirilir.
* Genellikle **son kullanıcı cihazları** (PC, yazıcı, IP telefon vb.) bu portlara bağlanır.

### 🔹 Çalışma Prensibi:

* Port, yalnızca atanmış VLAN’a ait trafiği kabul eder.
* Başka VLAN’dan gelen etiketli çerçeveler reddedilir.
* Bu porttan çıkan veri, karşı cihaza etiketsiz gönderilir.

### 🔹 Konfigürasyon Örneği (Cisco):

```bash
Switch(config)# interface fastethernet0/10
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
```


### 2. **Trunk Port**

Trunk port, **birden fazla VLAN’ın** trafiğini aynı fiziksel hat üzerinden taşıyabilen port türüdür. VLAN trafiği, **802.1Q** standardına göre **etiketlenerek (tagged)** gönderilir.

### 🔹 Özellikler:

* Birden çok VLAN’ı destekler.
* Trafik 802.1Q çerçeve etiketi (tag) ile taşınır.
* Bir **Native VLAN** atanabilir, bu VLAN’dan gelen/verilen trafik etiketlenmez (etiketsiz gider).
* Genellikle **switch-switch**, **switch-router**, **switch-server** bağlantılarında kullanılır.

### 🔹 Çalışma Prensibi:

* Gelen çerçeve üzerindeki VLAN etiketi okunarak ilgili VLAN'a yönlendirilir.
* Giden çerçeveye VLAN etiketi eklenerek hedef switch’e iletilir.

### 🔹 Konfigürasyon Örneği (Cisco):

```bash
Switch(config)# interface gigabitethernet0/1
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# switchport trunk native vlan 99
```


### 3. **Hybrid Port**&#x20;

Hybrid port, hem **access hem de trunk** özelliklerini destekleyebilen esnek port türüdür. Aynı anda **etiketsiz ve etiketli VLAN trafiğini** taşıyabilir.

### 🔹 Özellikler:

* **Bir VLAN için untagged**, diğer VLAN’lar için **tagged** yapı destekler.
* Genellikle **VoIP telefon + bilgisayar** gibi birden fazla cihazın aynı fiziksel porta bağlandığı senaryolarda kullanılır.
* Cisco cihazlarında doğrudan "hybrid" komutu yoktur; aynı işlevsellik özel yapılandırmalarla elde edilebilir.

### 🔹 Çalışma Prensibi:

* Belirli VLAN için gelen/verilen trafik etiketsizdir.
* Diğer VLAN’lara ait trafik etiketli olarak taşınır.

###

###  Karşılaştırma Tablosu

| Özellik        | Access Port      | Trunk Port          | Hybrid Port               |
| -------------- | ---------------- | ------------------- | ------------------------- |
| VLAN Desteği   | Sadece bir VLAN  | Birden fazla VLAN   | Birden fazla VLAN         |
| Etiketleme     | Etiketsiz        | Etiketli (802.1Q)   | Etiketli + Etiketsiz      |
| Kullanım Alanı | Son kullanıcılar | Switch/router arası | VoIP + PC ortak port gibi |
| Native VLAN    | Uygulanmaz       | Kullanılır          | Uygulanabilir             |

## **Cisco Switch'te Statik VLAN Yapılandırması (CLI ile)**

**Statik VLAN yapılandırması**, belirli portlara belirli VLAN’ların atanması işlemidir. Bu işlem, portların sadece belirli bir VLAN’a ait cihazları kabul etmesini sağlar ve ağda daha iyi trafik yönetimi ve güvenlik sağlar.

### **Adım Adım Statik VLAN Yapılandırması**

#### 1. **Switch'e Bağlantı Kurma**

Öncelikle **Cisco switch**'e bağlanmanız gerekir. Bunu, **console kablosu** ile veya uzaktan **SSH/Telnet** kullanarak yapabilirsiniz.

Bağlantı kurulduktan sonra, switch'in yönetim moduna erişmek için CLI'yi (Command Line Interface) kullanmalısınız.

```bash
Switch> enable
Switch# configure terminal
```

#### 2. **VLAN'ı Tanımlama**

İlk adımda, switch üzerinde **statik VLAN oluşturulması** gerekmektedir. VLAN ID'sini belirleyerek bir VLAN oluşturulur. Burada VLAN numarasını ve ismini belirleyebilirsiniz.

**VLAN oluşturma komutları:**

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit
```

* Bu örnekte, **VLAN 10** oluşturulmuş ve ismi **Sales** olarak atanmıştır.
* VLAN ID'si 10, VLAN ismi ise "Sales" olarak belirlenmiştir.

#### 3. **Portları VLAN’a Atama**

Şimdi, belirlediğiniz VLAN'a portları atamanız gerekiyor. Bunun için, **port yapılandırma moduna** geçilir ve ilgili portlar atanır.

##### **Access Port Yapılandırması:**

Eğer bir portu belirli bir VLAN'a **access port** olarak atayacaksanız, aşağıdaki adımları takip etmelisiniz.

Örnek olarak **FastEthernet0/1** portunu **VLAN 10 (Sales)**'a atayalım:

```bash
Switch(config)# interface fastethernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

* **`switchport mode access`**: Bu komut, portu **access port** olarak ayarlar.
* **`switchport access vlan 10`**: Bu komut ile portu **VLAN 10**'a atar.

##### **Trunk Port Yapılandırması (Opsiyonel):**

Eğer portu **trunk port** olarak ayarlayacaksanız ve birden fazla VLAN taşımak istiyorsanız, aşağıdaki komutları kullanabilirsiniz:

```bash
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit
```

* **`switchport mode trunk`**: Bu komut, portu **trunk port** olarak yapılandırır.
* **`switchport trunk allowed vlan 10,20`**: Bu komut ile sadece **VLAN 10** ve **VLAN 20**'yi trunk port üzerinden taşımayı sağlar.

#### 4. **Yapılandırmayı Kaydetme**

Yapılandırmayı tamamladıktan sonra, değişikliklerin kalıcı olması için **switch konfigürasyonunu kaydetmeniz** gerekir. Bu işlem, switch'in yeniden başlatılmasından sonra yapılan değişikliklerin kaybolmaması için önemlidir.

```bash
Switch# write memory
```

ya da

```bash
Switch# copy running-config startup-config
```

Bu komutlar, yaptığınız tüm değişiklikleri **startup-config** dosyasına kaydeder.

### **Statik VLAN Yapılandırma Örneği:**

Diyelim ki **VLAN 10** (Sales) ve **VLAN 20** (HR) oluşturacaksınız ve her iki VLAN’ı farklı portlara atayacaksınız.

1. **VLAN Tanımlaması:**

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit
```

2. **Portları VLAN’lara Atama:**

* **VLAN 10** için **FastEthernet0/1** portunu, **VLAN 20** için **FastEthernet0/2** portunu atayalım.

```bash
Switch(config)# interface fastethernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit

Switch(config)# interface fastethernet 0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit
```

### **VLAN Yapılandırmasında Dikkat Edilmesi Gerekenler:**

* **VLAN ID'leri benzersiz olmalıdır**. Aynı VLAN ID’sine sahip birden fazla VLAN oluşturulamaz.
* **Switchport mode access** komutu yalnızca bir VLAN'a ait trafiği taşıyan portlarda kullanılır.
* **Switchport mode trunk** komutu ile portu, birden fazla VLAN'ı taşımaya uygun hale getirebilirsiniz. Trunk portlarda VLAN etiketi eklenir.
* **VLAN’lar arası iletişim**, router veya Layer 3 switch üzerinden sağlanabilir. VLAN’lar birbirinden izole çalışır.


## **Cisco Switch'te Trunk Port Yapılandırması**

**Trunk port**, birden fazla VLAN’ın aynı fiziksel bağlantı üzerinden taşınmasını sağlayan port türüdür. Trunk portlar, **etiketlenmiş (tagged)** trafiği taşır ve genellikle **switch-to-switch** veya **switch-to-router** bağlantılarında kullanılır. Trunking, VLAN'lar arasında iletişimi mümkün kılar.

### **Trunk Port Yapılandırması Adımları**

#### 1. **Switch'e Bağlanma**

İlk olarak, Cisco switch'ine **console** veya uzaktan bağlantı (SSH/Telnet) ile bağlanmalısınız. Yönetim moduna geçmek için aşağıdaki komutları kullanabilirsiniz:

```bash
Switch> enable
Switch# configure terminal
```

#### 2. **Trunk Port Yapılandırması**

Trunk port yapılandırmasını, genellikle **GigabitEthernet** veya **FastEthernet** portlarında yaparsınız. Aşağıdaki adımları izleyerek trunk portu yapılandırabilirsiniz:

* Trunk portun etiketli trafik taşıyabilmesi için, portun **trunk mode** olarak ayarlanması gerekir.

**Trunk port yapılandırma komutları:**

```bash
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# exit
```

* **`switchport mode trunk`**: Bu komut portu trunk port olarak ayarlar.
* **`switchport trunk encapsulation dot1q`**: Trunk port için **802.1Q** etiketleme protokolünü belirler. **Dot1q**, VLAN etiketleme protokolüdür.
* **`switchport trunk allowed vlan 10,20,30`**: Bu komut, sadece **VLAN 10**, **VLAN 20** ve **VLAN 30**'un trunk port üzerinden taşınmasını sağlar.

#### 3. **Native VLAN Yapılandırması**

Trunk portlarda, **native VLAN** kullanımı önemlidir. Native VLAN, trunk port üzerinde **etiketsiz (untagged)** olarak gönderilen trafiğin ait olduğu VLAN'dır. Varsayılan olarak, **native VLAN** **VLAN 1**'dir. Ancak, bu VLAN değiştirilerek daha güvenli bir yapı oluşturulabilir.

**Native VLAN yapılandırma komutu:**

```bash
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# exit
```

* Bu komut, trunk portunun **native VLAN**'ını **VLAN 99** olarak ayarlar. Native VLAN'dan gelen trafik etiketsiz olarak iletilir.

#### 4. **VLAN'ların Trunk Üzerinden Taşınması**

Yapılandırma sonrasında, trunk portu üzerinden hangi VLAN'ların taşınacağını **allowed VLAN listesi** belirler. Eğer bir VLAN, trunk porttan geçmesine izin verilen VLAN’lar listesinde yer almıyorsa, bu VLAN'ın trafiği geçemez.

**VLAN ekleme veya kaldırma komutları:**

```bash
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport trunk allowed vlan add 40
Switch(config-if)# switchport trunk allowed vlan remove 30
Switch(config-if)# exit
```

* **`add`**: Bu komut, yeni bir VLAN'ı trunk port üzerinden taşınan VLAN listesine ekler.
* **`remove`**: Bu komut, mevcut bir VLAN'ı trunk portu üzerinden taşınan VLAN listesinden çıkarır.

#### 5. **Yapılandırmayı Kaydetme**

Son olarak, yapılandırmaların kaybolmaması için switch’in konfigürasyonunu kaydedin.

```bash
Switch# write memory
```

ya da

```bash
Switch# copy running-config startup-config
```
### **Dinamik VLAN Yapılandırması ve VMPS**

Dinamik VLAN yapılandırması, **VLAN'ların otomatik olarak atandığı** ve **daha esnek bir ağ yapısının oluşturulduğu** bir yöntemdir. Bu yapılandırma genellikle **VLAN Management Policy Server (VMPS)** kullanılarak yapılır. Dinamik VLAN'lar, ağ cihazlarına bağlanan cihazların türüne, MAC adresine veya diğer parametrelere göre VLAN'ların otomatik olarak atanmasını sağlar.

### **Dinamik VLAN Yapılandırması**

**Dinamik VLAN yapılandırması**, kullanıcıların veya cihazların VLAN'larını **manuel müdahale olmadan** değiştirebilmelerini sağlar. Bu tür yapılandırmalar, özellikle **büyük ağlarda** yönetimi kolaylaştırmak için oldukça etkilidir. **Dinamik VLAN**, port tabanlı değil, **cihaz tabanlı** bir VLAN atama süreci sunar.

#### **Dinamik VLAN'ın Temel Çalışma Prensibi:**

1. **Bağlantı Talebi**: Bir cihaz, switch'e bağlandığında, switch, cihazın **MAC adresini** ve **port numarasını** kullanarak VLAN'ı dinamik olarak atar.
2. **VMPS ile İletişim**: Switch, cihazın MAC adresini, **VLAN Management Policy Server (VMPS)**'ye gönderir.
3. **VLAN Ataması**: VMPS, cihazın hangi VLAN'a atanması gerektiğini belirler ve switch'e iletir.
4. **VLAN Ataması ve İletişim**: Switch, gelen yanıtla cihazı ilgili VLAN'a yönlendirir.

Dinamik VLAN yapılandırmasının en önemli avantajı, kullanıcıların veya cihazların hareketleri ile VLAN'ların değiştirilebilmesidir. Bu, özellikle **kullanıcıların farklı fiziksel lokasyonlarda çalıştığı** ağlarda faydalıdır.

### **VLAN Management Policy Server (VMPS)**

**VLAN Management Policy Server (VMPS)**, **dinamik VLAN atamalarını** yöneten bir sunucudur. VMPS, switch'lere VLAN atama için gerekli bilgileri sağlar. Switch'ler, cihazları bağladığında, VMPS sunucusundan bu cihazlara uygun VLAN bilgilerini alır. VMPS, cihazların MAC adreslerine göre hangi VLAN'a ait olduklarını belirler.

#### **VMPS'in Temel Fonksiyonları:**

* **VLAN Ataması**: VMPS, cihazların MAC adreslerine göre doğru VLAN'ı belirler ve switch'e iletir.
* **Veritabanı Yönetimi**: VMPS, bir veritabanı kullanarak cihazların MAC adreslerini ve bu adreslere atanan VLAN bilgilerini saklar.
* **Dinamik Konfigürasyon**: Switch'ler, cihazlar bağlandıkça VMPS ile iletişim kurarak VLAN bilgilerini dinamik olarak alır.

#### **VMPS Çalışma Prensibi:**

1. **Switch Bağlantısı**: Bir cihaz, switch'e bağlandığında, switch cihazın **MAC adresini** tespit eder.
2. **VMPS Sunucusuna İletişim**: Switch, cihazın MAC adresini **VMPS sunucusuna** gönderir.
3. **VLAN Ataması**: VMPS, MAC adresine göre doğru VLAN'ı bulur ve switch'e gönderir.
4. **VLAN Atamasının Uygulanması**: Switch, VMPS'ten aldığı yanıt doğrultusunda cihazı uygun VLAN'a yönlendirir.

#### **VMPS Yapılandırması:**

VMPS'i kullanabilmek için, Cisco switch üzerinde aşağıdaki adımları takip ederek yapılandırma yapılır.

1. **VMPS Sunucu Konfigürasyonu**: VMPS sunucusunun çalışması için öncelikle **VMPS veritabanı** oluşturulur. Bu veritabanında, cihazların MAC adreslerine göre VLAN atamaları yapılır.

```bash
Switch(config)# vmps server ip_address
Switch(config)# vmps database flash:vmps.dat
```

* **`vmps server ip_address`**: Bu komut, VMPS sunucusunun IP adresini belirtir.
* **`vmps database flash:vmps.dat`**: Bu komut, VMPS veritabanını belirler.

2. **Switch Konfigürasyonu**: Switch portları dinamik VLAN atamaları için yapılandırılır.

```bash
Switch(config)# interface range fa0/1 - 24
Switch(config-if-range)# switchport mode dynamic desirable
Switch(config-if-range)# exit
```

* **`switchport mode dynamic desirable`**: Bu komut, switch portlarının dinamik VLAN'ları kabul edecek şekilde yapılandırılmasını sağlar.

3. **Switch'in VMPS ile İletişimi**: Switch, cihazların MAC adreslerini VMPS sunucusuna iletir ve doğru VLAN'ı alır. büyük ve dinamik ağlarda bu yapılandırma, ağ yönetimini çok daha kolay ve verimli hale getirebilir.

## **Inter-VLAN Routing Nedir ve Neden Gereklidir?**

**Inter-VLAN Routing (IVR)**, farklı VLAN’lar arasında veri iletimi sağlamak için kullanılan bir tekniktir. Bir ağda farklı VLAN’lar oluşturulduğunda, bu VLAN'lar birbirlerinden izole edilir. Bu, aynı VLAN’daki cihazlar arasında iletişim sağlanabilirken, farklı VLAN’lardaki cihazlar arasında doğrudan iletişim sağlanamaz. İşte burada **Inter-VLAN Routing** devreye girer.

### Inter-VLAN Routing’in Gerekliliği

Bir ağda farklı VLAN’lar kullanıldığında, VLAN'lar birbirinden izole edilmiş olur. Örneğin, aşağıdaki iki VLAN’ı düşünün:

* **VLAN 10 (Sales)**: 192.168.10.0/24
* **VLAN 20 (HR)**: 192.168.20.0/24

Bu iki VLAN’daki cihazlar birbirleriyle **doğrudan iletişim kuramazlar** çünkü her VLAN, Layer 2 seviyesinde ayrı bir broadcast domain’i oluşturur. Yani, cihazlar **farklı VLAN’larda yer alıyorsa** onların birbiriyle veri alışverişi yapabilmesi için **yönlendirme yapılması** gerekir.

**Inter-VLAN Routing**, bu yönlendirme işlemini yaparak farklı VLAN’lardaki cihazlar arasında veri iletimi sağlar. Bu işlem, genellikle bir **Layer 3 cihaz (router veya Layer 3 switch)** tarafından gerçekleştirilir.

## **Router-on-a-Stick ile Inter-VLAN Routing Yapılandırması**

**Router-on-a-Stick** (RoS), tek bir fiziksel router portu üzerinden birden fazla VLAN’a yönlendirme yapılmasını sağlayan bir tekniktir. Bu, router'ın bir **trunk bağlantısı** üzerinden tüm VLAN’lar arasında yönlendirme yapmasına olanak tanır. Bu yapılandırma, küçük ağlarda maliyet etkin bir çözüm sunar.

### **Router-on-a-Stick Yapılandırması Adımları**

#### **1. Fiziksel Yapının Oluşturulması**

* **Switch’te VLAN’ları oluşturun**.
* **Router’ı trunk portu olarak yapılandırın**.

Örneğin, Switch’te aşağıdaki VLAN’ları oluşturalım:

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config)# vlan 20
Switch(config-vlan)# name HR
```

#### **2. Router’ın Trunk Portu ile Yapılandırılması**

Router’a trunk portu olarak kullanılacak bir sub-interface oluşturulmalıdır. Bu port üzerinden farklı VLAN’lara yönlendirme yapılacaktır. Aşağıdaki adımlar Router üzerinde gerçekleştirilir:

* Router üzerinde **sub-interface** oluşturulmalıdır. Bu sub-interface’ler, her VLAN’a ait IP adresi ve ağ maskesini alacaktır.

```bash
Router(config)# interface gigabitEthernet 0/0.10
Router(config-if)# encapsulation dot1Q 10
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown

Router(config)# interface gigabitEthernet 0/0.20
Router(config-if)# encapsulation dot1Q 20
Router(config-if)# ip address 192.168.20.1 255.255.255.0
Router(config-if)# no shutdown
```

Bu örnekte:

* **GigabitEthernet 0/0.10**: VLAN 10 için sub-interface.
* **GigabitEthernet 0/0.20**: VLAN 20 için sub-interface.
* **Encapsulation dot1Q**: Bu komut, 802.1Q etiketleme protokolünü etkinleştirir, bu sayede trunk bağlantısı üzerinden VLAN bilgisi taşınır.

#### **3. Switch Portlarını VLAN’lara Atamak**

Şimdi, switch portlarını doğru VLAN’lara atamalıyız. Bu işlem, cihazların doğru VLAN’lara ait olması için yapılır.

```bash
Switch(config)# interface range fa0/1 - 10
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10

Switch(config)# interface range fa0/11 - 20
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
```

* Port **fa0/1 - 10** VLAN 10’a,
* Port **fa0/11 - 20** VLAN 20’ye atanır.

#### **4. Trunk Bağlantısı Kurulması**

Router ile switch arasında trunk bağlantısı kurulur. Bu bağlantı, router’ın VLAN’lar arasında yönlendirme yapabilmesini sağlar.

```bash
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q
```

* **switchport mode trunk**: Bu komut trunk portu oluşturur.
* **switchport trunk encapsulation dot1q**: VLAN etiketleme protokolünü belirtir.

#### **5. Router ve Switch Yönlendirme Testi**

Artık yönlendirme işlemi tamamlanmıştır. Bu yapılandırmayı test etmek için her iki VLAN’dan cihazları kullanarak **ping** testleri yapılabilir.

Örneğin, **VLAN 10’daki PC**:

* IP: 192.168.10.2
* Gateway: 192.168.10.1 (Router sub-interface)

**VLAN 20’deki PC**:

* IP: 192.168.20.2
* Gateway: 192.168.20.1 (Router sub-interface)

Her iki PC’den birbirlerine **ping** atılabilir. Eğer her şey doğru yapılandırılmışsa, ping başarılı olacaktır.

---

### Router-on-a-Stick Yapılandırmasının Avantajları ve Dezavantajları

#### **Avantajlar:**

* **Maliyet Etkin**: Tek bir router portu üzerinden birden fazla VLAN’a yönlendirme yapılabilir.
* **Basit Yapılandırma**: Router'a yalnızca bir trunk bağlantısı yapılır, bu da yapılandırmayı basit ve hızlı hale getirir.

#### **Dezavantajlar:**

* **Performans Sorunları**: Router'ın tek bir port üzerinden tüm VLAN'lara yönlendirme yapması, ağ trafiğini bir noktada yoğunlaştırabilir.
* **Scalability (Ölçeklenebilirlik)**: Çok büyük ağlar için daha fazla router portuna ve daha gelişmiş yönlendirme yapılarına ihtiyaç duyulabilir.


## **Layer 3 Switch ile Inter-VLAN Routing Yapılandırması**

**Layer 3 switch** (veya multilayer switch), hem Layer 2 (Data Link) hem de Layer 3 (Network) işlevlerini yerine getirebilen bir cihazdır. Bu tür switch'ler, VLAN’lar arasında yönlendirme yapmak için geleneksel router’ların yerini alabilir. **Inter-VLAN Routing** işlemi, Layer 3 switch'lerde, **router-on-a-stick** gibi yapılandırmalar kullanmadan, doğrudan switch üzerinde yapılabilir. Bu, ağ yönetimini daha verimli hale getirebilir.

###  **Layer 3 Switch ve Inter-VLAN Routing**

Bir Layer 3 switch, her bir VLAN için bir **virtual interface (SVI - Switched Virtual Interface)** oluşturur. Bu sanal arayüzler, her VLAN için birer yönlendirme noktası (gateway) sağlar. Bu sayede, VLAN’lar arasındaki iletişim doğrudan switch tarafından yönlendirilir.

Layer 3 switch’lerde Inter-VLAN Routing, aşağıdaki adımlarla yapılır:

1. **SVI Oluşturulması**: Her VLAN için sanal arayüzler (SVI) oluşturulur ve her birine IP adresi atanır. Bu sanal arayüzler, VLAN’lar arasındaki yönlendirmeyi sağlar.
2. **Routing Protokollerinin Etkinleştirilmesi**: Switch, yönlendirme protokollerini (statik, RIP, OSPF, EIGRP vb.) etkinleştirebilir.
3. **Trunk Bağlantısı**: Farklı VLAN’lar arasındaki veri iletimi için trunk bağlantısı yapılandırılır.



###  **Layer 3 Switch ile Inter-VLAN Routing Yapılandırma Adımları**

#### **1. VLAN’ları ve IP Adreslerini Yapılandırma**

İlk olarak, switch üzerinde gerekli VLAN’ları oluşturup, her bir VLAN için bir IP adresi atanır. Bu IP adresleri, VLAN’lar arasındaki yönlendirme işlemleri için **gateway** olarak kullanılacaktır.

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config)# vlan 20
Switch(config-vlan)# name HR
```

Yukarıdaki komutlarla **VLAN 10** ve **VLAN 20** oluşturuldu.

Ardından, her VLAN için bir sanal arayüz (SVI) oluşturulup, IP adresi atanır:

```bash
Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown

Switch(config)# interface vlan 20
Switch(config-if)# ip address 192.168.20.1 255.255.255.0
Switch(config-if)# no shutdown
```

Bu komutlarla:

* **VLAN 10** için **192.168.10.1/24** IP adresi atanmış oldu.
* **VLAN 20** için **192.168.20.1/24** IP adresi atanmış oldu.

#### **2. Routing’in Etkinleştirilmesi**

Layer 3 switch’ler, yönlendirme yeteneklerine sahip olduklarından, yönlendirmeyi etkinleştirmek için `ip routing` komutunu kullanmak gerekir. Bu komut, switch’i yönlendirici gibi çalışacak şekilde yapılandırır.

```bash
Switch(config)# ip routing
```

Bu komut, switch üzerinde **Layer 3 routing** işlevini etkinleştirir.

#### **3. Trunk Bağlantısı Yapılandırılması**

Eğer VLAN’lar arasında veri iletimi yapılacaksa, switch üzerinde trunk bağlantıları yapılmalıdır. Trunk bağlantıları, birden fazla VLAN’ın aynı fiziksel port üzerinden iletilmesine olanak tanır.

```bash
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# no shutdown
```

Bu komutlarla, **GigabitEthernet 0/1** portu trunk portu olarak yapılandırılır. Bu port üzerinden **VLAN 10** ve **VLAN 20**'ye ait trafik iletilebilir.

#### **4. Test ve Yönlendirme Kontrolü**

Son olarak, VLAN'lar arasında veri iletiminin düzgün çalışıp çalışmadığını test etmek gerekir. **VLAN 10**'daki bir cihaz, **VLAN 20**'deki bir cihaza ping atabilir.

Örneğin:

* **VLAN 10 PC**: IP: 192.168.10.2, Gateway: 192.168.10.1
* **VLAN 20 PC**: IP: 192.168.20.2, Gateway: 192.168.20.1

Eğer yönlendirme doğru yapılandırılmışsa, **VLAN 10’daki PC**, **VLAN 20’deki PC**'yi **ping** edebilecektir.

## **Private VLAN (PVLAN) Nedir?**

PVLAN, temelde bir ana VLAN (Primary VLAN) ve bu VLAN'a bağlı olan izole edilmiş (Secondary VLAN) alt VLAN'lar arasında bir yapı kurar. PVLAN'lar, Layer 2'de ağ trafiğini kontrol etmeye yönelik bir çözüm sunar. PVLAN'lar, cihazların aynı VLAN içinde yer almasına rağmen, yalnızca belirli cihazlarla iletişim kurmasını sağlar. Bu özellik, özellikle güvenlik amacıyla kullanılan bir yapılandırmadır.

**Anahtar Kavramlar:**

* **Primary VLAN**: PVLAN yapısında ana VLAN'dır ve tüm trafik bu VLAN üzerinde taşınır.
* **Secondary VLAN**: Private VLAN’ın alt VLAN’larıdır. Bu VLAN’lar, birbiriyle iletişim kurmasına engel olacak şekilde yapılandırılabilir.

### PVLAN Türleri

PVLAN'lar, genellikle 3 türde sınıflandırılır:

1. **Isolated PVLAN**

   * Isolated PVLAN, bu türdeki cihazlar yalnızca **Primary VLAN**’a trafik gönderir ve yalnızca bu VLAN üzerinden gelen trafiği alır.
   * Bu yapıda, aynı **Secondary VLAN**'da yer alan cihazlar birbirleriyle doğrudan iletişim kuramaz. Sadece, **Primary VLAN** üzerinden iletişim sağlanabilir.
   * **Güvenlik** açısından, çok sıkı izolasyon gerektiren durumlarda kullanılır. Örneğin, misafir cihazlar veya güvenliğin yüksek olması gereken ağlarda.

2. **Community PVLAN**

   * Community PVLAN, aynı **Secondary VLAN**’da bulunan cihazların birbirleriyle iletişim kurmasına izin verir, ancak diğer **Secondary VLAN**'lar ile iletişim kurmalarına engel olur.
   * Bu tür, cihazların belirli gruplar içinde iletişim kurmasına olanak tanırken, diğer gruplardan izole eder.
   * **Community PVLAN**'lar, ağdaki bazı cihazları aynı VLAN içinde tutarken, güvenliği artırmak için başka cihazlarla iletişim kurmalarını engellemeye yönelik kullanılır. Örneğin, farklı departmanlardaki cihazlar birbiriyle iletişim kurabilirken, diğer departmanlarla iletişim kuramayabilir.

3. **Promiscuous PVLAN**

   * Promiscuous PVLAN, bu türdeki cihazlar **Primary VLAN** içindeki tüm cihazlarla iletişim kurabilir.
   * Bu tür cihazlar, hem **Isolated** hem de **Community** PVLAN’larındaki cihazlarla iletişim kurabilir. Promiscuous cihazlar, genellikle ağ geçidi, yönlendirici veya DHCP sunucusu gibi merkezi hizmetler sağlayan cihazlar olur.
   * **Promiscuous** cihazlar, ağın tüm trafiğini yönlendirebilecek veya kontrol edebilecek yeteneklere sahiptir.

### **Private VLAN Yapılandırması**

PVLAN yapılandırması, genellikle bir **Layer 2 switch** üzerinde yapılır. Aşağıda, bir Cisco switch üzerinde PVLAN yapılandırmasına ilişkin adımlar yer almaktadır.

#### 1. **PVLAN'lar için VLAN Yapılandırması**

Öncelikle, **Primary VLAN** ve **Secondary VLAN**'lar oluşturulur.

```plaintext
Switch(config)# vlan 10
Switch(config-vlan)# name Primary_VLAN
Switch(config-vlan)# exit

Switch(config)# vlan 100
Switch(config-vlan)# name Community_VLAN
Switch(config-vlan)# exit

Switch(config)# vlan 200
Switch(config-vlan)# name Isolated_VLAN
Switch(config-vlan)# exit
```

Bu adımda, **Primary VLAN (10)**, **Community VLAN (100)** ve **Isolated VLAN (200)** oluşturulmuş olur.

#### 2. **PVLAN'lar Arasındaki İlişkiyi Tanımlama**

**Isolated** ve **Community** VLAN’lar için ilişkiler yapılandırılır. Bu tür VLAN’ların, birbirleriyle ve Primary VLAN’la olan bağlantıları belirlenir.

```plaintext
Switch(config)# vlan 10
Switch(config-vlan)# private-vlan primary
Switch(config-vlan)# private-vlan association 100, 200
Switch(config-vlan)# exit
```

Bu adımda, **Primary VLAN (10)** ile **Community VLAN (100)** ve **Isolated VLAN (200)** ilişkilendirilmiştir.

#### 3. **Port Türü Belirleme**

PVLAN’larda, portlar üç farklı türde olabilir:

* **Promiscuous Port**: Tüm VLAN'larla iletişim kurabilir.
* **Isolated Port**: Diğer cihazlarla iletişim kuramaz, yalnızca **Promiscuous Port**'larla iletişim kurabilir.
* **Community Port**: Aynı **Community VLAN**'daki diğer cihazlarla iletişim kurabilir, ancak farklı **Community VLAN**'lardaki cihazlarla iletişim kuramaz.

**Promiscuous port** için örnek:

```plaintext
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport mode private-vlan promiscuous
Switch(config-if)# switchport private-vlan mapping 10
Switch(config-if)# exit
```

**Community port** için örnek:

```plaintext
Switch(config)# interface gigabitethernet 0/2
Switch(config-if)# switchport mode private-vlan community
Switch(config-if)# switchport private-vlan mapping 100
Switch(config-if)# exit
```

**Isolated port** için örnek:

```plaintext
Switch(config)# interface gigabitethernet 0/3
Switch(config-if)# switchport mode private-vlan isolated
Switch(config-if)# switchport private-vlan mapping 200
Switch(config-if)# exit
```

#### 4. **Portları VLAN’a Atama**

Portları, yapılandırılan **Primary** ve **Secondary VLAN**'lara atamak gerekir.

```plaintext
Switch(config)# interface range gigabitethernet 0/4 - 6
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit
```
### **Senaryo:**

* **Ana VLAN (Primary VLAN)**: 100
* **Community VLAN (Misafir VLAN)**: 101
* **Isolated VLAN (İzolasyon VLAN)**: 102
* **Promiscuous Port (İnternet erişimi sağlayacak port)**: 0/1
* **Community Port (Misafir cihazlarının bağlı olduğu portlar)**: 0/2, 0/3
* **Isolated Port (Misafir cihazlarının bağlantı noktası)**: 0/4

Misafir cihazları sadece **Primary VLAN** üzerinden iletişim kurabilir, ancak birbirleriyle doğrudan iletişim kuramayacaklardır. **Promiscuous port** üzerinden ise **İnternet** gibi dış hizmetlere erişimleri olacak.

### **1. VLAN’lar Oluşturuluyor:**

İlk adımda, **Primary VLAN**, **Community VLAN** ve **Isolated VLAN** oluşturulur.

```plaintext
Switch(config)# vlan 100
Switch(config-vlan)# name Primary_VLAN
Switch(config-vlan)# exit

Switch(config)# vlan 101
Switch(config-vlan)# name Community_VLAN
Switch(config-vlan)# exit

Switch(config)# vlan 102
Switch(config-vlan)# name Isolated_VLAN
Switch(config-vlan)# exit
```

Bu adımda:

* **Primary VLAN (100)**: Ana VLAN’dır, bütün trafiği taşıyan VLAN’dır.
* **Community VLAN (101)**: Misafir cihazlarının bağlı olduğu VLAN’dır.
* **Isolated VLAN (102)**: Misafir cihazlarının birbirleriyle iletişim kuramaması için kullanılan VLAN’dır.

---

### **2. Private VLAN Yapılandırması:**

**Primary VLAN**'ın altında, **Community VLAN** ve **Isolated VLAN**'ı ilişkilendiriyoruz.

```plaintext
Switch(config)# vlan 100
Switch(config-vlan)# private-vlan primary
Switch(config-vlan)# private-vlan association 101, 102
Switch(config-vlan)# exit
```

Burada:

* **Primary VLAN (100)** ile **Community VLAN (101)** ve **Isolated VLAN (102)** birbirine bağlanmıştır.

---

### **3. Port Türlerini Belirleme:**

#### **Promiscuous Port (İnternet Erişimi) Yapılandırması:**

Bu port **Primary VLAN**’daki cihazlarla ve **Community VLAN** ile iletişim kurabilecek cihaz olarak yapılandırılır.

```plaintext
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport mode private-vlan promiscuous
Switch(config-if)# switchport private-vlan mapping 100
Switch(config-if)# exit
```

Bu adımda:

* **GigabitEthernet 0/1** portu **Promiscuous port** olarak belirlenmiştir ve **Primary VLAN**’a bağlıdır.

---

#### **Community Port (Misafir Cihazları) Yapılandırması:**

Bu portlar, **Community VLAN**'daki cihazlarla iletişim kurabilen cihazlar için yapılandırılır.

```plaintext
Switch(config)# interface range gigabitethernet 0/2 - 3
Switch(config-if-range)# switchport mode private-vlan community
Switch(config-if-range)# switchport private-vlan mapping 101
Switch(config-if-range)# exit
```

Bu adımda:

* **GigabitEthernet 0/2** ve **0/3** portları **Community port** olarak belirlenmiştir.

---

#### **Isolated Port (Misafir Cihazları) Yapılandırması:**

Bu portlar, **Isolated VLAN**'daki cihazlarla iletişim kuramayan cihazlar için yapılandırılır.

```plaintext
Switch(config)# interface gigabitethernet 0/4
Switch(config-if)# switchport mode private-vlan isolated
Switch(config-if)# switchport private-vlan mapping 102
Switch(config-if)# exit
```

Bu adımda:

* **GigabitEthernet 0/4** portu **Isolated port** olarak belirlenmiştir ve **Isolated VLAN**’a bağlıdır.

---

### **4. Portlara VLAN Atamaları Yapmak:**

Her port, uygun VLAN'a atanmalıdır. **Community** portlarına **Community VLAN (101)**, **Isolated** portlarına ise **Isolated VLAN (102)** atanır.

```plaintext
Switch(config)# interface range gigabitethernet 0/2 - 3
Switch(config-if-range)# switchport access vlan 101
Switch(config-if-range)# exit

Switch(config)# interface gigabitethernet 0/4
Switch(config-if)# switchport access vlan 102
Switch(config-if)# exit
```

Bu adımda:

* **GigabitEthernet 0/2 ve 0/3** portları **Community VLAN (101)**’a atanmıştır.
* **GigabitEthernet 0/4** portu **Isolated VLAN (102)**’a atanmıştır.

---

### **5. Test ve Doğrulama:**

Yapılandırmanın doğruluğunu test etmek için **show vlan brief** komutuyla VLAN yapılandırmasını kontrol edebiliriz:

```plaintext
Switch# show vlan brief
```

Bu komut, oluşturulan VLAN’ları ve hangi portların hangi VLAN’lara ait olduğunu gösterir.

Ayrıca, her portun doğru şekilde yapılandırıldığını doğrulamak için **show interfaces switchport** komutunu kullanabiliriz:

```plaintext
Switch# show interfaces switchport
```

## **VLAN Sorun Giderme Yöntemleri ve Komutları**

VLAN yapılandırması, ağdaki cihazların mantıksal olarak gruplandırılmasını sağlar, ancak bazen ağda iletişim sorunları yaşanabilir. Bu tür sorunlar genellikle yanlış VLAN yapılandırmaları, erişim hataları, trunk bağlantısı problemleri, VLAN etiketleme sorunları veya port konfigürasyon hatalarından kaynaklanır. VLAN sorunlarını gidermek için belirli komutlar ve izleme yöntemleri kullanılarak tespit edilip çözüm sağlanabilir.

### **1. VLAN Yapılandırmasını Doğrulama**

VLAN ile ilgili en temel adım, VLAN’ların doğru şekilde yapılandırıldığını doğrulamaktır. Switch üzerinde VLAN yapılandırmasını doğrulamak için aşağıdaki komutlar kullanılır:

#### **VLAN’ları Görüntüleme:**

VLAN'ların doğru şekilde oluşturulup oluşturulmadığını görmek için aşağıdaki komut kullanılır:

```bash
Switch# show vlan brief
```

Bu komut, switch'teki tüm VLAN'ların bir listesini gösterir ve her bir VLAN için hangi portların atandığını belirtir. Bu komut ile eksik veya yanlış VLAN yapılandırmalarını tespit edebilirsiniz.

#### **VLAN Bilgilerini Detaylı Görüntüleme:**

Daha ayrıntılı bilgi için şu komut kullanılabilir:

```bash
Switch# show vlan id <VLAN_ID>
```

Bu komut, belirli bir VLAN hakkında detaylı bilgileri verir, örneğin hangi portların o VLAN'a atandığını.

### **2. Port Yapılandırmalarını Kontrol Etme**

Bir VLAN'daki iletişim sorununun nedeni, port yapılandırmasındaki hatalar olabilir. Switch portlarının doğru VLAN'a atanıp atanmadığını kontrol etmek için aşağıdaki komut kullanılır:

#### **Port Üzerindeki VLAN Bilgisi:**

```bash
Switch# show interface switchport
```

Bu komut, belirli bir portun bağlı olduğu VLAN’ı gösterir. Portun **Access** ya da **Trunk** olarak yapılandırıldığını ve doğru VLAN’a atanıp atanmadığını doğrulamaya yardımcı olur.

#### **Port Durumunu Kontrol Etme:**

Eğer portlar arasında iletişim yoksa, portların aktif olup olmadığını görmek için:

```bash
Switch# show interface status
```

Bu komut, portların durumunu (bağlantı durumu, VLAN, hız, vb.) gösterir. Portların **err-disabled** duruma düşüp düşmediği burada kontrol edilebilir.

### **3. Trunk Portlarını Kontrol Etme**

VLAN'lar arasında veri iletimi genellikle trunk portları üzerinden yapılır. Trunk bağlantısında bir problem varsa, VLAN'lar arası iletişim engellenebilir.

#### **Trunk Durumunu Görüntüleme:**

Trunk bağlantılarının doğru yapılandırıldığını ve hangi VLAN'ların geçişine izin verildiğini görmek için:

```bash
Switch# show interfaces trunk
```

Bu komut, trunk portları hakkında detaylı bilgi verir. Trunk portlarının **802.1Q** etiketi ile çalışıp çalışmadığını, hangi VLAN'ların aktarıldığını kontrol edebilirsiniz.

#### **Trunk Port Yapılandırmasını Kontrol Etme:**

Trunk portlarının doğru yapılandırıldığından emin olmak için:

```bash
Switch# show running-config interface <interface_name>
```

Bu komut, belirtilen interface'in yapılandırmasını gösterir ve trunk yapılandırmalarının doğruluğunu kontrol etmenize olanak tanır.

### **4. VLAN Etiketleme ve DTP Sorunlarını Gidermek**

Trunk portları, VLAN'ları **802.1Q** etiketi kullanarak iletir. Trunk portlarında VLAN etiketleme hataları, iletişimin engellenmesine yol açabilir.

#### **VLAN Etiketleme Durumunu Görüntüleme:**

Trunk portlarında etiketleme sorunlarını görmek için:

```bash
Switch# show interfaces trunk
```

Bu komut, trunk portları üzerindeki etiketli VLAN’ların doğru şekilde aktarıldığını ve **DTP** (Dynamic Trunking Protocol) protokolünün doğru yapılandırıldığını kontrol etmenizi sağlar.

#### **DTP (Dynamic Trunking Protocol) Durumunu Kontrol Etme:**

DTP protokolünün doğru çalışıp çalışmadığını görmek için:

```bash
Switch# show dtp interface <interface_name>
```

Bu komut, DTP'nin doğru şekilde yapılandırılıp yapılandırılmadığını kontrol eder.

### **5. VLAN Hopping ve Diğer Güvenlik Sorunlarını Kontrol Etme**

VLAN hopping, bir saldırganın VLAN’lar arasında geçiş yapmasına olanak tanıyabilir. Bu durumu engellemek için, trunk portlarında sadece gerekli VLAN’ların iletilmesi sağlanmalıdır.

#### **VLAN Hopping’i Engelleme:**

VLAN hopping’i engellemek için aşağıdaki komut kullanılır:

```bash
Switch(config-if)# switchport trunk allowed vlan <vlan_list>
```

Bu komut, sadece belirtilen VLAN’ların trunk portu üzerinden geçmesine izin verir. Ayrıca, **DTP** protokolünü kapatmak da VLAN hopping’i engellemeye yardımcı olur:

```bash
Switch(config-if)# no switchport mode dynamic desirable
Switch(config-if)# switchport mode trunk
```

### **6. VLAN ve IP Adresleme Sorunlarını Gidermek**

VLAN’lar arası iletişim genellikle bir Layer 3 cihaz (router veya Layer 3 switch) ile sağlanır. Eğer inter-VLAN routing sorunu varsa, yönlendirici veya Layer 3 switch yapılandırması kontrol edilmelidir.

#### **Router ve Layer 3 Switch'te VLAN Routing Durumu:**

VLAN’lar arasındaki yönlendirme için aşağıdaki komutla cihazın doğru şekilde yapılandırıldığını kontrol edebilirsiniz:

```bash
Router# show ip route
```

Bu komut, cihazın yönlendirme tablosunu gösterir ve VLAN’lar arası yönlendirme ile ilgili bir problem olup olmadığını belirlemenizi sağlar.

### **7. VLAN'lar Arası İletişim Sorunları**

VLAN'lar arası iletişimde bir problem varsa, yönlendirici veya Layer 3 switch üzerinde yapılandırma hataları veya yanlış yönlendirme olabilir. Bu tür sorunları gidermek için aşağıdaki komutlar kullanılabilir:

#### **VLAN IP Yapılandırmalarını Kontrol Etme:**

VLAN IP yapılandırmasının doğru olduğundan emin olmak için:

```bash
Router# show ip interface brief
```

Bu komut, VLAN'lar için yapılandırılmış IP adreslerini ve bağlantı durumlarını gösterir. IP yapılandırmasında hata yapmadığınızdan emin olabilirsiniz.

#### **VLAN İstemcisi IP Konfigürasyonunu Kontrol Etme:**

Ayrıca, istemcilerin doğru IP adresine ve ağ geçidine sahip olup olmadığını kontrol etmek için aşağıdaki komutu kullanabilirsiniz:

```bash
PC> ipconfig
```

Bu komut, istemcinin IP yapılandırmasını ve ağ geçidini gösterir.



## **IP Helper Address Nedir?**

Bir VLAN içindeki istemciler genellikle DHCP sunucusundan IP adresi almak ister. Ancak DHCP, **broadcast (yayın)** temelli çalışan bir protokoldür ve **router (yönlendirici)** broadcast paketlerini varsayılan olarak iletmez. Eğer DHCP sunucusu farklı bir VLAN veya ağda bulunuyorsa, bu yayınlar hedefe ulaşamaz.
Bu sorunu çözmek için router üzerinde, yayın paketlerinin belirli bir IP adresine **yönlendirilmesini sağlayan** bir komut kullanılır: `ip helper-address`.

**IP Helper Address**, yönlendiricinin aldığı broadcast (UDP) paketlerini **unicast** olarak belirtilen hedef IP'ye iletmesini sağlar.


### **DHCP Relay (Yönlendirme) Yapılandırması**

#### **Senaryo:**

* VLAN 10: 192.168.10.0/24
* DHCP Sunucusu: 192.168.100.10 (farklı bir VLAN’da veya merkez ağda)
* Router: VLAN 10’u yönlendiren cihaz

#### **Amaç:**

VLAN 10’daki istemcilerin, DHCP sunucusundan IP adresi alabilmesini sağlamak.

---

### **Yapılandırma Adımları (Cisco CLI ile)**

**1. Router Arayüzünde IP Helper Address Tanımlanması:**

```bash
R1(config)# interface GigabitEthernet0/0.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 192.168.10.1 255.255.255.0
R1(config-subif)# ip helper-address 192.168.100.10
```

* `ip helper-address 192.168.100.10`: VLAN 10’dan gelen DHCP isteklerinin, 192.168.100.10 IP’li DHCP sunucusuna iletilmesini sağlar.

---

### **İlgili DHCP Sunucusunun Yapılandırması (Opsiyonel)**

Eğer Cisco router DHCP sunucu olarak da kullanılacaksa:

```bash
R1(config)# ip dhcp pool VLAN10
R1(dhcp-config)# network 192.168.10.0 255.255.255.0
R1(dhcp-config)# default-router 192.168.10.1
```

---

### **Önemli Noktalar:**

* Router üzerindeki VLAN arabirimi ya da alt arayüz, VLAN’ın gateway’i olmalıdır.
* `ip helper-address` komutu yalnızca broadcast olan DHCPDISCOVER gibi mesajların yönlendirilmesini sağlar.
* DHCP sunucusunun yönlendiricinin ilettiği paketlere cevap verebilmesi için, sunucunun istemcinin VLAN ağına rota bilmesi gerekir (yönlendirme yapılandırması yapılmalıdır).


## **VLAN’larda QoS (Quality of Service) Yapılandırması**

**Quality of Service (QoS)**, ağ trafiğine öncelik vererek ses, video, veri gibi farklı türdeki paketlerin istenen performans kriterlerine göre (gecikme, jitter, kayıp, bant genişliği) iletilmesini sağlayan mekanizmalardır. VLAN ortamlarında QoS yapılandırması, trafiğin sınıflandırılmasına, etiketlenmesine, işlenmesine ve kuyruklanmasına olanak tanır. Bu, özellikle ses (VoIP), video konferans, gerçek zamanlı uygulamalar veya kritik iş uygulamalarında oldukça önemlidir.

### VLAN ve QoS Entegrasyonu: Temel Prensipler

VLAN'larda QoS uygulanmasının temel amacı, ağ üzerindeki farklı trafiğin birbirinden ayrılması ve her bir trafiğe uygun hizmet kalitesi sunulmasıdır. VLAN segmentasyonu, farklı trafik türlerini ayrı sanal ağlara ayırmak için kullanılırken, QoS bu segmentlere hizmet düzeyi uygulamak için kullanılır.

Örneğin:

* VLAN 10 → VoIP telefonlar
* VLAN 20 → Video konferans cihazları
* VLAN 30 → Bilgisayarlar (standart veri trafiği)

Her VLAN’daki trafiğe özel QoS politikaları uygulanarak ağ performansı optimize edilir.

## VLAN Tabanlı QoS Bileşenleri

QoS mekanizmaları aşağıdaki dört temel bileşeni içerir:

1. **Sınıflandırma (Classification):**
   Gelen trafiğin türüne göre sınıflandırılması. Bu işlem IP adresi, protokol, VLAN ID, MAC adresi, port numarası gibi kriterlere göre yapılabilir.

2. **İşaretleme (Marking):**
   Trafik sınıfına uygun şekilde işaretlenir. Ethernet çerçevesindeki **802.1Q Tag** içindeki **Class of Service (CoS)** alanı kullanılır. L3 seviyesinde ise IP başlığındaki **DSCP (Differentiated Services Code Point)** alanı kullanılır.

3. **Politikalar (Policing & Shaping):**
   Trafiğin bant genişliği sınırlandırılması veya belirli bir hız üzerinde gelen paketlerin düşürülmesi (policing), ya da geciktirilerek sıraya alınması (shaping) işlemleri.

4. **Kuyruklama (Queuing):**
   Trafiğin önceliğine göre kuyruğa alınması. Örneğin ses trafiği düşük gecikme için yüksek öncelik kuyruğuna alınır.

## Layer 2'de QoS (802.1Q CoS Kullanımı)

IEEE 802.1Q VLAN etiketi içinde 3 bitlik bir **CoS (Class of Service)** alanı bulunur. Bu alan, Layer 2 QoS işaretlemesi için kullanılır ve 0–7 arasında değer alabilir:

| CoS Değeri | Öncelik   | Trafik Türü               |
| ---------- | --------- | ------------------------- |
| 0          | En Düşük  | Arka plan verileri        |
| 1          | Düşük     | Veri                      |
| 3          | Orta      | Video akışı               |
| 5          | Yüksek    | Ses (VoIP)                |
| 7          | En Yüksek | Yönetim (network control) |

Bu CoS değerleri **trunk portlar** üzerinden VLAN’lar arasında taşınan trafiğe QoS politikalarının uygulanmasını sağlar.

## VLAN QoS İşaretleme ve Sınıflandırma (Cisco Switch Örneği)

Cisco switch’lerde VLAN trafiğine QoS uygulanırken genellikle **MLS QoS** (Multi-Layer Switching QoS) veya **Modular QoS CLI (MQC)** kullanılır.

### 1. QoS’u Aktif Etme:

```bash
Switch(config)# mls qos
```

### 2. Sınıflandırma İçin ACL Tanımlama:

```bash
Switch(config)# access-list 101 permit ip 192.168.10.0 0.0.0.255 any
```

### 3. Class-Map Tanımlama:

```bash
Switch(config)# class-map match-any VOICE
Switch(config-cmap)# match access-group 101
```

### 4. Policy-Map ile İşlem Belirleme:

```bash
Switch(config)# policy-map VLAN10-QOS
Switch(config-pmap)# class VOICE
Switch(config-pmap-c)# set dscp ef
```

`ef (Expedited Forwarding)` → VoIP gibi düşük gecikme gerektiren trafik için kullanılır.

### 5. QoS Politikasını VLAN Arayüzüne Uygulama:

```bash
Switch(config)# interface vlan 10
Switch(config-if)# service-policy input VLAN10-QOS
```

## Layer 3 QoS (DSCP Kullanımı)

Router gibi Layer 3 cihazlarda VLAN trafiğine DSCP (Differentiated Services Code Point) etiketiyle QoS uygulanır.

```bash
Router(config)# access-list 101 permit ip any any dscp default
Router(config)# class-map match-all NORMAL
Router(config-cmap)# match access-group 101
Router(config)# policy-map PRIORITY_POLICY
Router(config-pmap)# class NORMAL
Router(config-pmap-c)# set dscp af21
```

## Ses VLAN'larında QoS (Auto QoS)

Cisco, IP telefonlar için özel bir çözüm sunar: **Auto QoS**

```bash
Switch(config-if)# mls qos trust device cisco-phone
Switch(config-if)# mls qos trust cos
```

Bu komutlar, IP telefon tarafından iletilen CoS değerlerini otomatik olarak kabul eder ve VLAN 802.1Q etiketleme ile iletir.



### Uçtan Uca QoS ve VLAN

VLAN içinde QoS yapılandırması yapmak, trafiği uçtan uca (end-to-end) kaliteli iletmek için sadece bir adımdır. Gerçek QoS, trafiğin kaynak cihazdan hedef cihaza kadar tüm ağ boyunca işaretlenmesi, yönlendirilmesi ve önceliklendirilmesini içerir. VLAN bazlı QoS, bu sürecin başlangıcında segmentasyon ve sınıflandırma kolaylığı sağlar.



### Örnek Senaryo

* VLAN 10: VoIP Telefonlar
* VLAN 20: Video Konferans
* VLAN 30: Standart Veri

QoS yapılandırması:

* VLAN 10 trafiği → CoS 5, DSCP EF (en yüksek öncelik)
* VLAN 20 trafiği → CoS 3, DSCP AF41 (orta öncelik)
* VLAN 30 trafiği → CoS 0, DSCP default (en düşük)

Bu şekilde, VoIP ve video trafiği diğer veri trafiği tarafından engellenmeden iletilir.

### A. VLAN Tanımları ve Arayüz Atamaları

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name VoIP

Switch(config)# vlan 20
Switch(config-vlan)# name Video

Switch(config)# vlan 30
Switch(config-vlan)# name Data

Switch(config)# interface range fa0/1 - 2
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10

Switch(config)# interface range fa0/3 - 4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20

Switch(config)# interface range fa0/5 - 6
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 30
```

### B. QoS Aktif Edilmesi

```bash
Switch(config)# mls qos
```

### C. CoS Güven Ayarı (Trust CoS)

Her bir porta, bağlı cihazın CoS (Class of Service) değerine güvenmesi için ayar yapılır. Bu genellikle IP telefonlar için gereklidir.

```bash
Switch(config)# interface range fa0/1 - 2
Switch(config-if-range)# mls qos trust cos

Switch(config)# interface range fa0/3 - 4
Switch(config-if-range)# mls qos trust cos

Switch(config)# interface range fa0/5 - 6
Switch(config-if-range)# mls qos trust cos
```

> **Not:** Eğer IP telefonlar varsa, `mls qos trust device cisco-phone` komutu ile otomatik tanıma yapılabilir.

### D. QoS Sınıflandırma ve Politika Tanımlama

#### 1. Erişim Listeleri Oluşturma

```bash
Switch(config)# access-list 101 permit ip 192.168.10.0 0.0.0.255 any
Switch(config)# access-list 102 permit ip 192.168.20.0 0.0.0.255 any
Switch(config)# access-list 103 permit ip 192.168.30.0 0.0.0.255 any
```

#### 2. Class Map’ler Tanımlama

```bash
Switch(config)# class-map match-all VOICE
Switch(config-cmap)# match access-group 101

Switch(config)# class-map match-all VIDEO
Switch(config-cmap)# match access-group 102

Switch(config)# class-map match-all DATA
Switch(config-cmap)# match access-group 103
```

#### 3. Policy Map ile QoS Ayarları

```bash
Switch(config)# policy-map VLAN-QOS
Switch(config-pmap)# class VOICE
Switch(config-pmap-c)# set dscp ef
Switch(config-pmap-c)# set cos 5

Switch(config-pmap)# class VIDEO
Switch(config-pmap-c)# set dscp af41
Switch(config-pmap-c)# set cos 3

Switch(config-pmap)# class DATA
Switch(config-pmap-c)# set dscp default
Switch(config-pmap-c)# set cos 0
```

#### 4. QoS Politikasını VLAN Arayüzüne Uygulama

```bash
Switch(config)# interface vlan 10
Switch(config-if)# service-policy input VLAN-QOS

Switch(config)# interface vlan 20
Switch(config-if)# service-policy input VLAN-QOS

Switch(config)# interface vlan 30
Switch(config-if)# service-policy input VLAN-QOS
```

### Test ve Doğrulama Komutları

QoS yapılandırmasını kontrol etmek için:

```bash
Switch# show mls qos interface fa0/1
Switch# show policy-map interface vlan 10
Switch# show class-map
Switch# show policy-map
```

## Kaynakça

1. [Cisco – Understanding and Configuring VLAN Trunk Protocol (VTP)](https://www.cisco.com/c/en/us/support/docs/lan-switching/vtp/10558-21.html)
2. [RFC 5517 – Private VLANs: Scalable Security in a Multi-Client Environment](https://datatracker.ietf.org/doc/html/rfc5517)


