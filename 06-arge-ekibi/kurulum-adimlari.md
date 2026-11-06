# 06-Ar-Ge Ekibi: Kapsamlı Kurulum ve Devreye Alma (Sıfır Güven) SOP'si

Ar-Ge ofisindeki kurulum "Hiçbir Cihaza, Hiçbir Kullanıcıya ve Hiçbir Ağ Trafiğine Güvenme" felsefesiyle, tamamen yalıtılmış bir ağ inşası üzerine programlanmıştır.

1.  **Ağ İzolasyonu ve Segmentasyon:** 
    - Ar-Ge Firewall'u şirketin ana ağına bağlıdır (Yalnızca Yönetim ve Loglama için VPN vardır). Ancak, şirketin diğer bölümlerindeki kullanıcıların (İstanbul Genel Merkez veya Ankara İdari Ekibi vs.) Ar-Ge içindeki kaynak kod veya tasarım sunucularına RDP, SMB veya SSH yapması ağ, donanım ve IP seviyesinde "Deny All" kuralı ile kesilmiştir.
2.  **SSL Şifre Çözme (Forward Proxy) Konfigürasyonunun Kurulması:**
    - Firewall'un şifreli trafiği okuyabilmesi için Palo Alto PA-450 cihazında yerel bir Root CA (Sertifika Otoritesi) sertifikası üretilir.
    - Bu sertifika, Active Directory GPO (Group Policy Object) veya EDR yazılımı üzerinden tüm Ar-Ge mühendislerinin Windows/Linux bilgisayarlarına "Güvenilen Kök Sertifika (Trusted Root)" olarak otomatik yüklenir.
    - Böylece mühendisler internete (Örn: Google, Github) HTTPS ile çıktığında tarayıcılarında sertifika hatası almaz, ancak Firewall arka planda her paketin şifresini çözerek (Decrypt), içindeki veriyi kopyalayıp tarayabilir (Deep Packet Inspection).
3.  **Hassas DLP (Data Loss Prevention) Kuralları:**
    - Şirketin kaynak kodlarının yapıları (Örn: Python Scriptleri, C++ Class'ları) veya gizli projelerin adlarını içeren Düzenli İfade (Regular Expressions - Regex) kuralları Firewall'un Content-ID profiline eklenir.
    - Biri kodları kopyalayıp Github'a, Pastebin'e veya şifreli bir foruma HTTP/HTTPS POST komutuyla (Upload) yapıştırdığında, Firewall bağlantıyı her iki uçtan (Reset-Both) milisaniye içinde koparır. Ekrana "Şirket Politikası İhlali: Veri Sızdırma Engellendi" sayfası çıkar.
4.  **Host-Based Firewall (UFW) ve Laboratuvar Uygulamaları:**
    - Keyvan Arasteh'in OS-Lab firewall yönergeleri çerçevesinde, laboratuvar içindeki tasarım prototip sunucularının tamamında (Ubuntu/Linux tabanlı olanlar) yerleşik `ufw` komut setleri zorunludur:
    ```bash
    # Tüm gelen ve giden trafiği varsayılan olarak kes
    sudo ufw default deny incoming
    sudo ufw default deny outgoing
    
    # Sadece yönetim ve log sunucusuna kısıtlı erişim aç
    sudo ufw allow out to 10.6.20.5 port 514/udp # Log sunucusu
    sudo ufw allow in from 10.6.10.100 to any port 22 # IT Yonetici IP'si
    sudo ufw logging full
    sudo ufw enable
    ```
5.  **Otomasyon Entegrasyonu (Telegram ufw-logger Testi):**
    - Sunucudaki `ufw.log` dosyasını `tail -f` ile dinleyen Python tabanlı otomasyon aracı (`ufw-logger`), yetkisiz bir Ar-Ge mühendisi `10.6.10.100` harici bir IP'den sunucuya ping atmaya veya SSH yapmaya kalkıştığında logu yakalar.
    - Saniyeler içinde, Firewall'un sadece belirli URL'lere izin verdiği güvenli Telegram API (api.telegram.org) tüneli üzerinden, SOC L3 Analist (Tehdit Avcıları) grubuna "ALARM: Ar-Ge Prototip Sunucusuna Yetkisiz Erişim Denemesi Bloklandı" mesajı (JSON HTTP POST) gönderilir ve test (UAT) sonlandırılır.
