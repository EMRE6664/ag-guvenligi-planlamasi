# Şube ve Kapasite Bilgileri (Ankara Şubesi)

## 1. Lokasyon, Mimari ve Kullanıcı Kapasitesi
Ankara ofisimiz, şirketin resmi satış, kamu ilişkileri, bürokrasi ve lokal idari süreçlerini yürüten bölge müdürlüğüdür. Operasyonel stabilitenin yüksek olduğu, yenilikçi yazılım süreçlerinin *olmadığı* standart bir "Enterprise Branch" profiline sahiptir.
*   **İdari ve Satış Personeli:** 150 Kişi
*   **Bilgi İşlem (Teknik Destek) Ekibi:** 10 Kişi
*   **Yazılım / Ar-Ge / Öğrenci:** Bulunmamaktadır.

## 2. Bant Genişliği, Ağ Profili ve Altyapı Analizi
*   **Ana İnternet Hattı:** 1 Gbps Fiber Optik (Metro Ethernet)
*   **Yedek İnternet Hattı:** 100 Mbps VDSL (SD-WAN ile entegre)
*   **Trafik Profili (Network Behavior):** Ofis trafiğinin %80'i İstanbul merkezdeki ERP sistemlerine atılan SQL sorguları, Microsoft Office 365 (Bulut) servisleri ve kurumsal e-posta iletişimlerinden oluşmaktadır. Geri kalan %20'lik trafik ise VoIP (IP Telefon) trafiğidir.

## 3. IP ve VLAN Segmentasyon Planı
Ağ yapısı tamamen modüler tutularak "Düz Ağ (Flat Network)" kavramından uzaklaşılmıştır:
*   `VLAN 10` - İdari Personel (Subnet: `10.1.10.0/24`)
*   `VLAN 20` - Satış ve Müşteri Temsilcileri (Subnet: `10.1.20.0/24`)
*   `VLAN 30` - IT Yönetim (OOB) Ağı (Subnet: `10.1.30.0/24` - Güvenlik Duvarı kurallarında yüksek önceliklidir)
*   `VLAN 40` - IP Ses (VoIP) Ağı (Subnet: `10.1.40.0/24` - Trafik şekillendirme ile garanti bant genişliği atanmıştır)

## 4. Ağ Erişim Kuralları ve Güvenlik Politikaları
*   **Web Filtreleme (Web Filtering):** Kumar, yasa dışı içerik, şiddet ve bilinen oltalama (phishing) sitelerine erişim "Hard Block" statüsündedir.
*   **Sosyal Medya Yönetimi (App Control):** Facebook, Instagram ve TikTok trafik bandını yormaması için QoS kısıtlamalarına tabidir (Max 5 Mbps). Yalnızca öğle yemeği saatlerinde (12:00-13:30) bu kural esnetilerek bant genişliği 20 Mbps'ye çıkartılır.
*   **Host-Based Security (UFW):** Bu ofiste barınan yerel dosya sunucusunun (Print/File Server) sadece `VLAN 10` ve `VLAN 20` alt ağlarından SMB (Port 445) ve yazıcı (Port 9100) trafiklerini kabul etmesi için sunucu işletim sistemi içinde Linux UFW kısıtlamaları uygulanmıştır.
