# DTP 

**DTP** (Dynamic Trunking Protocol), Cisco tarafından geliştirilmiş bir protokoldür. DTP, ağ cihazları arasındaki trunk bağlantılarını otomatik olarak oluşturmak ve yönetmek amacıyla kullanılır. Trunk bağlantıları, farklı VLAN'ların aynı bağlantı üzerinden iletilmesini sağlayan bağlantılardır. Bu protokol, VLAN bilgilerini taşıyan ve trunk bağlantısı kurulması gereken durumları otomatikleştirir.

DTP, Ethernet bağlantıları arasında **dinamik olarak trunk bağlantıları** kurmak için kullanılır ve bu süreçte cihazlar birbirine bilgi gönderir, böylece bağlantı tipi (access veya trunk) otomatik olarak belirlenir. DTP, genellikle Switch cihazları arasındaki bağlantılarda, özellikle büyük ağlarda sıkça tercih edilir.

DTP, trunk bağlantısının yönetilmesi için farklı çalışma modlarına sahiptir ve bu modlar cihazlar arasında nasıl trunk kurulacağına dair anlaşmazlıkları çözmeye yardımcı olur.

## DTP'nin Amacı ve Kullanım Alanları

**Amacı:**

DTP'nin temel amacı, ağdaki cihazlar arasında trunk bağlantılarının dinamik bir şekilde kurulmasını sağlamaktır. Bu, manuel konfigürasyonları azaltır ve ağ yöneticisinin zamandan tasarruf etmesini sağlar. DTP, aşağıdaki avantajları sunar:

1. **Kolay Yapılandırma**: DTP, trunk bağlantılarının otomatik olarak kurulmasını sağlar, böylece kullanıcılar manuel olarak trunk bağlantılarını yapılandırmak zorunda kalmaz.
2. **Dinamik Bağlantı Kurulumu**: Ağ cihazları, birbirlerine bağlandıklarında DTP, bağlantıyı otomatik olarak **trunk** olarak yapılandırır. Böylece bağlantı türü hakkında cihazlar arasında anlaşmazlık yaşanmaz.
3. **VLAN Taşıma**: Trunk bağlantıları, VLAN bilgilerini taşıyabileceği için DTP, VLAN'ların ağ boyunca doğru şekilde yönlendirilmesine yardımcı olur.

**Kullanım Alanları:**

1. **Switchler Arası Trunk Bağlantıları**: DTP, iki Cisco switch'i arasında trunk bağlantılarının kurulması için yaygın olarak kullanılır. Bu bağlantılar, VLAN bilgilerini taşıdığı için ağın genişlemesi ve yönetilmesi açısından büyük önem taşır.

2. **VLAN Yayılımı**: Ağda bir VLAN oluşturulduğunda, trunk bağlantıları üzerinden bu VLAN’ın bilgileri yayılır. DTP, VLAN bilgilerini trunk bağlantılarında taşır ve farklı switch'ler arasında VLAN'ın kullanılmasını sağlar.

3. **Ağ Yapısında Esneklik**: Özellikle büyük ağlarda, DTP trunk bağlantılarını dinamik olarak kurarak esneklik sağlar. Böylece ağda değişiklik yapılması gerektiğinde (örneğin yeni bir switch eklendiğinde) ağ yöneticisinin yeniden yapılandırma yapması gerekmez.

4. **Otomatik Konfigürasyon ve Yönetim**: DTP'nin en büyük avantajlarından biri, ağ cihazları arasında trunk bağlantılarının otomatik olarak yapılandırılmasıdır. Bu özellik, ağ yöneticilerinin işlemleri manuel olarak yapmasını gerektirmez ve ağın yönetimini daha verimli hale getirir.

DTP, yalnızca Cisco cihazları arasında çalıştığı için, Cisco dışındaki cihazlarla yapılan trunk bağlantılarında farklı bir yöntem (genellikle manuel trunk konfigürasyonu) kullanılması gerekir.


## DTP Çalışma Prensibi

DTP'nin çalışma prensibi, ağdaki cihazlar arasında trunk bağlantılarını dinamik olarak oluşturmak için otomatik bir müzakere süreci kullanmaktır. DTP, bir switch portunun hangi bağlantı türünde (trunk ya da access) çalışacağını belirlemek için iki cihaz arasında bilgi alışverişi yapar. Bu süreç şu şekilde işler:

