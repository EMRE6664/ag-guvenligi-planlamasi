# 01-Ankara Ofisi: Kapsamlı Kurulum ve Devreye Alma SOP'si

Genel kurulum süreçlerine ek olarak, Ankara ofisine özel yapılacak aksiyonlar ve test komutları:

1.  **SD-WAN Zone ve Arayüz Konfigürasyonu:** 
    - Cihazın `Port 1` arayüzü Turkcell Fiber'e (WAN1), `Port 2` arayüzü Türk Telekom VDSL'e (WAN2) bağlanır. 
    - FortiOS üzerinden bir `SD-WAN Zone` oluşturulur.
    - Kural: "VoIP trafiği (UDP 5060) her zaman paket kaybı en düşük (Lowest Packet Loss) hattan gitsin."
2.  **IPsec VPN Tünellemesi (Hub & Spoke):** 
    - Ankara (Spoke) ofisi, İstanbul Merkez (Hub) ofisi ile Faz-1 ve Faz-2 tünelleri kurar. Şifreleme algoritması olarak AES-256-GCM ve SHA-256 seçilir (Gelişmiş güvenlik).
3.  **Yerel Sunucu (File Server) UFW Entegrasyonu:**
    - Ankara'da bulunan Ubuntu tabanlı dosya sunucusuna girilip `ufw` devreye alınır:
    ```bash
    sudo ufw default deny incoming
    sudo ufw allow from 10.1.10.0/24 to any port 445 # Idari personel SMB erişimi
    sudo ufw allow from 10.1.20.0/24 to any port 445 # Satis ekibi SMB erişimi
    sudo ufw allow from 10.1.30.0/24 to any port 22  # Sadece IT ekibi SSH yapsin
    sudo ufw enable
    ```
4.  **Failover Stres Testi (UAT - Kullanıcı Kabul Testi):**
    - Sistem odasında fiziksel olarak Fiber kablo çekilir. İçeride internetin veya merkeze bağlı uygulamanın kesilmediği, trafiğin anında VDSL'e kaydığı FortiView ekranlarından teyit edilir.
