# ROUTER

## **Router**

Router (yönlendirici), bir bilgisayar ağında verileri farklı ağlar arasında yönlendirmekten sorumlu olan bir ağ cihazıdır. Router'lar, genellikle yerel ağları (LAN – Local Area Network) geniş alan ağlarına (WAN – Wide Area Network) bağlamak için kullanılır. Örneğin, evdeki yerel ağınız ile internet servis sağlayıcınız (ISP) arasında köprü kuran cihaz genellikle bir router’dır.

Router, ağ katmanında (Layer 3 - Network Layer) çalışır ve IP adreslerini temel alarak veri paketlerinin en uygun yoldan hedefe ulaşmasını sağlar. Gelen veriyi analiz eder, hedef IP adresine göre uygun çıkış arabirimini (interface) belirler ve veriyi oraya yönlendirir. Bu süreçte yönlendirme tabloları ve yönlendirme protokolleri (statik ya da dinamik) kullanılır.

Router’lar sadece veriyi yönlendirmekle kalmaz, aynı zamanda farklı ağ teknolojilerini bir araya getirebilir, trafik yönetimi yapabilir, güvenlik duvarı (firewall) işlevi görebilir ve NAT (Network Address Translation) gibi işlemleri de gerçekleştirebilir.


## **Router'ın Temel Görevleri ve İşlevleri**

Router’lar ağlar arasında veri iletimini sağlarken bir dizi temel görev ve işlevi yerine getirir:

### 1. **Yönlendirme (Routing)**

Router’ın birincil görevi, veri paketlerini bir ağdan başka bir ağa yönlendirmektir. Bu işlemi, yönlendirme tablosuna ve kullanılan yönlendirme protokolüne (örneğin RIP, OSPF, EIGRP, BGP) göre yapar. Paketlerin hedefe en kısa, en hızlı veya en güvenli yoldan ulaşması için en uygun yolu belirler.

### 2. **Ağlar Arası Köprü Görevi**

Router’lar farklı ağları birbirine bağlayabilir. Örneğin, bir ofis LAN’ı ile uzak bir şubedeki başka bir LAN router üzerinden birbirine bağlanabilir.

### 3. **Alt Ağların (Subnet’lerin) Ayrılması**

Router’lar, büyük ağları daha küçük alt ağlara (subnet) ayırarak verimliliği artırır. Bu sayede yayın trafiği sınırlandırılır ve ağ performansı iyileştirilir.

### 4. **NAT (Network Address Translation)**

Router’lar özel IP adreslerini (örneğin 192.168.x.x) genel IP adreslerine dönüştürerek internete çıkışı mümkün kılar. Bu sayede birden fazla cihaz, tek bir genel IP adresi üzerinden internete erişebilir.

### 5. **Paket Filtreleme ve Güvenlik**

Router’lar, gelen ve giden trafiği filtreleyebilir. Erişim kontrol listeleri (ACL) yardımıyla belirli IP adreslerinden gelen paketlerin geçmesine veya engellenmesine karar verilebilir. Bazı router’lar entegre güvenlik duvarlarıyla birlikte gelir.

### 6. **QoS (Quality of Service) Uygulamaları**

Bazı router’lar, trafiği önceliklendirme özelliğine sahiptir. Örneğin, ses ve video gibi gecikmeye duyarlı uygulamalara öncelik verilebilir.



## **Router Donanım Bileşenleri ve Bağlantı Noktaları**

Router’lar yalnızca yazılım değil, aynı zamanda belirli donanım bileşenlerine de sahiptir. Bu donanım unsurları router’ın çalışma kapasitesini ve işlevselliğini belirler.

### 1. **İşlemci (CPU)**

Router’ın beyni olarak çalışır. Tüm yönlendirme kararları ve kontrol düzeyi görevleri burada işlenir. Yönlendirme tablolarını güncelleme, paket filtreleme, NAT işlemleri gibi görevleri yerine getirir.

### 2. **RAM (Geçici Bellek)**

Router çalışırken aktif bilgileri burada saklar:

* Çalışma zamanındaki yönlendirme tabloları
* ARP tabloları
* İşletim sistemi süreçleri
  Router kapatıldığında RAM içeriği silinir.

### 3. **ROM (Salt Okunur Bellek)**

Router’ın açılış sırasında ihtiyaç duyduğu başlangıç yazılımı (bootstrap) burada bulunur. Ayrıca bazı temel tanılama yazılımları da bu bellekte yer alır.

### 4. **NVRAM (Non-Volatile RAM)**

Yönlendirici yapılandırma dosyası (startup-config) burada saklanır. Router yeniden başlatıldığında bu yapılandırma dosyasını okur ve uygulamaya başlar.

### 5. **Flash Bellek**

Router’ın işletim sistemi (örneğin Cisco IOS) bu bellekte saklanır. Flash bellek kalıcıdır ve router yeniden başlatıldığında içerik silinmez.

### 6. **Bağlantı Noktaları (Portlar / Arabirimler)**

Router’lar çeşitli fiziksel bağlantı noktalarına sahiptir:

* **Ethernet Portları (FastEthernet / GigabitEthernet):** Yerel ağ cihazları ile bağlantı kurmak için kullanılır. LAN bağlantıları bu portlar üzerinden yapılır.
* **Seri Portlar:** WAN bağlantılarında (örneğin, iki router arasında) kullanılır. Genellikle eski WAN bağlantılarında tercih edilir.
* **Konsol Portu:** Router’ın ilk yapılandırması ve doğrudan yönetimi için kullanılır. Bir terminal veya bilgisayar yardımıyla doğrudan router’a bağlanılır.
* **AUX (Yardımcı) Portu:** Genellikle uzaktan modem bağlantıları için kullanılır. Artık modern router’larda çok sık kullanılmaz.
* **USB Portları (bazı modellerde):** Konfigürasyon dosyaları, IOS güncellemeleri veya yedeklemeler için kullanılabilir.



## **Router Çalışma Prensibi: Paket Yönlendirme Süreci**

Router’ın temel işlevi olan **paket yönlendirme** işlemi, ağ katmanında (Layer 3 - Network Layer) gerçekleşir. Bu süreç, bir veri paketinin bir ağdan başka bir ağa doğru en uygun yol üzerinden iletilmesini kapsar. Paket yönlendirme süreci aşağıdaki adımlarla gerçekleşir:

### 1. **Paketin Gelişi ve Alınması**

Bir router’a bağlı cihaz ya da başka bir router, hedef IP adresine sahip bir veri paketi gönderdiğinde, bu paket router’a gelir. Router, paketin **başlık (header)** kısmında bulunan hedef IP adresini inceler.

### 2. **Routing Table (Yönlendirme Tablosu) Kontrolü**

Router, kendi **yönlendirme tablosuna (routing table)** bakarak paketin hedef IP adresine hangi ağ arabirimi (interface) veya hangi sonraki yönlendirici (next-hop) üzerinden ulaşacağını belirler. 
Routing table verileri statik olarak elle tanımlanabilir veya dinamik yönlendirme protokolleri (RIP, OSPF, EIGRP gibi) aracılığıyla otomatik olarak öğrenilebilir.

### 3. **En Uygun Yolun Seçilmesi**

Router, hedefe ulaşmak için birden fazla yol biliyorsa, yönlendirme protokolünün kullandığı **metrik değeri** (örneğin, atlama sayısı, gecikme süresi, bant genişliği) sayesinde en uygun olan yolu seçer.

### 4. **Paketin Yönlendirilmesi**

Uygun çıkış arabirimi ve next-hop belirlendikten sonra, router paketi o arabirime iletir. Bu esnada Layer 2 başlığı (örneğin MAC adresi bilgileri), yeni çıkış ağına uygun şekilde yeniden oluşturulur.

### 5. **TTL (Time to Live) ve Paket Güncellemesi**

Router, paketin TTL (yaşam süresi) değerini bir azaltır. Bu işlem, sonsuz döngüleri önlemek için yapılır. TTL sıfıra düşerse paket atılır ve göndericiye ICMP "time exceeded" mesajı gönderilir.

### 6. **Yönlendirme Sürecinin Tekrarı**

Paket, hedefe ulaşana kadar birden fazla router üzerinden geçebilir. Her router, yukarıdaki süreci kendi yönlendirme tablosuna göre tekrarlar.

#### Örnek:

Bir paket, 192.168.1.10 adresli yerel bir cihazdan 10.0.0.5 adresli uzak bir cihaza gönderiliyorsa:

* Router hedef IP’nin (10.0.0.5) hangi ağa ait olduğunu kontrol eder.
* Eğer yönlendirme tablosunda 10.0.0.0/24 ağı için bir yol varsa, paketi o yöne gönderir.
* Eğer yol bilinmiyorsa ve varsayılan ağ tanımlıysa (0.0.0.0/0), paketi varsayılan ağ geçidine yönlendirir.


## **Router ve Switch Arasındaki Farklar**

Router ve switch cihazları genellikle aynı ağda birlikte çalışır, fakat görevleri, çalışma katmanları ve işlevleri farklıdır. Aşağıda bu farklar ayrıntılı bir şekilde açıklanmıştır:

| Özellik                       | **Router**                                     | **Switch**                                                             |
| ----------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------- |
| **Çalışma Katmanı**           | OSI Layer 3 (Ağ katmanı)                       | OSI Layer 2 (Veri bağlantı katmanı), bazıları Layer 3 (Layer 3 Switch) |
| **Görev**                     | Ağlar arasında veri yönlendirme                | Aynı ağ (LAN) içinde cihazlar arasında veri iletimi                    |
| **Adresleme Türü**            | IP adresi (mantıksal adresleme)                | MAC adresi (fiziksel adresleme)                                        |
| **Yönlendirme / Anahtarlama** | IP tabanlı yönlendirme (routing) yapar         | MAC tabanlı anahtarlama (switching) yapar                              |
| **Broadcast Alanı Yönetimi**  | Broadcast alanlarını böler                     | Broadcast alanını genişletir (aynı ağ içinde çalışır)                  |
| **Yönlendirme Tablosu**       | Routing Table kullanır                         | MAC Address Table kullanır                                             |
| **NAT Desteği**               | NAT işlemleri yapabilir                        | NAT işlemi yapamaz                                                     |
| **Subnet İşleme**             | Alt ağlar arasında yönlendirme yapabilir       | Alt ağları ayıramaz, tüm bağlantılar aynı subnet içinde kalmalıdır     |
| **Varsayılan Ağ Geçidi**      | Genellikle bir ağın varsayılan gateway'idir    | Gateway işlevi görmez                                                  |
| **Bağlantı Türü**             | Farklı ağları birbirine bağlar (ör. LAN ↔ WAN) | Aynı ağ içindeki cihazları bağlar                                      |
| **Yaygın Kullanım Yeri**      | Ev – İş yeri çıkış noktaları, ISP bağlantısı   | Yerel ağlar (LAN), ofis içi bağlantılar                                |
| **IP Konfigürasyonu**         | Arabirimlerine IP adresi atanır                | Genellikle arabirimlere IP atanmaz (Layer 3 Switch hariç)              |


## **Router'larda Kullanılan Yönlendirme Tabloları**

Router'lar, paketleri doğru ağlara yönlendirmek için **yönlendirme tablolarını** kullanır. Bu tablolar, router’a hangi ağlar arasında veri iletimi yapılacağı, hangi arabirimlerin kullanılacağı ve hangi yolların tercih edileceği hakkında bilgi sağlar. Router’lar, yönlendirme tablosuna göre verileri en verimli şekilde iletmek için **forwarding** (iletim) işlemi gerçekleştirir.

### **Yönlendirme Tablosu (Routing Table)**

Router’ın yönlendirme tablosu, ağdaki rotalarla ilgili bilgileri saklar. Bu tablo, statik yönlendirmeler, dinamik yönlendirme protokolleri (RIP, OSPF, EIGRP, BGP) veya her ikisinin birleşimiyle güncellenebilir. Bir yönlendirme tablosu genellikle şu bilgileri içerir:

1. **Hedef Ağ (Destination Network)**: Veri paketlerinin yönlendirileceği ağ adresi.
2. **Alt Ağ Maskesi (Subnet Mask)**: Hedef ağın maskesi, hangi kısmın ağ adresi olduğunu belirtir.
3. **Next-Hop (Sonraki Yönlendirici)**: Paketin bir sonraki yönlendirilmesi gereken IP adresi veya ağ geçidi.
4. **Çıkış Arabirimi (Outgoing Interface)**: Paketin hangi fiziksel arabirim üzerinden gönderileceği bilgisi.
5. **Metrik**: Yolun kalitesini gösteren bir değer. Düşük metrik, daha iyi bir yol anlamına gelir (örn. atlama sayısı, gecikme, bant genişliği vb.).
6. **Yönlendirme Kaynağı (Source)**: Yönlendirme bilgisinin kaynağı, örneğin statik yönlendirme, OSPF veya EIGRP gibi bir protokol.

Yönlendirme tablosu, router’ın veri paketlerini doğru yola yönlendirmesini sağlar. **Forwarding**, yönlendirme tablosunda bulunan bilgiye dayanarak, router’ın gelen bir paketi uygun arabirime iletmesidir. Bu süreç, paketlerin doğru hedefe ulaşması için kritik öneme sahiptir.

## **Statik Yönlendirme**

**Statik yönlendirme**, router’a manuel olarak belirli yönlendirme yollarının eklenmesi işlemidir. Bu tür yönlendirme, ağ yöneticisi tarafından statik olarak yapılandırılır ve genellikle ağdaki trafik, ağ cihazları ve yönlendirici değişmediği sürece sabit kalır.

### **Statik Yönlendirme Nasıl Çalışır?**

Statik yönlendirme, router’ın yönlendirme tablosuna **elle** girilen ağ yönlendirme bilgilerine dayanır. Yönlendirme tablosuna her hedef ağ için bir **yönlendirici (next-hop)** IP adresi ve **çıkış arabirimi (outgoing interface)** belirtilir. Bu bilgiler, ağın sabit ve önceden belirlenmiş yollarını oluşturur.

Örneğin:

* **IP route 192.168.1.0 255.255.255.0 10.0.0.2** komutuyla, router’a 192.168.1.0/24 ağına erişim için 10.0.0.2 IP adresine yönlendirme yapması söylenmiş olur.

