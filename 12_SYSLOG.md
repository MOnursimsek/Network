# **SYSLOG**
## Syslog Nedir?

Syslog, bilgisayar ağlarında log (kayıt) verilerinin merkezi bir şekilde toplanması ve yönetilmesi için kullanılan bir protokoldür. Sistemler, ağ cihazları, sunucular, uygulamalar ve güvenlik duvarları gibi çeşitli kaynaklardan gelen olay bilgilerini (log verilerini) Syslog protokolü aracılığıyla merkezi bir sisteme iletebilirler. Bu merkezi sistem genellikle bir log sunucusu olarak yapılandırılır. Syslog, özellikle büyük ağ altyapılarında, ağ yöneticilerinin güvenlik, performans izleme ve hata tespiti gibi işlemleri daha verimli bir şekilde gerçekleştirmesine yardımcı olur.

## Syslog Mesaj Yapısı ve Facility-Severity Seviyeleri

Syslog protokolü ile iletilen her mesaj belirli bir yapıya sahiptir. Bu yapı, hem insanlar hem de sistemler tarafından kolayca analiz edilebilmesi için standartlaştırılmıştır. Bir Syslog mesajı aşağıdaki temel bileşenlerden oluşur:

### 1. **Mesaj Formatı (RFC 3164’e göre geleneksel yapı)**

```
<PRI>HEADER MSG
```

* **`<PRI>`**\*\* (Priority - Öncelik)\*\*: Mesajın en başında yer alır ve mesajın **facility** ve **severity** (önem derecesi) bilgilerinin birleşiminden oluşur. Sayısal bir değerdir ve şu şekilde hesaplanır:

  ```
  PRI = (Facility * 8) + Severity
  ```

* **`HEADER`**: Zaman damgası (timestamp) ve mesajı gönderen cihazın hostname (sistem adı) gibi bilgileri içerir.

* **`MSG`**: Asıl mesaj içeriğidir. Olayın ne olduğunu açıklar; örneğin bir hata, uyarı ya da bilgi mesajı olabilir.


### 2. **Facility (Kaynak Türü)**

Facility, log mesajının hangi sistem bileşeninden ya da hizmetten geldiğini belirtir. Örneğin, kernel, mail servisi, sistem uygulamaları gibi. Facility değeri 0 ile 23 arasında bir sayı ile ifade edilir.

| Facility Kodu | Kaynak                           |
| ------------- | -------------------------------- |
| 0             | kernel messages                  |
| 1             | user-level messages              |
| 2             | mail system                      |
| 3             | system daemons                   |
| 4             | security/authorization messages  |
| 5             | syslogd internal messages        |
| 6             | line printer subsystem           |
| 7             | network news subsystem           |
| 8             | UUCP subsystem                   |
| 9             | clock daemon                     |
| 10            | security/authorization (private) |
| 11            | FTP daemon                       |
| 12            | NTP subsystem                    |
| 13            | log audit                        |
| 14            | log alert                        |
| 15            | clock daemon (not NTP)           |
| 16–23         | local0 – local7 (özel kullanım)  |

Bu alan, log’un hangi modülden geldiğini sınıflandırmak için kullanılır ve log analizi açısından önemlidir.



### 3. **Severity (Önem Derecesi)**

Severity, mesajın ciddiyet düzeyini belirtir. 0 en yüksek öncelikli (en kritik), 7 ise en düşük öncelikli (sadece bilgi amaçlı) seviyedir:

| Severity Kodu | Seviye Adı    | Açıklama                                        |
| ------------- | ------------- | ----------------------------------------------- |
| 0             | Emergency     | Sistem çalışamaz durumda, acil müdahale gerekir |
| 1             | Alert         | Hemen ele alınması gereken durum                |
| 2             | Critical      | Kritik düzeyde hata                             |
| 3             | Error         | Hata mesajı                                     |
| 4             | Warning       | Uyarı mesajı                                    |
| 5             | Notice        | Normal ama dikkat edilmesi gereken durum        |
| 6             | Informational | Bilgilendirme mesajları                         |
| 7             | Debug         | Hata ayıklama (debugging) mesajları             |