1. **Başlatma**: İki cihaz birbiriyle iletişime geçmeye başladığında, DTP protokolü aktif hale gelir. Portlar birbirlerine DTP paketleri göndererek, hangi bağlantı tipinin (access veya trunk) kullanılacağını belirler.

2. **Müzakere**: DTP, cihazlar arasında trunk bağlantısının kurulup kurulmayacağını belirlemek için bir müzakere süreci başlatır. Cihazlar, bu müzakerede trunk bağlantısının gerekip gerekmediğini belirler. Eğer iki cihaz da trunk bağlantısını destekliyorsa, bağlantı trunk olarak yapılandırılır. Aksi takdirde, port access portu olarak yapılandırılır.

3. **Bağlantı Kurulumu**: Eğer DTP başarılı bir şekilde trunk bağlantısı kurulmasını müzakere ederse, cihazlar trunk bağlantısı üzerinde VLAN bilgilerini taşımaya başlar. Eğer cihazlardan biri access modda çalışmak istiyorsa, port sadece belirli bir VLAN'a hizmet eder.

4. **Durum Güncelleme**: Trunk bağlantısı kurulduktan sonra, DTP protokolü bağlantı durumunu sürekli izler. Eğer bağlantıdaki durum değişirse (örneğin, cihazlar arasında bir bağlantı koparsa veya port üzerinde başka bir değişiklik olsa), DTP yeniden müzakere sürecini başlatır.

## DTP Modları

DTP, farklı çalışma modlarına sahip olup, her mod farklı davranış biçimleri sergiler. Cisco cihazlarında DTP'nin kullanılabileceği dört ana mod vardır:

1. **Access Mode (access)**:

   * **Açıklama**: Bu modda, port sadece tek bir VLAN'a hizmet verir. DTP burada pasif olarak çalışır, yani trunk bağlantısı kurmaya çalışmaz. Access portu, VLAN bilgilerini taşımaz.
   * **Kullanım Durumu**: Bu mod, genellikle istemci cihazları veya ağ cihazlarının bağlantıları için kullanılır. Sadece belirli bir VLAN’a hizmet eder.

2. **Trunk Mode (trunk)**:

   * **Açıklama**: Bu modda, port trunk bağlantısı olarak yapılandırılır ve VLAN bilgilerini taşır. Trunk bağlantısı otomatik olarak kurulmaz; bağlantının trunk olacağı garanti edilir. Bu durumda, port VLAN'ları taşımak için hazırdır.
   * **Kullanım Durumu**: Switch'ler arasında VLAN’ların taşınması gerektiğinde kullanılır. Trunk bağlantısı, farklı VLAN'ların aynı bağlantı üzerinden iletilmesini sağlar.

3. **Dynamic Auto Mode (desirable)**:

   * **Açıklama**: Bu mod, portun trunk bağlantısı kurmaya çalışacağı bir yapılandırmadır, ancak yalnızca karşı cihaz da trunk bağlantısı kurmaya uygun ise (yani karşı cihaz **desirable** ya da **trunk** modunda ise) trunk bağlantısı kurulur. Eğer karşı cihaz trunk bağlantısını istemezse, port access portu olarak çalışır.
   * **Kullanım Durumu**: Switch’ler arası bağlantıların otomatik olarak trunk yapılmasını sağlamak için kullanılır, ancak karşı cihaz trunk bağlantısı kurmak istemezse bağlantı access portu olarak devam eder.

4. **Dynamic Desirable Mode (auto)**:

   * **Açıklama**: Bu modda, port trunk bağlantısı kurmaya çalışmaz, ancak karşı cihaz trunk bağlantısı yapmaya çalışıyorsa bağlantıyı kabul eder. Eğer karşı cihaz trunk bağlantısı kurmak istemezse, port access portu olarak çalışır.
   * **Kullanım Durumu**: Switch’ler arasında bağlantı kurulurken, karşı cihazın trunk bağlantısını kurmasını bekleyen bir yapılandırmadır. Eğer karşı cihaz trunk bağlantısını destekliyorsa, otomatik olarak trunk bağlantısı kurulur.

### DTP Modlarının Özeti

