# 02-İstanbul Ofisi (HQ): Kapsamlı Kurulum ve Devreye Alma SOP'si

Bu lokasyondaki kurulum işlemi şubelerden farklı olarak çok daha karmaşık bir Active Directory, UFW ve Yedeklilik entegrasyonu gerektirir.

1.  **HA (High Availability) Cluster Konfigürasyonu:**
    - Birbirinin birebir aynısı iki adet Palo Alto PA-1410 cihaz rafa (rack) takılır.
    - `HA1 (Control Link)` ve `HA2 (Data/Session Link)` kabloları araya switch girmeden doğrudan iki cihaz arasına çekilir. 
    - Active-Passive mod yapılandırılarak, aktif cihazın anlık Session (oturum) tablosu pasif olana sürekli kopyalanır.
2.  **Kullanıcı Kimlik Entegrasyonu (User-ID Agent):**
    - Windows Domain Controller sunucusuna Palo Alto User-ID ajanı kurulur. Böylece log ekranında `10.1.110.15` yerine `ahmet.yilmaz` yazar. Bu olaylara (incident) müdahale hızını %80 artırır.
3.  **Tersine Şifre Çözme (SSL Inbound Inspection):**
    - DMZ'de bulunan kurumsal Web Sunucularının sertifikaları Firewall'a yüklenir. Böylece dışarıdan gelen HTTPS (şifreli) trafik firewall üzerinde çözülür (Decrypt), zararlı/Saldırı olup olmadığı IPS tarafından taranır, sonra sunucuya iletilir.
4.  **DMZ Sunucuları UFW ve Telegram Log Otomasyonu:**
    - Keyvan Arasteh 'OS-Lab' mimarisine sadık kalınarak, DMZ'deki Linux sunuculara şu ayarlar yapılır:
    ```bash
    sudo ufw default deny incoming
    sudo ufw allow 80,443/tcp
    # IT ofisinden SSH'a izin ver (Palo Alto VPN üzerinden geleni kabul et)
    sudo ufw allow from 10.1.120.0/24 to any port 22 
    sudo ufw enable
    ```
    - `/opt/ufw-logger/` dizinine kurulan Python/Bash scripti `systemd` ile ayağa kaldırılır. UFW log dosyasında `[UFW BLOCK]` ile engellenen Port 22 erişim denemeleri olduğunda (Örn: Brute-Force), SOC ekibinin Telegram grubuna anında Bot API üzerinden `{"chat_id": "-100xxxx", "text": "ALARM: DMZ-Web Sunucu 1 - SSH Tarama Engellendi"}` şeklinde JSON POST request atılır.
5.  **Simüle Edilmiş Kesinti Testi (Disaster Recovery):**
    - Mesai saatleri dışında ana Palo Alto cihazının kasıtlı olarak gücü (fişi) çekilir ve ikinci cihazın 1 saniyeden kısa sürede devreyi alıp almadığı test edilir.
