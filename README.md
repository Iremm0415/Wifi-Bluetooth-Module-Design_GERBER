# Wifi/Bluetooth Modülü Devre Tasarımı

Bu projede, Wi-Fi ve Bluetooth destekli ESP32-S3-MINI-1-N8 modülü kullanılarak, çok işlevli bir IoT cihazı devresi tasarlanmıştır. Sistem, çeşitli sensör ve sürücü bileşenleriyle donatılmış olup uzaktan izlenebilir ve kontrol edilebilir yapıda planlanmıştır.

## Sistem Bileşenleri ve Görevleri

### 1. Ana Denetleyici

ESP32-S3-MINI-1-N8, çift çekirdekli işlemcisi ve entegre Wi-Fi/Bluetooth haberleşme
yetenekleriyle hem veri toplama hem de uzaktan kontrol için sistemin merkezinde yer almaktadır. Cihaz, kablosuz haberleşme üzerinden mobil uygulama veya web arayüzleri ile entegre çalışabilecek şekilde yapılandırılmıştır.

### 2. Röle Çıkışı

Harici yüklerin (örneğin bir cihazın açma/kapama kontrolü) uzaktan tetiklenebilmesi amacıyla sisteme 1 adet röle çıkışı entegre edilmiştir.

### 3. Opto İzoleli Giriş/Çıkışlar

Endüstriyel sistemlerle güvenli etkileşim sağlamak için 2 adet opto-izoleli dijital giriş ve 2 adet opto-izoleli dijital çıkış kullanılmıştır. Bu yapı, dış etkenlerden kaynaklanan gerilim değişimlerine karşı mikrodenetleyiciyi korur.

### 4. Gerçek Zaman Saati (RTC)

DS3231 RTC entegresi, zamanlanmış görevlerin gerçekleştirilmesini sağlayacak şekilde cihazın tarih ve saat bilgisini yüksek hassasiyetle tutmaktadır. RTC modülü, düşük güç tüketimi ve sıcaklık kompanzasyon özellikleri sayesinde güvenilir bir zaman referansı sunar.

### 5. İvmeölçer

MPU6050 modülü, cihazın ivme ve açı bilgilerini ölçerek hareket veya sarsıntı durumlarında kullanılabilecek veri üretir. Bu veriler, hareket algılama ve konumsal kontrol senaryolarında kullanılmak üzere ESP32 tarafından işlenir.

### 6. Sıcaklık ve Nem Ölçümü

DHT22 sensörü aracılığıyla ortam sıcaklığı ve nem verileri periyodik olarak okunur. Elde edilen veriler, kablosuz olarak merkezi bir sunucuya iletilebilir ya da kullanıcıya gösterilebilir.

### 7. Step Motor Kontrolü

Açısal konumlandırma işlemleri için DRV8833PW step motor sürücü entegresi kullanılmıştır. Bu sürücü, 5V ile çalışan bir motorun hassas yön ve konum kontrolünü sağlar.

### 8. Sesli Uyarı Sistemi

Sistem durumları (örneğin hata, alarm, tetikleme) için bir buzzer entegre edilmiştir. Bu bileşen ile kullanıcıya sesli bildirim sağlanmaktadır.

### 9. Zamanlama ve Saat İşlemleri için Kristaller

Sistem kararlı ve senkron çalışabilmesi amacıyla iki farklı kristal osilatör kullanılmıştır:

### 10. 8 MHz kristal

ESP32'nin temel çalışma frekansını destekler.

### 11. 32.768 kHz kristal

RTC zamanlayıcısı ile birlikte hassas saat ölçümleri için kullanılır.

<img src="https://github.com/user-attachments/assets/b7d2787f-ca6c-443c-ba76-0967c1a0f596" width="480">

*Şekil 13 Wifi/Bluetooth Modülü Devresi Şematik*

## Çalışma Prensibi

Cihaz çalıştırıldığında, ESP32-S3 mikrodenetleyicisi tüm çevresel birimlerle haberleşmeyi başlatır. RTC üzerinden alınan zaman bilgisi senkronize edilir ve LCD ekrana yansıtılır.

