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

---

## How It Works

This is a closed-loop vision-to-motion pipeline: a webcam feed is analyzed in real time to find a target object, and its position is translated into precise stepper motor movement on a 2-axis gantry.

**1. Detection (Python + YOLOv8)**
A webcam feed is passed frame-by-frame through a trained YOLOv8 model (`best.pt`). When an object is detected, the bounding box center — the target's `(x, y)` pixel coordinates — is calculated and streamed to the microcontroller over serial at 115200 baud, as a `"X,Y\n"` string.

**2. Motion Control (Arduino/ESP32)**
The controller parses the incoming coordinates and converts them into stepper motor steps using a calibration factor (`stepsPerPixel`). Each axis moves in **two phases** for both speed and accuracy:
- **Fast phase** — 85% of the distance, covered quickly
- **Slow phase** — final 15%, covered at reduced speed for precise final positioning

Both stepper motors (X and Y) are driven simultaneously and independently via step/direction pins, so diagonal moves happen smoothly rather than one axis at a time.

**3. Result**
The end-effector arrives at the detected object's position — enabling applications like automated pick-and-place, inspection, or object-following without any manual joystick input.

<details>
<summary><b>Full technical breakdown (click to expand)</b></summary>

### Python — Detection & Serial Communication
- `serial`: handles the serial link to the microcontroller
- `cv2`: captures and displays the live camera feed
- `ultralytics.YOLO`: loads and runs the trained detection model
- Each frame is run through the model; if a detection exists, the bounding box center is computed as `((x1+x2)/2, (y1+y2)/2)` and sent as `int,int\n`
- Live detection is displayed via `cv2.imshow`; the loop exits on pressing `q`

### Motor Control
- Separate direction, step, and enable pins are defined for the X and Y stepper motors
- Incoming serial data is buffered character-by-character; a newline marks a complete coordinate pair
- The received `X,Y` values are converted to step counts via `stepsPerPixel`
- Movement is split into the fast (85%) and slow (15%) phases described above, with direction set based on the sign of the target
- Both axes are pulsed in parallel until each has completed its required steps

### Why the two-phase movement matters
Moving at full speed the whole distance risks overshoot and lost steps near the target. Moving slowly the whole distance is accurate but slow. The 85/15 split gets the best of both — quick traversal, precise arrival.

</details>

---

## Project Structure

```
vision-guided-cartesian-gantry/
├── python_code/         # YOLOv8 detection + serial communication script
├── arduino_code/        # Motor control firmware (ESP32/Arduino)
├── assets/
│   ├── images/          # Banner, wiring diagram, detection screenshots
│   └── demo.gif          # Demo of the system in action
└── README.md
```

---

## Hardware Used

| Component | Role |
|---|---|
| ESP32 / Arduino | Motor control, serial communication with PC |
| Stepper motors (x2) | X-axis and Y-axis actuation |
| Stepper drivers | Step/direction control per axis |
| Webcam | Overhead object detection feed |
| Custom XY gantry frame | Physical positioning mechanism |

**Pin mapping (as configured in firmware):**

| Signal | X-axis | Y-axis |
|---|---|---|
| Direction | Pin 2 | Pin 4 |
| Step | Pin 3 | Pin 5 |
| Enable | Pin 6 | Pin 7 |

---

## Setup & Usage

**1. Install Python dependencies**
```bash
pip install ultralytics opencv-python pyserial
```

**2. Flash the firmware**
- Open the file in `arduino_code/` using Arduino IDE
- Select your board (ESP32/Arduino) and correct COM port
- Upload

**3. Update the serial port in the Python script**
- Open `python_code/`, set `COM_PORT` to match your system (e.g. `COM3` on Windows, `/dev/ttyUSB0` on Linux)

**4. Run detection**
```bash
python detect_and_send.py
```
A live camera window will open. Press `q` to exit.

---

## Demo

<p align="center">
  <img src="assets/images/demo.gif" width="700">
</p>

*(Replace with your actual demo GIF/image once uploaded — see note below.)*

---

## Results & Limitations

- Successfully detects and positions the end-effector over target objects in real time using a single overhead camera
- Two-phase motion (fast + slow) reduces overshoot compared to constant-speed movement
- Current limitations: `stepsPerPixel` calibration is manual and camera-position-dependent; system assumes a single dominant object per frame

**Possible improvements:** closed-loop position feedback (encoders), multi-object handling with priority selection, camera-to-robot coordinate calibration via homography instead of a fixed scale factor.

---

## Author

**Muhammed Roshan S**
B.E. Robotics and Automation Engineering, PSG College of Technology
[LinkedIn](https://linkedin.com/in/muhammed-roshan-401a04288) · [GitHub](https://github.com/Muhammed-Roshan)