| Mod                   | DTP Davranışı                                                                                                                     |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Access**            | Port yalnızca bir VLAN'a hizmet eder. Trunk bağlantısı kurulmaz.                                                                  |
| **Trunk**             | Port trunk bağlantısı olarak yapılandırılır ve VLAN bilgilerini taşır. Trunk bağlantısı garantidir.                               |
| **Dynamic Auto**      | Port trunk bağlantısı kurmaya çalışır, ancak yalnızca karşı cihaz trunk bağlantısı kurmaya uygun olduğunda bağlantı kurulacaktır. |
| **Dynamic Desirable** | Port trunk bağlantısı kurmaya çalışmaz, ancak karşı cihaz trunk bağlantısı kurmaya çalışıyorsa bağlantıyı kabul eder.             |

Bu modlar, ağ yöneticilerine bağlantıların dinamik bir şekilde nasıl kurulacağını belirleme esnekliği sağlar. Trunk bağlantıları ve VLAN'lar arasındaki ilişkiyi yönetmek için bu modların uygun kullanımı ağda etkinlik ve verimlilik sağlar.



## DTP'nin Güvenlik Riskleri

DTP (Dynamic Trunking Protocol), ağdaki switch cihazları arasında trunk bağlantılarının otomatik olarak kurulmasına yardımcı olan bir protokoldür. Ancak, otomatik yapılandırma ve portların dinamik olarak trunk ya da access olarak ayarlanması, bazı güvenlik risklerini beraberinde getirebilir. Aşağıda DTP'nin potansiyel güvenlik riskleri detaylı olarak açıklanmıştır:

1. **Yetkisiz Trunk Bağlantıları**

   * **Açıklama**: DTP, portların trunk bağlantısı kurmasını otomatik hale getirir. Eğer bir switch portu yanlışlıkla veya kötü niyetli olarak trunk bağlantısı kurmaya teşvik edilirse, bu port, ağdaki VLAN’lar arasında istemeden veri iletebilir.
   * **Risk**: Yetkisiz bir cihazın, DTP'nin dinamik trunk oluşturma özelliğini kullanarak switch ağına bağlanması durumunda, bu cihaz ağda bulunan tüm VLAN'lara erişim kazanabilir. Bu, VLAN'lar arasındaki veri akışını istenmeyen bir şekilde açığa çıkarabilir ve saldırganın ağın iç yapısına erişmesini sağlayabilir.
   * **Çözüm**: DTP'yi devre dışı bırakmak ve portları manuel olarak trunk ya da access olarak yapılandırmak, yetkisiz trunk bağlantılarının önüne geçebilir. Ayrıca, ağdaki sadece yetkili cihazların trunk bağlantılarını kurabilmesi için 802.1X gibi kimlik doğrulama mekanizmaları kullanılabilir.

2. **VLAN Hopping (VLAN Atlama)**

   * **Açıklama**: VLAN hopping, bir saldırganın bir VLAN’dan diğerine geçiş yapabilmesi durumudur. Bu tür bir saldırı, DTP'nin trunk bağlantılarının yanlış yapılandırılması nedeniyle mümkündür. VLAN hopping, genellikle trunk bağlantısının güvenliğinin zayıf olduğu durumlarda gerçekleşir.
   * **Risk**: Eğer trunk bağlantıları doğru şekilde güvence altına alınmazsa, saldırgan, belirli VLAN’lar arasındaki veri trafiğini izleyebilir veya manipüle edebilir. DTP'nin otomatik olarak trunk bağlantısı kurması, bir saldırganın bir cihazı trunk bağlantısına zorlayarak VLAN'lar arasında gezinmesine imkan tanıyabilir.
   * **Çözüm**: Trunk bağlantılarında 802.1Q etiketleme protokolü kullanılarak VLAN etiketleme yapılmalı ve yalnızca belirli VLAN’ların trunk bağlantısı üzerinden taşınmasına izin verilmelidir. Ayrıca, DTP'yi devre dışı bırakmak ve portları manuel olarak yapılandırmak, VLAN hopping saldırılarını engellemek için önemlidir.

3. **Port Security İhlalleri**

   * **Açıklama**: DTP, ağdaki portları dinamik olarak trunk bağlantısına dönüştürür. Ancak, bu portlar üzerinde belirli güvenlik kontrolleri yapılmazsa, kötü niyetli cihazlar kolayca trunk bağlantısı kurabilir ve ağda daha fazla erişim elde edebilir.
   * **Risk**: Port security özelliği etkin değilse, DTP'nin otomatik trunk kurulumu sayesinde yetkisiz cihazlar ağda geçiş yapabilir ve veri trafiğine dahil olabilir. Port security, ağdaki cihazların sadece belirli MAC adresleriyle erişmesine izin verir, ancak DTP devreye girdiğinde, bu güvenlik önlemleri devre dışı kalabilir.
   * **Çözüm**: Port security kullanılarak yalnızca yetkili cihazların portlara erişimi sağlanmalı ve DTP'yi devre dışı bırakmak daha güvenli bir seçenek olabilir. Ayrıca, "port security violation" ile ilgili uyarılar ve önlemler alınabilir.

