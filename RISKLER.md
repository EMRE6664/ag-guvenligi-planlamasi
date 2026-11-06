# Siber Güvenlik Risk Yönetimi ve Tehdit Modellemesi

Şirketimizin geniş organizasyon şeması (Ar-Ge, Öğrenciler, Yazılımcılar) farklı siber tehdit vektörleri barındırmaktadır. Bu risklerin detaylı analizi aşağıdadır:

## 1. Kritik Varlıklarımız (Neyi Koruyoruz?)
* **PII (Kişisel Veriler):** 10.000 öğrencinin notları, sağlık kayıtları, personelin özlük ve maaş bilgileri (KVKK/GDPR uyumu zorunlu).
* **Fikri Mülkiyet (IP):** Ar-Ge laboratuvarlarında geliştirilen yeni patentli projelerin CAD çizimleri ve algoritmaları.
* **Kaynak Kod (Source Code):** Yazılım ekibinin CI/CD süreçlerinden geçirdiği mikroservis kodları.

## 2. Derinlemesine Tehdit Vektörleri
| Tehdit Tipi | Açıklama ve Etki Alanı | Hedef Şube | Risk Seviyesi |
| :--- | :--- | :--- | :--- |
| **Gelişmiş Sürekli Tehdit (APT)** | Devlet destekli veya profesyonel hacker gruplarının Ar-Ge ağına sızıp aylarca sessiz kalması. | Ar-Ge Ekibi | Kritik (Kırmızı) |
| **DDoS (Hizmet Aksatma)** | Akademik yerleşkede öğrencilerin botnet kurarak dışarıya veya içeriye 20Gbps'lik SYN Flood yapması. | Akademik Şube | Kritik (Kırmızı) |
| **Ransomware Yayılımı (Lateral Movement)** | Ankara ofisindeki bir çalışanın tıkladığı zararlı eklentinin (Phishing), SMB (Port 445) üzerinden sunuculara sıçraması. | İstanbul Merkez ve Ankara | Yüksek (Turuncu) |
| **Sıfırıncı Gün (Zero-Day) Açıkları** | Sunuculardaki Apache/Nginx veya işletim sistemi (Linux/Windows) güvenlik açıklarının UFW/IPTables konfigürasyonu zayıfken sömürülmesi. | Yazılım Ekibi / Sunucular | Yüksek (Turuncu) |
| **Shadow IT / Yetkisiz VPN** | Londra'daki kısıtlı personelin güvenlik duvarını aşmak için şirket bilgisayarına TOR browser veya yetkisiz VPN kurması. | Londra | Orta (Sarı) |

## 3. Risk Azaltma (Mitigasyon)
Bu riskleri minimuma indirmek için Ağ Segmentasyonu (VLAN'lar arası strict routing), Zero Trust Network Access (ZTNA) profilleri ve UFW ile donanım firewall'unun senkronize çalıştığı "Çok Katmanlı Savunma" uygulanmaktadır.
