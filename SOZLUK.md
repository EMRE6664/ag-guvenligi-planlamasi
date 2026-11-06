# Kapsamlı Ağ ve İşletim Sistemi Güvenliği Sözlüğü

* **NGFW (Next-Generation Firewall):** Uygulama katmanında (L7) filtreleme yapan, IPS ve antivirüs entegre donanım.
* **UFW (Uncomplicated Firewall):** Linux çekirdeğindeki iptables kurallarını yönetmek için kullanılan, kullanımı kolay (uncomplicated) işletim sistemi tabanlı güvenlik duvarı arayüzü.
* **iptables:** Linux sistemlerinde paket filtreleme kurallarını ayarlayan temel çekirdek (netfilter) modülü arayüzü.
* **Chain / Rule (Zincir ve Kural):** Firewall mimarisinde gelen paketin izlediği kurallar bütünü (INPUT, OUTPUT, FORWARD).
* **SIEM (Security Information and Event Management):** Çeşitli kaynaklardan (Ağ, Sunucu, UFW vb.) gelen logları birleştiren ve anlamlandıran merkezi yazılım.
* **SOC (Security Operations Center):** Siber olayları 7/24 izleyen, tespit eden uzmanlar takımı.
* **Telegram Bot API:** HTTP protokolü üzerinden mesaj gönderip almayı sağlayan arayüz. Projede `ufw-logger` loglarını ekibe iletmek için kullanılmıştır.
* **Zero Trust (Sıfır Güven):** Ağdaki hiçbir IP'ye, kullanıcıya veya cihaza varsayılan olarak güvenmeyen, sürekli doğrulama gerektiren mimari.
* **SSL Decryption (Şifre Çözme):** Kurum dışına çıkan şifreli (HTTPS) trafiğin içerik analizini yapmak için güvenlik duvarında sertifika aracılığıyla deşifre edilmesi işlemi.
* **DDoS (Distributed Denial of Service):** Binlerce cihazın aynı anda hedef sisteme anlamsız trafik göndererek bant genişliğini veya oturum (session) sınırlarını tüketmesi saldırısı.
