# esp32-tram
Compact ESP32-S3 multitool featuring CC1101 (Sub-GHz) and NRF24L01 (2.4 GHz) hardware modules.


# 🚋 esp32-tram

**esp32-tram** is a compact, portable wireless audit tool built on the **ESP32-S3 SuperMini**. The project integrates Sub-GHz (CC1101) and 2.4 GHz (NRF24L01) transceivers for RF research and penetration testing.

> ⚠️ **Disclaimer:** This project is intended strictly for educational purposes and authorized security auditing. The author assumes no responsibility for unauthorized or illegal use.

---

## 🛠 Hardware Stack

* **MCU:** ESP32-S3 SuperMini (Dual-core @ 240 MHz, Native USB OTG)
* **Sub-GHz Transceiver:** TI CC1101 (300–928 MHz)
* **2.4 GHz Transceiver:** Nordic NRF24L01+
* **Display:** 0.96" I2C OLED (SSD1306, 128x64)
* **Storage:** MicroSD Card Module (SPI Interface)

---

## 🔌 Hardware Pinout

Due to the limited GPIO count on the ESP32-S3 SuperMini, the **CC1101**, **NRF24L01**, and **MicroSD Module** share the hardware SPI bus (`FSPI`), controlled via individual Chip Select (`CSN`) lines.

### Shared SPI Bus:
| Signal | ESP32-S3 Pin |
| :--- | :--- |
| **SCK** | GPIO 12 |
| **MISO** | GPIO 13 |
| **MOSI** | GPIO 11 |

### Peripherals Control:
| Module | Signal | ESP32-S3 Pin |
| :--- | :--- | :--- |
| **CC1101** | CSN | GPIO 5 |
| | GDO0 (Interrupt) | GPIO 1 |
| **NRF24L01** | CSN | GPIO 6 |
| | CE | GPIO 7 |
| **OLED (I2C)** | SDA | GPIO 8 |
| | SCL | GPIO 9 |
| **MicroSD** | CSN | GPIO 4 |

> **Hardware Note:** Adding a decoupling capacitor (10–100 µF) between `3V3` and `GND` near the radio modules is recommended to prevent voltage drops during transmission peaks.

---

## Building & Flashing

The recommended development environment is **VS Code** with **PlatformIO**.

1. Clone the repository:
   ```bash
   git clone [https://github.com/YOUR_USERNAME/esp32-tram.git](https://github.com/YOUR_USERNAME/esp32-tram.git)
   cd esp32-tram