Bu seviyeler yöneticilere hangi olayların öncelikli olduğunu ayırt etme imkânı verir. Örneğin, sadece kritik ve hata mesajlarını göstererek sistemdeki sorunlar hızlıca tespit edilebilir.



### 4. **PRI Değerinin Hesaplanması Örneği**

Örnek: `Facility = 4 (security/authorization)` ve `Severity = 2 (Critical)`

```
PRI = (4 × 8) + 2 = 34
```

Bu durumda mesajın başında `<34>` ifadesi yer alır. Syslog sunucusu bu değeri okuyarak mesajın hangi kaynaktan ve hangi önem derecesiyle geldiğini anlayabilir.



### 5. **Mesaj Örneği**

```
<34>Oct 5 10:15:30 firewall01 sshd[1234]: Failed password for invalid user admin from 192.168.1.100 port 22
```

* `<34>`: Facility 4 (security) ve Severity 2 (critical)
* `Oct 5 10:15:30`: Zaman damgası
* `firewall01`: Hostname
* `sshd[1234]`: Süreci ve PID
* `Failed password...`: Mesaj içeriği

## Syslog'un Çalışma Prensibi

&#x20;Temel çalışma prensibi, log üreten cihazların (istemciler) meydana gelen olayları **standart bir formatta** derleyip bir **Syslog sunucusuna** göndermesidir. Bu yapı sayesinde sistem yöneticileri, farklı kaynaklardan gelen logları tek bir merkezde toplayarak analiz edebilir.

#### Çalışma Akışı Şu Şekilde Gerçekleşir:

1. **Olay Oluşumu (Event Generation)**: Bir cihazda bir olay meydana gelir (örneğin, bir kullanıcı oturum açar, bir hizmet başlatılamaz, bir saldırı teşebbüsü olur).

2. **Log Mesajı Oluşturulması**: Bu olay, sistem veya uygulama tarafından bir **Syslog mesajı** olarak oluşturulur. Bu mesaj, timestamp (zaman bilgisi), hostname, facility ve severity gibi bilgiler içerir.

3. **Mesajın İletimi**: Oluşturulan Syslog mesajı, UDP 514 (veya opsiyonel olarak TCP) portu üzerinden **Syslog sunucusuna gönderilir**.

4. **Sunucu Tarafında Kabul**: Syslog sunucusu, gelen mesajı alır, ilgili dosyalara yazar veya bir veritabanına kaydeder. Aynı zamanda log mesajı analiz edilip alarm üretilebilir veya bir bildirim tetiklenebilir.

5. **Analiz ve İzleme**: Syslog sunucusunda toplanan mesajlar filtrelenerek, örnekleme, uyarı üretme, raporlama ve görselleştirme işlemleri gerçekleştirilir.

#### Dikkat Edilmesi Gereken Noktalar:

* **UDP’nin Kullanımı**: Varsayılan olarak UDP kullanılır. Bu hızlıdır fakat güvenilir değildir; mesajlar kaybolabilir.
* **TCP ve TLS Seçenekleri**: Güvenilirlik veya şifreleme gerekliyse TCP veya TLS ile çalışan Syslog varyasyonları tercih edilir (örn. rsyslog, syslog-ng).
* **Zaman Senkronizasyonu**: Farklı cihazlardan gelen logların doğru sıralanabilmesi için NTP gibi zaman senkronizasyon hizmetleriyle cihazların saatleri uyumlu olmalıdır.

## Cisco Cihazlarında Syslog Yapılandırma Adımları

