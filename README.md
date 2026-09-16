# Base64 → HTML / Word Dönüştürücü

Base64 verisini çözüp içeriğini otomatik tanıyan, önizleyen ve dosya olarak kaydeden tek sayfalık web uygulaması.

## Özellikler

- **Otomatik içerik tespiti:** HTML, düz metin, PNG/JPEG/GIF/WEBP, PDF, Word (.docx), Excel (.xlsx), PowerPoint (.pptx), ZIP
- **HTML çıktısı:** önizleme, kaynak görünümü, `.html` olarak kaydetme
- **Word çıktısı:** HTML veya metin içeriğinden gerçek `.docx` üretir (başlık, liste, tablo, bağlantı, gömülü görsel)
- **Word girdisi:** base64 zaten bir `.docx` ise içeriği önizlenir ve dosya birebir kaydedilir
- **Kaynak dosya:** çözülen veriyi doğru uzantıyla (`.pdf`, `.png`, `.xlsx` …) kaydeder
- Girdi toleransı: `data:` öneki, satır sonları, URL-safe base64, eksik `=` dolgusu

## Gizlilik

Tüm işlem tarayıcıda yapılır. Uygulama kendisi hiçbir ağ isteği göndermez; yapıştırdığın veri sunucuya ulaşmaz.
(Çözülen HTML dış kaynaklı bir görsel içeriyorsa, önizleme o görseli kendi adresinden yükler.)

Önizleme ve "Yeni sekmede aç", çözülen içerikteki betikleri çalıştırmaz. Kaydedilen `.html` dosyası ise
içeriği olduğu gibi, betikleriyle birlikte saklar.

## Kullanım

- **Web:** GitLab Pages adresinden aç.
- **Yerel:** `index.html` dosyasına çift tıkla — kurulum veya internet gerekmez.

## Yayınlama

`.gitlab-ci.yml` içindeki `pages` işi, varsayılan dala yapılan her push'ta `index.html`'i GitLab Pages'e yayınlar.
Adres, projenin **Deploy → Pages** sayfasında görünür.

## Teknik notlar

- Tek dosya, harici kütüphane yok. `.docx` paketi (ZIP + OOXML) tarayıcıda sıfırdan üretilir.
- Sıkıştırılmış `.docx` okumak için `DecompressionStream` kullanılır (güncel Chrome, Edge, Firefox, Safari).
- Desteklenmeyenler: ZIP64 arşivleri, parola korumalı belgeler, eski ikili `.doc` biçimi.
