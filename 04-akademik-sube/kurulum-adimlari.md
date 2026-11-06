# 04-Akademik Şube (Kampüs): Kapsamlı Kurulum ve Devreye Alma SOP'si

Kampüs kurulumundaki en kritik faktör, ağ kesintisinin 10.000 kişiyi etkilemesi nedeniyle yapılacak olan Kesinti Penceresi (Maintenance Window) planlaması ve 5651 yasal loglama zorunluluklarıdır.

1.  **Fiziksel Kurulum ve Trunking (Omurga Bağlantısı):**
    - Cihaz gece 03:00'te veri merkezine fiziksel olarak monte edilir.
    - Cihazın 40/100 Gbps QSFP+ portlarından, kampüsün Core (Omurga) Switch'ine fiber kablolarla LACP (Link Aggregation - Port Birleştirme) trunk'ları yapılır.
2.  **Yasal Loglama ve 5651 Uyumluluğu:**
    - Üniversite veya şirket, 10.000 öğrencinin hangi saatte hangi web sayfasına girdiğini yasal olarak (5651 Sayılı Kanun gereği) kaydetmek ve TÜBİTAK/Kamusal Zaman Damgası ile mühürlemek zorundadır.
    - FortiGate üzerindeki tüm Firewall ve DNS trafik logları, ağa kurulan bir **FortiAnalyzer** veya yerel SIEM (Splunk) sunucusuna kesintisiz akacak (Syslog) şekilde ayarlanır.
3.  **Kimlik Doğrulama (Eduroam / 802.1x) Entegrasyonu:**
    - Öğrenciler ağa kimliksiz bağlanamaz. RADIUS sunucusu ile Firewall entegre edilerek (Identity-Based Policies), loglarda anlamsız `10.15.x.x` IP'leri yerine doğrudan öğrencinin okul numarası veya e-posta adresi yazdırılır.
4.  **Trafik Şekillendirme (Traffic Shaper) Kuralları:**
    - Per-IP (IP Başına) hız kısıtlaması (Max 20 Mbps kuralı) "Shared" (Paylaşımlı) değil, "Per-IP" şablonuyla sisteme girilir ve IPv6 (varsa) kurallarına da uygulanır.
5.  **Laboratuvar Ortamı ve Host-Based (UFW) Güvenlik Otomasyonu:**
    - Bilgisayar mühendisliği veya ağ laboratuvarlarındaki öğrenci test sunucularına, `ufw-logger` scriptleri kurulur. Öğrenciler birbirlerinin sunucularına Nmap port taraması yaptığında, Telegram Bot API üzerinden hocaların telefonuna "Lab-01 Sunucusunda Tarama Tespit Edildi" bildirimi gidecek bir otomasyon mimarisi kurgulanır. Bu, Keyvan Arasteh'in OS derslerindeki "Görünürlük ve Otomasyon" pratiklerini gerçeğe dönüştürür.
