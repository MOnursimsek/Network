# **Cisco IOS**

## **Cisco IOS Nedir?**

Cisco IOS (Internetwork Operating System), Cisco tarafından geliştirilen, yönlendiriciler (routers) ve anahtarlar (switches) başta olmak üzere birçok ağ cihazında çalışan, ağ işlevlerinin yönetilmesini sağlayan özel bir ağ işletim sistemidir. IOS, cihazın tüm ağ işlevlerini denetler; bu işlevler arasında yönlendirme, anahtarlama, trafik filtreleme, ağ güvenliği, QoS (Hizmet Kalitesi), arabirim yönetimi ve daha fazlası yer alır.

### **Temel Özellikleri:**

* **CLI (Command Line Interface)** tabanlıdır. IOS cihazlar genellikle komut satırı üzerinden yapılandırılır.
* **Modüler yapıya** sahiptir: Her bir işlev, farklı bir süreç olarak çalışır.
* **Gerçek zamanlı çalışır:** IOS, kesintisiz veri iletimi ve yönetim için tasarlanmıştır.
* **Çok kullanıcı destekler:** Farklı kullanıcılar, farklı ayrıcalık seviyelerinde oturum açabilir.
* **Çok protokollü destek:** OSPF, EIGRP, RIP, BGP gibi birçok yönlendirme protokolünü destekler.
* **Donanım bağımlıdır:** IOS sürümü, çalıştığı cihazın donanım modeline göre değişir.


Switch ve router gibi ağ cihazları, sadece yazılımsal değil, aynı zamanda **donanımsal olarak da kritik öneme sahip** sistemlerdir. Bu cihazların görevlerini yerine getirebilmesi için belirli donanım bileşenlerine ve açılış (boot) süreçlerine ihtiyaç vardır. Bu makalede, Cisco temelli ağ cihazlarının fiziksel yapısını ve açılış sırasındaki olayları detaylı şekilde ele alacağız.

##  Donanımsal Bileşenler (Cisco Router/Switch)

Cisco router ve switch'lerde bulunan temel donanım bileşenleri şunlardır:

### 1. **CPU (Central Processing Unit)**
- Tüm komutları işleyen merkezi işlem birimidir.
- IOS işletim sistemi, yönlendirme protokolleri, ACL gibi tüm işlemler burada yürütülür.

### 2. **RAM (Random Access Memory)**
- Geçici bellektir. Cihaz kapatıldığında içerik silinir.
- **Routing tablosu, ARP tablosu, running-config** gibi veriler burada tutulur.

### 3. **ROM (Read Only Memory)**
- Kalıcı bellektir. İçeriği cihaz kapansa bile silinmez.
- İçerisinde genellikle şu bileşenler bulunur:
  - **POST (Power-On Self Test)**  
  - **Bootstrap programı**
  - Mini IOS (bazı cihazlarda)

### 4. **NVRAM (Non-Volatile RAM)**
- Kalıcı bellektir, cihaz kapatılsa bile silinmez.
- **Startup-config** dosyası burada saklanır.

### 5. **Flash Bellek**
- IOS işletim sisteminin saklandığı bölümdür.
- Yazılım güncellemeleri buradan yapılır.

### 6. **Arayüz Portları**
- **Routerlarda**: Ethernet, Serial, Console, AUX
- **Switchlerde**: FastEthernet, GigabitEthernet, Console

### 7. **Console Port**
- İlk yapılandırma için kullanılan fiziksel bağlantı noktasıdır.
- Terminal emülatörü (PuTTY, TeraTerm) ile erişilir.


##  Cihazın Başlatılma (Boot) Süreci

Bir Cisco router veya switch açıldığında, donanım ve yazılım arasında şu sırayla olaylar gerçekleşir:



### 🔹 1. **POST (Power-On Self Test)**

