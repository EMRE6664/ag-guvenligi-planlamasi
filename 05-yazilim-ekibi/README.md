# Şube ve Kapasite Bilgileri (Yazılım Geliştirme ve DevOps Ekibi)

## 1. Lokasyon, Mimari ve Kullanıcı Kapasitesi
Yazılım ve DevOps ekibi şubesi, şirketin dijital ürünlerinin kodlandığı, sürekli entegrasyon ve dağıtım (CI/CD) süreçlerinin yürütüldüğü, altyapı olarak "Agile (Çevik)" ve "Otomasyon" odaklı mühendislik ofisidir. Ağın hantal olmaması (katı IT kuralları) ile güvenli olması arasındaki ince çizginin sağlandığı bölgedir.
*   **Yazılım Mühendisleri (Backend, Frontend, Mobile vs.):** 120 Kişi
*   **DevOps, Sistem, Veritabanı (DBA) Uzmanları:** 20 Kişi
*   **İdari Personel:** 0 (Burası tamamen teknik bir mühendislik kampüsüdür).

## 2. Bant Genişliği, Ağ Profili ve Altyapı Analizi
*   **Ana İnternet Hattı:** 2 Gbps Metro Ethernet.
*   **Trafik Profili (Network Behavior):** 
    - Github/Gitlab repolarına devasa veri gönderme (Push) veya çekme (Pull) işlemleri.
    - NPM, PyPI, Maven, Docker Hub gibi paket/imaj depolarından sürekli modül indirme trafiği.
    - Yazılımcıların AWS, Azure, Google Cloud (GCP) üzerindeki test (Staging) ve canlı (Production) ortamlarına, sunucularına doğru yaptıkları API ve SSH istekleri (Sanallaştırma ve konteyner trafiği).

## 3. IP ve VLAN Segmentasyon Planı
Geliştiricilerin test ortamlarının şirket ağını tehlikeye atmaması için ciddi bir izolasyon (Micro-segmentation) gereklidir:
*   `VLAN 50` - Geliştirici Personel Ağı (Subnet: `10.5.50.0/24`)
*   `VLAN 60` - Test ve Staging Sunucuları Ağı (Dev/Test Environment)
*   `VLAN 70` - CI/CD Pipeline (Jenkins, GitLab CI) Sunucuları
*   *İzolasyon Kuralı:* Test ağındaki (VLAN 60) bir sunucunun, şirketin Merkez Ofisindeki veya Ar-Ge ofisindeki sistemlere erişimi kati suretle donanım firewall'unda blokludur (Deny All).

## 4. Ağ Erişim Kuralları ve Güvenlik Politikaları
*   **Gevşetilmiş IPS Kuralları (Exceptions):** Yazılımcıların işini yapabilmesi için IPS (Saldırı Önleme) kuralları esnetilir. Örneğin, bir güvenlik yazılımcısı Nmap veya Metasploit aracıyla test yaparken Firewall bunu "Saldırı" sanıp internetini kesmemelidir (False Positive önleme). Sadece bu ağ (VLAN 50) için IPS profili "Prevent (Engelle)" modundan "Detect/Log Only (Sadece Logla)" moduna çekilebilir.
*   **IaC (Infrastructure as Code) ve API İzni:** Güvenlik ekiplerine bilet (ticket) açıp port açılmasını beklemek günümüz DevOps kültüründe yavaştır. Yazılım ekibi Terraform veya Ansible kodlarıyla Firewall'un API'sine istek atarak test ortamları için kendi güvenlik kurallarını (Policy) otomatik oluşturup silebilir.
*   **Zero Trust (Jump Box) ve UFW Entegrasyonu:** Yazılımcılar doğrudan şirket içi sunuculara SSH yapamaz. Şirkette bir "Bastion Host / Jump Box" sunucusu bulunur. Bu Ubuntu sunucu üzerinde sıkı `ufw` kuralları vardır (`sudo ufw limit ssh` ile brute-force koruması). Yazılımcı önce buraya SSH yapar (loglanır), oradan diğer sistemlere zıplar. Jump Box'ta yine `ufw-logger` devrededir ve 5 başarısız girişte Telegram'a (SOC ekibine) alarm yollar.
