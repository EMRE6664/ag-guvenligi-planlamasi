# Şube ve Kapasite Bilgileri (Londra Ofisi / Uydu Şube)

## 1. Lokasyon, Mimari ve Kullanıcı Kapasitesi
Londra ofisi, şirketin uluslararası satış, küresel pazarlama, operasyonlar ve hukuki süreçlerini yürüten kritik ancak fiziksel olarak küçük bir "Uydu Şube" (Branch Office / Spoke) niteliğindedir. 
*   **Uluslararası Satış ve Hukuk Personeli:** 50 Kişi
*   **Bilgi İşlem (Yerel Teknik Destek):** Sadece 2 Kişi (Biri masaüstü destek, diğeri ağ/sistem yardımcısı. Derin firewall bilgileri yoktur).
*   **Yazılım / Ar-Ge / Laboratuvar:** Yok.

## 2. Bant Genişliği, Ağ Profili ve Altyapı Analizi
*   **İnternet Hattı:** 500 Mbps geniş bant internet (Bölgesel ISS üzerinden, yedeklilik zorunluluğu düşük).
*   **Trafik Profili (Network Behavior):** Personel günün büyük kısmında Salesforce, Office 365, Teams ve Zoom gibi "Bulut" tabanlı SaaS servislerini kullanır. Ancak finansal raporlama veya sipariş girişi gibi kritik işlemlerde İstanbul'daki (HQ) ERP veritabanına sorgu atmak zorundadırlar. Trafik hacmi düşüktür.

## 3. IP ve VLAN Segmentasyon Planı
Küçük bir ofis olduğu için ağ tasarımı son derece basittir (Flat yapıya yakındır):
*   `VLAN 10` - Londra Kurumsal Çalışan Ağı (Subnet: `10.3.10.0/24`)
*   `VLAN 90` - Londra Misafir Ağı (Sadece İnternet Çıkışı - Subnet: `10.3.90.0/24`)

## 4. Ağ Erişim Kuralları ve Güvenlik Politikaları
Buradaki ana felsefe "Bulut Yönetimli Basitlik"tir. Kurallar karmaşık değildir.
*   **Split-Tunneling (Bölünmüş Tünel) Mimarisi:** Londra ofisinden internete çıkan her paketi (Örn: Birinin YouTube'dan dinlediği müzik) VPN üzerinden İstanbul'a gönderip oradan dışarı çıkarmak, İstanbul firewall'unu gereksiz yorar. Bu yüzden Split-Tunneling uygulanır: Kurumsal ERP ve Intranet hedeflerine giden trafik VPN tüneline (İstanbul'a) sokulur. Zoom, Office 365 ve genel internet trafiği doğrudan Londra'daki yerel hattan (Direct Internet Access - DIA) dışarı çıkar.
*   **Otomatik Şubeler Arası VPN:** Yeni bir kural veya VPN tüneli yazılması gerektiğinde bu işlem Londra'da yapılmaz, İstanbul'daki SOC ekibi tarafından bulut paneli üzerinden Merkezi olarak Londra cihazına basılır.
*   **Uç Nokta İstemcisi:** Seyahat eden yöneticiler cihazlarındaki yerleşik VPN istemcisiyle ofis dışından bu firewall'a bağlanabilir.