- Donanım bileşenlerinin (RAM, CPU, portlar) testi yapılır.
- Hatalı bir bileşen varsa cihaz başlatılmaz.
- Bu işlem ROM bellekteki POST yazılımı tarafından yürütülür.


### 🔹 2. **Bootstrap Programı**

- POST sonrası çalışan küçük bir yazılımdır.
- IOS işletim sistemini bulmak ve yüklemekle görevlidir.
- **ROM** bellekte saklanır.


### 🔹 3. **IOS’un Yüklenmesi**

- Bootstrap programı, **Flash bellekteki IOS dosyasını** bulur.
- Bu dosya RAM'e yüklenir ve çalıştırılır.
- Eğer Flash’ta IOS bulunamazsa, ROM’daki mini IOS devreye girer (ROMMON modu).


### 🔹 4. **Startup-config Yüklenmesi**

- IOS yüklendikten sonra cihaz **NVRAM**'de bulunan `startup-config` dosyasını RAM’e yükler.
- Bu dosya, cihazın son kaydedilen konfigürasyonunu içerir.
- Eğer startup-config yoksa, cihaz **initial configuration dialog** (ilk kurulum sihirbazı) başlatır.


### 🔹 5. **Cihaz Kullanıma Hazır**

- IOS tamamen yüklendiğinde CLI (komut satırı arayüzü) kullanıma açılır.
- Cihaz artık yönlendirme/switching görevlerini gerçekleştirebilir.


##  Başlangıç Modları (ROMMON ve Normal Mod)

| Mod      | Açıklama |
|----------|----------|
| **Normal Boot** | Flash’taki IOS yüklenir, config yüklenir. |
| **ROMMON (ROM Monitor Mode)** | IOS dosyası bozulmuşsa veya silinmişse bu moda geçilir. Temel komutlarla cihaz kurtarılabilir. |

ROMMON’a giriş için açılış sırasında `Ctrl + Break` tuş kombinasyonu kullanılır.

## **Running-config ve Startup-config Nedir?**

Cisco cihazlarında yapılandırma, iki temel konfigürasyon dosyası üzerinden yönetilir: **`running-config`** ve **`startup-config`**.

### **1. running-config (Çalışan Yapılandırma):**

* Cihazın **RAM** belleğinde geçici olarak bulunan yapılandırmadır.
* **Cihaz çalışır durumdayken** aktif olan ayarları içerir.
* Konfigürasyon modunda yaptığınız değişiklikler bu dosyada **anında** etkili olur.
* Ancak bu dosya **cihaz yeniden başlatıldığında silinir.**

**Görüntüleme Komutu:**

```bash
show running-config
```

### **2. startup-config (Başlangıç Yapılandırması):**

* **NVRAM** belleğinde (non-volatile RAM) kalıcı olarak saklanır.
* Cihaz her açıldığında bu dosya RAM’e yüklenir ve sistem bu yapılandırma ile başlar.
* `running-config` içeriği kalıcı hale getirilmek istendiğinde, `startup-config` dosyasına kopyalanmalıdır.

**Görüntüleme Komutu:**

```bash
show startup-config
```

## **Yapılandırma Dosyalarının Kaydedilmesi (write memory / copy run start)**

### **Yapılandırmanın Kalıcı Hale Getirilmesi:**

Yapılandırma sırasında yapılan değişiklikler \*\*yalnızca \*\***`running-config`** dosyasına yazılır. Bu nedenle, değişikliklerin cihaz yeniden başlatıldığında da geçerli olması için \*\*NVRAM’deki \*\***`startup-config`** dosyasına kaydedilmesi gerekir.

Bu işlem iki farklı komutla yapılabilir:

### **1. ****************************`write memory`**************************** Komutu:**

* Bu komut, `running-config`'i `startup-config`'e yazar.
* Daha eski IOS sürümlerinde yaygın olarak kullanılır.

```bash
write memory
```

Alternatif kısa hali:

```bash
wr
```

**Çıktı:**

```
Building configuration...
[OK]
```

