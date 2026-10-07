# Base64 → HTML / Word / PDF Dönüştürücü

Base64 verisini çözüp içeriğini otomatik tanıyan, önizleyen ve dosya olarak kaydeden tek sayfalık web uygulaması.

İki yönlü çalışır: base64'ü çözer, ya da dosya/metinden base64 üretir.

## Özellikler

### Dosya → Base64 (kodlama)

- Her tür dosyayı sürükle-bırak ya da seç; metin de yazılabilir
- Çıktı düz base64 veya `data:` URI olarak alınabilir
- 76 karakterde satır kırma (e-posta/MIME uyumu için)
- Panoya kopyala ya da `.txt` olarak kaydet

### Base64 → Dosya (çözme)

- **Otomatik içerik tespiti:** HTML, düz metin, PNG/JPEG/GIF/WEBP, PDF, Word (.docx), Excel (.xlsx), PowerPoint (.pptx), ZIP
- **HTML çıktısı:** önizleme, kaynak görünümü, `.html` olarak kaydetme
- **Word çıktısı:** HTML veya metin içeriğinden gerçek `.docx` üretir (başlık, liste, tablo, bağlantı, gömülü görsel)
- **Word girdisi:** base64 zaten bir `.docx` ise içeriği önizlenir ve dosya birebir kaydedilir
- **PDF çıktısı:** içeriği tarayıcının yazdırma penceresinden PDF olarak kaydeder
- **Kaynak dosya:** çözülen veriyi doğru uzantıyla (`.pdf`, `.png`, `.xlsx` …) kaydeder
- Girdi toleransı: `data:` öneki, satır sonları, URL-safe base64, eksik `=` dolgusu

## Gizlilik

Tüm işlem tarayıcıda yapılır. Uygulama kendisi hiçbir ağ isteği göndermez; yapıştırdığın veri sunucuya ulaşmaz.
(Çözülen HTML dış kaynaklı bir görsel içeriyorsa, önizleme o görseli kendi adresinden yükler.)

Önizleme ve "Yeni sekmede aç", çözülen içerikteki betikleri çalıştırmaz. Kaydedilen `.html` dosyası ise
içeriği olduğu gibi, betikleriyle birlikte saklar.

## Kullanım

- **Web:** GitHub Pages (veya GitLab Pages) adresinden aç.
- **Yerel:** `index.html` dosyasına çift tıkla — kurulum veya internet gerekmez.

## Yayınlama

Derleme adımı yoktur; `index.html` doğrudan yayınlanır.

**GitHub Pages:** depoda **Settings → Pages → Build and deployment** altında
*Source: Deploy from a branch*, *Branch: `main` / `(root)`* seç. Adres aynı sayfada görünür
(`https://<kullanıcı>.github.io/<depo>/`). Ücretsiz hesaplarda Pages yalnızca herkese açık depolarda çalışır.
`.nojekyll` dosyası, GitHub'ın siteyi Jekyll ile işlemesini kapatır.

**GitLab Pages:** `.gitlab-ci.yml` içindeki `pages` işi, varsayılan dala yapılan her push'ta
`index.html`'i yayınlar. Adres, projenin **Deploy → Pages** sayfasında görünür.

## Teknik notlar

- Tek dosya, harici kütüphane yok. `.docx` paketi (ZIP + OOXML) tarayıcıda sıfırdan üretilir.
- Sıkıştırılmış `.docx` okumak için `DecompressionStream` kullanılır (güncel Chrome, Edge, Firefox, Safari).
- Desteklenmeyenler: ZIP64 arşivleri, parola korumalı belgeler, eski ikili `.doc` biçimi.
