# Şube ve Kapasite Bilgileri (Akademik Yerleşke / Üniversite Kampüsü)

## 1. Lokasyon, Mimari ve Kullanıcı Kapasitesi
Üniversite kampüs (Akademik) ağı, ağ yöneticilerinin kabusu olan, anomali trafiğinin (Korsan yazılım, botnet yayılımı, P2P/Torrent paylaşımları, sürekli değişen cihazlar - BYOD) dünyada en yoğun ve en karmaşık yaşandığı ekosistemdir.
*   **Öğrenci Sayısı (BYOD):** 10.000+ (Her öğrencinin en az 2 veya 3 cihazı var: Akıllı Telefon, Laptop, Tablet).
*   **Akademisyenler (Hocalar):** 500
*   **İdari ve Destek Personeli:** 150
*   **Yerel Kampüs IT / Teknik Ekibi:** 30

## 2. Bant Genişliği, Ağ Profili ve Altyapı Analizi
*   **İnternet Hattı:** 20 Gbps (veya daha fazlası) Yüksek Kapasiteli Metro Fiber İletişim, 10G veya 40G QSFP+ portlarla backbone (omurga) switch'e bağlanır.
*   **Trafik Profili ve Darboğaz (Bottleneck) Analizi:** Kampüs ağlarında bant genişliği (Throughput) önemlidir, ancak cihazı çökerten asıl unsur **"Eşzamanlı Oturum (Concurrent Session)"** ve **"Saniyedeki Yeni Oturum (New Sessions Per Second)"** oranlarıdır. Örneğin bir öğrenci torrent programı açtığında veya çok sekme açtığında tek başına binlerce UDP oturumu başlatır. 10.000 öğrencinin bu davranışı standart bir Firewall'un işlemcisini (CPU) dakikalar içinde %100'e kilitler (Session Exhaustion Attack mantığı). Yüksek UDP paket oranlarına dayanıklı bir mimari şarttır.

## 3. IP ve VLAN Segmentasyon Planı (Kaba Hatlarıyla)
*   `VLAN 100-199` - Öğrenci Ağları (Eduroam) (Binlerce IP, /16 veya /20 bloklar)
*   `VLAN 200` - Akademisyen ve Laboratuvar Ağı
*   `VLAN 300` - İdari Ağ (Öğrenci İşleri ve Sunucular)
*   *Güvenlik Zafiyeti Önlemi:* VLAN'lar arası geçişte "Öğrenci ağından İdari Sunuculara" giden tüm (Any) trafik kati suretle blokludur (Network Isolation).

## 4. Ağ Erişim Kuralları ve Güvenlik Politikaları
Kampüsler kurumsal şirket gibi çok sıkı kısıtlanamaz, ancak yasal sınırları korumak şarttır.
*   **Traffic Shaping ve QoS (Trafik Şekillendirme):** 
    - 20 Gbps devasa bir hız olsa da 10.000 kişi için sınırsız değildir. Öğrenci başına "Per-IP Bandwidth Limit (Örn: Max 20 Mbps Download / 5 Mbps Upload)" kuralı uygulanır ki kimse hattı sömüremesin.
    - P2P (BitTorrent vb.) ve Crypto-Mining uygulamaları "App Control" modülüyle kökten düşürülür (Drop).
*   **Tehdit ve C&C İzolasyonu:** Yüzlerce virüslü (Trojan) öğrenci cihazı ağı kullanır. Firewall'un IPS'i (Saldırı Önleme Sistemi) bir Command & Control (Botnet merkezine haberleşme) trafiği yakaladığında, entegre NAC (Network Access Control) sistemiyle cihazın Switch portunu "Karantina VLAN"ına (Sadece virüs uyarı sayfası) düşürür.
*   **Öğrenci Projeleri İçin UFW Standartları:** Akademik projelerde kurulan Linux sunucularda hocaların (Keyvan Arasteh metodolojisi) OS-lab ilkelerine uygun olarak iptables/UFW yapılandırması zorunludur. `ufw default deny incoming` ve sadece port 80 açılışı, öğrencilere host-based güvenliği öğretmek için uygulanır.
