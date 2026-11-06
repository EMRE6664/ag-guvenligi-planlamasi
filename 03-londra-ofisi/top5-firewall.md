# Londra Ofisi: Top 5 Güvenlik Duvarı Adayı ve Detaylı Analiz

Uzakta olan, teknik personeli (ağ uzmanı) bulunmayan ve cihaz bozulursa yerine yenisinin hızlıca kurulması gereken (Plug-and-Play) şubeler için "Zero-Touch Provisioning (Sıfır Dokunuşla Kurulum)" özelliğine sahip NGFW ve UTM cihazları değerlendirilmiştir.

## Adaylar Listesi ve Pazar Karşılaştırması
1.  **Cisco Meraki MX68** (Otel, kafe ve uzak ofislerin kralı, %100 bulut tabanlı)
2.  **Sophos XGS 116** (Küçük şubeler için güçlü performans ve entegre switch portları)
3.  **FortiGate 60F** (Dünyanın en çok satan uzak şube Firewall cihazı)
4.  **Palo Alto PA-410** (Kurumsal seviye güvenliği küçük ofise getiren donanım)
5.  **WatchGuard M290** (Kompakt ve yönetimi kolay KOBİ/Şube cihazı)

## Seçilen Cihaz ve Mimari Karar: **Cisco Meraki MX68**

### Tercih Edilme Gerekçeleri (Neden Seçtik?):
*   **Zero-Touch Provisioning (Sıfır Dokunuşla Kurulum):** Londra ofisinde sadece 2 yerel IT asistanı vardır. Bir cihaz arızalandığında veya yeni bir şube açıldığında, donanım kutusuyla gelir. Herhangi biri kutuyu açıp WAN portuna internet kablosunu taktığı an, cihaz Cisco bulutuna bağlanıp seri numarasını doğrular, İstanbul ekibinin günler öncesinden buluta girdiği kuralları (Templates), VLAN'ları ve VPN ayarlarını 5 dakika içinde indirip kendini ayağa kaldırır. Londra'da uzman ihtiyacı sıfırlanır.
*   **Auto-VPN (Otomatik VPN Mesh):** İstanbul ile Londra arasında IPsec tüneli (Phase 1, Phase 2, IKEv2 anahtarları vs.) kurmak klasik cihazlarda (Fortinet/Palo Alto) detaylı bir işlemdir. Meraki Cloud Dashboard üzerinde sadece "Site-to-Site VPN'i Aç ve Hub olarak İstanbul'u seç" tuşuna tıklanır. Tüm şifreleme ve key-exchange (anahtar değişimi) arka planda otomatik yapılır. 
*   **Bütünleşik İzleme Paneli:** Londra ofisindeki Meraki Access Point'ler (Wi-Fi) ve Meraki switch'ler ile birlikte cihaz tek bir bulut dashboard ekranından izlenip yönetilebilir (Single Pane of Glass).

## Rakiplerin Elenme Nedenleri (Neden Seçmedik?):
*   *FortiGate 60F & Sophos 116:* FortiGate 60F teknik özellik (throughput, IPSec hızı, antivirüs performansı) olarak Meraki MX68'den kağıt üzerinde çok daha güçlüdür ve uzun vadede lisans maliyeti daha uygundur. Ancak, yönetim arayüzünün karmaşıklığı ve VPN sorunlarını çözmek (Troubleshooting) için ciddi teknik tecrübe gerektirmesi (Command Line - CLI becerisi), Londra ofisinin yapısına ("Tak ve unut" konseptine) uymadığı için tercih edilmemiştir.
*   *Palo Alto PA-410:* Kurumsal güvenliği küçük donanıma sığdırır, harikadır; ancak 50 kişilik satış personeli için (Ar-Ge veya yazılım yapmıyorlar) cihazın donanım fiyatı ve Threat Prevention lisansları çok ciddi bir "Overkill (Gereksiz aşırı güç)" yatırımı olacaktır.