### **2. ****************************`copy running-config startup-config`**************************** Komutu:**

* Bu komut, `running-config` içeriğini `startup-config` dosyasına açık bir şekilde kopyalar.
* Modern IOS sürümlerinde daha yaygın ve tercih edilen yöntemdir.

```bash
copy running-config startup-config
```

**İstem:**

```
Destination filename [startup-config]?
```

Burada **Enter** tuşuna basarsanız varsayılan hedef olan `startup-config` seçilir ve işlem tamamlanır.

### **Yapılandırma Yedekleme (isteğe bağlı bilgi):**

Aynı komut ile yapılandırmayı **TFTP sunucusuna yedeklemek** de mümkündür:

```bash
copy running-config tftp:
```

Bu şekilde dış ortamda yedekleme yapılabilir.

### **Kritik Not:**

* Eğer `running-config` dosyasında yaptığınız değişiklikleri kaydetmezseniz ve cihaz yeniden başlatılırsa **tüm ayarlar kaybolur.**
* Bu yüzden her yapılandırmadan sonra mutlaka aşağıdaki komutlardan biri kullanılmalıdır:

```bash
write memory
```

veya

```bash
copy running-config startup-config
```
## **Yapılandırma Dosyalarının Yedeklenmesi ve Geri Yüklenmesi**

Cisco cihazlarında `startup-config` veya `running-config` gibi yapılandırma dosyaları **yedeklenebilir** ve gerektiğinde **geri yüklenebilir**. Bu işlem; **TFTP**, **FTP**, veya **USB** gibi yöntemlerle gerçekleştirilir. Bu yedeklemeler, sistem arızası, konfigürasyon hataları ya da cihaz değiştirme durumlarında kritik önem taşır.

### 1. **TFTP Üzerinden Yedekleme ve Geri Yükleme**

### Gereksinimler:

* Aynı ağda çalışan bir **TFTP sunucusu** (örneğin: Tftpd32/Tftpd64)
* Router veya switch, TFTP sunucusuyla **iletişim kurabiliyor** olmalı (ping ile test edilebilir)

### Yedekleme (Running-config):

```bash
copy running-config tftp:
```

**İstemler:**

```
Address or name of remote host []? 192.168.1.100
Destination filename [running-config]? router_backup.cfg
```

Yedekleme tamamlandığında TFTP sunucusundaki belirtilen dizinde `.cfg` dosyası oluşur.

### Geri Yükleme (Startup-config veya Running-config):

```bash
copy tftp: running-config
```

**İstemler:**

```
Address or name of remote host []? 192.168.1.100
Source filename []? router_backup.cfg
```

Yüklenen yapılandırma **anında geçerli olur**, çünkü `running-config`’e aktarılır.

> İsteğe bağlı olarak şu şekilde `startup-config`’e de yükleme yapılabilir:

```bash
copy tftp: startup-config
```

> Ardından cihazı yeniden başlatmak gerekir:

```bash
reload
```

### 2. **FTP Üzerinden Yedekleme ve Geri Yükleme**

### Gereksinimler:

* Aktif bir **FTP sunucusu**
* FTP sunucusunda kullanıcı adı ve parola
* Cihazın FTP sunucusuna ağ erişimi olması

### Yedekleme:

```bash
copy running-config ftp:
```

**İstemler:**

```
Address or name of remote host []? 192.168.1.200
Destination filename [running-config]? router_ftp.cfg
Username? admin
Password? ****
```

### **Geri Yükleme:**

```bash
copy ftp: running-config
```

Aynı şekilde `startup-config`’e yüklemek isterseniz:

```bash
copy ftp: startup-config
```

##  Cisco Router ve Switch Cihazlarında Parola Kurtarma (Password Recovery)

