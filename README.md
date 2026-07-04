# Docker Öğrenme Günlüğü

Docker resmi dokümantasyonunu (docs.docker.com/get-started) takip ederek
yaptığım alıştırmalar ve notlarım.

Docker Hub profilim: https://hub.docker.com/u/emirhancsgn

## 01 - Build Cache Optimizasyonu
COPY komutunu ikiye bölerek yarn install katmanının cache'te kalmasını
sağladım. Kod değişikliğinde build süresi ~20sn'den ~1sn'ye düştü.

## 02 - Multi-stage Build
Spring Boot uygulamasını JDK'lı builder aşamasında derleyip, final imaja
sadece JAR'ı kopyaladım. İmaj boyutu 880MB'den 428MB'ye indi.

## 03 - Port Yayınlama
-p HOST:CONTAINER eşlemesini, ephemeral portları (-p 80) ve EXPOSE + -P
ilişkisini öğrendim. Aynı yayınlamayı Compose'da ports: alanıyla yazdım.

## 04 - Varsayılanları Ezme
-e ile ortam değişkeni, --memory/--cpus ile kaynak limiti, --network ile
özel ağ tanımladım. Compose'da entrypoint/command ile başlangıç komutunu ezdim.

## 05 - Volume
Postgres verisini volume'a bağladım; konteyneri silip yenisini açınca
veri yerindeydi. Konteyner geçici, volume kalıcı.

## 06 - Bind Mount
Kendi klasörümü Apache konteynerine bağladım; HTML'i kaydettiğim an site
güncellendi. Volume = Docker'ın yönettiği veri, bind mount = kendi dosyalarım.

## 07 - Multi-Container
Nginx reverse proxy + 2 Node.js + Redis mimarisini önce 5 ayrı docker run
komutuyla, sonra tek docker compose up ile kurdum. Round-robin yük
dengelemeyi canlı izledim.

## Workshop - Part 1: Konteynerize Etme
To-do uygulamasına sıfırdan Dockerfile yazdım. Yeni öğrendiklerim: # syntax
direktifi, npm --omit=dev ve -p 127.0.0.1:3000:3000 ile portu sadece
localhost'a açma (güvenlik).

## Workshop - Part 2: Uygulamayı Güncelleme
Kodu değiştirip imajı yeniden build ettim. Eski konteyner 3000 portunu
tuttuğu için "port is already allocated" hatası aldım; eskiyi rm -f ile
kaldırıp yenisini başlattım. Ders: imajı güncellemek çalışan konteyneri
güncellemez; konteyner değişince içindeki veri de gider.

## Workshop - Part 3: Uygulamayı Paylaşma
İmajı emirhancsgn/getting-started olarak tag'leyip Docker Hub'a push'ladım.
Yanlış isimle push "image does not exist locally" hatası verdi — imaj adı
hedef repoyu (namespace/repo) göstermeli. Build→push→pull akışı CI/CD'nin
temeli.

## Workshop - Part 4: Veritabanını Kalıcılaştırma
İki alpine konteyneriyle yazılabilir katman izolasyonunu kanıtladım (--rm
ile). SQLite dosyasının klasörünü --mount type=volume,src=todo-db,
target=/etc/todos ile volume'a bağladım; konteyneri silip yenisini açınca
maddeler yerindeydi. docker volume inspect ile volume'un diskteki gerçek
yerini (Mountpoint) gördüm.

## Workshop - Part 5: Bind Mount ile Geliştirme Konteyneri
Kaynak kodu bind mount ile çıplak node:24-alpine konteynerine bağlayıp
içeride nodemon'lu dev sunucusu çalıştırdım (build gerektirmeden). Kod
kaydettiğim an nodemon sunucuyu yeniden başlattı. Yeni araçlar: -w
(working dir), sh -c ile komut zinciri, docker logs -f ile canlı log.