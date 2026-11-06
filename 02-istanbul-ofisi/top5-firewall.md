# İstanbul Genel Merkez (HQ): Top 5 Güvenlik Duvarı Adayı ve Detaylı Analiz

Merkez ofisin hem veri merkezi güvenliğini sağlaması hem de binlerce IPsec VPN tünelini şifreleyerek yönetmesi gerektiği için üst düzey "Enterprise High-End" cihazlar (Uygulama Katmanı L7 odaklı) yarışmıştır.

## Adaylar Listesi ve Pazar Karşılaştırması
1.  **Palo Alto PA-1410** (Makine öğrenimi destekli Single-Pass Architecture, Üstün App-ID)
2.  **FortiGate 400F** (Maliyet-performans kralı, SPU/ASIC donanım hızlandırma)
3.  **Check Point Quantum 6200** (SmartConsole ile rakipsiz çok katmanlı kural yönetimi)
4.  **Cisco Secure Firewall 3110** (Snort 3 IPS motoru ve XDR entegrasyonu)
5.  **Sophos XGS 3300** (Xstream mimarisi ile güçlü TLS şifre çözme)

## Seçilen Cihaz ve Mimari Karar: **Palo Alto PA-1410 (Active-Passive High Availability Cluster)**

### Tercih Edilme Gerekçeleri (Neden Seçtik?):
*   **App-ID ve User-ID Teknolojisinde Altın Standart:** Merkez ofisteki trafik port tabanlı değildir (Sadece 80 veya 443 portu görmek yetmez). İçeride dönen trafiğin hangi uygulamanın hangi fonksiyonuna ait olduğunu (Örn: "Microsoft Teams ile dosya yükleniyor", "Google Drive'dan veri indiriliyor") anlamada sektördeki en isabetli ve granüler (ince ayarlı) teknoloji Palo Alto'ya aittir. Finans ve IK verilerinin dışarı sızmasını engellemek için trafiğin en derin katmanına inilmesi gerekiyordu.
*   **Makine Öğrenimi (Machine Learning) ile Satır İçi Koruma (Inline ML):** PA-1410 modeli, bilinen siber tehditleri (virüs imzalarını) buluttan indirmeyi beklemez. Kendi donanımı üzerinde çalışan makine öğrenimi modelleri ile daha önce dünyada hiç görülmemiş (Zero-Day) bir phishing sitesine girildiğini saniyeler içinde anlar ve o bağlantıyı anında düşürür (Drop).
*   **Active-Passive Yedeklilik (HA):** Genel merkez çökerse tüm şubelerin iletişimi kesilir. Bu yüzden iki cihaz (A ve B cihazları) birbiriyle Heartbeat kablolarıyla bağlanarak kümelenmiştir (Cluster). A cihazının fişi bile çekilse, B cihazı sıfır kesintiyle IP'leri ve açık olan sekmeleri/oturumları devralır.

## Rakiplerin Elenme Nedenleri (Neden Seçmedik?):
*   *FortiGate 400F & Sophos XGS 3300:* Şifreleme hızları ve port trafiği işleme güçleri muazzam olsa da, Palo Alto'nun "Tek Geçişli Mimarisi" (Single-Pass Architecture - Paketi açar, IPS, AntiVirus, URL filtrelemesini aynı anda tek turda yapar) kadar derin bir 7. Katman analizi sunamazlar. Merkez ofiste fiyattan kaçınılmayıp "Maksimum Görünürlük" talep edilmiştir.
*   *Cisco Firepower:* Eski Sourcefire altyapısı üzerine inşa edilen arayüzü çok yavaştır (Hantal). Siber güvenlik SOC analistleri kural yazarken (Troubleshooting) saniyelerle yarışır. Arayüzün yavaş tepki vermesi Cisco'nun elenmesindeki temel nedendir.
