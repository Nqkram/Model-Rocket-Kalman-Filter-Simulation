# 🚀 Model Rocket Telemetry System with Kalman Filter

## Overview

This project demonstrates a **model rocket telemetry and state estimation system** implemented on a **Teensy 4.1** microcontroller.
Sensor measurements are processed using a **Kalman filter** to reduce noise and produce stable estimates of the rocket’s flight state.

The system simulates a rocket flight up to **Max altitude: 5357 m**, fuses measurements from multiple sensors, and displays the processed data on an **I2C LCD display** while also providing telemetry through the serial monitor.

The project focuses on **state estimation, sensor fusion, and embedded flight computation**.

---

# System Architecture

The system estimates the rocket's state using a **6-DOF state vector**:

```
x = [ altitude, vertical_velocity, vertical_acceleration, roll, pitch, yaw ]
```

The Kalman filter processes measurements from simulated sensors and continuously updates the rocket's estimated state.

### Matrix Dimensions

| Matrix                 | Size  | Description            |
| ---------------------- | ----- | ---------------------- |
| State Vector (x)       | 6 × 1 | Rocket flight state    |
| State Transition (F)   | 6 × 6 | System dynamics        |
| Process Noise (Q)      | 6 × 6 | Model uncertainty      |
| Measurement Matrix (H) | 4 × 6 | Sensor mapping         |
| Measurement Noise (R)  | 4 × 4 | Sensor noise           |
| Covariance (P)         | 6 × 6 | Estimation uncertainty |
| Kalman Gain (K)        | 6 × 4 | Filter gain            |

---

# Hardware

The system is designed to run on:

* **Teensy 4.1**
* **I2C LCD Display (16x2, address 0x27)**

Libraries used:

```
Arduino
Wire
LiquidCrystal_I2C
math
```

---

# Flight Simulation

The code simulates realistic rocket flight physics including:

* Rocket thrust
* Mass change due to fuel burn
* Atmospheric pressure model
* Drag force
* Gravity

Key parameters:

| Parameter        | Value  |
| ---------------- | ------ |
| Rocket thrust    | 1800 N |
| Rocket mass      | 12 kg  |
| Fuel mass        | 5 kg   |
| Burn time        | 3.5 s  |
| Drag coefficient | 0.45   |
| Simulation step  | 0.05 s |

---

# Features

* Full **Kalman Filter implementation**
* **6-DOF state estimation**
* **Sensor fusion (dual pressure sensors + accelerometers)**
* **Real-time LCD data output**
* **Serial telemetry interface**
* Microsecond-level **processing time measurement**

---

# Serial Commands

Use the **Arduino Serial Monitor (115200 baud)**.

| Command | Function                    |
| ------- | --------------------------- |
| start   | Start simulation            |
| step    | Advance one simulation step |
| run N   | Run N steps automatically   |
| reset   | Reset system                |
| status  | Show current state          |
| help    | Show command list           |

Example:

```
run 100
```

Runs 100 simulation steps.

---

# LCD Output

The LCD displays filtered flight telemetry including:

* Estimated altitude
* Velocity
* Acceleration
* Orientation values

The display is updated in real time during the simulation.

---

# Mathematical Approach

The project uses a **discrete Kalman filter** to estimate the rocket state:

Prediction:

```
x = F·x
P = F·P·Fᵀ + Q
```

Update:

```
K = P·Hᵀ (H·P·Hᵀ + R)⁻¹
x = x + K(z − Hx)
P = (I − KH)P
```

This approach reduces sensor noise and provides smoother telemetry.

---

# Purpose of the Project

This project demonstrates:

* Embedded **state estimation**
* **Kalman filtering in aerospace systems**
* **sensor fusion techniques**
* real-time **flight telemetry processing**

It can serve as a **foundation for model rocket avionics systems**.

---

# Future Improvements

Possible extensions:

* Real sensor integration (BMP280, MPU6050)
* LoRa telemetry transmission
* SD card flight logging
* Ground station visualization
* Flight computer integration

---
