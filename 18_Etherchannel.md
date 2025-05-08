#  ETHERCHANNEL 

## 1. EtherChannel Nedir?

**EtherChannel**, birden fazla fiziksel bağlantının tek bir mantıksal bağlantı gibi gruplanmasını sağlayan bir bağlantı birleştirme (link aggregation) teknolojisidir. Cisco tarafından geliştirilmiş olan bu teknoloji, IEEE’nin standartlaştırılmış sürümü olan **LACP (IEEE 802.3ad)** ile desteklenmiştir.

EtherChannel; Layer 2 (Switch-to-Switch, Switch-to-Host) veya Layer 3 (Routing) seviyelerinde kullanılabilir.



## 2. EtherChannel’in Temel Amaçları

| Amaç | Açıklama |
|------|----------|
| **Bant Genişliğini Artırmak** | Birden fazla fiziksel bağlantı, bir mantıksal bağlantı gibi çalışarak toplam veri iletim kapasitesini artırır. |
| **Yedeklilik Sağlamak** | Bir bağlantı koparsa, diğer bağlantılar devreye girer; bağlantı sürekliliği bozulmaz. |
| **STP Uyumluluğu** | STP (Spanning Tree Protocol), EtherChannel’i tek bir bağlantı gibi görür, böylece yedek portları engellemesine gerek kalmaz. |
| **Yük Dengeleme** | Trafik, MAC adresi, IP adresi, TCP/UDP portları gibi kriterlere göre fiziksel bağlantılar arasında paylaştırılır. |



## 3. EtherChannel Türleri

### A) **Statik EtherChannel (Manuel)**

- Her iki cihazda EtherChannel yapılandırması manuel olarak yapılır.
- Protokol kullanılmaz.
- Uyumlu port konfigürasyonu çok önemlidir.

### B) **Dinamik EtherChannel (Protokollü)**

| Protokol | Açılımı | Standardı | Açıklama |
|----------|---------|-----------|----------|
| **PAgP** | Port Aggregation Protocol | Cisco Özel | Cisco cihazlar arasında dinamik EtherChannel oluşturur. |
| **LACP** | Link Aggregation Control Protocol | IEEE 802.3ad | Vendor bağımsız cihazlar arasında dinamik EtherChannel kurulumuna olanak tanır. |


## 4. EtherChannel Protokolleri ve Modları

### 🔹 **PAgP Modları (Cisco Only)**

| Mod | Anlamı | Etkileşim |
|-----|--------|------------|
| **auto** | Pasif mod, bağlantı kurmaz ama gelen isteğe cevap verir | `auto-desirable` veya `desirable-desirable` çalışır |
| **desirable** | Aktif olarak bağlantı kurmak ister | |

> `auto-auto` çalışmaz, çünkü iki taraf da pasiftir.


### 🔹 **LACP Modları (IEEE Standard)**

| Mod | Anlamı | Etkileşim |
|-----|--------|------------|
| **passive** | Pasif mod, sadece gelen LACP mesajlarına yanıt verir | `active-passive` veya `active-active` çalışır |
| **active** | Aktif olarak LACP mesajları gönderir | |

> `passive-passive` çalışmaz, çünkü her iki taraf da girişim başlatmaz.



## 5. EtherChannel Gereksinimleri

1. **Port Özellikleri Aynı Olmalı:**
   - Hız (`speed`)
   - Duplex modu
   - VLAN üyeliği
   - Trunk / Access modu
2. **Port Sayısı:**
   - LACP: Maksimum 16 bağlantı yapılabilir (8 aktif, 8 yedek)
   - PAgP: Maksimum 8 aktif bağlantı
3. **Layer Uyumluluğu:**
   - Layer 2: `switchport` modunda
   - Layer 3: IP adresi atanmış `port-channel` arayüzü



## 6. EtherChannel Yük Dengeleme Kriterleri

EtherChannel, veriyi hangi port üzerinden ileteceğine karar verirken yük dengeleme algoritmaları kullanır:

| Kriter                  | Açıklama |
|-------------------------|----------|
| Source MAC Address      | Gönderen MAC adresine göre |
| Destination MAC Address | Alıcı MAC adresine göre |
| Source & Destination MAC | Her ikisine göre hash yapılır |
| Source IP Address       | Gönderen IP adresine göre |
| Destination IP Address  | Alıcı IP adresine göre |
| Source & Destination IP | Her ikisine göre hash yapılır |

> `show etherchannel load-balance` komutu ile kullanılan algoritma öğrenilebilir.



## 7. STP ile Etkileşimi

- STP, bir EtherChannel grubunu **tek bir bağlantı** gibi görür.
- Eğer EtherChannel kurulmasaydı, STP yedek bağlantıları **bloklayabilirdi.**
- Bu yapı sayesinde **fazladan portların bloklanmasının** önüne geçilir.
- STP, Port-Channel arayüzü üzerinden BPDU gönderir ve alır.


## 8. Hatalar ve Sorunlar

| Sorun | Neden | Çözüm |
|-------|-------|--------|
| `suspended` durumu | Farklı hız, duplex, VLAN, port modları | Portları `default` hale getirip baştan yapılandır |
| Protokol uyuşmazlığı | Bir taraf PAgP, diğer taraf LACP veya statik olabilir | Her iki tarafın aynı protokolü kullandığından emin ol |
| VLAN mismatch | Portlar farklı VLAN’da | Uyumlu VLAN ayarı yap |
| LACP link’lerden biri `standby` oluyor | Maksimum 8 aktif link aşılmış olabilir | Gereksiz bağlantıyı kaldır ya da yapılandırmayı kontrol et |


