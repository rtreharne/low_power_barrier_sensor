# 🚧 Parking Barrier Activity Logger

Low-power, discreet LoRa-based system using an **accelerometer** to detect parking barrier movement. Sensor nodes mount directly on barrier arms, powered by LiPo + solar top-up, transmitting events to an office receiver connected to a Django dashboard.

---

## 🧾 Bill of Materials (Per Node)

| Component                                  | Example & Link                                                                                     | Qty | Unit Price | Total |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------|-----|------------|-------|
| Heltec WiFi LoRa 32 V3 Dev Board         | Amazon UK (“ESP32 LoRa V3” with OLED) :contentReference[oaicite:1]{index=1}             | 1   | £20        | £20   |
| LiPo Battery (1000 mAh, 3.7 V)           | Standard flat LiPo pack with JST connector                                                          | 1   | £6         | £6    |
| 3‑Axis Accelerometer (LIS3DH module)      | Adafruit LIS3DH breakout board :contentReference[oaicite:2]{index=2}            | 1   | £8         | £8    |
| TP4056 LiPo Charger Module (incl. protection) | Micro USB LiPo charger board                                                                      | 1   | £2         | £2    |
| Mini Solar Panel (0.5 W, 5 V)             | EVTSCAN polycrystalline panel 3.7×1.9 in :contentReference[oaicite:3]{index=3}                         | 1   | £4         | £4    |
| 3M VHB Mounting Tape                      | Small piece per device                                                                              | —   | £0.50      | £0.50 |
| 3D-Printed Case                           | PLA/PETG print material cost                                                                       | 1   | £2         | £2    |
| Wires, JST header, diode, misc parts      | For internal wiring                                                                                | —   | £1         | £1    |

**Total per sensor node:** **£43.50**  
**Two sensor nodes:** **£87**

---

## 🖥️ Office Receiver Hardware

| Component                      | Notes                              | Qty | Unit Price | Total |
|-------------------------------|-------------------------------------|-----|------------|-------|
| Raspberry Pi (Zero W)         | Assuming already available          | 1   | £0         | £0    |
| LoRa USB Dongle or HAT        | Works with Heltec radio            | 1   | £18        | £18    |

**Receiver Total:** **£18**

---

## 💸 Total Project Cost

- **2 × Sensor Nodes:** £87  
- **Office Receiver:** £18  
- **Overall Total:** **£105**

---

## 📡 System Description

1. **Sensor Node**  
   - LIS3DH wakes MCU on motion.  
   - Sends LoRa packet (“ENTRY” or “EXIT”).  
   - TP4056 recharges LiPo via solar panel outside the case.  
   - All contained in ~8x5x2 cm, < 100 g.

2. **Office Receiver (Raspberry Pi)**  
   - Listens via LoRa dongle.  
   - Logs events and pushes via REST to Django.

3. **Django Dashboard**  
   - Stores `BarrierEvent` entries.  
   - Shows usage charts, anomaly detection.

---

## 🗓️ 1-Month Work Plan

### Week 1 – Hardware & Motion Proof-of-Concept
- Order all components.
- Prototype motion detection using LIS3DH + Heltec.
- Write MCU code: sleep → wake on motion → send LoRa → sleep.
- Measure power usage and battery discharge.

### Week 2 – Enclosure & Solar Integration
- 3D print case with mount points for board and panel connector.
- Mount solar panel externally, internal TP4056.
- Deploy one unit to barrier; monitor battery recharge and event logs.

### Week 3 – Office Receiver Setup
- Install Raspberry Pi with LoRa USB/HAT.
- Write Python listener to parse packets and POST to Django API.
- Test full pipeline from barrier to office.

### Week 4 – Django Web App Development
- Models: `Barrier`, `BarrierEvent`.
- API endpoint to receive events.
- Dashboard UI: charts, daily counts, predicted alerts.
- Deploy web app (local server or cloud).
- Ensure Pi listener runs on boot, auto-reconnect on failure.

---

## 🛠️ Future Improvements

- Add user-configurable sensitivity in firmware.
- Tamper detection via case-open switch.
- LoRaWAN support for large-scale deployments.
- SMS/email alerts for anomalies (e.g. being stuck open over threshold).

---

## 🧠 Author

Dr. Robert Treharne  
Senior Lecturer in Technology Enhanced Learning  
University of Liverpool  