MPU6050 sensöründen ivme ve açısal konum bilgisi periyodik olarak okunur. Aynı şekilde, ortam sıcaklığı ve nem verileri DHT22 üzerinden elde edilerek ekranda gösterilir.

Kullanıcı, sistem üzerindeki butonlar yardımıyla çıkış voltajını seçebilir. Bu seçimler ESP32 tarafından yorumlanarak, röle kontrolü ve opto çıkışlar üzerinden uygun eylemler tetiklenir.
Açısal kontrol gerekiyorsa step motor sürülür. Sistem bir hata algıladığında (örneğin kısa devre veya veri kaybı), buzzer ve RGB LED ile kullanıcı uyarılır.

Tüm bu işlemler Wi-Fi veya Bluetooth üzerinden dış sistemlere veri iletebilecek veya uzaktan kontrol edilebilecek şekilde tasarlanmıştır. Bu sayede cihaz, IoT altyapısı içerisinde
haberleşebilir ve uzaktan erişimli uygulamalarla entegre olabilir.

<img src="https://github.com/user-attachments/assets/10d84c84-5598-4903-aaa4-4ab06f8bec9f" width="480">

*Şekil 14 Wifi/Bluetooth Modülü Devresi 2D Gösterim*

## Sonuç ve Değerlendirme

Geliştirilen bu IoT cihazı, farklı çevresel parametreleri ölçebilen, donanımsal olarak kontrol edilebilen ve kablosuz iletişim sayesinde uzaktan yönetilebilen bütünleşik bir sistem sunmaktadır. Endüstriyel otomasyon, ev otomasyonu, çevre izleme ve akıllı sistem uygulamaları gibi birçok alanda kullanılabilecek esnek ve ölçeklenebilir bir çözüm sunmaktadır.

<img src="https://github.com/user-attachments/assets/56cbaa1c-6504-4f4e-b775-e4c8b44c5154" width="480">

*Şekil 15 Wifi/Bluetooth Modülü Devresi 3D Gösterim*

<img src="https://github.com/user-attachments/assets/87e41824-e77e-48a9-80c5-73af776c5a43" width="480">

*Şekil 16 Wifi/Bluetooth Modülü Devresi 3D Gösterim*

## Yazılım Geliştirme Süreci

Bu projede yazılım geliştirme süreci, STM32CubeIDE ve ESP-IDF platformları
kullanılarak iki aşamalı olarak gerçekleştirilmiştir. STM32F103C8T6 mikrodenetleyici,
çevresel veri toplama ve temel kontrol işlevlerini yürütürken; ESP32-S3-MINI-1-N8 modülü kablosuz iletişim ve uzaktan erişim görevlerini üstlenmiştir.

STM32 tarafında, I2C üzerinden MPU6050 ve DS3231 sensörlerinden veri alınmış, zaman tabanlı okuma algoritması ile DHT22 sensöründen sıcaklık ve nem verileri elde edilmiştir. Toplanan veriler, UART protokolü ile ESP32’ye aktarılmış; röle, buzzer ve step motor gibi birimler GPIO çıkışları ve zamanlayıcılar (TIM) aracılığıyla kontrol edilmiştir.

ESP32 tarafında, UART üzerinden alınan veriler işlenmiş ve Wi-Fi/Bluetooth üzerinden IoT platformlarına iletilmiştir. Ayrıca, sistemin durumu ve sensör verileri web arayüzü veya mobil uygulamalar üzerinden kullanıcıya sunulmuştur. Gerekli durumlarda röle ve buzzer gibi çıkış birimleri doğrudan ESP32 tarafından kontrol edilebilmektedir.

Tüm iletişim yapısı senkronize ve güvenli veri aktarımına uygun şekilde yapılandırılmış; sistem, modüler ve ölçeklenebilir bir yazılım mimarisiyle geliştirilmiştir.

<img src="https://github.com/user-attachments/assets/2cce9dc0-c510-44fb-b14f-4ea1cc64afac" width="480">

*Şekil 17 Wifi/Bluetooth Modülü Devresi Pin-Clock Ayarlama*

<img src="https://github.com/user-attachments/assets/2f44e5f3-7f3a-4a8c-89d1-5304a2f4b617" width="480">

*Şekil 18 Wifi/Bluetooth Modülü Devresi Yazılımı*
