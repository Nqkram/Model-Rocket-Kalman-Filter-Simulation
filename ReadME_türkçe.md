---

# 🚀 Kalman Filtresi ile Model Roket Telemetri Sistemi

## Proje Hakkında

Bu projede **model roket uçuş verileri**, bir **Kalman filtresi algoritması** kullanılarak işlenmiş ve filtrelenmiş sonuçlar bir **LCD ekran üzerinde gerçek zamanlı olarak gösterilmiştir**.

Sistem, roket uçuşunu simüle eder ve sensörlerden elde edilen ölçümlerdeki gürültüyü azaltarak daha kararlı ve doğru durum tahminleri üretir.

Proje özellikle şu konulara odaklanmaktadır:

* Kalman filtresi ile **gürültü azaltma**
* **sensör füzyonu**
* gömülü sistemlerde **durum tahmini**
* **gerçek zamanlı telemetri gösterimi**

---

# Sistem Mimarisi

Sistemde roketin uçuş durumu **6 boyutlu bir durum vektörü** ile ifade edilir.

```
x = [yükseklik, dikey_hız, dikey_ivme, roll, pitch, yaw]
```

Kalman filtresi her simülasyon adımında sensör verilerini işleyerek roketin durumunu günceller.

---

# Kullanılan Donanım

Proje aşağıdaki donanımlar üzerinde çalışacak şekilde tasarlanmıştır:

* **Teensy 4.1**
* **16x2 I2C LCD ekran**

---

# Kullanılan Kütüphaneler

Projede aşağıdaki Arduino kütüphaneleri kullanılmıştır:

* Arduino
* Wire
* LiquidCrystal_I2C
* math

---

# Uçuş Simülasyonu

Kod içerisinde model roketin uçuşu fiziksel olarak simüle edilmektedir.

Simülasyonda dikkate alınan parametreler:

* Roket itki kuvveti
* Yakıt tüketimi
* Hava sürüklenmesi (drag)
* Yerçekimi
* Atmosfer basınç modeli

### Simülasyon Parametreleri

| Parametre           | Değer  |
| ------------------- | ------ |
| Roket itki kuvveti  | 1800 N |
| Roket kütlesi       | 12 kg  |
| Yakıt kütlesi       | 5 kg   |
| Yanma süresi        | 3.5 s  |
| Sürükleme katsayısı | 0.45   |
| Simülasyon adımı    | 0.05 s |

---

# Seri Port Komutları

Arduino **Serial Monitor (115200 baud)** üzerinden sistem kontrol edilebilir.

| Komut  | Açıklama                            |
| ------ | ----------------------------------- |
| start  | Simülasyonu başlatır                |
| step   | Tek bir simülasyon adımı çalıştırır |
| run N  | N adet adım çalıştırır              |
| reset  | Sistemi sıfırlar                    |
| status | Mevcut roket durumunu gösterir      |
| help   | Komut listesini gösterir            |

Örnek kullanım:

```
run 100
```

100 simülasyon adımı çalıştırır.

---

# LCD Çıkışı

LCD ekran üzerinde filtrelenmiş uçuş verileri gösterilir:

* yükseklik
* hız
* ivme
* yönelim değerleri

Veriler simülasyon sırasında **gerçek zamanlı olarak güncellenir**.

---

# Matematiksel Yöntem

Sistemde **ayrık zamanlı Kalman filtresi** kullanılmıştır.

### Tahmin Adımı

```
x = F · x
P = F · P · Fᵀ + Q
```

### Güncelleme Adımı

```
K = P · Hᵀ (H · P · Hᵀ + R)⁻¹
x = x + K(z − Hx)
P = (I − KH)P
```

Bu yöntem sensör ölçümlerindeki gürültüyü azaltarak daha stabil bir telemetri sağlar.

---

# Projenin Amacı

Bu proje aşağıdaki konuların gösterimi amacıyla geliştirilmiştir:

* Kalman filtresi uygulamaları
* gömülü sistemlerde durum tahmini
* model roket aviyonik sistemleri
* sensör verisi işleme teknikleri

---

# Gelecek Geliştirmeler

Proje aşağıdaki özelliklerle geliştirilebilir:

* gerçek sensör entegrasyonu (BMP280, MPU6050)
* LoRa telemetri haberleşmesi
* SD kart uçuş veri kaydı
* yer istasyonu görselleştirme sistemi
* gerçek uçuş bilgisayarı entegrasyonu

---

# Lisans

Bu proje **MIT License** altında yayınlanmıştır.

---