Statik yönlendirme, genellikle küçük ağlarda veya basit yönlendirme senaryolarında kullanılır.

### **Statik Yönlendirmenin Avantajları**

1. **Basitlik ve Kolay Konfigürasyon**: Küçük ağlarda veya sabit yapıdaki ağlarda statik yönlendirme oldukça basit ve hızlı bir çözüm sağlar.
2. **Kontrol**: Yönlendirme yolları tamamen ağ yöneticisinin kontrolündedir. Hangi yollardan geçileceği kesin olarak belirlenir.
3. **Düşük Kaynak Tüketimi**: Statik yönlendirme, dinamik yönlendirme protokollerine kıyasla daha az işlem gücü ve bellek tüketir.
4. **Güvenlik**: Yönlendirme protokollerinde oluşabilecek yanlış yönlendirmeler (örneğin, man-in-the-middle saldırıları) statik yönlendirmede daha az olasılıkla görülür çünkü rotalar sabittir ve değiştirilemez.

### **Statik Yönlendirmenin Dezavantajları**

1. **Esneklik Eksikliği**: Ağ topolojisi değiştiğinde, yönlendirme tablolarının manuel olarak güncellenmesi gerekir. Dinamik yönlendirme protokollerine kıyasla esneklikten yoksundur.
2. **Hata Riski**: Eğer ağ yöneticisi yanlış bir yönlendirme eklerse, ağda ciddi iletişim problemleri oluşabilir. Ayrıca, ağda bir bağlantı koparsa, yönlendirme tablosu güncellenmez, bu da paketlerin kaybolmasına veya hata mesajları alınmasına neden olabilir.
3. **Büyüyen Ağlarda Zorluk**: Ağ büyüdükçe, statik yönlendirme tablosunun yönetilmesi zorlaşır. Çok sayıda ağ ve yönlendirme kuralı gerektiğinde, manuel güncellemeler zaman alıcı ve hataya açık hale gelir.
4. **Düşük Ölçeklenebilirlik**: Büyük ağlarda, yeni ağ eklemek veya yönlendirmeleri değiştirmek manuel olarak yapılır ve bu durum verimliliği düşürür.


## **Dinamik Yönlendirme**

**Dinamik yönlendirme**, bir ağdaki yönlendiricilerin, ağ topolojisinde meydana gelen değişikliklere otomatik olarak adapte olabilmesini sağlayan bir yöntemdir. Statik yönlendirme ile karşılaştırıldığında, dinamik yönlendirme, yönlendirme tablosunun otomatik olarak güncellenmesini ve ağdaki herhangi bir değişikliğin (yeni bir ağ eklenmesi, bir bağlantının kopması, bir yönlendiricinin devre dışı kalması vb.) hemen yansımasını sağlar. Bu özellik, ağ yöneticisinin manuel müdahale gereksinimini ortadan kaldırır ve ağın verimli bir şekilde çalışmasını sağlar.

Dinamik yönlendirme, ağ topolojisindeki değişiklikleri sürekli olarak izler ve rotaları dinamik olarak günceller. Böylece ağda kesintiler meydana geldiğinde, yönlendirme tablosu otomatik olarak en iyi yolu seçer ve trafiği yeni yollar üzerinden yönlendirir.

### Dinamik Yönlendirmenin Temel Özellikleri:

1. **Otomatik Güncelleme**: Yeni ağlar eklendiğinde veya mevcut ağlar değiştiğinde, yönlendirme tablosu otomatik olarak güncellenir.
2. **Uyum Yeteneği**: Dinamik yönlendirme, ağ topolojisinin değişmesine bağlı olarak kendini adapte edebilir. Bu, ağdaki arızalar, yeni bağlantılar veya yol değişiklikleri durumunda önemli avantajlar sağlar.
3. **Yük Dengeleme ve Yedeklilik**: Dinamik yönlendirme, ağda en iyi rotaları seçerek yük dengelemesi yapabilir ve aynı zamanda yedeklilik sağlar.
4. **Daha Fazla Ölçeklenebilirlik**: Dinamik yönlendirme, ağ büyüdükçe ve karmaşıklaştıkça daha verimli bir çözüm sunar.


## **Dinamik Yönlendirme Protokolleri**

Dinamik yönlendirme protokolleri, yönlendiriciler arasındaki bilgi paylaşımını sağlamak için kullanılan kurallar bütünüdür. Bu protokoller, yönlendirme tablolarını sürekli olarak güncelleyerek en iyi rotayı seçmek için ağ topolojisini izler ve değişikliklere otomatik olarak adapte olur. Dinamik yönlendirme protokolleri, ağdaki yönlendiriciler arasındaki trafiği yönlendirmek için belirli algoritmalar kullanır.

Yönlendirme protokolleri, temelde iki ana grupta sınıflandırılır: **İç Yönlendirme Protokolleri (Interior Gateway Protocols - IGP)** ve **Dış Yönlendirme Protokolleri (Exterior Gateway Protocols - EGP)**.

### 1. **İç Yönlendirme Protokolleri (IGP)**

**İç Yönlendirme Protokolleri**, genellikle tek bir otonom sistem (AS) içinde çalışan protokollerdir. Bu protokoller, bir ağda yönlendirme bilgilerini paylaşan router’lar arasında veri iletmek için kullanılır. Yaygın iç yönlendirme protokollerinden bazıları şunlardır:

* **RIP (Routing Information Protocol)**: En eski ve en basit yönlendirme protokollerinden biridir. **RIP v1** ve **RIP v2** olmak üzere iki versiyonu vardır. RIP, ağdaki her yönlendiricinin bir "mesafe vektörü" (distance vector) kullanarak yönlendirme bilgilerini birbirine aktarmasını sağlar. RIP'in ana özelliği, yol uzunluğunun **atlama sayısı (hop count)** ile ölçülmesidir. Ancak, RIP’in sınırlamaları vardır. En büyük sınırlaması, ağda yalnızca 15 atlamaya kadar yol iletmesi ve verimli olmayan büyük ağlarda kullanılabilirliğinin kısıtlı olmasıdır.

* **OSPF (Open Shortest Path First)**: OSPF, **Link State Protocol**’dür, yani her yönlendirici kendi ağ bağlantı durumunu bilir ve bu bilgiyi diğer yönlendiricilere ileterek genel bir ağ topolojisi oluşturur. OSPF, daha büyük ağlar için daha verimli ve ölçeklenebilir bir çözüm sunar. Yönlendirme metrikleri, linkler arasındaki **bant genişliğine** göre belirlenir. OSPF, daha geniş ve karmaşık ağlarda RIP'ten çok daha iyi performans gösterir ve çok daha hızlı ağ değişikliklerine adapte olabilir.

* **EIGRP (Enhanced Interior Gateway Routing Protocol)**: EIGRP, **Cisco tarafından geliştirilmiş bir hibrit yönlendirme protokolüdür**. Hem **distance vector** hem de **link-state** protokollerinin özelliklerini birleştirir. EIGRP, ağdaki her yönlendiriciye, yol seçimi için birden fazla parametre sunar. EIGRP, özellikle büyük ve dinamik ağlar için uygun olan, hızlı ve verimli bir protokoldür. Ayrıca, **Dünya Çapında En İyi Yol Seçimi (Dijkstra Algoritması)** gibi daha karmaşık algoritmalar kullanır.

### 2. **Dış Yönlendirme Protokolleri (EGP)**

**Dış Yönlendirme Protokolleri**, farklı otonom sistemler arasındaki yönlendirme bilgilerini paylaşmak için kullanılır. Bu protokoller, internet gibi büyük ağlarda yönlendirme yapılmasını sağlar. En yaygın dış yönlendirme protokolü **BGP (Border Gateway Protocol)**’dir.

* **BGP (Border Gateway Protocol)**: **BGP**, internetin temel yönlendirme protokolüdür. BGP, **Path Vector Protocol** olarak sınıflandırılır ve her bir ağın, diğer ağlarla olan bağlantılarını belirten yol bilgilerini içerir. BGP, otonom sistemler arasındaki yönlendirme bilgilerini paylaşır ve internetteki yol trafiğini yönlendirir. BGP, yönlendirme bilgilerini, yönlendiricinin politikalarına ve yol özelliklerine göre kararlar alarak iletir. BGP, ağda trafik yoğunluğunu dengeleyebilir ve yönlendirme politikaları oluşturulmasına olanak tanır.

## **RIP V2**

**RIP v2 (Routing Information Protocol version 2)**, **mesafe vektörlü** bir yönlendirme protokolüdür. **RIP** protokolünün ikinci sürümü olan **RIP v2**, bazı iyileştirmeler sunarak **RIP v1**'in sınırlamalarını giderir. Yönlendirme protokollerinin temel amacı, ağdaki yönlendiricilerin hedeflere ulaşmak için en iyi yolları belirleyip birbirlerine bildirmeleridir. RIP v2, mesafe vektör algoritmasını kullanarak bu amaç doğrultusunda ağdaki yönlendirme tablolarını günceller.

### **RIP v2 Temel Çalışma Prensibi**

RIP v2, **mesafe vektör protokolü** türündedir, bu da her yönlendiricinin, hedeflere ulaşmak için gerekli olan hop sayısını (atlama sayısını) bildirdiği anlamına gelir. Yönlendirici, komşu yönlendiricilerine, ağdaki hedeflere ulaşmak için gereken hop sayısını bildirir. Yönlendiriciler, birbirlerinden aldıkları bu bilgileri kullanarak, ağda en uygun yönlendirme yollarını belirlerler.

RIP v2'nin temel prensipleri şu şekildedir:

1. **Yönlendirme Güncellemeleri**:
   Yönlendiriciler, ağdaki hedeflere yönelik yönlendirme bilgilerini her 30 saniyede bir günceller. Bu güncellemelerde, ağdaki her hedef için o hedefe ulaşmak için gereken hop sayısı bilgisi bulunur. Yönlendirici, bu bilgiyi **multicast** adresine gönderir. Multicast kullanımı, yalnızca RIP v2'yi destekleyen yönlendiricilerin bu güncellemeleri almasını sağlar, bu da ağdaki gereksiz trafiği engeller.

2. **Hop Sayısı**:
   Yönlendirme tablosunda her hedefin karşısında, o hedefe ulaşmak için geçilmesi gereken **hop sayısı** belirtilir. Bir hedefe ulaşmak için **maksimum 15 hop** desteklenir. Eğer bir yolun hop sayısı 16'ya ulaşırsa, bu yol geçersiz sayılır ve yönlendirme tablosundan silinir. Bu durum, RIP v2'nin büyük ağlar için uygun olmadığını gösterir, çünkü büyük ağlarda 15 hop'un üzerindeki mesafeler gerekebilir.

3. **Sınıfsız Yönlendirme (CIDR)**:
   RIP v2, **sınıfsız ağ yapısını** (CIDR) destekler. Bu, daha esnek adresleme yapabilmeyi sağlar. Yönlendirme tablolarında her IP adresiyle birlikte bir **alt ağ maskesi** de bulunur. Bu özellik, RIP v1'deki sınıf tabanlı adresleme ile kıyaslandığında daha verimli ve esnek bir yönlendirme sunar.

4. **Veri Kimlik Doğrulama**:
   RIP v2, yönlendirme bilgilerini daha güvenli bir şekilde iletmek için **kimlik doğrulama** mekanizması sağlar. Yönlendiriciler, belirli bir **şifre** kullanarak yönlendirme güncellemelerini alır ve bu şifre doğruysa bilgileri kabul eder. Bu özellik, ağ güvenliğini artırır ve sahte yönlendirme bilgilerini engeller.

5. **Yönlendirme Döngüleri ve Diğer Teknikler**:
   RIP v2, **mesafe vektör** algoritmasının yol açabileceği **yönlendirme döngülerini** engellemek için bir dizi teknik kullanır. Bu teknikler arasında **split horizon**, **route poisoning** ve **hold-down** mekanizmaları bulunur:

   * **Split Horizon**: Yönlendirici, aynı yönlendiriciden gelen bir yönlendirme bilgisini geri göndermez. Bu, yönlendirme döngülerini engellemeye yardımcı olur.
   * **Route Poisoning**: Eğer bir yol geçersiz hale gelirse, bu yol 16 hop olarak işaretlenir ve geçersiz sayılır. Bu, yönlendirme döngülerinin oluşmasını engeller.
   * **Hold-Down**: Bir yol geçersiz hale geldiğinde, o yolun yeniden kullanılmadan önce bir süre boyunca beklenmesi sağlanır. Bu, ağdaki geçici sorunların çözülmesi için zaman tanır.

### **Yönlendirme Güncellemelerinin Dağıtımı**

RIP v2'nin yönlendirme güncellemeleri, **multicast** adresi kullanılarak gönderilir. Bu adres, yalnızca RIP v2'yi destekleyen yönlendiriciler tarafından dinlenir. **224.0.0.9** multicast adresi, RIP v2'nin güncellemelerini iletmek için kullanılır. Bu sayede, RIP v1'in kullandığı **broadcast** iletişimi yerine, daha verimli bir şekilde yönlendirme bilgileri iletilir.

Her yönlendirici, aldığı yönlendirme bilgilerini kendi yönlendirme tablosuna ekler ve bu bilgiyi diğer yönlendiricilerle paylaşır. Bu süreç, ağdaki en iyi yolun bulunmasına yardımcı olur. Yönlendirme güncellemeleri, **30 saniyede bir** yapılır ve yönlendirici, komşularına en güncel yönlendirme bilgisini iletir.

### **RIP v2 ve Yönlendirme Tabloları**

Yönlendiriciler, ağdaki hedeflere ulaşmak için en uygun yolu belirlemek için **yönlendirme tablosu** kullanır. Yönlendirme tablosunda her hedef için **IP adresi**, **hop sayısı**, **ağ maskesi** ve hedefin bulunduğu **komşu yönlendirici** bilgisi yer alır. RIP v2, yönlendirme tablosunda **CIDR** destekleyerek daha verimli ağ yapılandırmalarını mümkün kılar.

### **RIP v2'nin Çalışma Süreci**

RIP v2'nin çalışma süreci şu şekilde işler:

1. Yönlendiriciler, yönlendirme tablolarını her 30 saniyede bir günceller.
2. Yönlendiriciler, **multicast** kullanarak güncel yönlendirme bilgilerini komşularına gönderir.
3. Yönlendiriciler, aldıkları yönlendirme bilgilerini kendi tablolarına ekler ve gerektiğinde yönlendirme tablosunu yeniden oluştururlar.
4. Yönlendiriciler, yönlendirme döngülerini engellemek için çeşitli teknikler kullanarak yönlendirme bilgilerini paylaşır.

Bu süreç, ağda en kısa yolun belirlenmesi için tekrarlanır. Yönlendirici, kendi tablosundaki hedeflere ulaşmak için en az hop sayısına sahip olan yolu seçer.


## **OSPF**

**OSPF (Open Shortest Path First)**, **Link-State** tabanlı bir yönlendirme protokolüdür ve **RIP** gibi **mesafe vektör** tabanlı protokollere göre daha gelişmiş özelliklere sahip bir yönlendirme protokolüdür. **OSPF**, özellikle büyük ve karmaşık ağlarda daha verimli ve dinamik bir yönlendirme sağlar. OSPF'nin ana avantajı, ağdaki her yönlendiricinin, ağ topolojisinin tam bir haritasına sahip olmasıdır. Bu, her yönlendiricinin ağdaki diğer yönlendiricilerle olan bağlantılarının tam bir resmini çizmesini ve bu bilgiyle en iyi yolu hesaplamasını sağlar.

### **OSPF Temel Çalışma Prensibi**

OSPF, **Link-State** tabanlı bir protokol olduğundan, her yönlendirici yalnızca kendi bağlantı durumu hakkında bilgi sahibi olur ve ağdaki diğer yönlendiricilerle bu bilgileri paylaşır. Bu sayede, ağda meydana gelen değişikliklere hızlı bir şekilde tepki verilir ve ağda yönlendirme döngüleri oluşmaz. OSPF, **Dijkstra algoritması** (Shortest Path First - SPF) kullanarak, her yönlendiricinin en kısa yolu hesaplamasını sağlar.

#### **1. Link-State ve LSDB (Link-State Database)**

OSPF'nin temel çalışma prensibi, her yönlendiricinin **Link-State Database (LSDB)** adı verilen bir veritabanı tutmasıdır. Bu veritabanı, ağdaki yönlendiricilerin birbirleriyle olan bağlantılarını ve ağda bulunan tüm bağlantı durumlarını içerir. Her yönlendirici, **Link-State Advertisement (LSA)** adı verilen paketlerle, ağda bulunan komşularına ve diğer yönlendiricilere bağlantı durumu hakkında bilgi gönderir.

* **LSA Paketleri**: OSPF, yönlendiriciler arasında ağdaki bağlantıların durumunu belirten **LSA** paketlerini gönderir. Bu paketler, ağdaki her yönlendirici ve bağlantısı hakkında bilgi içerir. Bu sayede her yönlendirici, ağdaki tüm bağlantıları görmek için birbirine **LSA** paketleri gönderir.

* **LSDB**: Yönlendirici, aldığı **LSA paketlerini** kullanarak, ağdaki tüm bağlantıların bilgisini içeren bir **LSDB** oluşturur. Bu veri tabanı, yönlendiricinin ağ topolojisini tam olarak anlamasına olanak tanır.

#### **2. SPF (Shortest Path First) Algoritması**

OSPF, **Dijkstra'nın SPF algoritmasını** kullanarak en kısa yolu hesaplar. Bu algoritma, ağdaki her yönlendiriciye olan en kısa yolu hesaplamak için **LSDB**'yi kullanır. Yönlendirici, **LSDB**'yi analiz ederek ağdaki tüm yolları ve bu yolların maliyetlerini değerlendirir ve en kısa yolu seçer.

* **Maliyet (Cost)**: OSPF, her bağlantıya bir **maliyet** (cost) değeri atar. Bu değer, genellikle bağlantının hızına göre belirlenir. Örneğin, daha hızlı bağlantılar daha düşük maliyetlere sahip olabilir. Yönlendirici, ağdaki hedeflere ulaşmak için bu maliyetleri dikkate alarak en kısa yolu hesaplar.

* **SPF Hesaplaması**: OSPF, her yönlendirici için bağımsız olarak SPF algoritmasını çalıştırarak, ağdaki her hedefe en kısa yolun belirlenmesini sağlar.

#### **3. OSPF Alanları (Areas)**

OSPF, büyük ağlarda daha verimli çalışabilmesi için **alanlar** (areas) kullanır. Bir ağ, birden fazla OSPF alanına bölünebilir. Her alan, ağdaki yönlendiricilerin birbirleriyle olan bağlantılarını içerir. OSPF, tüm ağın bir **backbone** alanı (Area 0) üzerinden birbirine bağlanmasını sağlar. Bu yapı, OSPF'nin ölçeklenebilirliğini artırır.

* **Backbone Area (Area 0)**: OSPF ağı, **Area 0** adı verilen ana alan üzerinden birbirine bağlanır. Bu, ağdaki tüm diğer alanların birbirleriyle bağlantı kurmasını sağlar. OSPF alanları, her bir alanın kendi içindeki yönlendirme bilgilerini tutarak, ağdaki yönlendirme verisinin daha verimli bir şekilde yönetilmesini sağlar.

* **Area Types**: OSPF’de farklı alan türleri vardır:

  * **Internal Area**: Aynı alandaki yönlendiriciler arasındaki bağlantıları içerir.
  * **Stub Area**: Yalnızca dışa bağlantısı olan ve dışa veri alması kısıtlanmış alanlardır.
  * **Totally Stubby Area**: Dış bağlantıların tamamıyla engellendiği alanlardır.
  * **NSSA (Not So Stubby Area)**: Dışa bağlantıların kısıtlı şekilde alındığı alanlardır.

#### **4. OSPF Durumları ve Komşuluk İlişkileri**

OSPF, komşuluk ilişkileri kurarak çalışır. Yönlendiriciler, ağdaki diğer yönlendiricilerle doğrudan komşuluk kurar ve bu komşuluk üzerinden yönlendirme bilgilerini değiş tokuş ederler. OSPF komşuluk ilişkilerinin kurulma süreci aşağıdaki adımlardan oluşur:

1. **Down State**: Yönlendirici, komşu yönlendiriciyi henüz tanımıyor.
2. **Init State**: Yönlendirici, komşu yönlendiriciden bir mesaj almış ancak henüz bir veri alışverişi yapılmamıştır.
3. **Two-Way State**: Yönlendirici, komşu yönlendirici ile veri alışverişi yapmaya başlamış, ancak bağlantı hala tam olarak kurulmaktan uzaktır.
4. **ExStart State**: Yönlendirici, komşu yönlendirici ile **Hello** paketleri üzerinden bağlantı kurmaya çalışır.
5. **Exchange State**: Yönlendiriciler, birbirlerine yönlendirme bilgilerini göndermeye başlar.
6. **Loading State**: Yönlendirici, komşudan aldığı yönlendirme bilgilerini doğrular.
7. **Full State**: Yönlendirici ve komşusu, birbirlerinin yönlendirme tablolarını tam olarak eşitlemiş ve bağlantı tamamen kurulmuştur.

#### **5. OSPF Topoloji Değişiklikleri ve Yönlendirme Güncellemeleri**

OSPF, ağda meydana gelen değişiklikleri hızla fark eder ve bu değişiklikleri yönlendiricilere bildirir. OSPF, ağda bir topoloji değişikliği olduğunda, yalnızca değişen bilgiyi günceller ve yayar. Bu özellik, ağda meydana gelen herhangi bir değişikliğe hızlı bir şekilde tepki verilmesini sağlar. Yönlendiriciler, topoloji değişikliği olduğunda **LSA** güncellemeleri gönderirler.

#### **6. OSPF ve Hiyerarşi**

OSPF, geniş ağları daha verimli bir şekilde yönetebilmek için **hiyerarşik yapı** kullanır. OSPF’de, **Area 0** (backbone area) dışında farklı alanlar tanımlanabilir. Bu yapı, yönlendirme tablosunun büyüklüğünü kontrol altında tutar ve yönlendirme bilgilerini sadece gerekli alanlara iletir.


## **EIGRP**

**EIGRP (Enhanced Interior Gateway Routing Protocol)**, Cisco tarafından geliştirilen ve **daha hızlı** ve **daha verimli** yönlendirme için **IETF (Internet Engineering Task Force)** tarafından kabul edilen **gelişmiş bir iç yönlendirme protokolü**dür. EIGRP, **distance-vector** tabanlı bir protokoldür, ancak **Link-State** protokollerinin bazı avantajlarına da sahip olan hibrit bir protokoldür. EIGRP, **daha hızlı stabilizasyon**, **gelişmiş yönlendirme** ve **güvenlik** gibi avantajlar sunarak, büyük ağlarda yönlendirme performansını artırmayı hedefler.

EIGRP, **RIP (Routing Information Protocol)** ve **OSPF (Open Shortest Path First)** gibi protokollere göre daha verimli ve dinamik bir yapı sunar. Bu nedenle, özellikle **Cisco cihazları** üzerinde yaygın bir şekilde kullanılır.

### **EIGRP Temel Çalışma Prensibi**

EIGRP, **distance-vector** protokolü olmasına rağmen, **Link-State** protokollerinin bazı özelliklerini birleştirerek, **hibrit bir protokol** olarak çalışır. Bu özellikler sayesinde, EIGRP, **daha hızlı** ve **güvenilir** yönlendirme sağlar.

#### **1. EIGRP'nin Temel Yapısı ve Bileşenleri**

EIGRP'nin temel bileşenleri ve çalışma prensibi şunlardır:

* **Neighbor Table**: Yönlendirici, komşu yönlendiricileriyle bağlantı kurarak, **komşuluk tablosu** oluşturur. Bu tablo, yönlendiricinin doğrudan iletişim kurduğu komşu cihazlar hakkındaki bilgileri içerir. EIGRP, komşuluk ilişkisinin kurulabilmesi için **Hello paketleri** kullanır.

* **Topology Table**: Yönlendirici, ağdaki tüm bağlantılar hakkında bilgi sahibi olmak için **topoloji tablosu** tutar. Bu tablo, ağdaki her hedefe ulaşmak için geçerli olan yolların tümünü içerir. EIGRP, her hedef için alternatif yolların bulunduğu bir **topoloji** oluşturur.

* **Routing Table**: **Yönlendirme tablosu**, yönlendiricinin en iyi yolları seçtiği tablodur. EIGRP, en iyi yolu **Dual Algorithm** (Diffusing Update Algorithm) kullanarak hesaplar ve bu yolu yönlendirme tablosuna ekler.

#### **2. EIGRP Komşuluk İlişkileri**

EIGRP, komşuluk ilişkileri kurarak çalışır. Yönlendiriciler, ağda doğrudan bağlantılı oldukları diğer yönlendiricilerle **komşuluk ilişkisi** kurar. Bu komşuluk ilişkisi, EIGRP'nin **Hello paketleri** göndererek kurulur ve **ACK (Acknowledgment)** kullanarak doğrulanır.

EIGRP, komşularına düzenli olarak güncellemeler gönderir. Bu güncellemeler, ağda meydana gelen değişiklikleri iletir. EIGRP, **Hello** paketlerinin belirli bir süre boyunca alınmaması durumunda, komşuluğu sonlandırır.

#### **3. EIGRP Yönlendirme Güncellemeleri**

EIGRP, yönlendirme güncellemelerini sadece ağda meydana gelen değişiklikler olduğunda gönderir. Bu, **Link-State** protokollerinin aksine, yönlendiricilerin her zaman tüm ağ hakkında bilgi gönderdiği bir yapıdan daha verimli bir yöntemdir. EIGRP'nin **incremental update** yöntemi sayesinde, yalnızca değişen veriler iletilir, bu da ağ trafiğini azaltır.

EIGRP'nin yönlendirme güncellemeleri, **bounded updates** olarak bilinir ve yalnızca gerektiğinde yapılır. Bu, EIGRP'nin **daha hızlı** güncellemeler gönderdiği ve ağdaki değişiklikleri hızla yansıttığı anlamına gelir.

#### **4. EIGRP Metrik Hesaplama**

EIGRP, yönlendirme kararlarını verirken bir **metrik** kullanır. EIGRP'nin metrik hesaplama yöntemi, **kapsama alanı, gecikme, bant genişliği, yük ve güvenilirlik** gibi faktörlere dayanır. EIGRP'nin metrik hesaplama formülü şu şekildedir:

$$
\text{Metrik} = \left( \frac{10^7}{Bant Genisliği} + Gecikme \right)
$$

* **Bant Genişliği**: Bağlantının bant genişliği, metrik hesaplamasında önemli bir faktördür. EIGRP, düşük bant genişliğine sahip bağlantıları daha pahalı (yüksek metrik) olarak değerlendirir.

* **Gecikme**: EIGRP, her bağlantı için gecikme (delay) değerini de hesaba katar. Gecikme, bağlantının ne kadar hızlı veri iletebildiğini gösterir.

* **Yük ve Güvenilirlik**: Yönlendirme kararlarında yük ve güvenilirlik gibi parametreler de dikkate alınabilir. Ancak bu parametreler genellikle daha az önemli kabul edilir.

#### **5. Dual Algoritması (Diffusing Update Algorithm)**

EIGRP'nin en önemli özelliklerinden biri, yönlendirme kararlarını **Dual Algorithm** (Diffusing Update Algorithm) kullanarak vermesidir. Bu algoritma, ağdaki her hedef için en kısa yolu hesaplamak ve en iyi yolu seçmek için kullanılır.

* **DUAL** algoritması, **geçici yönlendirme döngülerinin** oluşmasını engeller. Bu, ağdaki değişiklikler sırasında, yönlendiricilerin doğru yolu bulmalarını sağlar.

* **Backup Routes**: DUAL algoritması, yalnızca ana yolu değil, aynı zamanda alternatif yolları da hesaba katar. Eğer ana yol geçersiz hale gelirse, yedek yol hemen devreye girer.

#### **6. EIGRP'yi Hızlı Yönlendirme Sağlayan Özellikler**

* **Quick Convergence**: EIGRP, ağda meydana gelen değişiklikleri çok hızlı bir şekilde fark eder ve buna göre yönlendirme tablolarını günceller. **Hızlı stabilizasyon** sağlar.

