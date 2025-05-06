#  Ağ Cihazlarının Donanımsal Özellikleri ve Başlatılma Süreci



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

##  Packet Tracer ile Donanım Görselleştirme

Packet Tracer üzerinde bir Cisco router veya switch’e tıkladığınızda:

- **Physical Tab**: Donanımı ve modülleri görebilirsiniz.
- **Config Tab**: RAM’deki running-config’i düzenleyebilirsiniz.
- **CLI Tab**: IOS üzerinde komut satırıyla işlem yapabilirsiniz.

