# Drone Teslimat Optimizasyonu
Bu proje, çoklu drone teslimat sistemleri için gelişmiş rota optimizasyonu algoritmaları içerir. A* yol bulma algoritması ve genetik algoritma kullanarak, uçuş yasağı bölgelerini dikkate alarak optimal teslimat rotaları oluşturur.

🚁 Özellikler
Çoklu Drone Desteği: Farklı kapasitelerde birden fazla drone ile eşzamanlı teslimat
A Yol Bulma*: Engelleri ve yasak bölgeleri dikkate alan akıllı rota planlama
Genetik Algoritma: Optimal rota kombinasyonları için evrimsel optimizasyon
Uçuş Yasağı Bölgeleri: Poligon tabanlı yasak bölge tanımları ve çakışma kontrolü
Gerçek Zamanlı Kısıtlar: Ağırlık, batarya, zaman penceresi kısıtları
Görselleştirme: Matplotlib ile detaylı rota ve harita görselleştirmesi
Performans Analizi: Kapsamlı metrik ve istatistik raporlama
📋 Gereksinimler
matplotlib>=3.5.0
numpy>=1.21.0
python>=3.8
🚀 Kurulum
Repoyu klonlayın:
git clone https://github.com/kullanici/drone-delivery-optimization.git
cd drone-delivery-optimization
Gerekli paketleri yükleyin:
pip install matplotlib numpy
Programı çalıştırın:
python ucak.py
🏗️ Sistem Mimarisi
Ana Bileşenler
1. Veri Modelleri
Ucak: Drone özellikleri (kapasite, batarya, hız, konum)
TeslimatNoktasi: Teslimat detayları (konum, ağırlık, öncelik, zaman)
UcusYasakBolgesi: Yasak bölge tanımları (koordinatlar, aktif zaman)
2. Algoritma Modülleri
A Yol Bulma*: Engel kaçınmalı optimal yol hesaplama
Genetik Algoritma: Çoklu drone rota optimizasyonu
Kısıt Kontrolü: Fiziksel ve operasyonel kısıt doğrulama
3. Yardımcı Fonksiyonlar
Geometrik hesaplamalar (mesafe, çakışma kontrolü)
Poligon içi nokta kontrolü
Çizgi-poligon kesişim tespiti
🔧 Kullanım
Temel Kullanım
from ucak import *

# Drone'ları oluştur
dronlar = dron_uret(5)  # 5 drone

# Teslimat noktalarını oluştur
teslimatlar = teslimat_uret(20)  # 20 teslimat

# Yasak bölgeleri tanımla
yasak_bolgeler = yasak_bolge_uret(2)  # 2 yasak bölge

# Optimizasyonu çalıştır
en_iyi_rotalar, sure = genetik_optim(
    dronlar, 
    teslimatlar, 
    yasak_bolgeler,
    nesil_sayisi=50,
    pop_boyutu=30
)

# Sonuçları görselleştir
rota_ciz(en_iyi_rotalar, yasak_bolgeler, teslimatlar)
Özelleştirilmiş Senaryo
# Manuel drone tanımlama
drone1 = Ucak(
    idx=0,
    maks_agirlik=10.0,  # kg
    batarya=10000,      # mAh
    hiz=12.0,           # m/s
    baslangic=(50, 50)  # başlangıç koordinatı
)

# Manuel teslimat noktası
teslimat1 = TeslimatNoktasi(
    idx=0,
    konum=(75, 25),
    agirlik=2.5,
    oncelik=5,
    zaman_araligi=(datetime.time(9, 0), datetime.time(17, 0))
)

# Manuel yasak bölge (kare)
yasak_bolge = UcusYasakBolgesi(
    idx=0,
    koordinatlar=[(20, 20), (40, 20), (40, 40), (20, 40)],
    aktif_zaman=(datetime.time(0, 0), datetime.time(23, 59))
)
📊 Algoritma Detayları
A* Yol Bulma Algoritması
Zaman Karmaşıklığı: O(E log V)
Heuristik: Öklid mesafesi + yasak bölge cezası
Özellikler:
8 yönlü hareket
Dinamik adım boyutu
Yasak bölge kaçınma
Genetik Algoritma
Zaman Karmaşıklığı: O(G × P × D × T)
Operatörler:
Çaprazlama: Kısmi eşleşme
Mutasyon: Yer değiştirme, transfer, ekleme/çıkarma
Seçim: Elitist seçim
Kısıt Yönetimi
Ağırlık Kısıtı: Toplam yük ≤ Drone kapasitesi
Batarya Kısıtı: Enerji tüketimi ≤ Batarya kapasitesi
Zaman Kısıtı: Teslimat zamanı ∈ Zaman penceresi
Yasak Bölge Kısıtı: Rota ∩ Yasak bölge = ∅
📈 Performans Metrikleri
Teslimat Oranı: Tamamlanan teslimat yüzdesi
Enerji Verimliliği: Ortalama enerji tüketimi
Mesafe Optimizasyonu: Toplam uçuş mesafesi
Çalışma Süresi: Algoritma hesaplama süresi
🎯 Test Senaryoları
Senaryo 1: Küçük Ölçek
5 Drone
20 Teslimat noktası
2 Yasak bölge
Senaryo 2: Orta Ölçek
10 Drone
50 Teslimat noktası
5 Yasak bölge
📊 Örnek Çıktı
Nesil 1: En İyi Uygunluk = 1250.75
Nesil 10: En İyi Uygunluk = 1456.32
Nesil 20: En İyi Uygunluk = 1523.89
Nesil 30: En İyi Uygunluk = 1567.45

Performans Analizi:
Tamamlanan teslimat sayısı: 18/20
Teslimat yüzdesi: %90.00
Ortalama enerji tüketimi: 45.67 birim
Ortalama mesafe: 234.56 metre
Algoritma çalışma süresi: 12.34 saniye

Uçak Bazında Sonuçlar:
Uçak 0: 4 teslimat, 187.23 metre, 38.45 enerji
Uçak 1: 3 teslimat, 156.78 metre, 32.12 enerji
Uçak 2: 5 teslimat, 298.45 metre, 67.89 enerji
Uçak 3: 3 teslimat, 145.67 metre, 29.34 enerji
Uçak 4: 3 teslimat, 184.12 metre, 40.56 enerji
🔬 Zaman Karmaşıklığı
Algoritma	Karmaşıklık	Açıklama
A*	O(E log V)	E: kenar, V: düğüm sayısı
Genetik	O(G × P × D × A)	G: nesil, P: popülasyon, D: drone, A: A* çağrısı
Kısıt Kontrolü	O(D × T)	D: drone, T: teslimat sayısı
Toplam	O(G × P × D × T × E log V)	Genel sistem karmaşıklığı
🛠️ Geliştirme
Kod Yapısı
ucak.py
├── Veri Modelleri (Ucak, TeslimatNoktasi, UcusYasakBolgesi)
├── Yardımcı Fonksiyonlar (geometrik hesaplamalar)
├── A* Algoritması (yol bulma)
├── Genetik Algoritma (optimizasyon)
├── Görselleştirme (matplotlib)
└── Performans Analizi (metrikler)
