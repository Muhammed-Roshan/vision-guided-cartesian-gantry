# 🤖 Vision-Guided Cartesian Pick-and-Place Robot using YOLOv8


<p align="center">

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Object%20Detection-red)
![ESP32](https://img.shields.io/badge/ESP32-Microcontroller-green)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-orange)
![Arduino](https://img.shields.io/badge/Arduino-IDE-teal)

</p>

---

## 📌 Overview

This project presents a **vision-guided Cartesian robotic system** that autonomously detects objects using **YOLOv8** and positions a custom-built **2-axis Cartesian gantry** over the detected object.

A fixed overhead camera captures the workspace, YOLOv8 identifies the object's centroid, and the coordinates are transmitted to an **ESP32**. The controller converts the received coordinates into motor steps and simultaneously drives two NEMA17 stepper motors to accurately position the end-effector.

The project demonstrates the integration of **Computer Vision**, **Embedded Systems**, **Motion Control**, and **Mechanical Design** into a complete robotic automation system.

---

## 🚀 Key Features

- Real-time object detection using **YOLOv8**
- Custom-built **2-axis Cartesian gantry**
- ESP32-based motion controller
- Simultaneous X-Y motion control
- Pixel-to-Cartesian coordinate mapping
- Dual-speed positioning algorithm for improved accuracy
- Modular hardware and software architecture

---

## ⚙️ System Workflow

```text
Camera
   │
   ▼
YOLOv8 Detection
   │
   ▼
Object Centroid
   │
   ▼
Coordinate Mapping
   │
   ▼
Serial Communication
   │
   ▼
ESP32 Controller
   │
   ▼
Cartesian Gantry Motion
   │
   ▼
Target Position Reached
```

---

## 🏗️ System Architecture

```text
Overhead Camera
       │
       ▼
Python + YOLOv8
       │
Serial Communication
       │
       ▼
ESP32 Controller
       │
 ┌─────┴─────┐
 ▼           ▼
X Stepper   Y Stepper
       │
       ▼
Cartesian Gantry
```

---

## 🛠️ Hardware

| Component | Specification |
|-----------|--------------|
| Controller | ESP32 |
| Vision System | USB Camera |
| Detection Model | YOLOv8 |
| Motors | 2 × NEMA17 Stepper Motors |
| Drivers | A4988 |
| Motion System | TR8 Lead Screw |
| Frame | Aluminium Extrusion |

---

## 💻 Software Stack

- Python
- YOLOv8 (Ultralytics)
- OpenCV
- Arduino IDE
- ESP32 Firmware
- Serial Communication

---

## 📈 Highlights

- Designed and fabricated a custom Cartesian gantry mechanism
- Implemented real-time vision-guided positioning
- Developed a dual-speed motion algorithm for improved positioning accuracy
- Integrated AI, embedded systems, and motion control into a single automation platform

---

## 🚀 Future Improvements

- Automatic pick-and-place using a robotic gripper
- Multi-object detection and sorting
- Closed-loop position feedback using encoders
- Camera calibration using homography
- Conveyor-based industrial automation

---

## 👨‍💻 Author

**Muhammed Roshan S**

B.E. Robotics and Automation Engineering

PSG College of Technology

📧 LinkedIn: https://www.linkedin.com/in/muhammed-roshan-s-401a04288
💻 GitHub: https://github.com/Muhammed-Roshan
