# Ankara Ofisi: Top 5 Güvenlik Duvarı Adayı ve Detaylı Analiz

Kapasite, throughput (veri işleme hacmi) ve kullanıcı sayısı doğrultusunda Orta Ölçekli İşletme (Mid-Range Enterprise) cihazları detaylı değerlendirilmiştir.

## Adaylar Listesi ve Pazar Karşılaştırması
1.  **FortiGate 200F** (Donanımsal ivmelendirme - ASIC SPU CP9, Dahili SD-WAN)
2.  **Palo Alto PA-440** (Pazarın en iyi makine öğrenimi tabanlı App-ID çözümü)
3.  **Sophos XGS 2100** (Deep Learning ve senkronize uç nokta koruması)
4.  **Check Point Quantum 3600** (Kapsamlı Threat Extraction yetenekleri)
5.  **Cisco Meraki MX100** (%100 bulut tabanlı ve dashboard üzerinden yönetim)

## Seçilen Cihaz ve Mimari Karar: **FortiGate 200F**

### Tercih Edilme Gerekçeleri (Neden Seçtik?):
*   **Rakipsiz SD-WAN Mimarisi:** Ankara ofisinin 1 Gbps Fiber ve 100 Mbps VDSL olmak üzere iki farklı hattı vardır. FortiGate, ek bir lisans maliyeti talep etmeksizin FortiOS işletim sistemiyle "Application-Aware SD-WAN" sunar. Örneğin, bir satış personelinin Zoom görüşmesi sırasındaki veri paketlerinin gecikmesi (Jitter/Latency) fiber hatta 50ms'yi aşarsa, firewall bu sesi kesinti hissettirmeden VDSL hatta kaydırır.
*   **Donanımsal Hız (ASIC):** FortiGate'in Network Processor (NP) işlemcileri, standart bir x86 Intel işlemciye kıyasla IPSec VPN paketlerini donanım üzerinde şifreleyip çözer. Ankara'dan İstanbul'a giden ERP trafiği bu sayede sıfır gecikmeyle (Hardware Offloading) işlenir. 

## Rakiplerin Elenme Nedenleri (Neden Seçmedik?):
*   *Palo Alto PA-440:* Palo Alto siber güvenlik dünyasının Rolls-Royce'udur. Uygulama analizi olağanüstüdür ancak standart Excel ve CRM kullanan Ankara idari ofisinde bu granülerliğe (ince ayarlara) ihtiyaç yoktur. PA-440 cihazı, FortiGate 200F'e göre aynı performansta çok daha yüksek bütçe (CAPEX) gerektirir.
*   *Cisco Meraki MX100:* Kullanımı çok kolay olmasına rağmen bulut lisans modeli (OPEX) yıllar içinde şirket bütçesine büyük yük bindirmektedir. Şirket donanımın fiziksel olarak kendisine ait olmasını istediği için (Perpetual License mantığına yakın) Meraki elenmiştir.
*   *Sophos/Check Point:* İstanbul ve büyük şubelerde Fortinet/Palo Alto mimarisi standartlaştığı için, SOC ekibinin farklı ekranlara bakıp "Alarm Yorgunluğu" yaşamaması adına vendor-konsolidasyonu tercih edilmiştir.
