# hacktahon-tracker
A mini-hackathon tracker project for GDGoC

---

## Project Description

### GÖREV: Mini Hackathon Takip ve Puanlama Sistemi

#### BAĞLAM
Kulüp olarak [tarih]'te 2 saatlik bir mini hackathon düzenliyoruz. Takımlar 2 saatin sonunda basit de olsa çalışan bir uygulama teslim edecek. AI kodlama araçları serbest. İzin verilen diller: Python ve JavaScript/TypeScript. Beklenen katılım: [takım sayısı] takım, takım başı [kişi sayısı] kişi.

Sizden iki şey istiyoruz:
1) Herkesin her takımın ilerlemesini canlı görebildiği bir pano
2) Kod kalitesini otomatik ölçen bir sistem

#### 1. CANLI İLERLEME PANOSU
- Tüm takım repoları tek bir GitHub organizasyonunda açılacak (takım başı 1 repo).
- Pano herkese açık bir web sayfası olacak, projeksiyona yansıtılacak.
- Otomatik takip (GitHub API veya webhook): repo açıldı mı, commit sayısı, son commit zamanı ve mesajı, kimlerin commit attığı.
- Elle takip: takımlar şu aşamaları kendileri işaretleyecek:
  - [ ] Fikir belirlendi
  - [ ] Repo açıldı
  - [ ] İlk çalışan sürüm
  - [ ] Ana özellik bitti
  - [ ] Demo hazır
  - [ ] Teslim edildi
- Panoda kalan süre sayacı olacak.
- Süre bitiminden sonra atılan commit'ler değerlendirmeye alınmayacak; sistem bitiş anındaki son commit'i baz almalı.

#### 2. KOD KALİTESİ ÖLÇÜMÜ
- Her dil için bir statik analiz aracı araştırıp seçin (örnek: Python için pylint veya ruff, JS/TS için ESLint). Hangi aracı neden seçtiğinizi kısaca yazın.
- Araç her repoda aynı ayarlarla çalışmalı (ayar dosyasını siz sağlayın, takımlar değiştiremesin).
- Farklı dillerin sonuçları ortak bir 0-100 puanına çevrilmeli ki Python ve JS takımları adil kıyaslansın. Dönüşüm formülünü belgeleyin.
- Ölçüm süre bitiminde tüm repolar için tek komutla çalışabilmeli.

#### 3. PUANLAMA (toplam 100)
- **Çalışan ürün:** 30 (jüri) - uygulama açılıyor ve vaat ettiğini yapıyor mu
- **Yaratıcılık:** 25 (jüri) - fikir ve çözümün özgünlüğü
- **Kod kalitesi:** 20 (otomatik) - 2. maddedeki araç puanı
- **Kullanım ve sunum:** 15 (jüri) - arayüz, demo anlatımı
- **Süreç:** 10 (yarı otomatik) - düzenli commit, README, iş bölümü

Jüri puanlarını girebileceği basit bir form olmalı; sistem toplamı hesaplayıp sıralamayı çıkarmalı. Sıralama etkinlik sonuna kadar gizli kalabilmeli.

#### 4. TESLİM EDECEKLERİNİZ
- Çalışan pano (link) ve kaynak kodu
- Takımlar için 1 sayfalık kullanım kılavuzu (repo nasıl açılır, aşama nasıl işaretlenir)
- Kalite aracı seçimi ve puan dönüşümünü anlatan kısa not
- Etkinlikten en geç [X gün] önce 2-3 sahte takımla yapılmış deneme

#### 5. DİKKAT EDİLECEKLER
- GitHub API istek limitine takılmamak için token kullanın ve [takım sayısı] repo ile test edin.
- Etkinlik günü sistem çökerse yedek plan: [örn. ortak bir tablo].
- Sistemin basit olması, özellik zenginliğinden önemli; önce 1. maddeyi bitirin.

---

## Iş bölümü:

