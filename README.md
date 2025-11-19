# 08_Dizi_LED_Yak_Son (Paralel Dizi Yöntemi)

Bu proje, **STM32F407-Discovery** kartı üzerinde 4 adet LED'i, önceden tanımlanmış statik bir desene (`1-0-1-1`) göre yakar.

Bu depo, C dilindeki **"paralel dizilerin" (parallel arrays)** donanım programlamada nasıl verimli kullanılabileceğini gösterir. Pinler bir dizide (`ledler[]`), bu pinlerin alacağı durumlar (AÇIK/KAPALI) ise başka bir dizide (`led_durum[]`) saklanır.

* **Pin Dizisi:** `ledler[]` dizisi `GPIO_PIN_1`'den `GPIO_PIN_4`'e kadar olan pinleri listeler.
* **Durum Dizisi:** `led_durum[]` dizisi, her pine karşılık gelen durumu (`1` veya `0`) tutar.

> **🔜 Sonraki Adım (Animasyonlu Uygulama)**

> Bu projede tek bir durum dizisi ile **sabit (statik)** bir desen oluşturduk.
> Bu yöntemi kullanarak **hareketli bir flaşör animasyonu** (Çift/Tek yakma) yapmak için, birden fazla durum dizisinin kullanıldığı bir sonraki projeyi inceleyebilirsiniz:
> 
> ➡️ **[09_Cift_Tek_LED_Yakma (Flaşör Efekti)](https://github.com/yurttaskardelen/09_Cift_Tek_LED_Yakma)**

---

### 🎯 Proje Senaryosu

Kod, `while(1)` döngüsü içinde sürekli olarak `ledler[]` ve `led_durum[]` dizilerini gezer ve statik deseni pinlere uygular.

1.  **Diziler:**
    * `ledler[] = {GPIO_PIN_1, GPIO_PIN_2, GPIO_PIN_3, GPIO_PIN_4}`
    * `led_durum[] = {1, 0, 1, 1}`
2.  **Uygulama (for döngüsü):**
    * `i=0`: `ledler[0]` (`PA1`) -> `led_durum[0]` (`1`) -> **SET** (Yanar).
    * `i=1`: `ledler[1]` (`PA2`) -> `led_durum[1]` (`0`) -> **RESET** (Söner).
    * `i=2`: `ledler[2]` (`PA3`) -> `led_durum[2]` (`1`) -> **SET** (Yanar).
    * `i=3`: `ledler[3]` (`PA4`) -> `led_durum[3]` (`1`) -> **SET** (Yanar).
3.  Döngü biter ve `while(1)` nedeniyle hemen başa döner.

**Zamanlama:**
* **Adım Arası Bekleme:** 1000 ms (1 saniye). Döngüdeki `HAL_Delay(1000)` komutu, her bir LED'in durumunun 1 saniye arayla ayarlanmasını sağlar.

---

### 🛠️ Gerekli Donanım

* **1x** STM32F407-Discovery Geliştirme Kartı
* **4x** Tercih edilen renklerde LED
* **4x** 220 ya da 330 Ohm Direnç (LED'ler için ön direnç)
* Breadboard ve Jumper kablolar

---

### 🔌 Devre Şeması

LED'lerin anot (uzun) bacakları STM32 pinlerine, katot (kısa) bacakları ise direnç üzerinden GND hattına bağlanmalıdır.

| LED | Direnç | STM32 Pini |
| :--- | :--- | :--- |
| LED 1 | 220 Ohm | `PA1` |
| LED 2 | 220 Ohm | `PA2` |
| LED 3 | 220 Ohm | `PA3` |
| LED 4 | 220 Ohm | `PA4` |
| (Tümü) | - | `GND` |

<img width="473" height="404" alt="Pin_Baglantilari" src="https://github.com/user-attachments/assets/2faf879d-af80-4f97-9495-9c89e4afac5b" />

### Kod Bloğu

<img width="898" height="383" alt="image" src="https://github.com/user-attachments/assets/cf6d134d-a6b9-4743-8b77-07203a9dc908" />

---

### 🚀 Nasıl Kullanılır?

1.  Bu depoyu klonlayın (`git clone ...`).
2.  STM32CubeIDE yazılımını açın.
3.  `File > Open Projects from File System...` seçeneği ile proje klasörünü seçin.
4.  Proje içindeki `.ioc` dosyasını açarak pin yapılandırmasını inceleyebilirsiniz.
5.  Derleyin (Build) ve ST-Link V2 üzerinden kartınıza yükleyin (Run).