Cisco router ve switch’lerde Syslog yapılandırması, cihazdan oluşan olayların merkezi bir Syslog sunucusuna gönderilmesini sağlar. Bu yapılandırma sayesinde ağ yöneticileri, cihaz loglarını merkezi olarak toplayabilir, analiz edebilir ve olaylara hızlı şekilde müdahale edebilir. Cisco IOS, syslog mesajlarını varsayılan olarak konsola ve buffer'a yazarken, istenirse uzak bir syslog sunucusuna yönlendirmek mümkündür.

Aşağıda Cisco cihazlarda syslog yapılandırması için gerekli adımlar detaylı şekilde açıklanmıştır:

#### 1. **Zaman Doğruluğunu Sağlayın (Opsiyonel ama önerilir)**

Syslog mesajlarının analizinde zaman bilgisi çok önemlidir. Tüm cihazların aynı saat diliminde olması gerekir. Bunun için NTP yapılandırması önerilir.

```shell
conf t
clock timezone TR +3       ! Türkiye için saat dilimi
ntp server 192.168.1.100    ! NTP sunucusu IP'si
exit
```

#### 2. **Syslog Sunucusunun Belirlenmesi**

Cisco cihazdan log mesajlarının gönderileceği Syslog sunucusunun IP adresi tanımlanmalıdır. Syslog mesajları varsayılan olarak UDP 514 portunu kullanır.

```shell
conf t
logging 192.168.1.200      ! Syslog sunucusunun IP adresi
exit
```

> Not: Cisco cihazın Syslog sunucusuna ulaşabildiğinden (routing ve ACL açısından) emin olun.

#### 3. **Log Seviyesinin Belirlenmesi**

Cisco cihazlar, hangi seviyedeki log mesajlarının gönderileceğini belirlemeye olanak tanır. `logging trap` komutu ile log gönderim eşiği tanımlanır. Severity seviyesi ne kadar düşükse (0–7 arası), o kadar detaylı log gönderilir.

```shell
conf t
logging trap warnings
exit
```

| Seviye | Adı           | Açıklama                          |
| ------ | ------------- | --------------------------------- |
| 0      | emergencies   | Cihaz çalışamaz durumda           |
| 1      | alerts        | Hemen müdahale gerektiren olaylar |
| 2      | critical      | Kritik hatalar                    |
| 3      | errors        | Hatalar                           |
| 4      | warnings      | Uyarılar                          |
| 5      | notifications | Normal fakat önemli olaylar       |
| 6      | informational | Bilgilendirici mesajlar           |
| 7      | debugging     | Ayrıntılı hata ayıklama mesajları |

> Örnek: `logging trap errors` komutu yalnızca severity 0–3 arasındaki mesajları gönderir.

#### 4. **Z Log Mesajlarının Zaman Bilgisiyle Görünmesi (Opsiyonel)**

CLI'de çıkan log mesajlarında zaman damgası olmasını sağlamak, olayları daha iyi takip etmenize yardımcı olur:

```shell
conf t
service timestamps log datetime msec
exit
```

Bu komut sayesinde log mesajlarına tarih, saat ve milisaniye bilgisi eklenir.

#### 5. **Logging Konsol ve Terminal Ayarları (Opsiyonel)**

Cihazın terminalinde veya konsolunda ne tür logların görüneceğini belirlemek için aşağıdaki komutlar kullanılır:

```shell
conf t
logging console warnings     ! Konsol ekranı için log seviyesi
logging monitor informational ! VTY (SSH/Telnet) oturumu için
exit
```

#### 6. **Log Buffer Ayarları (Opsiyonel)**

Cisco cihaz, log mesajlarını RAM içinde belirli bir buffer alanında da tutar. Bu alanın boyutu ve içeriği ayarlanabilir:

```shell
conf t
logging buffered 16384 warnings
exit
```

> Bu komut, RAM'deki log buffer boyutunu 16.384 byte yapar ve warning (sev. 4) seviyesinden yukarı logları tutar.

#### 7. **Yapılandırmayı Kaydetme**

Yapılan değişikliklerin kalıcı olması için yapılandırma kaydedilmelidir:

```shell
write memory
```

