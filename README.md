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
komutuyla, sonra tek docker compose up ile kurdum. Round-robin yük dengelemeyi
canlı izledim.

## Workshop - Part 1: Konteynerize Etme
To-do uygulamasına sıfırdan Dockerfile yazdım. Yeni: # syntax direktifi,
npm --omit=dev, -p 127.0.0.1:3000:3000 ile portu sadece localhost'a açma.