# Şirket Ağ Güvenliği Planlamasi ve OS-Seviyesi Firewall (UFW) Entegrasyon Projesi

## 1. Projenin Genişletilmiş Amacı ve Kapsamı
Bu proje, uluslararası çapta faaliyet gösteren ve Ankara, İstanbul, Londra ofislerinin yanı sıra devasa bir akademik şube (10.000+ öğrenci) ile yüksek gizlilik gerektiren Ar-Ge ve Yazılım ekiplerini barındıran devasa bir yapının siber güvenlik mimarisini kurgulamaktadır. 

Mimarimiz sadece sınır güvenliğini (Perimeter Security) sağlayan donanım tabanlı Yeni Nesil Güvenlik Duvarlarından (NGFW - Palo Alto, FortiGate, Check Point vb.) ibaret değildir. "Savunma Derinliği" (Defense in Depth) prensibince, ağın içindeki sunucuların bizzat kendilerini koruyabilmeleri adına İşletim Sistemi (OS) seviyesinde yapılandırılan, Keyvan Arasteh'in İşletim Sistemleri Laboratuvarı (os-lab) firewall konseptlerinden ilham alan **UFW (Uncomplicated Firewall) ve iptables** entegrasyonlarını da kapsamaktadır.

## 2. Karma Mimari Yaklaşım (Zero Trust + Host-Based Security)
Kurumsal ağ mimarisinde iki katmanlı bir savunma hattı uygulanmaktadır:
* **Ağ Katmanı (Network Layer):** Şubeler arası VPN tünellerini, kampüs ağının yük dengesini, L7 uygulama denetimlerini ve SSL şifre çözme (SSL Decryption) işlemlerini üstlenen donanımsal NGFW cihazları.
* **Uç Nokta ve Sunucu Katmanı (Host-Based Layer):** DMZ ve iç ağda çalışan Ubuntu/Linux sunucuların üzerinde çalışan, doğrudan çekirdek (kernel) seviyesinde netfilter kancalarına takılan UFW kuralları. Bir saldırgan donanımsal firewall'u atlatıp iç ağa sızsa bile, her sunucu kendi kapılarını UFW ile koruyacaktır.

## 3. Depo (Repository) Yapısı
Bu depo, profesyonel bir ağ güvenliği dokümantasyonu standartlarına göre hazırlanmıştır:
* **Kök Dizin Dosyaları:** Şirket genelindeki ortak standartları, UFW kurulumlarını, `ufw-logger` ve Telegram entegrasyonlu izleme mimarisini (SOC) barındırır.
* **Şube Klasörleri (01-06):** O lokasyona özel kapasite analizlerini, IP/VLAN segmentasyon tablolarını, cihaz seçimlerini ve teknik kurulum talimatlarını barındırır.
