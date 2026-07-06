# Vision-Guided Cartesian Gantry Robot for Object Detection and Positioning

> A low-cost vision-guided robotic system that integrates **YOLOv8**, **ESP32**, and a **custom-built two-axis Cartesian gantry** to automatically detect objects and move the end-effector to their corresponding positions.

<p align="center">
  <img src="assets/images/banner.png" width="900">
</p>

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![YOLOv8](https://img.shields.io/badge/YOLO-v8-red)
![ESP32](https://img.shields.io/badge/ESP32-Microcontroller-green)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-orange)
![Arduino](https://img.shields.io/badge/Arduino-IDE-teal)
![License](https://img.shields.io/badge/License-MIT-purple)

</p>

---

## Overview

This project presents a **vision-guided Cartesian robotic system** capable of detecting objects using **YOLOv8**, estimating their positions from an overhead camera, converting image coordinates into robot coordinates, and commanding an ESP32-controlled XY gantry to move toward the detected object.

The system combines **computer vision**, **embedded systems**, and **precision motion control** into a single autonomous robotic platform suitable for academic research, industrial automation, and intelligent manufacturing applications.
