# DC Motor Controller - Real-Time Position Control System

## Overview

This repository contains a complete embedded system for **precise DC motor position control**. The system is divided into four major components:

- **Firmware** - ESP32-S3 real-time motor control firmware with PID and motion profiling
- **Hardware** - Custom Altium Designer PCB with motor driver, power management, and sensing
- **SCADA** - LabVIEW HMI for real-time monitoring and PID tuning
- **Simulation** - Python-based Fuzzy Logic vs PID control algorithm comparison

---

## System Architecture

```
┌──────────────────┐    Micro-USB     ┌──────────────────────────────────────────────┐
│   Host PC        │◄────────────────►│  Custom PCB                                  │
│                  │   USB CDC        │                                              │
│  LabVIEW SCADA   │  (TinyUSB)       │  ESP32-S3 ──► DRV8876 H-Bridge ──► DC Motor  │
│  - Position plot │                  │      ▲                               │       │
│  - PID tuning    │                  │      └──── PCNT ◄── Quadrature Encoder       │
│  - Monitoring    │                  │                                              │
└──────────────────┘                  └──────────────────────────────────────────────┘

┌──────────────────┐
│  Simulation      │  Validates control algorithms offline
│  (Python)        │  Fuzzy Logic vs PID comparison
└──────────────────┘
```

---

## Repository Structure

```
DC-Motor-Controller/
├── DC-Motor-Controller-Firmware/                    # ESP32-S3 firmware (C++, ESP-IDF)
├── DC-Motor-Controller-Hardware/                    # Altium Designer PCB design
├── DC-Motor-Controller-SCADA/                       # LabVIEW HMI interface
├── DC-Motor-Postion-Control-Fuzzy-PID-Simulation/   # Python control simulation
└── README.md
```

---

## Firmware

**Directory:** `DC-Motor-Controller-Firmware/`

| | |
|---|---|
| **Platform** | ESP32-S3 |
| **Framework** | ESP-IDF v5.5.1 |
| **Language** | C++ |
| **Version** | v1.2.0 |

**Key features:**
- PID position control with anti-windup
- DRV8876 motor driver (PWM, fault detection, ramp control)
- Quadrature encoder via ESP32 PCNT peripheral with speed filtering
- USB CDC communication (TinyUSB)
- Motion profiling (trapezoid and S-curve acceleration shaping)
- Modular interface-based architecture (IMotorController, IEncoder, IMotorDriver, IComm, IPIDController)
- RGB LED status indication
- 6 example projects included

**Build & flash:**
```bash
idf.py set-target esp32s3
idf.py build
idf.py flash monitor
```

---

## Hardware

**Directory:** `DC-Motor-Controller-Hardware/`

| | |
|---|---|
| **Tool** | Altium Designer |
| **Schematics** | 16 sheets (modular organization) |

**Key subsystems:**
- ESP32-S3 MCU (power and I/O)
- DRV8876 H-bridge motor driver
- Power generation (buck converter + LDO)
- Quadrature encoder input (position sensing)
- Temperature and voltage sensing
- USB-C and RS485 communication interfaces
- Programmer interface
- RGB LED user indicator

**Manufacturing outputs included** - CAMtastic files, ready for PCB fabrication.

---

## SCADA

**Directory:** `DC-Motor-Controller-SCADA/`

| | |
|---|---|
| **Platform** | LabVIEW |
| **Communication** | VISA (USB/Serial) |

**Features:**
- Real-time position feedback visualization
- Live PID parameter tuning
- Serial communication configuration
- Status and fault monitoring
- 3D visualization controls

---

## Simulation

**Directory:** `DC-Motor-Postion-Control-Fuzzy-PID-Simulation/`

| | |
|---|---|
| **Language** | Python 3.10+ |
| **Dependencies** | numpy, scipy, scikit-fuzzy, matplotlib, simple-pid |

**Features:**
- Fuzzy Logic vs PID controller comparison
- Realistic DC motor physics (electrical + mechanical modeling)
- Encoder simulation with quantization (1000 PPR) and Gaussian noise
- Comprehensive visualization (membership functions, 3D control surfaces, phase plane analysis)

**Quick start:**
```bash
./setup.sh
./run_simulation.sh start_position=0 end_position=90
./run_simulation.sh start_position=-90 end_position=45 controller=pid
```

---

## Requirements

| Component | Requirement |
|-----------|-------------|
| Firmware | [ESP-IDF v5.5.1](https://docs.espressif.com/projects/esp-idf/) |
| Hardware | [Altium Designer](https://www.altium.com/) (viewing/editing) |
| SCADA | [NI LabVIEW Runtime Engine](https://www.ni.com/en/support/downloads/software-products.html) |
| Simulation | Python 3.10+ with `pip install -r requirements.txt` |

---

## License

(c) 2026 Nagy Richard.
This project is intended for **educational and prototyping purposes only**.
Commercial use, distribution, or modification requires **prior written permission** from the author.