* **Route Aggregation**: EIGRP, yönlendirme tablosunun boyutunu küçültmek için **yol agregasyonu** (route aggregation) kullanabilir. Bu, çok sayıda küçük ağın tek bir büyük ağ olarak gruplanmasını sağlar.

* **Topology Table**: EIGRP, ağdaki her bağlantı için alternatif yolları saklar ve gerektiğinde bu yolları kullanabilir.

#### **7. EIGRP ve Hiyerarşi**

EIGRP, **flat (düz) bir yapı**da çalışabilir. Yani, ağda **bölümler** (areas) gibi ek yapılar bulunmaz. Ancak, EIGRP ağlarında **hiyerarşik yapı** kurmak mümkündür. Yönlendiriciler, ağda her bölge için bir **çeşitli yönlendirme tablosu** oluşturabilirler. Bu yapı, ağın daha verimli çalışmasını sağlar.


# **ROUTER YAPILANIDIRMALARI**

### **Router IOS Temelleri ve Komut Modları**

**Router IOS (Internetwork Operating System)**, Cisco yönlendiricilerinin işletim sistemidir. IOS, yönlendirici cihazlarını yönetmek ve yapılandırmak için kullanılan bir yazılımdır. IOS, yönlendiricinin çeşitli modlarında çalışarak, farklı seviyelerde komutlar girilmesine olanak tanır. Bu modlar, kullanıcının yetki düzeyine göre değişir ve her bir modun kendine ait bir işlevi vardır.

#### **1. User Exec Mode**

* **Tanım**: Yönlendiricinin ilk modudur. Kullanıcı, yönlendiriciye bağlandığında doğrudan bu modda bulunur.
* **Komutlar**: Bu modda, genellikle temel komutlar girilebilir ve bazı temel sistem bilgileri görülebilir. Örneğin, **show** komutlarıyla sistem durumu veya arayüz durumu görüntülenebilir.
* **Giriş**: Kullanıcı, yönlendiricinin IP adresine bağlandığında veya bir terminal üzerinden giriş yapıldığında bu modda bulunur.
* **Komutlar**: Bu modda sınırlı komutlar çalıştırılabilir. Komutlar genellikle yalnızca veri gösterimi ve bazı sistem özelliklerini inceleme amaçlıdır.
* **Görüntü**:

  ```
  Router>
  ```

#### **2. Privileged Exec Mode (Enable Mode)**

* **Tanım**: **User Exec Mode**'den daha fazla yetkiye sahip bir moddur. Bu modda, sistem yapılandırmalarına dair daha fazla işlem yapılabilir.
* **Komutlar**: Bu modda, yapılandırma, yönlendirme, ağ protokolleri ve cihaz ayarları hakkında komutlar girilebilir. Ayrıca, cihazı test etmek veya belirli ağ bilgilerini görüntülemek için daha fazla komut mevcuttur.
* **Giriş**: **User Exec Mode**'den **enable** komutuyla geçilir.
* **Komutlar**: Bu modda, **show running-config**, **show interfaces**, **show ip route** gibi komutlar çalıştırılabilir.
* **Görüntü**:

  ```
  Router#
  ```

#### **3. Global Configuration Mode**

* **Tanım**: **Privileged Exec Mode**'den geçilebilen moddur ve yönlendirici cihazının yapılandırmalarının yapıldığı yerdir. Bu modda, yönlendiricinin her türlü yapılandırması değiştirilebilir.
* **Komutlar**: Bu modda, ağ arayüzleri, yönlendirme protokolleri, VLAN yapılandırmaları ve diğer sistem ayarları değiştirilebilir. Örneğin, IP adresleri atanabilir, yönlendirme protokollerine yönelik ayarlar yapılabilir.
* **Giriş**: **Privileged Exec Mode**'de iken **configure terminal** komutuyla bu modda çalışılmaya başlanır.
* **Komutlar**: **interface**, **ip address**, **router ospf**, **hostname** gibi komutlarla yönlendiricinin yapılandırması yapılır.
* **Görüntü**:

  ```
  Router(config)#
  ```

#### **4. Interface Configuration Mode**

* **Tanım**: Bu modda, yönlendiricinin fiziksel veya sanal ağ arayüzlerine özgü ayarlar yapılabilir. IP adresi atama, arayüz etkinleştirme veya devre dışı bırakma gibi işlemler burada gerçekleştirilir.
* **Komutlar**: **ip address**, **shutdown**, **no shutdown** gibi komutlarla arayüzlere ayar yapılabilir.
* **Giriş**: **Global Configuration Mode**'de iken **interface \[interface\_adı]** komutuyla bu modda çalışılır.
* **Komutlar**: Arayüzlere özel yapılandırmalar yapılır, örneğin **interface gig0/1**, **ip address 192.168.1.1 255.255.255.0** gibi komutlar kullanılabilir.
* **Görüntü**:

  ```
  Router(config-if)#
  ```

#### **5. Line Configuration Mode**

* **Tanım**: Bu modda, yönlendiricinin konsol, vty (uzaktan erişim) veya AUX portlarının ayarları yapılır.
* **Komutlar**: **login**, **password**, **transport input ssh** gibi komutlar kullanılarak portlara özgü yapılandırmalar yapılabilir.
* **Giriş**: **Global Configuration Mode**'de iken **line console 0** veya **line vty 0 4** komutlarıyla bu modda çalışılır.
* **Komutlar**: Konsol veya uzak bağlantı güvenliği için **password** ve **login** gibi komutlar burada ayarlanabilir.
* **Görüntü**:

  ```
  Router(config-line)#
  ```



## **Router Arayüzlerinin Yapılandırılması (Interface IP Ayarları)**

Router arayüzlerinin yapılandırılması, yönlendiricinin farklı ağlarla iletişime geçebilmesi için kritik öneme sahiptir. Bu işlem, her bir ağ arayüzüne IP adresi atamayı, arayüzü etkinleştirmeyi ve gerektiğinde yönlendirme yapılandırmaları yapmayı içerir.

#### **1. Arayüz Yapılandırması İçin Temel Adımlar**

Yönlendiricinin arayüzlerine IP adresi atamak ve bu arayüzleri yapılandırmak için aşağıdaki temel adımlar izlenir:

* **Interface Seçimi**: Her bir ağ arayüzü, yönlendiricinin donanımında belirli bir portu temsil eder. Örneğin, **GigabitEthernet 0/1**, **FastEthernet 0/0** gibi arayüzler olabilir. Bu arayüzlere yapılandırma yapmak için, her bir arayüzün yapılandırma moduna geçmek gerekir.

* **IP Adresi Atama**: Her arayüze uygun bir IP adresi atamak gereklidir. Bu, yönlendiricinin bir ağdan diğerine doğru paket yönlendirmesini sağlamak için önemlidir.

* **Arayüzün Etkinleştirilmesi (no shutdown)**: Bir arayüz, varsayılan olarak devre dışıdır. Bu nedenle, IP adresi atandıktan sonra **no shutdown** komutuyla arayüz aktif hale getirilmelidir.

#### **2. Örnek Yapılandırma Adımları**

**Adım 1: Arayüz Yapılandırma Moduna Geçiş**

Öncelikle, **Global Configuration Mode**'den sonra belirli bir arayüze geçilmesi gereklidir. Bunun için aşağıdaki komut kullanılır:

```
Router(config)# interface gigabitEthernet 0/1
```

Bu komut, **GigabitEthernet 0/1** arayüzünü yapılandırma moduna geçirir.

**Adım 2: IP Adresi Atama**

Arayüz yapılandırma modunda, **ip address** komutuyla IP adresi ve alt ağ maskesi atanır. Örneğin:

```
Router(config-if)# ip address 192.168.1.1 255.255.255.0
```

Bu komut, **GigabitEthernet 0/1** arayüzüne **192.168.1.1/24** IP adresini atar.

**Adım 3: Arayüzü Etkinleştirme**

Yönlendiricinin arayüzü, varsayılan olarak kapalıdır. Arayüzü etkinleştirmek için şu komut kullanılır:

```
Router(config-if)# no shutdown
```

Bu komut, arayüzü aktif hale getirir.

**Adım 4: Çıkış ve Yapılandırmayı Kaydetme**

Arayüz yapılandırmaları tamamlandıktan sonra, **exit** komutuyla arayüz yapılandırma modundan çıkılır ve yapılandırmalar kaydedilebilir:

```
Router(config-if)# exit
Router(config)# write memory
```


## **Packet Tracer ile Temel Router Yapılandırması (CLI Uygulaması)**

Cisco Packet Tracer, ağ simülasyonu yapmaya olanak tanıyan güçlü bir eğitim aracıdır. Temel bir router yapılandırması, yönlendiricinin çalışması için gerekli olan minimum ayarları içerir. Bu yapılandırma; hostname tanımlama, parolaların belirlenmesi, IP adresi atama, arayüzleri etkinleştirme ve kaydetme işlemlerinden oluşur. Aşağıda CLI (Command Line Interface) kullanılarak temel bir router yapılandırmasının nasıl yapıldığı adım adım açıklanmıştır.

#### **1. Başlangıç: Cihaz Bağlantılarının Kurulması**

Packet Tracer içinde:

* Router’a bağlı en az iki bilgisayar veya switch yerleştirilir.
* Router'ın uygun arayüzlerine (örneğin `GigabitEthernet0/0`, `GigabitEthernet0/1`) bağlantılar yapılır.
* Bilgisayarlara IP adresleri atanır (ör. 192.168.1.10 / 192.168.2.10 gibi).

#### **2. Router CLI’a Giriş ve Hostname Ayarı**

```plaintext
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)#
```

> `enable` komutu ile Privileged Exec Mode’a, `configure terminal` ile Global Config Mode’a girilir. Ardından yönlendirici ismi "R1" olarak ayarlanır.

#### **3. Arayüz IP Ayarları ve Aktif Hale Getirme**

```plaintext
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface gigabitEthernet 0/1
R1(config-if)# ip address 192.168.2.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
```

> Her bir ağ için farklı bir arayüze IP adresi atanır ve `no shutdown` ile arayüz etkinleştirilir. Bu sayede router, farklı ağlara çıkış sağlayabilir.

#### **5. Yapılandırmanın Kaydedilmesi**

```plaintext
R1# write memory
```



> Yönlendirici yeniden başlatıldığında ayarların korunması için yapılandırma dosyası kalıcı belleğe kaydedilir.

#### **6. Ağ Testi (Ping)**

Her iki bilgisayardan, router arayüz IP’leri pinglenerek bağlantı kontrolü yapılır. Örnek:

```bash
> ping 192.168.1.1
> ping 192.168.2.1
```

Eğer ping başarılıysa, router yapılandırması temel düzeyde doğrudur.

## **Routing Table İnceleme ve Doğru Yönlendirme Analizi**

Routing table (yönlendirme tablosu), bir yönlendiricinin hangi ağlara nasıl ulaşabileceğini gösteren dinamik bir listedir. Yönlendirici bu tabloyu kullanarak, kendisine gelen IP paketlerini doğru arayüze yönlendirir. Routing tablosu CLI üzerinden `show ip route` komutuyla incelenebilir.

#### **1. Routing Table Görüntüleme**

```plaintext
R1# show ip route
```

Bu komutun çıktısında aşağıdaki gibi satırlar yer alır:

```plaintext
C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
C    192.168.2.0/24 is directly connected, GigabitEthernet0/1
```

> Buradaki `C` ifadesi, bu ağların doğrudan bağlı (Connected) olduğunu gösterir. Router, bu ağlara doğrudan ulaşabilir.

#### **2. Routing Tablosundaki Temel Kodlar**

* **C** → Connected (doğrudan bağlı)
* **S** → Static route (elle yapılandırılmış)
* **D** → EIGRP ile öğrenilmiş yol
* **O** → OSPF ile öğrenilmiş yol
* **R** → RIP ile öğrenilmiş yol
* **S\*** → Default static route (varsayılan yönlendirme)

#### **3. Routing Table Yorumlama Örneği**

Örnek Çıktı:

```plaintext
R1# show ip route

Gateway of last resort is not set

C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
C    192.168.2.0/24 is directly connected, GigabitEthernet0/1
```

* Bu tabloda `R1` router’ının 192.168.1.0 ve 192.168.2.0 ağlarına doğrudan bağlı olduğu görülür.
* Her iki ağ arasında yönlendirme mümkündür çünkü router her iki ağı tanır.
* Eğer farklı router’lar arasında yönlendirme yapılacaksa, o zaman **statik yönlendirme** veya **dinamik protokol** (RIP, OSPF, EIGRP) gerekir.



## **Statik Route Yapılandırma (Packet Tracer Uygulaması)**

Statik yönlendirme (static routing), yönlendiricilere ağ yollarının manuel olarak tanımlandığı bir yönlendirme türüdür. Bu yöntemde, ağ yöneticisi her bir hedef ağa giden yolu açıkça belirtir. Dinamik protokollere göre daha basit ve kontrol edilebilirdir, ancak büyük ağlarda yönetimi zordur.

Cisco Packet Tracer üzerinde, iki veya daha fazla yönlendirici içeren bir ağda statik yönlendirme yapılandırılarak farklı ağlar arasında iletişim sağlanabilir.

---

### **Senaryo Hazırlığı:**

**Topoloji:**

* 2 router (R1 ve R2)
* Her router’a bağlı 1 PC
* Arada bir doğrudan bağlantı (serial veya Ethernet)

**IP Planı:**

* **PC0 ↔ R1 G0/0**: 192.168.1.0/24
* **PC1 ↔ R2 G0/0**: 192.168.2.0/24
* **R1 G0/1 ↔ R2 G0/1**: 10.0.0.0/30 (Backbone)

---

### **Adım 1: Router Arayüz Yapılandırmaları**

#### R1 Üzerinde:

```plaintext
enable
configure terminal
hostname R1

interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface gigabitEthernet 0/1
ip address 10.0.0.1 255.255.255.252
no shutdown
exit
```

#### R2 Üzerinde:

```plaintext
enable
configure terminal
hostname R2

interface gigabitEthernet 0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

interface gigabitEthernet 0/1
ip address 10.0.0.2 255.255.255.252
no shutdown
exit
```

---

### **Adım 2: PC’lere IP Atamaları**

#### PC0:

* IP Address: `192.168.1.10`
* Subnet Mask: `255.255.255.0`
* Default Gateway: `192.168.1.1`