4. **VLAN ID Çakışmaları ve Yanıltıcı Yapılandırmalar**

   * **Açıklama**: DTP, switch'ler arasında trunk bağlantısını otomatik olarak kurarken, bazen yanlış yapılandırmalar sonucu VLAN ID’lerinde çakışmalar olabilir. Bu, bir VLAN’a ait olan trafiğin yanlış bir VLAN’a yönlendirilmesine veya bir VLAN’daki verilerin başka bir VLAN ile karışmasına yol açabilir.
   * **Risk**: Yanıltıcı yapılandırmalar sonucu VLAN ID çakışmaları, verilerin güvenliği açısından ciddi bir tehdit oluşturabilir. Özellikle, VLAN'lar arasında veri iletimi yapılırken, veri akışındaki hatalar ağ güvenliğini tehlikeye atabilir.
   * **Çözüm**: VLAN’ların doğru bir şekilde yapılandırılması ve DTP'nin düzgün çalışabilmesi için her iki tarafın VLAN yapılandırmalarının uyumlu olması sağlanmalıdır. Ayrıca, trunk bağlantılarındaki VLAN’ların yalnızca belirli VLAN’larla sınırlandırılması (VLAN pruning) güvenlik için önemlidir.

5. **Ağ İzolasyonunun Zayıflaması**

   * **Açıklama**: DTP, ağ cihazları arasında otomatik trunk bağlantıları kurarak ağın daha esnek ve genişletilebilir olmasını sağlar. Ancak, bu esneklik, ağ izolasyonunun zayıflamasına yol açabilir. Eğer DTP'yi devre dışı bırakmadan trunk bağlantıları kurulursa, izole edilmiş ağ segmentleri birbirine bağlanabilir.
   * **Risk**: Ağ segmentlerinin yanlışlıkla birbirine bağlanması, ağdaki izolasyonun kaybolmasına ve bir VLAN’daki trafiğin diğer VLAN’a taşınmasına sebep olabilir. Bu da, ağda istem dışı bir trafik akışına ve potansiyel olarak güvenlik açıklarına yol açabilir.
   * **Çözüm**: Trunk bağlantıları dikkatlice yapılandırılmalı ve VLAN’lar yalnızca gerekli cihazlar arasında taşınmalıdır. Ağda izolasyon sağlamak için DTP yerine manuel trunk yapılandırması kullanılabilir. Ayrıca, VLAN'lar arasında düzgün güvenlik duvarı ve ACL (Access Control List) kuralları uygulanmalıdır.

6. **Man-in-the-Middle (MitM) Saldırıları**

   * **Açıklama**: DTP’nin otomatik trunk kurma özelliği, bir saldırganın ağdaki trunk bağlantılarını manipüle etmesine veya dinlemesine imkan tanıyabilir. Bu tür bir saldırıda, saldırgan ağ trafiğini izler veya değiştirir.
   * **Risk**: DTP'nin güvenli olmayan trunk bağlantıları kurmasına izin vermesi, man-in-the-middle saldırılarına kapı aralayabilir. Saldırgan, bu trunk bağlantısı üzerinden ağdaki veri trafiğini izleyebilir, değiştirebilir veya yönlendirebilir.
   * **Çözüm**: Trunk bağlantılarının güvenliği, VLAN'lar arası trafiği şifreleme ve doğrulama ile sağlanabilir. DTP'yi devre dışı bırakmak ve yalnızca yetkili cihazların trunk bağlantıları kurmasına izin vermek, bu tür saldırıları engelleyebilir. Ayrıca, ağda güvenli iletişim için VPN veya IPsec gibi şifreleme yöntemleri kullanılabilir.


## Packet Tracer Uygulamasında DTP Yapılandırması

DTP (Dynamic Trunking Protocol), ağdaki switch'ler arasında trunk bağlantılarının dinamik olarak kurulmasını sağlar. Cisco Packet Tracer'da DTP yapılandırması yapmak için aşağıdaki adımları takip edebilirsiniz. Bu örnekte, iki Cisco switch'i kullanarak DTP yapılandırması yapılacaktır ve switch'ler arasındaki trunk bağlantısının otomatik olarak kurulmasını sağlayacağız.

