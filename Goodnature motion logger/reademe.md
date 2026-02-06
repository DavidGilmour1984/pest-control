# ESP32 Acceleration Trap Monitor

This project turns an **ESP32 + MPU6050** into a self-hosted acceleration event logger with a live web interface.  
It is designed for detecting **short, infrequent acceleration bursts** (e.g. traps, impacts, triggers), logging each event with **NZ-local time**, **peak acceleration**, and persistent storage across reboots.

---

## 1. Hardware Setup

### Required
- ESP32 (tested with ESP32-WROOM)
- MPU6050 (I²C)
- WiFi network (2.4 GHz)

### MPU6050 Pinout (ESP32)
| MPU6050 | ESP32 |
|------|------|
| VCC | 3.3 V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

---

## 2. What This Does

- Hosts a **web dashboard** at a fixed IP address  
- Displays **live net acceleration**  
- Automatically **tares (zeros)** regardless of orientation  
- Periodically re-tares to remove drift  
- Detects events when acceleration exceeds a threshold  
- Records:
  - NZ date & time (DST aware)
  - Peak acceleration for each event  
- Prevents double-counting using a **cooldown time**  
- Stores all settings and events in **flash (Preferences)**  
- Allows:
  - Editing threshold & cooldown
  - Selecting individual events
  - Clearing selected events only
  - Checking all events with one button  

---

## 3. Network Configuration

The ESP32 uses a **static IP**.

```cpp
IPAddress local_IP(192, 168, 1, 50);
IPAddress gateway(192, 168, 1, 1);
IPAddress subnet(255, 255, 255, 0);
IPAddress dns(192, 168, 1, 1);
