# DC Motor Controller – Real-Time Position Control System

## Overview

This repository contains a complete embedded system project for **precise DC motor position control**. The system is divided into three major components:

- **Hardware** – Custom PCB design for motor control
- **Firmware** – ESP32-S3 firmware implementing PID-based control
- **SCADA Interface** – LabVIEW-based HMI for real-time monitoring and tuning

---

## Hardware

- Developed using **Altium Designer**
- Custom-designed PCB for DC motor control applications
- Includes motor driver circuitry, encoder interface, power regulation, and communication interfaces (USB/RS485)
- Schematic and layout files included in the `/hardware` directory

---

## Firmware

- Platform: **ESP32-S3**
- Framework: **ESP-IDF**
- Language: **C++**
- Implements closed-loop position control using a PID controller
- Communication interface for command/feedback
- Real-time feedback processing from encoders
- Configurable control parameters via external commands

All source code and configuration files are located in the `/firmware` directory.

---

## SCADA Interface

- Implemented in **LabVIEW**
- Provides a graphical user interface (GUI) for:
  - Real-time position feedback
  - Live tuning of PID parameters
  - Serial communication configuration
  - Status and fault monitoring

All `.vi` files and LabVIEW resources are available in the `/labview` directory.

---
## Repository Structure
```
DC-Motor-Controller/
├── Hardware/    # Altium PCB design files
├── Firmware/    # ESP32-S3 firmware source code (ESP-IDF)
├── LabVIEW/     # LabVIEW SCADA interface (.vi)
└── README.md    # Project documentation
```
---
## Requirements

- [ESP-IDF v5.4](https://docs.espressif.com/projects/esp-idf/) for firmware development
- [NI LabVIEW Runtime Engine](https://www.ni.com/en/support/downloads/software-products.html) for SCADA interface

---

## License

© 2025 Nagy Richárd.  
This project was created as part of the **Graphic Programming** course.

It is intended for **educational and prototyping purposes only**.  
Commercial use, distribution, or modification requires **prior written permission** from the author.
