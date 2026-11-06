# Ortak Güvenlik Duvarı Kurulum ve Entegrasyon Adımları (NGFW + OS Firewall)

Bir şubeye yeni bir güvenlik duvarı veya sunucu kurulurken izlenmesi gereken standart operasyon prosedürü (SOP) aşağıda detaylandırılmıştır. Donanımsal firewall'lara ek olarak, Keyvan Arasteh'in OS-Lab firewall yönergelerine dayanan UFW kurulumları da sisteme dahil edilmiştir.

## Faz 1: Donanımsal NGFW (Ağ Katmanı) Kurulumu
1. **Keşif (Site Survey) ve Montaj:** Cihazların sistem odasına UPS destekli çift PSU ile montajı.
2. **Kablolama ve Trunking:** WAN, LAN, DMZ, ve OOB (Out-of-Band) portlarının etiketlenmesi. LACP protokolü ile Switch'lere trunk yapılması.
3. **Firmware ve Lisanslama:** Üreticinin (Vendor) en stabil OS (işletim sistemi) sürümünün kurulması. IPS, Anti-Malware, URL Filtering lisanslarının doğrulattırılması.
4. **Temel Kural Yapılandırması:** 
   - `Default Deny` (Tüm trafiği sessizce düşür) kuralının listenin en altına (Bottom) yerleştirilmesi.
   - NAT (Network Address Translation) ayarları (Source NAT ve Destination NAT).
   - SD-WAN yapılandırması ve Failover testleri.

## Faz 2: İşletim Sistemi Seviyesi Firewall (Linux UFW Kurulumu)
Kurum içi tüm Ubuntu/Debian tabanlı sunucularda donanım firewall'una ek olarak UFW zorunlu kılınmıştır.

### UFW Temel Konfigürasyon Adımları
Linux işletim sistemlerinde `netfilter` altyapısını kullanan `iptables`'ı yönetmenin en güvenli yolu UFW'dir. Sunucu ayağa kalktığında ilk yapılacak işlemler:

1. **Varsayılan Politikaların Belirlenmesi:**
   Sıfır Güven (Zero Trust) felsefesi gereği, gelen tüm istekler reddedilmeli, sunucunun dışarı çıkışına izin verilmelidir.
   ```bash
   sudo ufw default deny incoming
   sudo ufw default allow outgoing
   ```
2. **Kritik Servislere İzin Verilmesi (Allow Rules):**
   Yönetim ve web trafiği için gerekli portlar açılır. SSH portu değiştirilmişse (Örn: 2222) o porta izin verilir.
   ```bash
   sudo ufw allow 22/tcp      # Standart SSH (Mümkünse IP kısıtlamalı yapılmalı)
   sudo ufw allow 80/tcp      # HTTP Trafiği
   sudo ufw allow 443/tcp     # HTTPS Trafiği
   ```
3. **IP ve Subnet Kısıtlamaları:**
   Sadece belirli bir ofisin (Örn: İstanbul HQ Yazılım Ekibi VLAN'ı) sunucuya erişmesine izin vermek için:
   ```bash
   sudo ufw allow from 10.0.50.0/24 to any port 22
   ```
4. **Loglamanın Aktف Edilmesi ve Sistemin Başlatılması:**
   UFW loglama seviyesi belirlenir ve firewall devreye alınır.
   ```bash
   sudo ufw logging on
   sudo ufw enable
   ```
5. **Durum ve Kural Kontrolü:**
   Uygulanan kuralların sırasıyla ve numaralandırılmış olarak listelenmesi:
   ```bash
   sudo ufw status numbered
   ```
