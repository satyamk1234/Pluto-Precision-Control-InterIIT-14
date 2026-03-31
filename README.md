# Precision Motion & Stabilization System | Inter IIT Tech Meet 14.0

This repository contains the firmware implementation for a robust, production-grade control system designed for indoor nano-drones. Developed for the **Inter IIT Tech Meet 14.0** challenge hosted by **Drona Aviation**, the system enables autonomous takeoff, stable position-locking, and discrete 10-20 cm micro-movements triggered by user commands.

## Project Overview
Indoor nano-drones operate under strict sensing and compute constraints. Without GPS or external tracking, stability depends on how effectively the firmware interprets onboard sensors and closes the loop in real time. This project delivers a fused control pipeline capable of maintaining a steady hover and executing precise, repeatable displacements.

### **Key Features**
* **Autonomous Hover:** Independent stabilization and altitude hold (up to 2 meters) immediately after takeoff without pilot input.
* **Precision Micro-Movements:** Stick inputs (Pitch/Roll/Throttle) translate into discrete 10-20 cm movements rather than continuous velocity.
* **Centimeter-Level Accuracy:** Designed to stop at commanded displacements with a $\pm2$ cm tolerance and no overshoot.
* **Disturbance Recovery:** Robust logic to resist and recover from external physical disturbances such as pushes or pulls.

## Technical Architecture

### **1. Cascaded Control Loop**
The system utilizes a **Position-Velocity-Attitude (PVA)** cascaded architecture:
* **Position Loop:** Maintains the X-Y-Z coordinates and locks position during hover.
* **Velocity Loop:** Converts optical-flow pixel shifts into real-world motion for drift minimization.
* **Attitude Loop:** Manages the drone's orientation based on high-frequency IMU updates.

### **2. Sensor Fusion Strategy**
To maintain a consistent state estimate, the firmware fuses four primary data sources:
* **Optical Flow:** Provides horizontal velocity estimation, adjusted for yaw changes.
* **Time-of-Flight (ToF):** Delivers real-time altitude data to scale optical flow and maintain height.
* **IMU:** Tracks orientation and filters micro-vibrations caused by motors.
* **Barometer:** Used in conjunction with ToF for stable altitude control.

### **3. Motion Profiling**
Each micro-movement follows a smooth motion profile with controlled acceleration and deceleration to minimize jerk. Small, accidental stick noise is rejected to ensure only intentional inputs trigger motion.

## Deliverables
* **Firmware:** Complete modular codebase running within the **MagisV2** environment.
* **Documentation:** Detailed PID tuning approach, sensor fusion strategy, and performance results.
* **Validation:** Demonstrated stability across varied textures, lighting conditions, and altitudes.

---
Developed for the Inter IIT Tech Meet 14.0 Low-Prep challenge.
**Problem Statement Provider:** Drona Aviation Pvt. Ltd.
