# Şube ve Kapasite Bilgileri (Ar-Ge ve İnovasyon Merkezi)

## 1. Lokasyon, Mimari ve Kullanıcı Kapasitesi
Araştırma ve Geliştirme (Ar-Ge) birimi, şirketin can damarıdır. Milyonlarca dolarlık endüstriyel tasarımların, patent aşamasındaki teknolojilerin (Fikri Mülkiyet / Intellectual Property - IP), gizli kodların ve ticari sırların bulunduğu, fiziksel ve siber olarak şirketin en yalıtılmış (İzole) tesisidir.
*   **Ar-Ge Mühendisleri (Ekip):** 40 Kişi
*   **Yönetici ve İdari Personel:** 10 Kişi
*   **Ar-Ge'ye Özel Siber Güvenlik Uzmanları:** 5 Kişi (Merkez ofisten bağımsız çalışırlar).

## 2. Bant Genişliği, Ağ Profili ve Altyapı Analizi
*   **İnternet Hattı:** 1 Gbps Özel Hat. (Hızdan veya bant genişliğinden ziyade, kriptografi, şifreleme ve derin analizin ön planda olduğu, trafiğin çok yavaş ama aşırı incelemeli aktığı bir hattır).
*   **Trafik Profili (Network Behavior):** Genel internet sörfü yoktur. Trafik genelde "Kapalı Devre (Air-Gapped veya paronayak)" profildedir. Cihazlar dış dünyaya kapalıdır. Sadece araştırmaya yönelik makalelerin ve akademik verilerin bulunduğu "Beyaz Listeli (Whitelisted)" sitelere çok kısıtlı bir trafik çıkar.

## 3. IP ve VLAN Segmentasyon Planı
Ağ yapısı tamamen "Zero Trust (Sıfır Güven)" üzerine tasarlanmıştır:
*   `VLAN 10` - Ar-Ge Mühendisleri Çalışma Ağı (Sadece şirket zimmetli, şifreli diskli bilgisayarlar - `10.6.10.0/24`)
*   `VLAN 20` - Ar-Ge Veritabanı ve Proje Depo (Repository) Ağı (`10.6.20.0/24`)
*   *İzolasyon:* VLAN 10'daki bir cihaz, şirketin (Örn: Ankara ofisi) diğer ağlarıyla iletişime geçemez. Her şey Ar-Ge binasında başlar ve biter.

## 4. Ağ Erişim Kuralları ve Güvenlik Politikaları (Paranoyak Kural Seti)
*   **Tam Zero Trust (Sıfır Güven):** Dışarıdan hiçbir bağlantı (Inbound) Ar-Ge ağına giremez. İçerideki cihazlar da varsayılan (Default) olarak dışarıya (Outbound) çıkamaz. İnternete erişim sadece IP adreslerine değil, URL kategorilerine ve kişi kimliğine göre tek tek açılır.
*   **Veri Sızdırma Koruması (Dışarıya Upload Yasağı):** Güvenlik duvarından dışarıya (İnternete) dosya yükleme (HTTP POST request, FTP Put, SMTP attachment) donanım, uygulama ve içerik seviyesinde "Tamamen Blokludur". Google Drive, WeTransfer, Dropbox, kişisel Gmail erişimi yasaktır.
*   **Donanımsal Uç Nokta ve USB Kısıtı:** Bilgisayarlara takılan USB bellekler Endpoint Protection (EDR) yazılımlarıyla (Örn: Cortex XDR) engellenir ve merkezi Firewall/SIEM loglarına "İzinsiz USB Takıldı" olarak düşer.
*   **Cihaz Kısıtlaması (NAC):** Sadece şirketin verdiği, diskleri BitLocker ile şifrelenmiş (Full Disk Encryption) ve MAC bazında kayıtlı cihazlar 802.1x sertifika doğrulamasıyla ağdan IP alabilir. Dışarıdan bir misafir (veya casus) laptopunun ethernet kablosunu duvara taksa dahi hiçbir ağa erişemez (Rogue Device Isolation).
