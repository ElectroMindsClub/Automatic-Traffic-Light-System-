# Automatic Traffic Light System Using ESP32

> **© Electro Minds Club  
> University Mohamed El Bachir El Ibrahimi — Bordj Bou Arreridj (`#we_learn_together`)  

---

## 1. Project Presentation

This project designs and builds a **two-way automatic traffic light system** powered by an **ESP-32S** microcontroller. It controls six LEDs representing two opposing traffic directions (Direction A and Direction B), each equipped with Red, Orange/Yellow, and Green lights.

Pressing the start push button activates a non-blocking **Finite State Machine (FSM)** using rollover-safe `millis()` timing and software debouncing (`50 ms`). Mandatory **1-second All-Red clearance phases** ensure that both directions never receive a green signal simultaneously, keeping the intersection sequence safe and continuous.

* **Club:** Electro Minds Club
* **University:** University Mohamed El Bachir El Ibrahimi — Bordj Bou Arreridj
* **Authors:** Krid Abderrahmane, Mecheri Abdelhak, Deghima Saif Eddine
* **Category:** Embedded Systems / Automation

---

## 2. Repository Description

This repository follows the official **Electro Minds Club** architecture (`Hardware/`, `Software/`, and `Documentation/`):

```text
Automatic-Traffic-Light-System/
├── README.md
│
├── Hardware/
│   ├── Circuit_Diagram/
│   │   └── HARDWARE.png                             # Breadboard prototype & wiring photo
│   ├── BOM.csv                                      # Complete Bill of Materials
│   ├── Circuit_Schematic/                           # Electrical / PCB schematic files
│   └── 3D_Printed_Parts/
│       └── traffic_light.stl                        # 3D printable traffic light model
│
├── Software/
│   ├── Algorithms.pdf                               # FSM flowchart, debounce & timing logic
│   ├── Firmware/
│   │   ├── Automatic-Traffic-Light-System/
│   │   │   └── Automatic-Traffic-Light-System.ino   # ESP32 Arduino firmware
│   │   └── libraries/                               # External Arduino libraries (none required)
│   └── Software/                                    # Platform, cloud, or IoT code (if added later)
│
└── Documentation/
    ├── Technical_Card.pdf                           # Project technical specification card
    ├── Datasets/                                    # Datasets (if applicable)
    ├── Project_Documentation/
    │   └── DOCUMENTATION-TRAFIC_LIGHT.docx          # Full Word project report
    └── Datasheets/                                  # Sensor & component datasheets (ESP-32S, LEDs)
```

### Directory Overview

| Directory | Contents |
| --- | --- |
| [`Hardware/`](./Hardware/) | Breadboard wiring photo (`Circuit_Diagram/HARDWARE.png`), component list (`BOM.csv`), electrical schematic folder (`Circuit_Schematic/`), and 3D-printable model (`3D_Printed_Parts/traffic_light.stl`). |
| [`Software/`](./Software/) | Finite State Machine documentation (`Algorithms.pdf`), ESP32 Arduino sketch (`Firmware/Automatic-Traffic-Light-System/`), and reserved folder for optional IoT/cloud extensions (`Software/`). |
| [`Documentation/`](./Documentation/) | Project technical specification sheet (`Technical_Card.pdf`), full project documentation (`Project_Documentation/DOCUMENTATION-TRAFIC_LIGHT.docx`), and folders for `Datasets/` and component `Datasheets/`. |

---

## 3. How to Make It

### Step 1: Gather Components 
* 1× **ESP-32S** microcontroller board
* 6× **LEDs** (2 Red, 2 Orange/Yellow, 2 Green)
* 6× **220 Ω Resistors** (LED current-limiting protection)
* 1× **Push Button**
* 1× **Breadboard**, **Jumper Wires**, and **USB Cable**
* *(Optional)* 3D-print the housing from [`Hardware/3D_Printed_Parts/traffic_light.stl`](./Hardware/3D_Printed_Parts/traffic_light.stl)

### Step 2: Wire the Hardware
Assemble the circuit on the breadboard following [`Hardware/Circuit_Diagram/HARDWARE.png`](./Hardware/Circuit_Diagram/HARDWARE.png) and the GPIO table below. Always place a **220 Ω resistor** in series with each LED and connect all LED cathodes and one side of the push button to `GND`.

| Component | Direction / Role | ESP32 GPIO Pin | Pin Mode |
| --- | --- | :---: | :---: |
| Red LED A | Direction A | `GPIO 25` | `OUTPUT` |
| Orange / Yellow LED A | Direction A | `GPIO 26` | `OUTPUT` |
| Green LED A | Direction A | `GPIO 27` | `OUTPUT` |
| Red LED B | Direction B | `GPIO 16` | `OUTPUT` |
| Orange / Yellow LED B | Direction B | `GPIO 17` | `OUTPUT` |
| Green LED B | Direction B | `GPIO 18` | `OUTPUT` |
| Start Push Button | System Start | `GPIO 14` | `INPUT_PULLUP` |

### Step 3: Upload the Firmware
1. Install the [Arduino IDE](https://www.arduino.cc/en/software) and add the **ESP32** board package via the Boards Manager.
2. Clone or download this repository:
   ```bash
   git clone https://github.com/ElectroMindsClub/Automatic-Traffic-Light-System-.git
   ```
3. Open [`Software/Firmware/Automatic-Traffic-Light-System/Automatic-Traffic-Light-System.ino`](./Software/Firmware/Automatic-Traffic-Light-System/Automatic-Traffic-Light-System.ino) in the Arduino IDE (no external third-party libraries are required).
4. Select your **ESP32 Dev Module** board and the correct **COM Port** under **Tools**.
5. Click **Upload** to flash the firmware onto the ESP-32S.

### Step 4: Test & Verify Operation
Power the ESP32 via USB and press the push button on `GPIO 14`. Confirm the 16-second automatic cycle runs continuously (full FSM details in [`Software/Algorithms.pdf`](./Software/Algorithms.pdf)):

| Phase | Direction A | Direction B | Duration |
| :---: | :---: | :---: | :---: |
| 1 | Green | Red | 5 s |
| 2 | Orange / Yellow | Red | 2 s |
| 3 | Red | Red | 1 s |
| 4 | Red | Green | 5 s |
| 5 | Red | Orange / Yellow | 2 s |
| 6 | Red | Red | 1 s |

### Notes & Future Improvements
* Double-check all breadboard connections and polarity before powering the ESP-32S.
* Always use **220 Ω resistors** to protect the LEDs and ESP32 GPIO pins.
* Future enhancement: add pedestrian crossing push buttons and walk/stop indicator LEDs.

---

**All rights are reserved to Electro Minds Club.**
