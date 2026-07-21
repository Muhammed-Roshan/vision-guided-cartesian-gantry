# 🤖 Vision-Guided Cartesian Pick-and-Place Robot using YOLOv8 and ESP32

<p align="center">

<img src="assets/images/banner.png" width="1000">

</p>

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Object%20Detection-red)
![ESP32](https://img.shields.io/badge/ESP32-Microcontroller-green)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-orange)
![Arduino](https://img.shields.io/badge/Arduino-IDE-teal)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-lightgrey)
![License](https://img.shields.io/badge/License-MIT-blueviolet)

</p>

---

# 📌 Overview

Modern manufacturing increasingly relies on intelligent robotic systems capable of perceiving their environment and autonomously interacting with objects. Traditional pick-and-place systems often require expensive industrial vision sensors and precision controllers, making them unsuitable for educational institutions, research laboratories, and low-cost automation applications.

This project presents a **Vision-Guided Cartesian Pick-and-Place Robot** that combines **Deep Learning**, **Computer Vision**, **Embedded Motion Control**, and **Mechanical Design** into a unified automation platform.

The system uses a fixed overhead camera together with a **YOLOv8** object detection model to identify the position of an object in real time. The detected image coordinates are transformed into robot coordinates and transmitted to an **ESP32 microcontroller**, which controls a custom-built two-axis Cartesian gantry using NEMA17 stepper motors.

Unlike conventional demonstration projects, this system integrates every stage of an industrial automation pipeline:

- Object Detection
- Coordinate Transformation
- Motion Planning
- Embedded Motor Control
- Precision Positioning

The entire workflow operates autonomously without manual intervention, making the system suitable for intelligent material handling, laboratory automation, academic research, and industrial prototyping.

---

# 🎯 Project Objectives

The primary objective of this project is to design and implement a low-cost intelligent robotic system capable of autonomously locating and positioning itself over detected objects using computer vision.

The project aims to

- Detect objects in real time using YOLOv8
- Compute the centroid of the detected object
- Convert image coordinates into Cartesian robot coordinates
- Transmit coordinates to an ESP32 through serial communication
- Drive a two-axis Cartesian gantry with synchronized stepper motors
- Improve positioning accuracy using a dual-speed motion strategy
- Demonstrate the integration of Artificial Intelligence with Embedded Robotics

---

# 🚀 Key Features

✅ Custom-designed Cartesian Gantry Robot

✅ YOLOv8-based Real-Time Object Detection

✅ ESP32 Motion Controller

✅ OpenCV Image Processing

✅ Pixel-to-Cartesian Coordinate Transformation

✅ Dual-Speed Precision Motion Algorithm

✅ Simultaneous Two-Axis Motion Control

✅ Automatic Object Positioning

✅ Low-Cost Hardware Architecture

✅ Modular Software Design

---

# 🎥 Demonstration

<p align="center">

<img src="assets/demo/demo.gif" width="750">

</p>

> **Real-time object detection and autonomous Cartesian positioning using YOLOv8 and ESP32.**

---

# 🏗 System Architecture

```text
                 ┌────────────────────────┐
                 │    Overhead Camera     │
                 └────────────┬───────────┘
                              │
                              ▼
                     Live Image Capture
                              │
                              ▼
                 ┌────────────────────────┐
                 │     YOLOv8 Detector    │
                 └────────────┬───────────┘
                              │
                  Bounding Box Detection
                              │
                              ▼
                   Calculate Object Centre
                              │
                              ▼
              Pixel → Cartesian Transformation
                              │
                              ▼
                 Serial Communication (USB)
                              │
                              ▼
                      ESP32 Controller
                              │
                ┌─────────────┴──────────────┐
                ▼                            ▼
         X-axis Stepper               Y-axis Stepper
                │                            │
                └─────────────┬──────────────┘
                              ▼
                 Cartesian Gantry Motion
                              │
                              ▼
                   Object Position Reached
```

---

# ⚙ Working Principle

The complete system operates as a sequential perception-to-action pipeline.

### Step 1 — Image Acquisition

A fixed overhead USB camera continuously captures images of the workspace.

---

### Step 2 — Object Detection

Each captured frame is processed by a trained **YOLOv8** model.

The detector identifies

- Object Class
- Bounding Box
- Confidence Score
- Pixel Coordinates

The centre of the detected bounding box is calculated and selected as the target position.

---

### Step 3 — Coordinate Mapping

The image coordinates are converted into robot coordinates using a calibrated pixel-to-distance mapping.

This enables the robotic system to interpret image measurements as physical positions inside the workspace.

---

### Step 4 — Serial Communication

The calculated coordinates are transmitted to the ESP32 using high-speed serial communication operating at **115200 baud**.

Coordinate format:

```text
X,Y
```

Example:

```text
642,318
```

---

### Step 5 — Motion Planning

The ESP32 converts the received coordinates into motor steps using the calibrated motion constants.

Both axes move simultaneously while maintaining synchronization throughout the trajectory.

---

### Step 6 — Precision Positioning

Instead of moving at a constant speed, the robot follows a two-stage movement strategy.

- Fast movement for approximately 85% of the total travel distance.
- Slow movement for the remaining distance to improve positioning accuracy and reduce overshoot.

This significantly improves repeatability while maintaining high traversal speed.

---

### Step 7 — Final Position

Once both motors complete their movements, the end-effector reaches the detected object's location and is ready for subsequent operations such as

- Pick and Place
- Inspection
- Sorting
- Material Handling

---

# 🏗 Hardware Architecture

The proposed system consists of four major subsystems working together to achieve autonomous object localization and positioning.

```text
                    +-----------------------+
                    |   Overhead Camera     |
                    +-----------+-----------+
                                │
                                ▼
                   Computer Vision Processing
                                │
                                ▼
                      Python + YOLOv8 Model
                                │
                 Pixel Coordinates (X,Y)
                                │
                       USB Serial (115200)
                                │
                                ▼
                           ESP32 Controller
                                │
              +-----------------+-----------------+
              │                                   │
              ▼                                   ▼
        A4988 Driver                        A4988 Driver
              │                                   │
              ▼                                   ▼
       NEMA17 Stepper                     NEMA17 Stepper
          X-Axis                             Y-Axis
              │                                   │
              └──────────────┬────────────────────┘
                             ▼
                  Cartesian Gantry Mechanism
                             ▼
                     End-Effector Position
```

---

# 🔩 Hardware Components

| Component | Specification | Purpose |
|-----------|--------------|---------|
| Camera | USB Webcam | Captures live workspace images |
| Controller | ESP32 | Motion control and serial communication |
| Vision Model | YOLOv8 | Real-time object detection |
| X-axis Motor | NEMA17 Stepper | Horizontal movement |
| Y-axis Motor | NEMA17 Stepper | Vertical movement |
| Motor Driver | A4988 | Stepper motor control |
| Motion System | TR8 Lead Screw | Rotary to linear conversion |
| Guide Mechanism | Linear Rods | Stable linear movement |
| Frame | Aluminium Extrusion | Mechanical structure |

---

# ⚙ Mechanical Design

Unlike conventional robotic manipulators, this project employs a **Cartesian Gantry Architecture**.

The robot consists of two independent linear axes:

- X-axis for horizontal movement
- Y-axis for vertical movement

Each axis is driven using

- NEMA17 stepper motor
- TR8 lead screw
- Linear guide rods
- Sliding carriage

The use of lead screws enables precise conversion of rotary motion into linear displacement while maintaining high positional repeatability.

This configuration provides

- High positioning accuracy
- Simple kinematic model
- Low manufacturing cost
- Easy scalability

making it highly suitable for laboratory automation and industrial positioning applications.

---

# 📷 Computer Vision Module

Object localization is achieved using the **Ultralytics YOLOv8** object detection framework.

For every incoming camera frame

1. Image acquisition
2. Object detection
3. Bounding box extraction
4. Centroid calculation
5. Coordinate transmission

The centre of the detected bounding box is computed as

```
Center X = (x1 + x2) / 2

Center Y = (y1 + y2) / 2
```

These coordinates represent the target position of the robot.

The model performs inference in real time, enabling continuous object localization with minimal latency.

---

# 🎯 Coordinate Transformation

YOLOv8 outputs object locations in **pixel coordinates**.

However, the robotic system operates in **physical Cartesian coordinates**.

Therefore, a coordinate transformation stage converts image coordinates into robot coordinates before motion execution.

The mapping process consists of

```
Image Coordinates

        ↓

Workspace Calibration

        ↓

Pixel-to-Distance Conversion

        ↓

Robot Coordinates

        ↓

Motor Steps
```

This calibration allows the gantry to accurately reach the physical position corresponding to the detected object.

---

# 🔌 Serial Communication

The communication between the vision system and the robotic controller is established using USB Serial communication.

**Communication Parameters**

| Parameter | Value |
|----------|-------|
| Baud Rate | 115200 |
| Data Format | ASCII |
| Message | X,Y |

Example

```
685,312
```

The ESP32 continuously listens for incoming coordinate packets.

Whenever a valid coordinate pair is received, it immediately initiates the motion planning algorithm.

---

# ⚡ Motion Control Algorithm

The ESP32 converts image coordinates into motor commands.

Unlike traditional implementations where one motor moves after the other, this project performs **simultaneous two-axis movement**, allowing smooth diagonal trajectories.

The motion planning algorithm consists of

```
Receive Coordinates

        │

Convert to Steps

        │

Determine Direction

        │

Split Movement

        │

Fast Motion

        │

Slow Motion

        │

Target Position Reached
```

---

# 🚀 Dual-Speed Motion Strategy

One of the key contributions of this project is the implementation of a **two-stage positioning algorithm**.

Instead of moving at a constant speed throughout the trajectory, motion is divided into two phases.

## Phase 1 — Fast Traversal

Approximately **85%** of the required displacement is covered at high speed.

Advantages

- Reduced travel time
- Improved productivity

---

## Phase 2 — Precision Positioning

The remaining **15%** of the displacement is completed at a significantly lower speed.

Advantages

- Reduced overshoot
- Higher positioning accuracy
- Improved repeatability
- Stable stopping behaviour

This strategy provides an effective compromise between positioning speed and positioning precision.

---

# 🔄 Software Workflow

```text
Camera

   │

Capture Frame

   │

YOLOv8 Detection

   │

Bounding Box

   │

Centroid Calculation

   │

Coordinate Mapping

   │

Serial Communication

   │

ESP32

   │

Motion Planning

   │

Dual-Speed Control

   │

Stepper Motors

   │

Cartesian Motion

   │

Target Position
```

---

# 📂 Repository Structure

```
vision-guided-cartesian-robot/

│

├── python_code/
│   ├── detect_and_send.py
│   ├── best.pt
│   └── requirements.txt
│
├── esp32_firmware/
│   ├── gantry_controller.ino
│   └── calibration.h
│
├── assets/
│   ├── banner.png
│   ├── architecture.png
│   ├── demo.gif
│   └── images/
│
├── docs/
│   ├── project_report.pdf
│   └── algorithm.pdf
│
└── README.md
```

---

# 🧮 Motion Calculation

The mechanical system uses

- 200-step NEMA17 motors
- 1/8 microstepping
- TR8 lead screw with 2 mm pitch

Therefore

```
Steps/mm

=

(Motor Steps × Microstepping)

──────────────────────────────

Lead Screw Pitch

=

(200 × 8)

──────────

2

=

800 steps/mm
```

This conversion factor enables accurate translation from physical displacement into motor steps.

---

# 📊 Experimental Results

The developed system successfully demonstrates the integration of **computer vision**, **embedded motion control**, and **mechanical automation** into a unified robotic platform capable of autonomously detecting and positioning itself over target objects.

The experimental setup was evaluated using a fixed overhead camera, a custom-built Cartesian gantry, and an ESP32-based motion controller. Objects placed within the calibrated workspace were detected using a trained YOLOv8 model, and their centroid coordinates were translated into physical robot positions for autonomous movement.

The proposed system achieved:

- ✅ Reliable real-time object detection using YOLOv8
- ✅ Stable serial communication between Python and ESP32
- ✅ Accurate pixel-to-Cartesian coordinate transformation
- ✅ Smooth simultaneous X-Y axis movement
- ✅ Improved positioning using dual-speed motion control
- ✅ Fully autonomous vision-to-motion operation

---

# 📸 Project Demonstration

## Complete System

<p align="center">

<img src="assets/images/system_overview.jpg" width="850">

</p>

---

## YOLOv8 Detection

<p align="center">

<img src="assets/images/object_detection.png" width="700">

</p>

The vision system continuously detects objects inside the workspace and computes their centroid coordinates. These coordinates are transmitted to the ESP32 controller through serial communication for motion execution.

---

## Cartesian Gantry

<p align="center">

<img src="assets/images/gantry_robot.jpg" width="700">

</p>

The custom-designed two-axis Cartesian mechanism converts rotational motion from the stepper motors into accurate linear displacement using TR8 lead screws and linear guide rails.

---

## Motion Execution

<p align="center">

<img src="assets/images/motion.png" width="700">

</p>

After receiving the target coordinates, the robot autonomously moves to the detected object location using synchronized motion of both axes.

---

# 🎬 Demonstration Video

<p align="center">

<img src="assets/demo/demo.gif" width="850">

</p>

The animation demonstrates the complete perception-to-action pipeline.

1. Image Capture
2. YOLOv8 Detection
3. Coordinate Calculation
4. Coordinate Transmission
5. Motion Planning
6. Cartesian Positioning

---

# 📈 Performance Highlights

| Parameter | Performance |
|-----------|------------|
| Object Detection | Real-Time |
| Detection Model | YOLOv8 |
| Motion Controller | ESP32 |
| Motion Type | Simultaneous X-Y |
| Positioning Strategy | Dual-Speed |
| Coordinate Transfer | Serial Communication |
| Motion Accuracy | Pixel-Calibrated |
| Control Method | Vision-Guided |

---

# 💡 Engineering Contributions

Unlike many educational demonstrations where object detection and robot control are treated as separate modules, this project integrates the complete automation pipeline into a single intelligent robotic system.

The project combines expertise in multiple engineering domains.

### 🤖 Artificial Intelligence

- YOLOv8 Deep Learning Model
- Object Localization
- Real-Time Detection

---

### 👁 Computer Vision

- Image Processing
- Bounding Box Extraction
- Centroid Computation
- Coordinate Transformation

---

### ⚡ Embedded Systems

- ESP32 Programming
- Serial Communication
- Real-Time Motion Control

---

### ⚙ Robotics

- Cartesian Kinematics
- Stepper Motor Synchronization
- Motion Planning
- Precision Positioning

---

### 🔩 Mechanical Design

- Custom Aluminium Frame
- Lead Screw Transmission
- Linear Motion Design
- Two-Axis Gantry

---

# 🏭 Applications

The developed robotic platform can be adapted for numerous industrial and research applications.

### Industrial Automation

- Automated Pick-and-Place
- Material Handling
- Assembly Assistance
- Small Component Positioning

---

### Smart Manufacturing

- Intelligent Sorting
- Packaging Systems
- Conveyor Automation
- Quality Inspection

---

### Research

- Robotics Laboratories
- AI-Based Manipulation
- Vision-Based Motion Planning
- Embedded Robotics

---

### Education

- Robotics Projects
- Embedded Systems
- Computer Vision
- Motion Control

---

# ⚠ Current Limitations

Although the proposed system successfully demonstrates autonomous positioning, several limitations remain.

- Fixed overhead camera configuration
- Manual workspace calibration
- Open-loop motor control
- Single-camera localization
- Limited workspace dimensions
- Single-object positioning

These limitations provide opportunities for future improvements.

---

# 🚀 Future Improvements

The project can be extended in several directions.

### Robotics

- Three-axis Cartesian Robot
- Automatic Homing
- Limit Switch Integration
- Closed-Loop Servo Control
- Encoder Feedback

---

### Computer Vision

- Multi-Object Tracking
- Instance Segmentation
- Depth Estimation
- Camera Calibration
- Homography-Based Mapping

---

### Artificial Intelligence

- Object Classification
- Reinforcement Learning
- Vision-Based Grasp Planning
- Automatic Path Optimization

---

### Industrial Automation

- Conveyor Belt Integration
- Automatic Sorting
- Barcode Detection
- QR Code Tracking
- PLC Integration

---

# 📚 Technologies Used

| Category | Technologies |
|-----------|-------------|
| Programming | Python, Embedded C++ |
| AI Framework | Ultralytics YOLOv8 |
| Computer Vision | OpenCV |
| Embedded Platform | ESP32 |
| IDE | Arduino IDE |
| Communication | Serial UART |
| Motion Control | Stepper Motors |
| CAD | SolidWorks |
| Mechanical System | Cartesian Gantry |

---

# 📖 References

1. Ultralytics YOLOv8 Documentation

2. OpenCV Documentation

3. ESP32 Technical Reference Manual

4. Arduino Documentation

5. Redmon J. et al., *You Only Look Once: Unified, Real-Time Object Detection*

6. Robotics and Automation literature on Cartesian Manipulators

---

# 🙏 Acknowledgement

This project was developed as part of the **B.E. Robotics and Automation Engineering** curriculum at **PSG College of Technology**.

The work represents an interdisciplinary integration of **Artificial Intelligence**, **Computer Vision**, **Embedded Systems**, **Mechanical Design**, and **Industrial Automation** into a unified robotic system.

---

# 👨‍💻 Author

## Muhammed Roshan S

**B.E. Robotics and Automation Engineering**

PSG College of Technology

### Areas of Interest

- Autonomous Mobile Robots
- Industrial Automation
- Computer Vision
- Robot System Integration
- Motion Planning
- Embedded Systems
- ROS 2
- Artificial Intelligence

---

## 📬 Connect with Me

<p align="left">

<a href="https://github.com/Muhammed-Roshan">
<img src="https://img.shields.io/badge/GitHub-Muhammed--Roshan-181717?style=for-the-badge&logo=github">
</a>

<a href="https://linkedin.com/in/muhammed-roshan-401a04288">
<img src="https://img.shields.io/badge/LinkedIn-Muhammed%20Roshan-0077B5?style=for-the-badge&logo=linkedin">
</a>

</p>

---

# ⭐ Support

If you found this project interesting, consider giving the repository a ⭐.

Contributions, suggestions, and discussions are always welcome.

---