### 1. Yusif
- **GitHub Altyapısı:** Yarışmacıların repolarını açacağı GitHub organizasyonunu kurmak, API limitine takılmamak için Personal Access Token üretmek ve test için 2–3 sahte takım reposu açmak.
- **Süreç Puanı Kontrolü:** Basit bir Python scriptiyle (veya dokümantasyon/kontrol listesiyle) repolarda `README.md` varlığını ve takım üyelerinin commit dağılımını doğrulamak.
- **Sahte Takım Stres Testi:** Etkinlikten birkaç gün önce 2–3 sahte takımla prova yapmak; özellikle süre bittikten sonra commit atarak sistemin bunu engellediğini test etmek.
- **Dokümantasyon & B Planı:** Takımlar için 1 sayfalık kullanım kılavuzunu (repo açma + aşama işaretleme) ve etkinlik günü sistem çökerse devreye girecek yedek Google Sheets tablosunu hazırlamak.

### 2. Çınar – Backend GitHub Entegrasyonu
- **Veritabanı & API Mimarisi:** Takımlar, aşama durumları, commit geçmişi ve jüri puanları için veritabanı tablolarını ve API uçlarını (endpoints) oluşturmak.
- **Otomatik Repo & Commit Takibi:** GitHub API/Webhook ile organizasyondaki repoları dinleyip repo açılış durumunu, toplam commit sayısını, son commit zamanını/mesajını ve commit atan ekip üyelerini çekmek.
- **Süre Sonu (Cutoff) Kilidi:** 2 saatlik süre dolduğu anda o saniyeden önce atılmış son geçerli commit hash'ini kilitlemek ve sonrasında gelen commit'leri yok saymak.
- **Rate Limit Yönetimi:** GitHub token kullanımı ve önbellekleme (caching) ile beklenen takım sayısında API limitine takılmadan veri akışı sağlamak.

### 3. Mert - Frontend Canlı İlerleme Panosu
- **Projeksiyon Panosu:** Herkese açık, giriş gerektirmeyen, uzaktan rahat okunabilen ana canlı takip ekranını tasarlamak.
- **Geri Sayım Sayacı:** Etkinlik bitişine kalan süreyi gösteren büyük, net ve senkronize sayacı eklemek.
- **Canlı Durum Gösterimi:** Backend'den gelen verilerle her takımın repo durumunu, commit sayısını, son commit mesajını ve işaretlediği son aşamayı anlık güncellemek.

### 4. Zeynel - Frontend Takım Arayüzü & Jüri Puanlama Sistemi
- **Takım Aşama İşaretleme Ekranı:** Takımların kendi ilerlemelerini (Fikir belirlendi, Repo açıldı, İlk çalışan sürüm, Ana özellik bitti, Demo hazır, Teslim edildi) işaretleyebileceği basit ekranı yapmak (takımların birbirini değiştirmemesi için takım başı basit PIN korumasıyla).
- **Jüri Puanlama Formu:** Jürinin Çalışan ürün (30), Yaratıcılık (25) ve Kullanım/sunum (15) puanlarını girebileceği mobil uyumlu basit formu oluşturmak.
- **Sıralama & Gizlilik Kilidi:** Jüri puanları, otomatik kod kalitesi puanı (20) ve süreç puanını (10) toplayıp sıralamayı çıkarmak; sıralama tablosunu etkinlik sonuna kadar gizli tutacak admin anahtarını eklemek.

### 5. Elvin Kod Kalitesi Analiz Motoru (CLI)
- **Tek Komutla Toplu Tarama:** Süre bitiminde tek bir terminal komutuyla organizasyondaki tüm takım repolarını otomatik çeken ve tarayan scripti yazmak.
- **Kod Kalitesi Kuralları & Formül:** Python (Ruff) ve JS/TS (ESLint) için takımların değiştiremeyeceği sabit ayar dosyalarını (`.ruff.toml`, `eslint.config.js`) hazırlamak; iki dili adil kıyaslayacak 0–100 puan dönüşüm formülünü ve seçim gerekçesini yazmak.
- **Cutoff Commit & Sabit Ayar Zorunluluğu:** Repoları en güncel halinden değil, Backend'in kilitlediği bitiş anındaki son commit hash'inden çekmek; takımın kendi linter ayarını yok sayıp hazırlanan merkezi `.ruff.toml` ve `eslint.config.js` dosyalarını zorunlu uygulamak.
- **0–100 Puan Çıktısı:** Belirlenen dönüşüm formülünü koda dökerek her takım için 0–100 arası (veya 20 üzerinden) nihai kalite puanını JSON/veritabanı formatında üretmek.

---

## Connection between members

<img width="939" height="676" alt="image" src="https://github.com/user-attachments/assets/e849e1af-dbd1-480d-928d-61334bce8479" />
