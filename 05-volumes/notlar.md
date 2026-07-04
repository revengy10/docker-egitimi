# Volume Alıştırması

- `-v volume_adi:/konteyner/yolu` ile volume bağladım
  (örn. `-v postgres_data:/var/lib/postgresql`)
- Postgres'te tasks tablosu oluşturup veri ekledim,
  konteyneri silip aynı volume ile yenisini açtım:
  SELECT sorgusu aynı veriyi döndürdü.
- Veri konteynerde değil volume'da yaşıyor;
  konteyner geçici, volume kalıcı.
- Yönetim: docker volume ls / rm / prune