### Senaryo:

* Switch1 ve Switch2 arasında trunk bağlantısı kurulacak.
* DTP protokolü, switchler arasında trunk bağlantısının dinamik olarak kurulmasını sağlayacak.
* Switch1'in portu **Fa0/1** ve Switch2'nin portu **Fa0/1** trunk bağlantısı için kullanılacak.

#### Adımlar:

1. **Switch'leri ve Bağlantıyı Konfigüre Etme**

   * Packet Tracer’da yeni bir proje oluşturun ve iki Cisco switch ekleyin. Switch1 ve Switch2 olarak adlandırılacak.
   * Switch'ler arasında bir bağlantı kurun. Switch1'in **Fa0/1** portunu Switch2'nin **Fa0/1** portuna bağlayın.

2. **Switch1 Konfigürasyonu**

   Switch1 üzerinde, port **Fa0/1**'i trunk bağlantısı kuracak şekilde yapılandıracağız. Bu, DTP'nin çalışabilmesi için önemlidir.

   **Switch1 Konfigürasyonu:**

   * Switch1'e CLI (Command Line Interface) üzerinden erişim sağlayın.
   * Aşağıdaki komutları kullanarak **Fa0/1** portunu trunk olarak yapılandırın.

   ```bash
   Switch1> enable
   Switch1# configure terminal
   Switch1(config)# interface fa0/1
   Switch1(config-if)# switchport mode dynamic desirable
   Switch1(config-if)# end
   ```

   **Açıklamalar:**

   * `switchport mode dynamic desirable`: Bu komut, portu trunk bağlantısı kurmaya çalışacak şekilde yapılandırır. DTP, port üzerinde trunk bağlantısının kurulmasını sağlar.

3. **Switch2 Konfigürasyonu**

   Switch2 üzerinde de benzer bir yapılandırma yapacağız. Switch2'nin portu da trunk bağlantısı kurmaya çalışacak.

   **Switch2 Konfigürasyonu:**

   * Switch2'ye CLI üzerinden erişim sağlayın.
   * Aşağıdaki komutları kullanarak **Fa0/1** portunu trunk olarak yapılandırın.

   ```bash
   Switch2> enable
   Switch2# configure terminal
   Switch2(config)# interface fa0/1
   Switch2(config-if)# switchport mode dynamic auto
   Switch2(config-if)# end
   ```

   **Açıklamalar:**

   * `switchport mode dynamic auto`: Bu komut, portu trunk bağlantısına izin verecek şekilde yapılandırır. Switch2, Switch1 tarafından trunk bağlantısı kurulmaya çalışıldığında otomatik olarak trunk bağlantısını kabul eder.

4. **DTP Çalışmasını Test Etme**

   Yapılandırma tamamlandıktan sonra, DTP'nin doğru çalışıp çalışmadığını test edebiliriz.

   * **Show Komutları ile Kontrol Etme**: Aşağıdaki komutları kullanarak trunk bağlantısının kurulduğunu ve DTP'nin çalıştığını kontrol edebilirsiniz.

   **Switch1 üzerinde:**

   ```bash
   Switch1# show interfaces fa0/1 trunk
   ```

   **Switch2 üzerinde:**

   ```bash
   Switch2# show interfaces fa0/1 trunk
   ```

   Bu komutlar, portlar arasında trunk bağlantısının kurulup kurulmadığını gösterir. Çıktılar, trunk bağlantısının başarıyla kurulduğunu ve VLAN'ların taşındığını belirtmelidir.

5. **Sonuçları Kontrol Etme**

   DTP'nin düzgün çalıştığını ve trunk bağlantısının doğru şekilde kurulduğunu doğrulamak için, her iki switch'te de aşağıdaki komutları çalıştırabilirsiniz.

   **Switch1 üzerinde trunk bağlantısını kontrol etme:**

   ```bash
   Switch1# show interface fa0/1 switchport
   ```

   **Switch2 üzerinde trunk bağlantısını kontrol etme:**

   ```bash
   Switch2# show interface fa0/1 switchport
   ```

   Eğer trunk bağlantısı doğru şekilde kurulmuşsa, bu komutlar trunk bağlantısının başarılı olduğunu ve VLAN bilgilerini taşıdığını gösterecektir.







