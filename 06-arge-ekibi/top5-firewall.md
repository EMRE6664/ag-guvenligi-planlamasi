# Ar-Ge Merkezi: Top 5 Güvenlik Duvarı Adayı ve Detaylı Analiz

Bant genişliğinin düşük olduğu bu ofiste, karar mekanizması tamamen "SSL Şifre Çözme (Decryption) Mükemmelliği", "Sıfırıncı Gün (Zero-Day) Zararlı Yazılım Yakalama Sandbox Mimarisi" ve "Data Loss Prevention (DLP)" kriterleri üzerinden şekillenmiştir. Sektördeki en hassas ve en keskin (paronayak) cihazlar yarışmıştır.

## Adaylar Listesi ve Pazar Karşılaştırması
1.  **Palo Alto PA-450** (Zero Trust lideri, Rakipsiz WildFire Sandbox ve App-ID entegrasyonu)
2.  **FortiGate 100F** (Güçlü şifreleme ve lokal donanım güvenliği)
3.  **Check Point Quantum 3600** (Gelişmiş Threat Prevention (SandBlast) modülleri)
4.  **Cisco Firepower 1010** (Küçük boyutta Snort 3 tabanlı güçlü IPS koruması)
5.  **Sophos XGS 2100** (Deep Learning (Derin Öğrenme) tabanlı anomali izleme)

## Seçilen Cihaz ve Mimari Karar: **Palo Alto PA-450**

### Tercih Edilme Gerekçeleri (Neden Seçtik?):
*   **SSL Şifre Çözme (SSL Decryption) ve DLP Mükemmelliği:** Ar-Ge departmanından dışarı (veya rakip şirketlere) sızdırılmaya çalışılan bir kurum sırrı veya proje dosyası, sızdıran kişi (İç Tehdit / Insider Threat) tarafından mutlaka şifreli (HTTPS) bir bağlantı, tünel veya bulut depolama kullanılarak gizlenmeye çalışılacaktır. Palo Alto, trafiğin güvenilir sertifikasını (CA) kırıp Araya Girme (Man in the Middle) yöntemiyle paketin en derinini (App-ID) okuma, ardından içindeki içeriği tarama (Content-ID) konusunda pazarın en kusursuz ve stabil mimarisine sahiptir. Belgedeki bir algoritma (Regex) yakalandığı an bağlantı düşürülür (Reset-Both).
*   **WildFire (Sandbox - Sanal Kum Havuzu) Mimarisi:** Siber casuslar Ar-Ge mühendisine "Önemli Proje İhalesi" başlıklı bir Spear-Phishing (hedefli oltalama) maili attıklarında, içindeki virüs, bilinen bir Antivirüs imza veritabanında (Signature-based) kayıtlı olmayacaktır (Sıfırıncı Gün / Zero-Day saldırısı). PA-450, dosyayı anında Palo Alto WildFire bulut sanal ortamına (veya on-prem sandbox'a) atar, dosyanın arka planda ne yapmaya çalıştığını (registry değiştirme, ağ tarama vb.) saniyeler içinde analiz eder. Eğer dosya zararlı davranış sergilerse (Verdict: Malicious), ağa inmesine (Download edilmesine) izin vermeden "Drop" eder. Bu proaktif koruma için WildFire dünyada "Altın Standart" olarak kabul görür.

## Rakiplerin Elenme Nedenleri (Neden Seçmedik?):
*   *FortiGate 100F:* Donanımsal olarak (IPSec şifreleme ve düz hız olarak) harika bir üründür. Ancak, HTTPS (SSL/TLS) trafiğinin şifresini çözüp içeriğine bakma işlemi (Deep Packet Inspection) devreye girdiğinde, FortiGate'in imza ve port tabanlı proxy veya flow-based yapısı, Palo Alto'nun tek geçişte Uygulama-Kullanıcı-İçerik (App/User/Content-ID) taraması yapan hassasiyetine ulaşamamaktadır. Ar-Ge'de performans (Hız) hiçbir zaman "Tavizsiz Analizin (Güvenliğin)" önüne geçemez.
*   *Check Point & Sophos:* Check Point'in SandBlast çözümü de muazzamdır, ancak Sıfır Güven (Zero Trust) kurallarının Firewall Yönetim paneline uygulanması, kuralların IP yerine doğrudan Active Directory kullanıcılarına ve Uygulama fonksiyonlarına göre yazılması sadeliği bakımından Palo Alto sektör lideri olduğu ve bu ofiste bütçe (CAPEX) kısıtlaması (tavanı) bulunmadığı için PA-450 modeli direkt olarak birinci tercih olmuştur.
