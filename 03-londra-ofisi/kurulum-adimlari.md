# 03-Londra Ofisi: Kapsamlı Kurulum ve Devreye Alma SOP'si

Londra kurulumu, şirketin diğer ofislerinde görülmeyen "Bulut Üzerinden Yönetim (Cloud-Native)" stratejisiyle gerçekleştirilir. 

1.  **Bulut Paneli (Dashboard) Hazırlığı (İstanbul'da Uygulanır):**
    - Cihaz kargoya verilip Londra'ya ulaşmadan günler önce, cihazın arkasındaki "MAC/Serial Number" İstanbul'daki SOC ekibi tarafından `dashboard.meraki.com` paneline tanımlanır.
    - Şube Network Template'i oluşturulur: (VLAN 10, VLAN 90 IP'leri, DHCP server ayarları).
    - Web filtreleme kuralları (Adult, Gambling block) ve IPS (Saldırı önleme modu: Prevention) açılır.
2.  **Fiziksel Kurulum ve Otomatik Besleme (Londra'da Uygulanır):**
    - Londra'daki idari bir asistan kutuyu açar, adaptörü fişe, internet kablosunu cihazın WAN girişine (Internet 1) takar.
    - Cihaz DHCP'den bir IP alır, internete çıkar çıkmaz Cisco sunucularına ulaşıp Firmware güncellemesini yapar, reboot eder ve LED ışığı beyaza döndüğünde sistem tamamen hazırdır. Konsol kablosu veya CLI komutu girilmez.
3.  **Auto-VPN Entegrasyonu ve Testi:**
    - Cihaz yeşile döndükten saniyeler sonra, İstanbul ile IPsec VPN tüneli bulut üzerinden otomatik kurulur.
    - Londra'dan bir dizüstü bilgisayarla İstanbul'daki ERP sunucusuna ping atılır ve bağlantı doğrulanır.
4.  **Log Entegrasyonu:**
    - Cihazın ürettiği loglar (Event Logs ve Flow Logs) Meraki API'si ve Syslog yönlendirmesiyle güvenli bir tünel üzerinden İstanbul'daki ana SIEM (Loglama) sunucusuna gönderilerek merkezi izleme (Centralized Monitoring) sağlanır.