## 9. Güvenlik Önerileri

- EtherChannel sadece güvenilir cihazlar arasında yapılandırılmalı.
- STP ile birlikte şu önlemler önerilir:
  - **BPDU Guard:** Access portlarında etkinleştir.
  - **Port Security:** Belirli MAC adreslerini sınırla.
  - **Root Guard:** Switch’in root bridge olmasını engelle.
- **Unused portlar kapatılmalı.**



## 10. Kullanım Alanları

| Cihazlar Arası | Senaryo |
|----------------|---------|
| Switch - Switch | Core – Distribution bağlantıları |
| Switch - Server | NIC teaming ile yüksek performans |
| Switch - Router | Router-on-a-stick yapılandırmalarında trunk üzerinden |
| Data Center | Yüksek performanslı sistemler için |



## 11. Layer 2 vs Layer 3 EtherChannel

| Özellik | Layer 2 EtherChannel | Layer 3 EtherChannel |
|---------|----------------------|----------------------|
| Kullanım Yeri | Switch-to-Switch (trunk) | Switch-to-Router veya L3 Switch-to-L3 Switch |
| IP Atama | Hayır | Evet |
| VLAN Taşır | Evet (trunk) | Hayır |
| Yönlendirme Yapabilir | Hayır | Evet |


## 12. Komut Özeti 

| Komut | Açıklama |
|--------|----------|
| `interface range` | Çoklu port yapılandırması |
| `channel-group <no> mode <mod>` | Portları gruba dahil et |
| `interface port-channel <no>` | Mantıksal EtherChannel arayüzü |
| `show etherchannel summary` | Genel durum bilgisi |
| `show interfaces port-channel` | Fiziksel bağlantı detayı |
| `show etherchannel load-balance` | Yük dengeleme algoritması kontrolü |



#  EtherChannel Yapılandırma Örnekleri (Packet Tracer)

**Topoloji Önerisi:**  
- 2 adet Switch (örneğin: **SW1** ve **SW2**)  
- Her switch’te 2 port (örneğin: **FastEthernet0/1** ve **FastEthernet0/2**)  
- Portlar doğrudan birbirine bağlanacak.  
- VLAN 10 üzerinde trunk yapılandırılacak (Layer 2 senaryosu).

---

##  1. Statik EtherChannel Yapılandırması 

> Bu yapılandırma, hiçbir protokol (PAgP veya LACP) kullanmadan doğrudan manuel yapılır.

###  SW1’de Yapılacaklar:

```bash
enable
configure terminal
interface range fa0/1 - 2
switchport mode trunk
channel-group 1 mode on
exit

interface port-channel 1
switchport mode trunk
exit
```

###  SW2’de Yapılacaklar:

```bash
enable
configure terminal
interface range fa0/1 - 2
switchport mode trunk
channel-group 1 mode on
exit

interface port-channel 1
switchport mode trunk
exit
```

 **Açıklama:**  
- `mode on`: Statik EtherChannel oluşturur, protokol kullanılmaz.  
- Her iki taraf da “on” olmalı.

---

##  2. PAgP ile EtherChannel (Cisco Protokolü)

> PAgP sadece **Cisco cihazlarda** çalışır.

###  SW1 – Aktif (Desirable) Mod:

```bash
enable
configure terminal
interface range fa0/1 - 2
switchport mode trunk
channel-group 1 mode desirable
exit

interface port-channel 1
switchport mode trunk
exit
```

###  SW2 – Pasif (Auto) Mod:

```bash
enable
configure terminal
interface range fa0/1 - 2
switchport mode trunk
channel-group 1 mode auto
exit

interface port-channel 1
switchport mode trunk
exit
```

 **Açıklama:**
- `desirable-auto` eşleşmesi PAgP protokolüyle çalışır.
- `auto-auto` veya `desirable-desirable` da çalışır ama bir taraf mutlaka aktif olmalı.

 **Durum Kontrolü:**  
```bash
show etherchannel summary
```

---

##  3. LACP ile EtherChannel (IEEE 802.3ad Standardı)

> Cisco dışı cihazlarla uyumludur. Cisco’da da desteklenir.

###  SW1 – Aktif Mod:

```bash
enable
configure terminal
interface range fa0/1 - 2
switchport mode trunk
channel-group 1 mode active
exit

interface port-channel 1
switchport mode trunk
exit
```

###  SW2 – Passive Mod:

```bash
enable
configure terminal
interface range fa0/1 - 2
switchport mode trunk
channel-group 1 mode passive
exit

interface port-channel 1
switchport mode trunk
exit
```

**Açıklama:**  
- `active-passive` veya `active-active` çalışır.  
- `passive-passive` çalışmaz çünkü ikisi de bekler.

---

##  Ortak Test Komutları

EtherChannel’in doğru çalıştığını doğrulamak için her switch’te aşağıdaki komutları kullanabilirsin:

```bash
show etherchannel summary
show interfaces port-channel 1
show spanning-tree
```

---

## Hatalı Durumların Kontrolü

```bash
show etherchannel summary
```

| Durum | Açıklama |
|-------|----------|
| `P`   | Protokol: PAgP |
| `L`   | Protokol: LACP |
| `U`   | Kullanımda |
| `D`   | Down / çalışmıyor |
| `s`   | Suspended / yapılandırma hatası |
| `I`   | Individual – EtherChannel’a dahil edilmemiş |


