# 05-Yazılım Ekibi (DevOps): Kapsamlı Kurulum ve Devreye Alma SOP'si

Yazılım ekibindeki kurulum, cihazın prize takılmasından ziyade yazılım mimarisine kod üzerinden (IaC - Infrastructure as Code) entegre edilmesine dayanır.

1.  **Distributed (Dağıtık) Mimari Kurulumu (Check Point):**
    - Check Point cihazları "All-in-one" çalıştırılmaz. Önce Sanal (VMWare) veya bulut ortamında bir **"Security Management Server (SMS)"** ayağa kaldırılır. Bu beynin kendisidir.
    - Fiziksel Quantum 6400 cihazı ise "Security Gateway" olarak ağa bağlanır ve SIC (Secure Internal Communication) şifreli sertifikası ile Management Server'a tanıtılır.
2.  **Otomasyon (API Key) Yapılandırması:**
    - Firewall üzerinde DevOps ekibi için (Örn: Jenkins sunucusu kullanacak) sınırlı yetkilere sahip bir "Service Account (API Kullanıcısı)" oluşturulur.
    - Terraform ile test amaçlı olarak "Dummy_Web_Server_Kuralı" isimli bir kural kod üzerinden Firewall'u post edilir ve Policy Install (Kural Kurulumu) işleminin otomatik tetiklendiği doğrulanır.
3.  **Sunucularda Host-Based Defense (Keyvan Arasteh - OS Lab Mimarisi):**
    - Sadece donanımsal Firewall'u güvenilmez. Geliştirilen yazılımların çalıştığı tüm test/dev Ubuntu sunucularında IPTables/UFW pratikleri uygulanır.
    - Sunucunun UFW konfigürasyonu Ansible ile tüm makinelere basılır:
    ```bash
    # Ansible ile tüm test makinelerinde çalıştırılacak shell komutları:
    sudo ufw default deny incoming
    sudo ufw allow in on eth1 from 10.5.70.0/24 to any port 8080 # CI/CD erisimi
    sudo ufw logging on
    sudo ufw --force enable
    ```
4.  **Veri Sızıntısı (DLP) Regex Kontrolleri:**
    - Yazılımcıların yanlışlıkla şirket içi AWS API Key'lerini (Root Password, Secret Token) veya veritabanı şifrelerini GitHub/Pastebin gibi açık ortamlara kopyalamasını engellemek için, Check Point'in Data Loss Prevention modülüne bu token yapılarına uyan "Düzenli İfadeler (Regular Expressions - Regex)" girilir. Tespit edildiğinde Drop edilir ve loglanır.
5.  **UFW-Logger ve Telegram Entegrasyon Doğrulaması:**
    - Test sunucularına Nmap ile Port 22 (SSH) taraması yapılır. `ufw` bu taramayı engeller, `/var/log/ufw.log` dosyasına yazar. `/opt/ufw-logger/` klasöründe koşan Python scripti bunu yakalar ve saniyeler içinde "Sistem Yöneticileri" Telegram kanalına "Test Sunucusu - Nmap Taraması Engellendi" şeklinde HTTP POST atarak SOC entegrasyon testini (UAT) tamamlar.
