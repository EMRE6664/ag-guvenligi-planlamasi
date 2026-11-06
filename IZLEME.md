# İzleme (Monitoring), SIEM ve ufw-logger Telegram Entegrasyonu

Profesyonel dünyada ağ güvenliği altyapısı, ağ katmanı (SIEM) ve sunucu katmanı (`ufw-logger`) olarak entegre bir şekilde izlenir. L1, L2 ve L3 SOC analistleri bu verileri 7/24 takip eder.

## 1. Sistematik Ağ İzleme (Network Monitoring & SIEM)
* **Merkezi Loglama:** Şubelerdeki tüm güvenlik duvarlarından gelen syslog, CEF veya LEEF formatındaki loglar merkezi QRadar veya Splunk sisteminde toplanır.
* **Korelasyon:** VPN ile Londra'dan bağlanan bir çalışanın hesabının aynı saniye içinde Ankara'dan da giriş yapmaya çalışması gibi anormallikler (Impossible Travel) anında SIEM üzerinde korelasyon kuralına takılır ve alarm (Offense) üretir.
* **NPM (Network Performance Monitoring):** Zabbix veya PRTG ile SNMP üzerinden firewall CPU, RAM durumları, arayüz trafik doluluk oranları (NetFlow ile kim nereye bağlanıyor) takip edilir.

## 2. Sunucu Bazlı İzleme: `ufw-logger` ve Telegram Bot API Entegrasyonu
Donanım firewall'unun arkasındaki DMZ sunucularında UFW loglarının anlık izlenmesi, Keyvan Arasteh'in projelerinde sıkça vurgulanan otomasyon pratikleriyle sağlanır. Bu projede, sunuculara yapılan port taramaları veya yetkisiz erişim denemeleri Telegram üzerinden anında SOC ekibine iletilir.

### Telegram Bot Çalışma Mantığı
1. **BotFather Üzerinden Bot Oluşturma:** Telegram'da `@BotFather` kullanılarak kurumsal bir bot (Örn: `SirketSOC_Bot`) oluşturulur ve `HTTP API Token` alınır.
2. **Logların Takibi:** UFW logları default olarak `/var/log/ufw.log` veya `/var/log/kern.log` dosyasına düşer.
3. **ufw-logger Scripti:** Sunucuda arka planda (systemd servisi olarak) çalışan bir Python veya Bash scripti, UFW log dosyasını `tail -f` mantığıyla okur.
4. **Anlık Bildirim (Alerting):** Eğer log dosyasında `[UFW BLOCK]` ibaresi art arda 5 kez aynı IP adresinden gelirse (Örn: SSH Brute Force), script Telegram API'sine (`https://api.telegram.org/bot<TOKEN>/sendMessage`) bir POST isteği atar.
5. **Örnek Telegram Alarm Çıktısı:**
   ```
   🚨 [GÜVENLİK İHLALİ] 🚨
   Sunucu: web-server-ist-01
   Tarih: 2026-11-06 14:30
   Olay: 22 (SSH) Portuna İzinsiz Erişim Denemesi
   Saldırgan IP: 192.168.1.105 (UFW Tarafından Bloklandı)
   ```

## 3. İnsan Faktörü (SOC Ekipleri)
* **L1 (Triage):** Telegram'a veya SIEM ekranına düşen bu uyarıya ilk bakan ve "Acaba bizim ekipten biri mi şifreyi yanlış girdi?" analizini yapan analisttir.
* **L2 (Incident Responder):** Eğer saldırı gerçekse, Palo Alto/FortiGate donanım cihazına girip söz konusu IP'yi "Global Ban List" (Karantina) içine ekler.
