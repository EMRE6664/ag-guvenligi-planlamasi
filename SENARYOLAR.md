# Olay Müdahale (Incident Response) Playbook Senaryoları

Siber güvenlik operasyon merkezinde (SOC), bir kriz anında kimsenin ne yapacağını düşünmemesi için olaylar önceden kurgulanmış "Playbook" senaryolarına bağlanmıştır.

## Senaryo 1: Linux Sunucuya Yönelik SSH Brute Force Saldırısı ve Telegram Alarmı
* **Olay:** Şirketin DMZ'inde bulunan ve Ubuntu işletim sistemiyle çalışan açık kaynaklı bir veritabanı sunucusuna dışarıdan veya içeriden bir IP adresinden saniyede 50 adet SSH (Port 22) giriş denemesi yapılır.
* **Tespit (Detection - ufw & ufw-logger):** İşletim sistemindeki `ufw` önceden belirlenen limit kuralları (Örn: `sudo ufw limit ssh/tcp`) sayesinde ardışık bağlantıları otomatik olarak düşürür (`[UFW BLOCK]`). Arka planda çalışan `ufw-logger` scripti bu logları analiz eder ve Telegram SOC kanalına anında "Brute Force Tespit Edildi" bildirimini basar.
* **Müdahale (Containment):** L2 analist Telegram bildirimindeki saldırgan IP'yi (Örn: 45.33.x.x) alır. İstanbul'daki ana Palo Alto (NGFW) cihazına bağlanır ve bu IP adresini en dış sınırda (Perimeter) karantinaya alarak (Drop All) saldırının sunucuya kadar gelmesini temelden keser.
* **İyileştirme (Recovery):** Sunucunun SSH portu değiştirilir veya SSH erişimi tamamen Zero Trust (ZTNA) istemcisi arkasına gizlenerek dış dünyaya kapatılır.

## Senaryo 2: Akademik Şubeden C&C (Command & Control) Botnet Trafiği
* **Olay:** Öğrenci yurdundaki enfekte olmuş bir laptop, dark web üzerindeki bir Botnet kontrol sunucusuyla (C&C) HTTPS veya DNS tünellemesi üzerinden haberleşmeye çalışır.
* **Tespit:** FortiGate 4400F cihazının "Gateway Antivirus" ve "IPS" modülü, bilinen zararlı (Malicious) C&C sunucularının IP/Domain imzasını tanır ve bağlantıyı otomatik keser. SIEM ekranına "C&C Traffic Detected" alarmı düşer.
* **Müdahale:** Entegre NAC (Network Access Control) sistemi, öğrencinin MAC adresini tespit edip Switch üzerinden bağlı olduğu portu anında "Karantina VLAN"ına taşır. Öğrenci sadece "Lütfen cihazınızı virüs taramasından geçirin" yazan bir web sayfasına erişebilir.

## Senaryo 3: Ar-Ge Fikri Mülkiyet (IP) Sızıntısı
* **Olay:** İstifa aşamasındaki bir Ar-Ge mühendisi, kod deposundan çektiği bir projeyi kişisel Google Drive hesabına "Proje_Yedek.zip" olarak yüklemeye çalışır.
* **Tespit ve Müdahale:** Palo Alto cihazı "SSL Decryption" özelliği ile şifreli HTTPS trafiğini araya girerek kırar (Man in the Middle). "Data Loss Prevention (DLP)" modülü paketin içindeki kodu veya "GİZLİ" etiketini tarar ve veri eşleşmesi bulur. Dosyanın dışarı yüklenmesi (HTTP POST) işlemi anında "Reset-Both" komutuyla bağlantı koparılarak engellenir. İK departmanına otomatik rapor gider.
