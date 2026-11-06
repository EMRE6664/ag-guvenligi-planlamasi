# Akademik Şube (Kampüs): Top 5 Güvenlik Duvarı Adayı ve Detaylı Analiz

On binlerce anlık kullanıcının üreteceği devasa oturum sayısını (Session) ve saniyedeki paket (PPS - Packets Per Second) hızını kaldırabilmek için yazılım veya klasik CPU tabanlı değil, tamamen "Donanım İvmeli Şasi" (High-End Carrier-Grade) cihazları değerlendirilmiştir.

## Adaylar Listesi ve Pazar Karşılaştırması
1.  **FortiGate 4400F** (Hyperscale Mimari, NP7 ASIC Çipleri ile rakipsiz oturum hızı)
2.  **Palo Alto PA-5450** (Modüler ve ölçeklenebilir 7. Katman analizi canavarı)
3.  **Cisco Firepower 4100/9300 Series** (Carrier-grade, Telekom operatörü seviyesi şasi)
4.  **Check Point Quantum 16600** (Veri merkezi ve hyperscale ağ güvenliği)
5.  **Juniper SRX4600** (Dünyanın en iyi Router yetenekleri ile harmanlanmış Firewall)

## Seçilen Cihaz ve Mimari Karar: **FortiGate 4400F**

### Tercih Edilme Gerekçeleri (Neden Seçtik?):
*   **Muazzam Oturum Yönetimi (Session Setup Rate):** Diğer Firewall markaları paketleri analiz için standart Intel/AMD işlemcilere yollar, bu da darboğaz yaratır. Fortinet ise kendi ürettiği özel donanımsal çipler (Network Processor 7 - NP7 ve Content Processor 9 - CP9) kullanır. Bu ASIC çipleri, 10.000 öğrencinin ürettiği milyonlarca eşzamanlı oturumu ve küçük boyutlu UDP paketlerini (Elephant vs Mice flows) ana işlemciye uğramadan (Hardware Offloading) donanım hızında iletir. 4400F, Session Setup (Saniyedeki yeni oturum açma) kapasitesinde rakiplerine devasa bir fark atar.
*   **DDoS (Hizmet Aksatma) Savunması:** Donanım bazlı işleme (NP7) özelliği, kampüs içinden dışarıya botnetler aracılığıyla başlayan veya dışarıdan içeriye gelen Syn Flood / UDP Flood DDoS saldırılarını, cihazın işlemcisini şişirmeden, hattan geldiği hızda (line-rate) kesip atabilir.

## Rakiplerin Elenme Nedenleri (Neden Seçmedik?):
*   *Palo Alto PA-5450:* Siber güvenlik ve uygulama bazlı kontrolde en iyisi olmasına rağmen, donanım mimarisi x86 işlemciler ve FPGA'ler üzerine kuruludur. Akademik bir ağın istediği "Uçarı Packet Per Second (PPS) ve Session" sayısına ulaşması için PA-5450'nin en dolu modüllerle donatılması gerekir. Bu da şirket (veya üniversite) bütçesine (CAPEX) Fortinet'e kıyasla kabul edilemez, astronomik bir maliyet çıkarır. İdari bir personelin her adımını izlemek önemlidir, ancak bir öğrencinin trafiğinde 7. katman derin analizinden çok "Hız, Kapasite ve Ucuz Maliyet" önemlidir.
*   *Juniper SRX4600:* Juniper dünyadaki en iyi "Router" markalarından biridir, yönlendirme (routing) özellikleri kusursuzdur. Ancak cihazın UTM (Antivirüs, Saldırı Önleme, Web Filtreleme) motorları devreye alındığında Throughput (Veri işleme kapasitesi) radikal bir biçimde (%60-70 oranında) düşmektedir. Akademik ağda IPS şart olduğu için Juniper elenmiştir.
