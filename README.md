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