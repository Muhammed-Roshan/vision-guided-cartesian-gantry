# Vision-Guided Cartesian Pick-and-Place Robot using YOLOv8 and ESP32

<p align="center">
  <img src="assets/images/banner.png" width="900">
</p>

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-orange?logo=opencv&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-IDE-00979D?logo=arduino&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blueviolet)

</p>

> A low-cost vision-guided robotic system that detects objects with **YOLOv8** and autonomously positions a custom-built two-axis Cartesian gantry over them using an **ESP32** motion controller — a complete perception-to-action pipeline in one platform.

---

## Demo

<p align="center">
  <img src="assets/demo/demo.gif" width="750">
</p>

---

## Overview

Conventional pick-and-place systems typically need expensive industrial vision sensors, making them impractical for labs, education, and low-cost automation. This project builds the full pipeline from scratch: an overhead camera + YOLOv8 detect an object's position in real time, image coordinates are converted to physical robot coordinates, and an ESP32 drives NEMA17 stepper motors to move the end-effector to that exact position — autonomously, with no manual input.

Built for the B.E. Robotics and Automation Engineering curriculum at PSG College of Technology, this integrates AI, computer vision, embedded systems, and mechanical design into one working system.

---

## System Architecture

```text
Overhead Camera → YOLOv8 Detection → Centroid Calculation
      → Pixel-to-Cartesian Transformation → Serial (115200 baud)
      → ESP32 → Simultaneous X/Y Stepper Control → Gantry Motion → Target Reached
```

---

## Key Features

- Real-time object detection with YOLOv8
- Pixel-to-Cartesian coordinate transformation
- Simultaneous two-axis motor control (smooth diagonal motion, not sequential)
- **Dual-speed positioning** — 85% fast traversal + 15% precision slow-down, reducing overshoot while keeping speed high
- Fully autonomous vision-to-motion operation, no manual intervention

---

## Results

- Reliable real-time detection and stable serial communication between Python and ESP32
- Accurate pixel-to-Cartesian transformation, validated across the calibrated workspace
- Dual-speed control measurably reduced overshoot compared to constant-speed motion
- Fully autonomous end-to-end operation from detection to final positioning

---

## Hardware

| Component | Spec | Role |
|---|---|---|
| Camera | USB Webcam | Overhead workspace capture |
| Controller | ESP32 | Motion control + serial comms |
| Motors | NEMA17 (×2) | X/Y axis actuation |
| Driver | A4988 | Stepper control |
| Motion | TR8 lead screw, 2mm pitch | Rotary → linear conversion |
| Frame | Aluminium extrusion + linear rods | Structure & guidance |

**Steps/mm calculation:** `(200 steps × 8 microstepping) / 2mm pitch = 800 steps/mm`

---

## Repository Structure

```
vision-guided-cartesian-gantry/
├── python_code/
│   ├── detect_and_send.py
│   ├── best.pt
│   └── requirements.txt
├── esp32_firmware/
│   ├── gantry_controller.ino
│   └── calibration.h
├── assets/
│   ├── images/
│   └── demo/
├── docs/
│   └── technical-details.md
└── README.md
```

---

## Setup & Usage

```bash
pip install -r requirements.txt
```
1. Flash `esp32_firmware/gantry_controller.ino` via Arduino IDE
2. Set the correct COM port in `detect_and_send.py`
3. Run: `python python_code/detect_and_send.py`

---

## Limitations & Next Steps

**Current limitations:** fixed camera position, manual workspace calibration, open-loop motor control (no encoder feedback), single-object detection only.

**Planned improvements:** encoder feedback for closed-loop control, multi-object tracking, homography-based camera calibration, conveyor/QR integration for sorting applications.

---

## Full Technical Deep-Dive

For the complete write-up — detailed working principle, mechanical design rationale, coordinate transformation math, and motion planning pseudocode — see **[`docs/technical-details.md`](docs/technical-details.md)**.

---

## Author

**Muhammed Roshan S**
B.E. Robotics and Automation Engineering, PSG College of Technology

[![GitHub](https://img.shields.io/badge/GitHub-Muhammed--Roshan-181717?logo=github&logoColor=white)](https://github.com/Muhammed-Roshan)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Muhammed%20Roshan-0077B5?logo=linkedin&logoColor=white)](https://linkedin.com/in/muhammed-roshan-401a04288)
