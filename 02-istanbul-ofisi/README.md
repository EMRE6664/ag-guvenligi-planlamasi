# Şube ve Kapasite Bilgileri (İstanbul Genel Merkez - HQ)

## 1. Lokasyon, Mimari ve Kullanıcı Kapasitesi
İstanbul ofisi, uluslararası şirketin ana yönetim merkezi (Headquarters - HQ), veri merkezinin (Data Center) barındığı ve en üst düzey şirket kararlarının alındığı yerleşkedir. Tüm ağ mimarisinin kalbi burasıdır.
*   **İdari, Finans, İK ve Yöneticiler:** 300 Kişi
*   **Sistem, Ağ, Sızma Testi ve Siber Güvenlik Ekibi (SOC):** 20 Kişi
*   *(Not: Yazılım ve Ar-Ge ekipleri bağımsız binalarda bulunmaktadır, HQ içinde değillerdir).*

## 2. Bant Genişliği, Ağ Profili ve Altyapı Analizi
*   **Ana İnternet Hattı:** 2 Gbps Tam Yedekli Metro Ethernet (Birbirinden bağımsız iki farklı servis sağlayıcı - ISP1 ve ISP2, iki farklı fiziksel rögardan ofise girer).
*   **Trafik Profili (Network Behavior):** 
    - Tüm şubelerden (Ankara, Londra, Kampüs vb.) gelen VPN tünellerinin ana toplanma noktasıdır (Hub).
    - Trafik çok büyük oranda "Dışarıdan İçeriye" (Inbound - Merkez sunuculara doğru) akar.
    - Ayrıca Veri Merkezinde barınan sunucular arası (East-West Traffic) trafik çok yoğundur.

## 3. IP ve VLAN Segmentasyon Planı
Kapsamlı bir iç ağ güvenlik mimarisi tasarlanmıştır:
*   `VLAN 100` - Yönetim Kurulu ve Üst Yöneticiler (Executives) (Limitsiz İnternet)
*   `VLAN 110` - İdari ve Finans Ekipleri (Sıkı web filtreli)
*   `VLAN 120` - IT ve SOC Ekipleri (Tüm portlara geçiş izni olan tek ağ)
*   `VLAN 200` - DMZ (Demilitarized Zone - İnternete açık sunucular: Web, Mail, Proxy)
*   `VLAN 999` - Guest Wi-Fi (Tamamen yalıtılmış Misafir Ağı)

## 4. Ağ Erişim Kuralları ve Güvenlik Politikaları
Bu ofis için "Strict Enterprise Security" (Sıkı Kurumsal Güvenlik) ve Zero Trust temelleri kurgulanmıştır.
*   **Kimlik Tabanlı Erişim (User-ID):** Güvenlik duvarı kurallarında IP adresleri yazmaz. Şirketin Active Directory (Windows Server) yapısıyla entegre olunur. Kuralda IP yerine grup yazar: "Eğer kullanıcı 'Finans_Grubu'ndaysa, DMZ'deki 'Muhasebe_SQL_Sunucusu'na 1433 portundan erişsin." 
*   **Misafir Ağı (Captive Portal):** Ofise gelen misafirler için şirket ağına fiziksel erişim bile olsa kurumsal kaynaklara ulaşım (Deny) yasaktır. Misafirler yalnızca TC Kimlik Numarası (veya Yabancı Pasaport No) ile doğrulama yapıp cep telefonlarına gelen SMS şifresi ile internete çıkabilirler (5651 Sayılı loglama Kanunu gereği).
*   **Sunucu Seviyesi Güvenlik (UFW ve Logger):** DMZ bölgesindeki (VLAN 200) tüm Linux tabanlı web ve proxy sunucularında `ufw` zorunlu aktif edilmiştir. Keyvan Arasteh'in otomasyon pratikleri uyarınca `ufw-logger` scripti bu sunucularda çalışır ve yetkisiz SSH/HTTP taramalarını (Nmap scans) anında SOC ekibinin Telegram kanalına iletir.
