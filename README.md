# 🎈 AR Hand-Track Balloon Pop Game

**Unity** ve **MediaPipe** teknolojileri kullanılarak geliştirilmiş, web kamerası aracılığıyla **el hareketleriyle** oynanan interaktif bir artırılmış gerçeklik (AR) oyunu.

Bu proje, görüntü işleme (computer vision) tekniklerini oyun mekanikleriyle birleştirerek oyuncunun **işaret parmağını** 3D uzayda bir kontrolcüye dönüştürür.

## 🎮 Oyun Mekaniği

Oyunun temel amacı, ekranda verilen renkli görevleri takip ederek doğru balonları patlatmaktır.

1.  **Sanal İmleç:** Web kamerasından alınan görüntü işlenir ve oyuncunun işaret parmağı (Index Finger) oyun dünyasında bir küre (Cursor) ile eşleştirilir.
2.  **Dinamik Görev Sistemi:** Oyun sürekli olarak rastgele bir hedef belirler (Örn: *"MAVİ Balonu Patlat"*).
3.  **Etkileşim ve Geri Bildirim:**
    * ✅ **Doğru Cevap:** Eğer istenen renge dokunulursa, balon parçalanır ("Break" efekti), oyuncu tebrik edilir ve oyun **bir sonraki levele (yeni renge)** geçer.
    * ❌ **Yanlış Cevap:** Yanlış renge dokunulursa, balon oyuncuya saldırır ("Attack" efekti) ve uyarı verilir. **Görev değişmez**, oyuncu doğruyu bulana kadar aynı hedefte kalır.

## 🛠 Kullanılan Teknolojiler ve Kütüphaneler

* **Oyun Motoru:** Unity 2022
* **El Takibi (Hand Tracking):** MediaPipe Unity Plugin
* **Dil:** C#
* **Platform:** PC / WebCam

## 📂 Teknik Detaylar ve Kod Yapısı

Proje, **Singleton Design Pattern** ve modüler bir mimari üzerine kurulmuştur.

### 1. `GameManager.cs` (Oyunun Beyni)
* **Singleton Yapısı:** Sahnede birden fazla yönetici oluşmasını engelleyen ve "Hayalet Yönetici" sorununu çözen `Awake()` kontrolü içerir.
* **Görev Mantığı:** Rastgelelik içerir ancak oyuncu **sadece doğru balonu patlattığında** yeni görev üretir. Yanlış cevaplarda veya bekleme durumunda görev asla değişmez.
* **UI Yönetimi:** TextMeshPro ile entegre çalışır, ekrandaki yönergeleri ve renkleri dinamik olarak günceller.

### 2. `HandToGameBridge.cs` (Kamera-Oyun Köprüsü)
* **Koordinat Dönüşümü:** MediaPipe'ten gelen 2D ekran koordinatlarını, Unity'nin 3D dünya koordinatlarına (WorldToScreenPoint -> ScreenToWorldPoint) çevirir.
* **Ghost Hand (Hayalet El) Koruması:** Oyuncu elini kameradan çektiğinde, sanal imlecin sahnede asılı kalıp yanlışlıkla balonları patlatmasını önlemek için imleci sahne dışına (Vector3: 1000, 1000, 1000) ışınlar.

### 3. `BalloonMovement.cs` (Balon Fiziği)
* **Fiziksel Kilit (Collider Lock):** Bir balona dokunulduğu milisaniye içinde o balonun `Collider` bileşeni kapatılır. Bu sayede elin titremesinden kaynaklı "çift tıklama" veya "üst üste puan alma" hataları %100 engellenir.
* **Spawn & Destroy:** Balonlar ekranın altından rastgele X koordinatlarında üretilir ve ekran dışına çıktığında performansı korumak için yok edilir.

## 🚀 Kurulum

1.  Projeyi bilgisayarınıza indirin (Clone/Download).
2.  Unity Hub üzerinden projeyi açın.
3.  Bilgisayarınızın kamerasının çalıştığından emin olun.
4.  Unity Editöründe **Play** tuşuna basın ve elinizi kameraya gösterin!

---
**Geliştirici:** [Dudu Feyza Kavun]
