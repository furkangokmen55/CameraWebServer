# CameraWebServer

ESP32 tabanlı kameralı geliştirme kartları (ESP32-CAM, ESP-EYE, M5Stack, XIAO ESP32S3 Sense, Freenove vb.) için kablosuz kamera web sunucusu. Kart, kendi WiFi ağına bağlanır ve tarayıcı üzerinden canlı görüntü akışı (MJPEG stream) sunar; ayrıca çözünürlük, kalite, parlaklık gibi kamera ayarlarını web arayüzünden değiştirmeye izin verir.

## Özellikler

- Gerçek zamanlı MJPEG video akışı
- Tarayıcı üzerinden anlık fotoğraf çekme
- Çözünürlük, JPEG kalitesi, parlaklık, doygunluk gibi ayarları canlı değiştirme
- Birden fazla ESP32 kamera kartı modelini destekler (`board_config.h` üzerinden seçim)
- PSRAM varsa otomatik olarak daha yüksek çözünürlük ve çift frame buffer kullanır

## Gereksinimler

- Bir ESP32 kamera kartı (ESP32-CAM (AI-Thinker), ESP-EYE, M5Stack Wide/ESP32CAM, ESP32S3-EYE, XIAO ESP32S3 Sense vb.)
- [Arduino IDE](https://www.arduino.cc/en/software) + ESP32 board desteği kurulu olmalı
- PSRAM'li bir kart önerilir (yüksek çözünürlük ve akıcı akış için)

## Kurulum

1. Bu repoyu klonla veya indir:
   ```
   git clone https://github.com/furkangokmen55/CameraWebServer.git
   ```
2. `CameraWebServer.ino` dosyasını Arduino IDE ile aç.
3. `board_config.h` içinden kullandığın kamera modelini seç (ilgili satırın başındaki `//` işaretini kaldır, diğerlerini yorumda bırak).
4. `CameraWebServer.ino` içindeki WiFi bilgilerini kendi ağınla değiştir:
   ```cpp
   const char *ssid = "YOUR_WIFI_SSID";
   const char *password = "YOUR_WIFI_PASSWORD";
   ```
5. Arduino IDE'de doğru kart ve port seçili olduğundan emin ol, ardından kodu ESP32'ye yükle.
6. Seri Monitör'ü aç (115200 baud) — kart WiFi'a bağlandığında sana bir IP adresi verecek.
7. O IP adresini tarayıcına yaz, kamera arayüzü karşına çıkacak.

## Dosya Yapısı

| Dosya | Açıklama |
|---|---|
| `CameraWebServer.ino` | Ana program — kamera ve WiFi kurulumu |
| `app_httpd.cpp` | Web sunucusu ve stream/fotoğraf endpoint'leri |
| `board_config.h` | Kullanılacak kamera kartı modelinin seçildiği yer |
| `camera_pins.h` | Farklı kart modelleri için pin tanımlamaları |
| `camera_index.h` | Web arayüzünün HTML/JS içeriği |
| `partitions.csv` | ESP32 flash bellek bölümleme tablosu |

## Notlar

- WiFi bilgilerini kod içine yazmak yerine ortam değişkeni veya ayrı bir config dosyası kullanmak, bu bilgileri yanlışlıkla GitHub'a yüklememek açısından daha güvenlidir.
- PSRAM olmayan kartlarda çözünürlük otomatik olarak düşürülür (SVGA).