### Örnek Syslog Yapılandırması (Tam Konfigürasyon)

```shell
conf t
logging 192.168.1.200
logging trap informational
service timestamps log datetime msec
logging buffered 16384 debugging
logging console warnings
logging monitor informational
exit
```

### Yapılandırma Kontrolü

Aşağıdaki komutlarla yapılandırma ve log durumu kontrol edilebilir:

```shell
show logging            ! Genel log durumu
show running-config | include logging   ! Logging konfigürasyonları
```

### Packet Tracer'da Syslog Örnek

Cisco Packet Tracer, sanal bir ağ ortamında Cisco cihazlarının yapılandırılmasını ve test edilmesini sağlayan bir simülasyon aracıdır. Packet Tracer içinde yerleşik olarak gelen **"Server" cihazı**, Syslog sunucusu olarak yapılandırılabilir. Bu kurulum sayesinde, router veya switch gibi cihazlardan gelen log mesajları merkezi bir noktada görüntülenebilir.

### 1. **Topoloji Oluşturma**

Packet Tracer’da aşağıdaki temel topolojiyi kurun:

* 1 adet **Router** (örneğin: R1)
* 1 adet **Switch** (isteğe bağlı)
* 1 adet **Server** (Syslog sunucusu olarak yapılandırılacak)
* 1 adet **PC veya Laptop** (yönetim için isteğe bağlı)
* Hepsini uygun şekilde kablolarla bağlayın (genellikle Copper Straight-Through)

### 2. **IP Adreslerinin Ayarlanması**

#### Router’da:

```shell
R1> enable
R1# configure terminal
R1(config)# interface fastethernet0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
```

#### Server’da:

* Server’a çift tıklayın → **Desktop** sekmesine gelin → **IP Configuration** uygulamasını açın.
* IP Address: `192.168.1.10`
* Subnet Mask: `255.255.255.0`
* Default Gateway: `192.168.1.1`

### 3. **Syslog Hizmetinin Etkinleştirilmesi (Server Üzerinde)**

1. Server’a çift tıklayın.
2. **Services** sekmesine geçin.
3. Sol menüden **Syslog** seçeneğine tıklayın.
4. Sağ tarafta **Syslog Service: ON** konumuna getirin.
5. Gelen mesajları görebileceğiniz log ekranı otomatik olarak aktif olur.

Bu işlemle sunucu artık gelen Syslog mesajlarını kabul etmeye hazır hale gelir.

### 4. **Router Üzerinde Syslog Ayarları**

Router'dan Syslog sunucusuna log gönderebilmek için aşağıdaki yapılandırmayı uygulayın:

```shell
R1> enable
R1# configure terminal
R1(config)# logging 192.168.1.10        ! Syslog sunucusunun IP adresi
R1(config)# logging trap informational  ! Gönderilecek log seviyesi
R1(config)# service timestamps log datetime msec
R1(config)# exit
```

### 5. **Test Etme: Log Mesajı Oluşturma**

Örnek olarak yanlış bir komut girin ya da bir arayüzü kapatıp açın:

```shell
R1# conf t
R1(config)# interface fa0/0
R1(config-if)# shutdown
R1(config-if)# no shutdown
R1(config-if)# exit
```

Bu işlemler Syslog sunucusuna bir veya birden fazla log mesajı gönderir.

### 6. **Logları Görüntüleme**

Server’a dönün:

* **Services → Syslog** ekranında, router’dan gelen log mesajlarının listelendiğini göreceksiniz.
* Mesajlar zaman bilgisi, cihaz ismi ve olay içeriği ile birlikte gösterilir.


### Kaynakça

1. [RFC 3164 – The BSD Syslog Protocol](https://datatracker.ietf.org/doc/html/rfc3164)
2. [RFC 5424 – The Syslog Protocol](https://datatracker.ietf.org/doc/html/rfc5424)
3. [RFC 5425 – Syslog over TLS](https://datatracker.ietf.org/doc/html/rfc5425)