Cisco cihazlara erişimi sağlayan **parolalar unutulduğunda**, cihazı sıfırlamadan **yapılandırmayı kaybetmeden** parola kurtarma işlemi yapılabilir. Bu işlemin temel mantığı:
- **Startup-config** dosyasını korumak,
- **Yapılandırmayı atlayarak** cihaza giriş yapmak,
- **Enable veya konsol parolasını sıfırlamak** ve
- **Config-register değerini eski haline getirerek** cihazı normal modda yeniden başlatmaktır.

Bu işlemler hem router hem switch cihazlar için benzer adımları izler.



###  Genel Yaklaşım

1. **Cihaz yeniden başlatılır ve açılışta ROMMON/Mode’a girilir.**
2. **Configuration Register değeri 0x2142 yapılır** (Startup-config atlanır).
3. Cihaz açılır, CLI’ye parolasız erişilir.
4. Startup-config dosyası RAM’e alınır.
5. Gerekli parolalar silinir veya değiştirilir.
6. Config-register değeri 0x2102’ye geri alınır.
7. Yapılandırma kaydedilir ve cihaz yeniden başlatılır.



###  Router'da Parola Kurtarma – Adım Adım

###  Senaryo: `enable secret` parolası unutulmuş



###  1. Cihazı Yeniden Başlat ve ROMMON’a Geç
- Cihaz açılırken klavyeden `Ctrl + Break` veya `Ctrl + Shift + 6, Break` tuşlarına bas.

Cihaz ROMMON moduna geçer (ekranda `rommon 1 >` gibi bir ifade görünür).


###  2. Configuration Register Değerini Değiştir
```bash
rommon 1 > confreg 0x2142
rommon 2 > reset
```

> Bu komutla cihaz, startup-config dosyasını atlayarak yeniden başlatılır.



###  3. Cihaz Açıldığında Initial Config Sihirbazını Atla
```
Would you like to enter the initial configuration dialog? [yes/no]: no
```


###  4. CLI’ye Giriş Yap ve Yapılandırmayı RAM’e Al
```bash
Router> enable
Router# copy startup-config running-config
```

> Şu anda tüm yapılandırma RAM’de, ama parola hala aktif.


###  5. Parolayı Sil veya Değiştir

```bash
Router# configure terminal
Router(config)# no enable secret
Router(config)# enable secret yeni-sifre
```

Gerekirse diğer parolaları da değiştir:
```bash
Router(config)# line console 0
Router(config-line)# password yeni-console
Router(config-line)# login
```


###  6. Config-Register’ı Varsayılana Geri Al
```bash
Router(config)# config-register 0x2102
Router(config)# end
```


###  7. Yapılandırmayı Kaydet ve Cihazı Yeniden Başlat
```bash
Router# write memory
Router# reload
```

Artık cihaz normal şekilde açılır ve yeni parolanızla giriş yapılabilir.


###  **Switch'te Parola Kurtarma**

Switch’lerde süreç router ile çok benzerdir. Ancak bazı modellerde ROMMON yerine **mode** tuşu bulunur.



###  1. Fiziksel Mode Tuşu ile ROMMON’a Gir

1. Switch'i kapat.
2. Ön paneldeki **Mode** butonuna basılı tut.
3. Cihazı açarken butonu basılı tutmaya devam et.
4. Ekranda `switch:` prompt’u çıktığında bırak.



###  2. Konfigürasyonu Atlamak İçin Environment Ayarı Yap
```bash
switch: flash_init
switch: load_helper
switch: rename flash:config.text flash:config.old
switch: boot
```

Bu komutlar ile cihaz config dosyasını görmeden açılır.


### 3. CLI'ye Gir ve Eski Konfigürasyonu Yükle
```bash
Switch> enable
Switch# rename flash:config.old flash:config.text
Switch# copy flash:config.text system:running-config
```



### 4. Parolaları Sıfırla
```bash
Switch# configure terminal
Switch(config)# no enable secret
Switch(config)# enable secret yeni-sifre
```


### 5. Kaydet ve Yeniden Başlat
```bash
Switch# write memory
Switch# reload
```