#### PC1:

* IP Address: `192.168.2.10`
* Subnet Mask: `255.255.255.0`
* Default Gateway: `192.168.2.1`

---

### **Adım 3: Statik Route Tanımları**

#### R1'e: 192.168.2.0/24 ağına nasıl ulaşacağını öğret

```plaintext
R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

> Bu komut: 192.168.2.0/24 ağına gönderilecek tüm paketlerin **10.0.0.2** (R2'nin bağlantı noktası) adresine yönlendirilmesini sağlar.

#### R2'ye: 192.168.1.0/24 ağına nasıl ulaşacağını öğret

```plaintext
R2(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

---

### **Adım 4: İletişim Testi (Ping)**

PC0 üzerinden PC1’e ping at:

```bash
> ping 192.168.2.10
```

Eğer yapılandırmalar doğruysa, ping başarılı olur. Statik yönlendirme sayesinde router’lar doğrudan bağlı olmadıkları ağlara da yönlendirme yapabilir.

---

### **Adım 5: Yönlendirme Tablosunun Kontrolü**

#### R1:

```plaintext
R1# show ip route
```

Çıktıda aşağıdakine benzer bir satır görünmelidir:

```plaintext
S    192.168.2.0/24 [1/0] via 10.0.0.2
```

#### R2:

```plaintext
R2# show ip route
```

Çıktı:

```plaintext
S    192.168.1.0/24 [1/0] via 10.0.0.1
```

Bu, statik yönlendirme kurallarının başarıyla eklendiğini gösterir.



## **RIPv2 Yapılandırması (Packet Tracer Uygulaması)**

RIPv2 (Routing Information Protocol version 2), mesafe vektör tabanlı bir dinamik yönlendirme protokolüdür. CIDR (Classless Inter-Domain Routing) desteği sayesinde alt ağ maskeleriyle birlikte çalışır. Aynı zamanda RIPv1’e kıyasla çok daha gelişmiştir ve UDP port 520 üzerinden çalışır.

Bu uygulamada, Cisco Packet Tracer üzerinde üç yönlendirici ile RIPv2 kullanılarak farklı ağlar arasında otomatik yönlendirme yapılandırılacaktır.

---

### **Senaryo Hazırlığı:**

**Topoloji:**

* 3 router (R1, R2, R3)
* Her router’a bağlı 1 PC
* Router’lar point-to-point bağlantılarla birbirine bağlı

**IP Planı:**

| Aygıt | Arayüz | IP Adresi       | Ağ             |
| ----- | ------ | --------------- | -------------- |
| PC0   | —      | 192.168.1.10/24 | 192.168.1.0/24 |
| R1    | G0/0   | 192.168.1.1/24  | 192.168.1.0/24 |
| R1    | G0/1   | 10.0.0.1/30     | 10.0.0.0/30    |
| R2    | G0/0   | 10.0.0.2/30     | 10.0.0.0/30    |
| R2    | G0/1   | 10.0.0.5/30     | 10.0.0.4/30    |
| R3    | G0/0   | 10.0.0.6/30     | 10.0.0.4/30    |
| R3    | G0/1   | 192.168.3.1/24  | 192.168.3.0/24 |
| PC1   | —      | 192.168.3.10/24 | 192.168.3.0/24 |

---

### **Adım 1: Router Arayüz Yapılandırmaları**

#### R1:

```plaintext
enable
configure terminal
hostname R1

interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface gigabitEthernet 0/1
ip address 10.0.0.1 255.255.255.252
no shutdown
exit
```

#### R2:

```plaintext
enable
configure terminal
hostname R2

interface gigabitEthernet 0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
exit

interface gigabitEthernet 0/1
ip address 10.0.0.5 255.255.255.252
no shutdown
exit
```

#### R3:

```plaintext
enable
configure terminal
hostname R3

interface gigabitEthernet 0/0
ip address 10.0.0.6 255.255.255.252
no shutdown
exit

interface gigabitEthernet 0/1
ip address 192.168.3.1 255.255.255.0
no shutdown
exit
```

---

### **Adım 2: PC IP Ayarları**

* **PC0:**

  * IP: `192.168.1.10`
  * Subnet: `255.255.255.0`
  * Gateway: `192.168.1.1`

* **PC1:**

  * IP: `192.168.3.10`
  * Subnet: `255.255.255.0`
  * Gateway: `192.168.3.1`

---

### **Adım 3: RIPv2 Yapılandırması**

#### R1:

```plaintext
router rip
version 2
no auto-summary
network 192.168.1.0
network 10.0.0.0
```

#### R2:

```plaintext
router rip
version 2
no auto-summary
network 10.0.0.0
```

#### R3:

```plaintext
router rip
version 2
no auto-summary
network 192.168.3.0
network 10.0.0.0
```

> `version 2` komutu, RIPv2 kullanılacağını belirtir.
> `no auto-summary` komutu, sınıf temelli yönlendirmeyi kapatır ve CIDR desteği sağlar.
> `network` komutları, yönlendiricinin dahil edeceği ağları belirtir. Burada dikkat edilmesi gereken, **ağ adreslerinin** girilmesidir; arayüz IP’leri değil.

---

### **Adım 4: Doğrulama ve Test**

#### Routing tablolarını kontrol et:

Örneğin R1'de:

```plaintext
R1# show ip route
```

Beklenen çıktı:

```plaintext
R    10.0.0.4/30 [120/1] via 10.0.0.2, 00:00:xx, GigabitEthernet0/1
R    192.168.3.0/24 [120/2] via 10.0.0.2, 00:00:xx, GigabitEthernet0/1
```

#### PC0’dan PC1’e ping at:

```bash
> ping 192.168.3.10
```

Ping başarılıysa RIPv2 yapılandırması doğrudur ve yönlendiriciler birbirlerinin yönlendirme tablolarını öğrenmiştir.



## **OSPF Yapılandırması (Packet Tracer Uygulaması)**

**OSPF (Open Shortest Path First)**, link-state (bağlantı durumu) temelli bir iç ağ yönlendirme protokolüdür. Dijkstra algoritmasını kullanarak en kısa yolu belirler ve büyük, karmaşık ağlarda hiyerarşik yapı desteği sayesinde verimli çalışır. OSPF, yönlendirici kimlikleri (Router ID), alanlar (areas), metrik olarak cost (maliyet) kavramlarını ve multicast IP adreslerini (224.0.0.5, 224.0.0.6) kullanır.

---

### **Senaryo Hazırlığı (Topoloji ve IP Planı)**

**Topoloji:**

* 3 router (R1, R2, R3)
* Her router’a bağlı 1 PC
* Router’lar doğrudan birbirine bağlı
* Tüm yönlendiriciler **Area 0** içinde

**IP Planı:**

| Aygıt | Arayüz | IP Adresi       | Ağ             |
| ----- | ------ | --------------- | -------------- |
| PC0   | —      | 192.168.1.10/24 | 192.168.1.0/24 |
| R1    | G0/0   | 192.168.1.1/24  | 192.168.1.0/24 |
| R1    | G0/1   | 10.0.0.1/30     | 10.0.0.0/30    |
| R2    | G0/0   | 10.0.0.2/30     | 10.0.0.0/30    |
| R2    | G0/1   | 10.0.0.5/30     | 10.0.0.4/30    |
| R3    | G0/0   | 10.0.0.6/30     | 10.0.0.4/30    |
| R3    | G0/1   | 192.168.3.1/24  | 192.168.3.0/24 |
| PC1   | —      | 192.168.3.10/24 | 192.168.3.0/24 |

---

### **Adım 1: Router Arayüz IP Yapılandırmaları**

#### R1:

```plaintext
enable
configure terminal
hostname R1

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 10.0.0.1 255.255.255.252
no shutdown
exit
```

#### R2:

```plaintext
enable
configure terminal
hostname R2

interface g0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
exit

interface g0/1
ip address 10.0.0.5 255.255.255.252
no shutdown
exit
```

#### R3:

```plaintext
enable
configure terminal
hostname R3

interface g0/0
ip address 10.0.0.6 255.255.255.252
no shutdown
exit

interface g0/1
ip address 192.168.3.1 255.255.255.0
no shutdown
exit
```

---

### **Adım 2: PC IP Ayarları**

* **PC0:**

  * IP: `192.168.1.10`
  * Subnet: `255.255.255.0`
  * Gateway: `192.168.1.1`

* **PC1:**

  * IP: `192.168.3.10`
  * Subnet: `255.255.255.0`
  * Gateway: `192.168.3.1`

---

### **Adım 3: OSPF Yapılandırması**

Her router için OSPF konfigürasyonu:

#### R1:

```plaintext
router ospf 1
router-id 1.1.1.1
network 192.168.1.0 0.0.0.255 area 0
network 10.0.0.0 0.0.0.3 area 0
```

#### R2:

```plaintext
router ospf 1
router-id 2.2.2.2
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
```

#### R3:

```plaintext
router ospf 1
router-id 3.3.3.3
network 192.168.3.0 0.0.0.255 area 0
network 10.0.0.4 0.0.0.3 area 0
```

> **router-id** komutuyla her yönlendiriciye benzersiz bir kimlik atanır. Bu, seçim ve tanıma işlemlerinde kullanılır.
> **network** komutu, OSPF’in çalışacağı ağları ve hangi OSPF alanında (area) olduğunu belirtir.
> **0.0.0.255** ve **0.0.0.3** kısımları, wildcard mask’lardır. Alt ağlara uyacak şekilde yazılır.

---

### **Adım 4: OSPF’in Çalıştığını Doğrulama**

#### Komşulukların oluştuğunu kontrol et:

```plaintext
show ip ospf neighbor
```

Beklenen çıktı (örneğin R2'de):

```plaintext
Neighbor ID     Pri   State           Address         Interface
1.1.1.1         1     FULL/DR         10.0.0.1        Gig0/0
3.3.3.3         1     FULL/DR         10.0.0.6        Gig0/1
```

#### Yönlendirme tablosunu kontrol et:

```plaintext
show ip route
```

Beklenen çıktı (örneğin R1’de):

```plaintext
O    192.168.3.0/24 [110/2] via 10.0.0.2, ...
```

> `O` harfi OSPF üzerinden öğrenilen yolları ifade eder.
> `[110/X]` kısmı, OSPF’in varsayılan idari mesafesi olan 110'u ve metrik (cost) bilgisini gösterir.

---

### **Adım 5: Test (Ping)**

**PC0’dan PC1’e ping at:**

```bash
> ping 192.168.3.10
```

Ping başarılıysa OSPF yapılandırman doğru şekilde çalışıyordur.


## **EIGRP Yapılandırması (Packet Tracer Uygulaması)**

**EIGRP (Enhanced Interior Gateway Routing Protocol)**, Cisco tarafından geliştirilmiş, **distance vector** (mesafe vektör) protokolü tabanlı ama **link-state özellikleriyle geliştirilen** hibrit bir yönlendirme protokolüdür. **DUAL (Diffusing Update Algorithm)** algoritması sayesinde hızlı yeniden yapılandırma ve döngü önleme sağlar. Metrik olarak **bandwidth (bant genişliği)** ve **delay (gecikme)** değerlerini kullanır.

EIGRP, **AS (Autonomous System)** numarası kullanarak yönlendiricilerin aynı gruba ait olduğunu belirler. Multicast IP adresi olarak **224.0.0.10** kullanır.

---

### **Senaryo (Topoloji ve IP Planı)**

**Topoloji:**

* 3 router: R1, R2, R3
* Her router’a bir PC bağlı
* Router'lar doğrudan birbirine bağlı (seri veya ethernet bağlantı)

**IP Planı:**

| Aygıt | Arayüz | IP Adresi       | Ağ             |
| ----- | ------ | --------------- | -------------- |
| PC0   | —      | 192.168.1.10/24 | 192.168.1.0/24 |
| R1    | G0/0   | 192.168.1.1/24  | 192.168.1.0/24 |
| R1    | G0/1   | 10.0.0.1/30     | 10.0.0.0/30    |
| R2    | G0/0   | 10.0.0.2/30     | 10.0.0.0/30    |
| R2    | G0/1   | 10.0.0.5/30     | 10.0.0.4/30    |
| R3    | G0/0   | 10.0.0.6/30     | 10.0.0.4/30    |
| R3    | G0/1   | 192.168.3.1/24  | 192.168.3.0/24 |
| PC2   | —      | 192.168.3.10/24 | 192.168.3.0/24 |

---

### **Adım 1: Router Arayüz Yapılandırmaları**

#### R1:

```plaintext
enable
configure terminal
hostname R1

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 10.0.0.1 255.255.255.252
no shutdown
exit
```

#### R2:

```plaintext
enable
configure terminal
hostname R2

interface g0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
exit

interface g0/1
ip address 10.0.0.5 255.255.255.252
no shutdown
exit
```

#### R3:

```plaintext
enable
configure terminal
hostname R3

interface g0/0
ip address 10.0.0.6 255.255.255.252
no shutdown
exit

interface g0/1
ip address 192.168.3.1 255.255.255.0
no shutdown
exit
```

---

### **Adım 2: PC IP Ayarları**

* **PC0:**

  * IP: `192.168.1.10`
  * Subnet Mask: `255.255.255.0`
  * Default Gateway: `192.168.1.1`

* **PC2:**

  * IP: `192.168.3.10`
  * Subnet Mask: `255.255.255.0`
  * Default Gateway: `192.168.3.1`

---

### **Adım 3: EIGRP Yapılandırması (AS: 100)**

#### R1:

```plaintext
router eigrp 100
network 192.168.1.0 0.0.0.255
network 10.0.0.0 0.0.0.3
no auto-summary
```

#### R2:

```plaintext
router eigrp 100
network 10.0.0.0 0.0.0.3
network 10.0.0.4 0.0.0.3
no auto-summary
```

#### R3:

```plaintext
router eigrp 100
network 192.168.3.0 0.0.0.255
network 10.0.0.4 0.0.0.3
no auto-summary
```

> `network` komutu ile yönlendiricideki hangi ağlar EIGRP’ye dahil edileceği belirlenir.
> `no auto-summary` komutu, EIGRP’nin sınıf temelli otomatik ağ özetlemesini devre dışı bırakır.

---

### **Adım 4: Doğrulama ve Gözlem**

#### Komşulukların Oluştuğunu Kontrol Et:

```plaintext
show ip eigrp neighbors
```

> Her router, doğrudan bağlı olduğu diğer router’larla komşu (neighbor) olur.

#### Yönlendirme Tablosunu Kontrol Et:

```plaintext
show ip route
```

> EIGRP ile öğrenilen yollar `D` harfiyle gösterilir (D = DUAL):

```
D    192.168.3.0/24 [90/2172416] via 10.0.0.2, ...
```

#### EIGRP Topolojisini Görmek:

```plaintext
show ip eigrp topology
```

---

### **Adım 5: İletişim Testi (Ping)**

**PC0'dan PC2'ye ping:**

```bash
ping 192.168.3.10
```

Eğer ping başarılıysa, EIGRP yönlendirme yapılandırması doğru çalışıyordur.



## **Router-on-a-Stick (VLAN Arası Yönlendirme) Yapılandırması**

###  **Router-on-a-Stick Nedir?**

Router-on-a-Stick, birden fazla VLAN’ın bulunduğu bir ağda **VLAN’lar arası yönlendirme (inter-VLAN routing)** sağlamak için kullanılan bir yöntemdir. Bu yöntemde bir router (veya Layer 3 Switch) üzerinde **tek bir fiziksel arayüz** kullanılır, ancak bu arayüz üzerinde **alt arayüzler (sub-interfaces)** tanımlanarak her bir VLAN’a yönlendirme yapılır.

Bu yapılandırma genellikle **Layer 2 switch + Router** kombinasyonuyla yapılır ve maliyeti düşürmek için tercih edilir.

---

###  **Senaryo:**

**Topoloji:**

* Bir adet Layer 2 switch
* Bir adet router (örnek: R1)
* İki VLAN: VLAN 10 (Muhasebe), VLAN 20 (İK)
* Her VLAN’a ait birer PC

**IP Planı:**

| VLAN | Aygıt | IP Adresi              | VLAN ID | Ağ           |
| ---- | ----- | ---------------------- | ------- | ------------ |
| 10   | PC0   | 192.168.10.10          | 10      | 192.168.10.0 |
| 20   | PC1   | 192.168.20.10          | 20      | 192.168.20.0 |
| —    | R1    | G0/0.10 = 192.168.10.1 |         |              |

```
            G0/0.20 = 192.168.20.1 | — | —             |
```

---

###  **Adım Adım Yapılandırma**

### 1. **Switch Yapılandırması (VLAN Oluşturma ve Port Atama)**

#### VLAN Oluştur:

```bash
enable
configure terminal
vlan 10
name Muhasebe
exit
vlan 20
name IK
exit
```

#### Portlara VLAN Ata (örneğin: PC0 = Fa0/1, PC1 = Fa0/2):

```bash
interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
exit

interface fastEthernet 0/2
switchport mode access
switchport access vlan 20
exit
```

#### Router’a Giden Portu Trunk Yap:

```bash
interface fastEthernet 0/24
switchport mode trunk
exit
```

---

### 2. **Router Yapılandırması (Alt Arayüzler ve IP Atamaları)**

#### Alt arayüzleri tanımla:

```bash
enable
configure terminal
interface gigabitEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit

interface gigabitEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit

interface gigabitEthernet 0/0
no shutdown
exit
```

> `encapsulation dot1Q [VLAN_ID]` komutu, o alt arayüzün hangi VLAN'a ait olduğunu belirtir.
> Alt arayüz ismi `interface [ana_arayüz].[vlan_id]` şeklinde olmalıdır.

---

### 3. **PC'lerde IP Ayarlarını Yap**

#### PC0 (VLAN 10):

* IP: `192.168.10.10`
* Subnet Mask: `255.255.255.0`
* Gateway: `192.168.10.1`

#### PC1 (VLAN 20):

* IP: `192.168.20.10`
* Subnet Mask: `255.255.255.0`
* Gateway: `192.168.20.1`

---

### 4. **İletişimi Test Et (Ping)**

**PC0’dan PC1’e ping gönder:**

```bash
ping 192.168.20.10
```

Eğer yapılandırma doğruysa, farklı VLAN’larda bulunan bu iki bilgisayar birbirleriyle iletişim kurabilir.

---

### 🔍 **Doğrulama Komutları**

#### Router'da:

```bash
show ip interface brief
show running-config
```

#### Switch'te:

```bash
show vlan brief
show interfaces trunk
```


##  **Router’da DHCP Sunucusu Yapılandırması**

###  **DHCP Nedir?**

**DHCP (Dynamic Host Configuration Protocol)**, istemcilere (PC, printer, IP kamera, vb.) otomatik olarak IP adresi, alt ağ maskesi, varsayılan ağ geçidi, DNS gibi ağ yapılandırma bilgilerini atayan bir ağ protokolüdür.

Bir ağda router, Layer 3 switch veya ayrı bir DHCP sunucusu bu hizmeti sağlayabilir. Küçük ve orta ölçekli ağlarda Cisco router üzerinde DHCP servisi aktif hale getirilerek kolayca IP dağıtımı yapılabilir.

---

### **Senaryo:**

* Bir router (örnek: R1)
* Bir switch
* Switch’e bağlı bir PC
* Ağ: `192.168.1.0/24`
* DHCP ile dağıtılacak IP aralığı: `192.168.1.100 – 192.168.1.150`
* Varsayılan ağ geçidi: `192.168.1.1`

---

###  **Adım 1: Router Arayüzüne IP Ver**

Öncelikle, IP dağıtımı yapılacak ağa bağlı olan router arayüzüne IP adresi verilir:

```bash
enable
configure terminal

interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

> Bu IP, istemcilere dağıtılacak IP'ler için **default gateway** olarak kullanılacaktır.

---

###  **Adım 2: DHCP Havuzu Oluştur**

```bash
ip dhcp pool OFIS_AĞI
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8 1.1.1.1
lease 7
```

Açıklamalar:

* `ip dhcp pool [HAVUZ_ADI]`: Yeni bir DHCP havuzu oluşturur.
* `network`: Dağıtılacak IP adreslerinin bulunduğu ağı belirtir.
* `default-router`: DHCP istemcilerine atanacak varsayılan ağ geçidi.
* `dns-server`: Varsayılan olarak atanacak DNS sunucuları.
* `lease`: IP adreslerinin kira süresi (gün cinsinden). `lease 7` → 7 gün.

---

### **Adım 3: Dağıtılmayacak IP’leri Hariç Tut (Excluded Address)**

Örneğin: `192.168.1.1` router için, `192.168.1.2-99` sunucu ve yazıcılar için kullanılacaksa:

```bash
ip dhcp excluded-address 192.168.1.1 192.168.1.99
```

Bu komutlar, belirli IP adreslerinin istemcilere atanmasını **engeller**. Genelde router, sunucu ve printer gibi cihazlar için manuel IP ayrılır ve DHCP’den hariç tutulur.

---

##  **PC Üzerinde DHCP Testi (Packet Tracer)**

1. Packet Tracer’da PC’ye tıkla.
2. **Desktop > IP Configuration** sekmesine gel.
3. “DHCP” seçeneğine tıkla.
4. PC, router’dan otomatik IP alır.

> Alınan bilgiler: IP adresi, subnet maskesi, varsayılan ağ geçidi ve DNS sunucuları.

### DHCP Durumunu Görüntüleme:

```bash
show ip dhcp binding
```

→ IP alan istemcileri gösterir.

### DHCP Hatalarını Görüntüleme:

```bash
show ip dhcp conflict
```

→ IP çakışması varsa gösterir.

### DHCP Konfigürasyonunu Görüntüleme:

```bash
show running-config | section dhcp
```


##  **NAT (Network Address Translation) YAPILANDIRMASI**

**NAT (Network Address Translation)**, bir ağın özel (private) IP adreslerini, genel (public) IP adreslerine çevirmeyi sağlayan bir tekniktir. Bu, genellikle birden fazla cihazın tek bir genel IP adresi ile internet erişimini paylaşmasını sağlamak için kullanılır. NAT, genellikle güvenlik amacıyla da tercih edilir, çünkü özel IP adresleri dış dünya tarafından doğrudan erişilemez.

NAT, **gizliliği artırır** ve aynı zamanda **IP adresi tasarrufu** sağlar, çünkü genel IP'ler sınırlıdır. Ev ağlarında ve küçük ofislerde genellikle kullanılır.

---

###  **NAT Türleri**

### 1. **Static NAT (Statik NAT)**

**Static NAT**, her özel IP adresinin **tek bir genel IP** ile eşlenmesi durumudur. Bu eşleme sabittir, yani her zaman aynı özel IP adresi aynı genel IP adresine çevrilir.

**Kullanım Alanları:**

* İnternet üzerinde erişilmesi gereken cihazlar için (örneğin web sunucusu, FTP sunucusu, oyun sunucusu).
* Dışarıdan gelen trafiğin belirli bir iç cihazı hedef alması gerektiği durumlar.

**Örnek:**

* **192.168.10.10** IP’sine sahip bir sunucunun internetten **200.1.1.100** IP’siyle erişilmesini sağlayalım.

### Yapılandırma:

```bash
interface gigabitEthernet 0/0
ip address 192.168.10.1 255.255.255.0
ip nat inside
exit

interface gigabitEthernet 0/1
ip address 200.1.1.1 255.255.255.0
ip nat outside
exit

ip nat inside source static 192.168.10.10 200.1.1.100
```

#### Açıklama:

* `ip nat inside`: Router’ın iç arayüzü, yani özel IP’lerin bulunduğu ağ.
* `ip nat outside`: Router’ın dış arayüzü, yani genel IP’nin bulunduğu ağ.
* `ip nat inside source static`: Bu komut, belirli bir iç IP’yi sabit bir dış IP ile eşler.

---

### 2. **Dynamic NAT (Dinamik NAT)**

**Dynamic NAT**, özel IP adreslerinin bir grup genel IP adresiyle eşlenmesi işlemidir. Bu eşlemeler dinamik olarak yapılır, yani her seferinde farklı bir genel IP atanabilir. **Özel IP’ler** için belirli bir **genel IP havuzu** oluşturulur ve bu havuzdaki IP'ler, ihtiyaç duyulduğunda her bağlantı için atanır.

**Kullanım Alanları:**

* Çok sayıda kullanıcıya internet erişimi sağlanması gerektiğinde, ancak her kullanıcıya sabit bir genel IP verilmemesi durumunda.

**Örnek:**

* Özel ağda bulunan 192.168.10.0/24 IP bloğundaki cihazlar, 200.1.1.10-200.1.1.20 IP havuzunu kullanarak internete çıkabilirler.

### Yapılandırma:

```bash
ip nat pool GENEL_IPLER 200.1.1.10 200.1.1.20 netmask 255.255.255.0

access-list 1 permit 192.168.10.0 0.0.0.255

ip nat inside source list 1 pool GENEL_IPLER
```

#### Açıklama:

* `ip nat pool GENEL_IPLER`: NAT havuzunun tanımlanması. Bu havuz, özel IP’lerin dışa çıkarken kullanacağı genel IP’leri içerir.
* `access-list 1 permit 192.168.10.0 0.0.0.255`: NAT işlemi için geçerli olan IP aralığını belirler. Bu liste, 192.168.10.0/24 aralığındaki IP’lere uygulanır.
* `ip nat inside source list 1 pool GENEL_IPLER`: Bu komut, erişim listesi (ACL) ile belirlenen IP aralığındaki cihazlara, NAT havuzundaki genel IP’leri atar.

---

### 3. **PAT (Port Address Translation) - NAT Overload**

**PAT**, çok sayıda cihazın **tek bir genel IP adresi** üzerinden internete çıkabilmesini sağlar. Ancak, her cihaz farklı **port numaraları** kullanarak dışa çıkar. Bu yöntem, genellikle **NAT Overload** olarak adlandırılır. Birçok cihaz tek bir genel IP ile internete bağlanabilir, her cihazın bağlantısı farklı port numarası ile ayrılır.

**Kullanım Alanları:**

* Ev ağlarında veya küçük ofislerde kullanılan, birkaç cihazın tek bir genel IP ile internete çıkmasını sağlayan yöntem.

**Örnek:**

* 192.168.10.0/24 ağındaki cihazlar, tek bir **200.1.1.1** genel IP adresini kullanarak internete çıkacak.

### Yapılandırma:

```bash
access-list 1 permit 192.168.10.0 0.0.0.255

ip nat inside source list 1 interface gigabitEthernet 0/1 overload
```

#### Açıklama:

* `overload`: Bu komut, aynı genel IP ile birden fazla özel IP’nin çıkmasına izin verir. Farklı port numaraları kullanarak her cihaz farklı bağlantı kurar.
* `interface gigabitEthernet 0/1`: Genel IP’nin bulunduğu dış arayüz.
* `access-list 1`: 192.168.10.0/24 ağındaki cihazlar bu listeye dahil olur ve NAT yapılır.

---

###  **NAT Yapılandırmalarını Paket Tracer’da Test Etmek**

1. **Özel IP’lerin Genel IP’ye Çevrilmesi:**
   Her bir cihazın IP ayarlarını yaparak, doğru NAT işleminin yapıldığını doğrulamak mümkündür. Bunun için `show ip nat translations` komutunu kullanabilirsiniz.

2. **Ping Testi:**

   * **Özel IP ile Ping:** 192.168.10.x IP adresine sahip cihazlar, 200.1.1.x IP adresi üzerinden dışarıya çıkabilir.
   * **Genel IP ile Ping:** Dışa çıkmaya çalışan cihaz, dış dünyaya bağlandığında **PAT** sayesinde her cihaz için farklı port numaraları atanır.

3. **Doğrulama Komutları:**
   NAT yapılandırmasının doğru yapıldığını doğrulamak için aşağıdaki komutlar kullanılır:

   ```bash
   show ip nat translations
   ```

   Bu komut, router’ın NAT eşlemelerini listeleyecek ve hangi özel IP’nin hangi genel IP ile eşlendiğini gösterecektir.

   ```bash
   show ip nat statistics
   ```

   Bu komut ise NAT istatistiklerini gösterir, özellikle kullanılan genel IP’ler ve NAT işlemleri hakkında bilgi sağlar.



## Router Üzerinde Access Control List (ACL) Yapılandırılması



####  **ACL Nedir? Neden Kullanılır?**

ACL (Access Control List), bir router’ın veya switch’in trafiği filtrelemesini sağlayan kurallar bütünüdür. Her ACL, ağ trafiği üzerinde bir **güvenlik duvarı gibi çalışır**. Router üzerindeki arayüzlere uygulanarak, belirli bir trafik türüne **izin verilir (permit)** veya **engellenir (deny)**.

ACL’ler aşağıdaki sebeplerle kullanılır:

* **Ağ Güvenliği**: Belirli ağlar veya kullanıcılar arasında erişimi sınırlamak.
* **Trafik Yönetimi**: Hassas veya önemli servislere yalnızca belirli kullanıcıların erişmesine izin vermek.
* **Politika Uygulama**: Firma içi kurallara göre belirli zamanlarda veya belirli kullanıcı gruplarına erişim sağlamak/engellemek.
* **Veri Akışını Sınırlandırmak**: Broadcast/multicast trafiği veya yoğun uygulama trafiğini engellemek.


###  ACL'nin Router Üzerindeki Yeri

Bir router bir paketi aldığında aşağıdaki sıralamaya göre işlem yapar:

1. **Routing Table’e bakar**: Paket nereye gidecek?
2. **ACL varsa** kontrol eder: Bu pakete izin veriliyor mu?
3. **Eğer izinliyse**, paket yönlendirilir. Değilse, düşürülür.

ACL'ler, **arayüzlere** (`interface`) uygulanır ve 2 yönü vardır:

* **in**: Paketin router arayüzüne *girişinde* kontrol.
* **out**: Paketin router arayüzünden *çıkışında* kontrol.


###  ACL Türleri: Ayrıntılı Karşılaştırma

#### 1.  Standard ACL (1-99)

##### Özellikleri:

* Sadece **kaynak IP adresini** kontrol eder.
* Daha basit ve hızlı çalışır.
* Belirli bir kaynaktan gelen tüm trafiği tamamen engellemek veya izin vermek için kullanılır.
* Sadece *L3 (network layer)* filtreleme yapar.

##### Kısıtlamalar:

* Trafiğin **protokolü (TCP, UDP, ICMP vs.)** ve **port numarası** gibi bilgileri göz önünde bulundurmaz.
* Geniş kapsamlı olduğundan fazla hassas filtreleme yapılamaz.

##### Örnek:

```bash
access-list 10 deny 192.168.1.0 0.0.0.255
access-list 10 permit any
interface GigabitEthernet0/0
ip access-group 10 out
```

Açıklama:

* `192.168.1.0/24` kaynak adresli tüm trafiği engeller.
* Geri kalan her şeye izin verilir.
* ACL, arayüzden çıkan trafiğe uygulanır.


#### 2.  Extended ACL (100-199)

##### Özellikleri:

* **Kaynak ve hedef IP**, **port numarası**, **protokol (TCP, UDP, ICMP vs.)** gibi çok daha detaylı kriterlerle filtreleme yapabilir.
* Hem giriş hem de çıkış yönünde uygulanabilir.
* **L3 (IP)** ve **L4 (port/protokol)** seviyelerinde çalışır.
* Karmaşık ağ güvenlik politikalarını tanımlamak mümkündür.

##### Güçlü Yanları:

* Belirli kullanıcıların sadece belirli servislere erişimini sağlayabilir.
* Hem giriş hem çıkış yönünde ayrı filtreler uygulanabilir.

##### Örnek:

```bash
access-list 110 permit tcp 192.168.10.0 0.0.0.255 host 192.168.20.10 eq 80
access-list 110 deny tcp any any
access-list 110 permit ip any any
interface GigabitEthernet0/0
ip access-group 110 in
```

Açıklama:

* Sadece `192.168.10.0/24` kaynak adresli istemciler, `192.168.20.10` IP adresine **HTTP (port 80)** üzerinden erişebilir.
* Diğer tüm TCP bağlantıları engellenir.
* IP dışındaki tüm protokollere izin verilir (örneğin ICMP - ping).


###  Wildcard Mask 

ACL’lerde klasik subnet mask yerine **wildcard mask** kullanılır.


Örnek:

* IP: `192.168.1.0`
* Wildcard Mask: `0.0.0.255`
* Bu ifade, `192.168.1.0 - 192.168.1.255` aralığını kapsar.


###  ACL Uygulama Yönü: “in” ve “out” Farkı

#### in:

* Paket **arayüze gelirken** filtrelenir.
* Örn: `ip access-group 110 in`

#### out:

* Paket **arayüzden çıkarken** filtrelenir.
* Örn: `ip access-group 10 out`

**Not:** ACL’yi uygulayacağınız yönü doğru belirlemezseniz filtreleme çalışmaz veya hatalı olur.


###  ACL Yazımında Sıra Neden Önemlidir?

ACL’ler **ilk eşleşen kuralda durur.** Yani en özel kural üstte, en genel kural altta olmalıdır. Aksi takdirde tüm trafik engellenebilir.

```bash
access-list 100 deny tcp any any eq 80
access-list 100 permit ip any any
```

Yukarıdaki ACL, **HTTP trafiğini engeller**, diğer tüm trafiğe izin verir.



###  Kontrol ve Hata Ayıklama Komutları

| Komut                 | Açıklama                                            |
| --------------------- | --------------------------------------------------- |
| `show access-lists`   | ACL içeriklerini listeler.                          |
| `show ip interface`   | Arayüze hangi ACL’nin uygulandığını gösterir.       |
| `show running-config` | ACL’leri ve yapılandırmayı gösterir.                |
| `debug ip packet`     | Gerçek zamanlı trafik izleme (dikkatli kullanılır). |



###  Varsayılan `deny any`

ACL tanımladığınızda, sonunda **gizli bir `deny any`** kuralı otomatik olarak eklenir.

Bu nedenle **izin verilecek trafiği açıkça tanımlamak**, ardından genel `permit` kuralları ile desteklemek gerekir.



###  Örnek Topoloji Senaryosu

#### Topoloji:

* PC1 → 192.168.1.10
* PC2 → 192.168.2.20
* Router üzerindeki G0/0 → 192.168.1.1
* Router üzerindeki G0/1 → 192.168.2.1

Amaç: PC1 sadece PC2’ye ICMP (ping) gönderebilsin. Diğer tüm trafiği engelle.

```bash
access-list 120 permit icmp host 192.168.1.10 host 192.168.2.20
access-list 120 deny ip any any
interface GigabitEthernet0/0
ip access-group 120 in
```


##  Router Güvenliği: 

Bir router’ın güvenliği, yalnızca ağ içerisindeki saldırılara karşı değil, aynı zamanda fiziksel erişime sahip kişilere ve uzaktan bağlantı kuran kullanıcılarına karşı da sağlanmalıdır. Bu nedenle **şifre yönetimi**, **erişim kontrolü** ve **erişim yetkilendirmesi**, router güvenliğinin temel taşlarındandır.

####  1. Erişim Şifreleri Türleri

Cisco router’larda erişim katmanlarına göre farklı seviyelerde şifreleme mümkündür:

* **Console Password**: Fiziksel olarak router’a bağlı konsol portundan erişimi sınırlar.
* **VTY Password (Virtual Terminal)**: Telnet/SSH oturumları için şifre doğrulaması sağlar.
* **Enable Password / Enable Secret**: Kullanıcıların User EXEC moddan Privileged EXEC moda geçmesini sınırlar.


####  2. `enable password` vs. `enable secret`

Bu komutlar router’ın **privileged mode (enable moduna)** geçişini kontrol eder. Ancak aralarındaki farklar çok önemlidir:

| Özellik           | `enable password`                                       | `enable secret`         |
| ----------------- | ------------------------------------------------------- | ----------------------- |
| Şifreleme         | Düz metin (plaintext)                                   | MD5 ile şifrelenmiş     |
| Güvenlik Seviyesi | Düşük                                                   | Yüksek                  |
| Öncelik           | `enable secret` varsa `enable password` göz ardı edilir | Her zaman tercih edilir |

**Öneri**: Daima `enable secret` kullanın. `enable password` yalnızca eski cihazlarla geriye uyumluluk içindir.

**Örnek:**

```bash
enable secret Sifre123
```

####  3. Console Port Güvenliği

Console portu, router’a fiziksel erişimle doğrudan komut girişi yapılmasını sağlar. Bu nedenle mutlaka şifre ile korunmalıdır.

**Yapılandırma:**

```bash
line console 0
password Konsol123
login
```

Açıklama:

* `line console 0`: Console portunu seçer.
* `password`: Şifre belirlenir.
* `login`: Şifre istemesi için bu komut gereklidir.



####  4. VTY (Virtual Terminal) Hatları – Telnet/SSH Güvenliği

Router’a uzaktan erişim Telnet veya SSH ile sağlanabilir. Bu hatlar `line vty 0 4` komutu ile yapılandırılır.

**Yapılandırma:**

```bash
line vty 0 4
password Uzaktan123
login
transport input ssh
```

Açıklama:

* `password`: VTY bağlantıları için şifre belirlenir.
* `login`: Şifre kullanılsın.
* `transport input ssh`: Yalnızca SSH bağlantısına izin ver, Telnet'i engelle.

**Ek Güvenlik:** VTY hatlarında kullanıcı doğrulamasını daha gelişmiş hale getirmek için “username/password” kimlik doğrulaması da yapılabilir:

```bash
username admin privilege 15 secret Admin123
line vty 0 4
login local
transport input ssh
```


###  Router’da Banner Mesajları ve Kullanım Amacı

Router'larda **banner (açılış mesajı)** kullanımı, özellikle yasal uyarılar vermek, kullanıcıları bilgilendirmek ve sistemin sorumluluğunu hatırlatmak için kullanılır. Router’a erişen herkes bu mesajı görür.

####  1. Banner Türleri

| Tür            | Açıklama                                                                   |
| -------------- | -------------------------------------------------------------------------- |
| `banner motd`  | Message Of The Day – Günlük bilgilendirme mesajı. En yaygın kullanılandır. |
| `banner login` | Kullanıcı girişinden hemen önce gösterilir.                                |
| `banner exec`  | Kullanıcı oturum açtıktan sonra gösterilir.                                |

####  2. En Yaygın Kullanım: `banner motd`

**Örnek:**

```bash
banner motd #
Yetkisiz erişim yasaktır! Bu sistem yalnızca yetkili personel içindir!
#
```

Açıklama:

* `#` karakteri başlangıç ve bitiş ayırıcıdır. Herhangi bir karakter kullanılabilir, ancak aynı karakterle açılıp kapanmalıdır.
* Bu mesaj, kullanıcı **giriş ekranında** görünür.

####  3. Yasal Önemi

Bazı kurumlar için bu mesajlar, kullanıcıya **yasal sorumluluğunu** hatırlatmak için önemlidir. Örneğin, aşağıdaki gibi uyarılar içerir:

```
Uyarı: Bu cihaza izinsiz erişim yasaktır. Tüm işlemler kaydedilmektedir.
```

Bu tür mesajlar, ileride hukuki işlemlerde kanıt olarak kullanılabilir.

##  Router’larda Zaman Ayarı ve NTP Yapılandırması

Router’larda doğru zaman ayarı, günlük kayıtlarının (log), zaman damgalı olayların, güvenlik kontrollerinin ve zaman bağımlı ACL gibi yapıların sağlıklı işlemesi için kritik öneme sahiptir. Zaman ayarı manuel olarak yapılabileceği gibi, ağ üzerinden otomatik olarak **NTP (Network Time Protocol)** ile senkronize edilebilir.

####  1. Manuel Zaman ve Tarih Ayarlama

Manuel olarak tarih ve saat şu şekilde ayarlanabilir:

```bash
clock set HH:MM:SS DAY MONTH YEAR
```

**Örnek:**

```bash
clock set 10:45:00 5 May 2025
```

> Bu komut yalnızca geçici bir zaman ayarıdır. Cihaz yeniden başlatıldığında silinir çünkü çoğu router’da donanımsal saat (battery-backed clock) bulunmaz.

####  2. Saat Dilimini Ayarlama

Zaman dilimi ayarlamak için:

```bash
clock timezone ZONE_NAME OFFSET
```

**Örnek:**

```bash
clock timezone TR +3
```

Bu komut Türkiye için UTC+3 zaman dilimini tanımlar.

####  3. NTP ile Otomatik Zaman Senkronizasyonu

NTP (Network Time Protocol), router’ın bir zaman sunucusuna bağlanarak doğru zamanı otomatik olarak almasını sağlar.

##### NTP Sunucusunun Ayarlanması

```bash
ntp server 192.168.1.100
```

Yukarıdaki komut, router'ı belirtilen IP adresindeki NTP sunucusuna bağlar. Eğer internetteki bir sunucu kullanılacaksa DNS desteği varsa şu şekilde de olabilir:

```bash
ntp server time.google.com
```

##### NTP Durumunu Görüntüleme

```bash
show ntp status
```

Bu komut ile router’ın zaman sunucusuna ulaşıp ulaşmadığı ve senkronize olup olmadığı görülebilir.

##### NTP ile Doğrulama (Opsiyonel)

Güvenlik için, NTP sunucusu kimlik doğrulaması yapılabilir. Bunun için NTP anahtarı ve doğrulama mekanizması yapılandırılır:

```bash
ntp authenticate
ntp authentication-key 1 md5 NTPsifre123
ntp trusted-key 1
ntp server 192.168.1.100 key 1
```
## Packet Tracer CLI Uygulaması: NTP Yapılandırması

###  Senaryo:

* **Router1** bir NTP sunucusuna bağlanacak.
* NTP sunucusu olarak bir başka router (örneğin: Router2) yapılandırılacak.
* Router1 zamanı Router2’den alacak.

---

###  1. NTP Sunucusu (Router2) Yapılandırması

```bash
hostname Router2
clock set 12:00:00 5 May 2025
ntp master 1
```

> `ntp master 1` → Router’ı yerel bir NTP sunucusu yapar (Stratum 1).

---

###  2. Router1 Üzerinde NTP İstemcisi Yapılandırması

```bash
hostname Router1
interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

clock timezone TR +3
ntp server 192.168.1.2
```

> Router2’nin IP’si 192.168.1.2 olarak varsayılmıştır.

Zamanın başarıyla alınıp alınmadığını kontrol etmek için:

```bash
show ntp status
```

> Senkronizasyon sağlandıysa “Clock is synchronized” mesajı görünür.

---


## Uzaktan Router Yönetimi: Telnet ve SSH Yapılandırması

Router’a fiziksel erişim olmadan uzaktan CLI bağlantısı yapmak mümkündür. Bunun için **VTY (Virtual Terminal Lines)** aracılığıyla Telnet veya SSH kullanılır. Telnet veri iletimini şifrelemez, SSH ise güvenli ve şifreli bir bağlantı sağlar.

####  1. Telnet Yapılandırması (Güvenli Değildir)

**Adımlar:**

1. Router’da bir IP adresi atanmış aktif bir arayüz olmalıdır.
2. VTY hatlarına şifre atanmalıdır.

```bash
line vty 0 4
password Telnet123
login
```

**Uzak bağlantı:**

```bash
telnet 192.168.1.1
```

>  Telnet oturumlarında tüm veri düz metin olarak iletildiğinden **güvenli değildir**. SSH tercih edilmelidir.


####  2. SSH Yapılandırması (Güvenli Yöntem)

SSH yapılandırması için router’ın hostname’i, domain’i ve RSA anahtarları ayarlanmalıdır. Ardından yerel kullanıcı tanımlanır ve VTY hatları SSH’a yönlendirilir.

**Adımlar:**

1. Hostname ve domain adı belirlenir:

```bash
hostname Router1
ip domain-name example.local
```

2. RSA anahtarı oluşturulur:

```bash
crypto key generate rsa
```

> Key uzunluğu sorulduğunda genellikle **1024 veya 2048** seçilir.

3. Kullanıcı oluşturulur:

```bash
username admin privilege 15 secret Admin123
```

4. VTY hatları yapılandırılır:

```bash
line vty 0 4
login local
transport input ssh
```

5. SSH sürümü zorunlu kılınabilir (opsiyonel ama önerilir):

```bash
ip ssh version 2
```

**SSH ile bağlantı komutu (istemci tarafından):**

```bash
ssh -l admin 192.168.1.1
```

####  SSH Durumunu Görme

```bash
show ip ssh
```

Bu komut ile SSH’ın aktif olup olmadığı, sürümü ve zaman aşımı değerleri kontrol edilir.

## Packet Tracer CLI Uygulaması: SSH Yapılandırması

### Senaryo:

* Router'a uzaktan SSH ile bağlanmak istiyoruz.
* Router’a bir IP atanmış ve erişilebilir durumda olmalı.
* SSH sürüm 2 ve yerel kullanıcı doğrulaması yapılacak.



###  1. Router SSH Sunucusu Olarak Yapılandırma

```bash
hostname Router1
ip domain-name example.local
crypto key generate rsa
```

> RSA key boyutu istendiğinde 1024 veya 2048 yazın.

---

### 2. Kullanıcı Oluşturma

```bash
username admin privilege 15 secret Admin123
```

---

### 3. Arayüz ve IP Ayarları

```bash
interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

---

### 4. VTY Hatları SSH için Yapılandırma

```bash
line vty 0 4
login local
transport input ssh
exit
```

---

### 5. SSH Sürümünü Belirleme (Opsiyonel ama önerilir)

```bash
ip ssh version 2
```

###  6. Durum Kontrolü

```bash
show ip ssh
```

### 7. SSH ile Bağlanma (PC Terminal’den)

1. Packet Tracer’daki bir PC'yi aç.
2. Desktop > Terminal > SSH
3. Aşağıdaki bilgileri gir:

* **Host**: 192.168.1.1
* **Port**: 22
* **Username**: admin
* **Password**: Admin123

Bağlantı sağlandığında router CLI ekranı gelir. Artık router’a güvenli bir şekilde uzaktan erişim sağlanmıştır.


Elbette. Aşağıda yalnızca "**IPv6 Yönlendirme ve Yapılandırma (Statik ve OSPFv3)**" başlığı ayrıntılı bir şekilde açıklanmıştır. Başka başlık eklenmemiştir.



##  IPv6 Yönlendirme ve Yapılandırma (Statik ve OSPFv3)

IPv6, IPv4'ün adresleme sınırlamalarını aşmak için geliştirilmiş yeni nesil bir internet protokolüdür. IPv6 yönlendirme, IPv6 adreslerini temel alarak ağlar arasında veri paketlerinin iletilmesini sağlar. IPv6, yönlendirme protokolleri açısından IPv4’e benzerlik gösterse de yapılandırma ve protokol uyarlamaları açısından önemli farklar içerir.



##  IPv6 Statik Yönlendirme

Statik yönlendirme, ağ yöneticisinin manuel olarak yönlendirme yollarını tanımladığı basit ve kontrollü bir yönlendirme yöntemidir.

###  Yapılandırma Adımları

1. **Arayüzlere IPv6 Adresi Verilmesi**

```bash
interface g0/0
ipv6 address 2001:DB8:1::1/64
no shutdown
exit
```

2. **Statik Route Tanımlama**

```bash
ipv6 route <hedef_ağ> <çıkış_arayüzü veya next-hop>
```

**Örnek:**

```bash
ipv6 route 2001:DB8:2::/64 2001:DB8:1::2
```

> Bu komut, hedef ağ olan `2001:DB8:2::/64`’e ulaşmak için next-hop olarak `2001:DB8:1::2` IPv6 adresini kullanır.

###  Avantajları

* Kontrol tamamen yöneticidedir.
* Küçük ağlarda yapılandırması kolaydır.

###  Dezavantajları

* Büyük ağlarda yönetimi karmaşıklaşır.
* Otomatik adaptasyon yoktur (topoloji değişimlerinde manuel müdahale gerekir).



##  OSPFv3 ile IPv6 Dinamik Yönlendirme

**OSPFv3**, IPv6 için özel olarak tasarlanmış OSPF sürümüdür. OSPFv2 IPv4 ile çalışırken, OSPFv3 doğrudan IPv6 adresleriyle çalışır.

###  Temel Özellikler

* Link-state protokolüdür.
* Router ID tanımlanmalıdır (IPv4 adresi formatında, ama IPv4 bağlantısı gerekmez).
* Her bir arayüz üzerinden `ipv6 ospf` komutlarıyla yapılandırılır.
* Multicast adresleri:

  * All OSPF routers: `FF02::5`
  * All DR/BDR routers: `FF02::6`


###  OSPFv3 Yapılandırma Adımları

#### 1. Router ID Ayarı

OSPFv3 için IPv4 benzeri bir Router ID tanımlanmalıdır:

```bash
ipv6 router ospf 1
router-id 1.1.1.1
exit
```

> Router-ID 32 bit’lik bir tanımlayıcıdır ve loopback arayüzü yoksa manuel verilmelidir.

#### 2. Arayüzlerde IPv6 Adresleme ve OSPF Etkinleştirme

```bash
interface g0/0
ipv6 address 2001:DB8:1::1/64
ipv6 ospf 1 area 0
no shutdown
```

> OSPFv3, IPv4'te olduğu gibi `network` komutu ile değil, her arayüzde ayrı ayrı etkinleştirilir.

#### 3. OSPF Durumunu Görüntüleme

```bash
show ipv6 ospf neighbor
show ipv6 ospf interface
show ipv6 route ospf
```

---

###  Örnek Topoloji

#### Router1:

```bash
interface g0/0
ipv6 address 2001:DB8:12::1/64
ipv6 ospf 1 area 0
no shutdown

ipv6 router ospf 1
router-id 1.1.1.1
```

#### Router2:

```bash
interface g0/0
ipv6 address 2001:DB8:12::2/64
ipv6 ospf 1 area 0
no shutdown

ipv6 router ospf 1
router-id 2.2.2.2
```


# Router Sorun Giderme: Ping, Traceroute, Show ve Debug Komutları

Bir ağ ortamında yönlendirici (router) üzerinden sorun giderme (troubleshooting), temel ağ hizmetlerinin çalışıp çalışmadığını test etmek ve yapılandırma hatalarını bulmak için hayati öneme sahiptir. Cisco IOS, ağ yöneticisine pek çok yerleşik komut sunar. Bunların en yaygın olanları şunlardır:

* `ping`
* `traceroute`
* `show` komutları
* `debug` komutları



##  **Ping Komutu**

### Görevi:

Ağ katmanında bir cihazın başka bir cihaza ulaşabilir olup olmadığını test eder. ICMP Echo Request ve Echo Reply mesajlarını kullanır.

### Kullanım:

```bash
ping <hedef_ip_adresi>
```

### Örnek:

```bash
ping 192.168.1.1
```

### Sonuçlar:

* **!!!!!** : 5 başarılı ping
* **.....** : Cevap alınamadı (timeout)
* **U.U.U** : Destination unreachable

### Uygulama Notları:

* Ping, bağlantı testinde ilk adımdır.
* Her ping paketi yaklaşık 100 ms içinde geri dönmelidir.


## Traceroute Komutu

### Görevi:

Bir paketin hedefe ulaşırken geçtiği yönlendirici (router) adımlarını (hops) listeler. Her "hop" TTL değerinin bir artırılması ile belirlenir.

### Kullanım:

```bash
traceroute <hedef_ip_adresi>
```

### Örnek:

```bash
traceroute 8.8.8.8
```

### Çıktı:

```
1  192.168.1.1  1 ms
2  10.0.0.1     5 ms
3  172.16.0.1   10 ms
4  8.8.8.8      15 ms
```

### Uygulama Notları:

* Hangi noktada kopukluk olduğunu gösterir.
* Ağ gecikmelerini tespit etmeye yarar.
* ICMP veya UDP protokolünü kullanır (platforma göre değişebilir).

## Show Komutları

###  Görevi:

Router’ın mevcut durumu, yapılandırması ve istatistikleri hakkında bilgi verir.

### Sık Kullanılan Show Komutları:

| Komut                     | Görevi                                                                       |
| ------------------------- | ---------------------------------------------------------------------------- |
| `show ip interface brief` | Tüm arayüzlerin IP ve durum özetini verir.                                   |
| `show running-config`     | Aktif çalışan konfigürasyonu gösterir.                                       |
| `show ip route`           | Yönlendirme tablosunu gösterir.                                              |
| `show version`            | IOS sürümü, donanım bilgisi ve çalışma süresi gibi sistem bilgilerini verir. |
| `show protocols`          | Arayüzlerin IP protokolleri ve durumunu listeler.                            |
| `show ipv6 route`         | IPv6 yönlendirme tablosunu gösterir.                                         |
| `show cdp neighbors`      | Cihaza doğrudan bağlı olan Cisco cihazlarını listeler.                       |

### Örnek:

```bash
show ip interface brief
```

> IP adresi atanmış mı, arayüz açık mı gibi özet bilgi verir.

```bash
show ip route
```

> Ağlar arasında yol var mı, statik mi dinamik mi anlaşılır.

---

## Debug Komutları

### Görevi:

Cihazın çalışırken gerçekleştirdiği işlemleri gerçek zamanlı olarak izlemeye yarar. Derinlemesine hata ayıklama için kullanılır.

### Dikkat:

* `debug` komutları CPU'ya yük bindirir. Üretim ortamlarında dikkatle kullanılmalıdır.
* Gereksiz yere açık bırakmak performansı düşürebilir.

### Yaygın Debug Komutları:

| Komut             | Görevi                                      |
| ----------------- | ------------------------------------------- |
| `debug ip packet` | IP paketlerinin geçişini izler.             |
| `debug ip rip`    | RIP güncellemelerini canlı olarak gösterir. |
| `debug icmp`      | Ping gibi ICMP mesajlarını görüntüler.      |
| `debug ipv6 ospf` | OSPFv3 mesajlarını canlı izler.             |

### Örnek:

```bash
debug ip rip
```

> RIP mesajlarını, yönlendirme güncellemelerini anlık olarak izler.

### Debug Kapatmak:

```bash
undebug all
```

veya

```bash
no debug all
```

---

## Uygulamalı Sorun Giderme Senaryosu

**Senaryo:**
Router’dan 192.168.2.1 IP adresine ping atılamıyor.

**Adım Adım Sorun Giderme:**

1. **Arayüz Durumu Kontrolü**

```bash
show ip interface brief
```

> Down durumda arayüz varsa `no shutdown` ile etkinleştirilir.

2. **Yönlendirme Tablosunu Kontrol Et**

```bash
show ip route
```

> Hedef ağ için yol var mı?

3. **Ping ile Test Et**

```bash
ping 192.168.2.1
```

> Cevap gelmiyorsa, sorun başka bir yönlendiricide olabilir.

4. **Traceroute ile Hangi Noktada Takıldığını Gör**

```bash
traceroute 192.168.2.1
```

5. **Debug ile Paketlerin Geçip Geçmediğini İzle**

```bash
debug ip packet
```

> Paket yönlendirme sorunu varsa buradan analiz edilebilir.

6. **Sorun Giderildikten Sonra Debug Kapat**

```bash
undebug all
```

## Kaynakça

1. [Cisco – NAT Configuration Guide](https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/13772-12.html)

2. [RFC 826 – An Ethernet Address Resolution Protocol](https://datatracker.ietf.org/doc/html/rfc826)

3. [RFC 1058 – Routing Information Protocol (RIP)](https://datatracker.ietf.org/doc/html/rfc1058)

4. [RFC 2453 – RIP Version 2](https://datatracker.ietf.org/doc/html/rfc2453)

5. [RFC 2328 – OSPF Version 2](https://datatracker.ietf.org/doc/html/rfc2328)

6. [RFC 5340 – OSPF for IPv6 (OSPFv3)](https://datatracker.ietf.org/doc/html/rfc5340)

7. [RFC 7868 – EIGRP Routing Protocol](https://datatracker.ietf.org/doc/html/rfc7868)

8. [RFC 4861 – Neighbor Discovery for IP version 6 (IPv6)](https://datatracker.ietf.org/doc/html/rfc4861)

9. [Cisco – DHCP Configuration Guide](https://www.cisco.com/c/en/us/support/docs/ip/dynamic-address-allocation-resolution/27470-100.html)

10. [Cisco – OSPF Configuration Examples](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/7039-1.html)

11. [Cisco – NTP Configuration Guide](https://www.cisco.com/c/en/us/support/docs/availability/high-availability/19643-ntpm.html)



