# ORBITA: AI-Enabled Smart Organ Transport System

An open-source, low-cost intelligent retrofit module for conventional organ preservation and transport boxes. Powered by an **ESP32 microcontroller**, multi-sensor IoT telemetry (Temperature, Humidity, Kinematic Shock, GPS, Lid-open tampering, and Battery SoC), active thermoelectric cooling (Peltier), and a mathematically formulated **Transport Risk Index (TRI)**.

---

## 🌐 Live GitHub Pages Demo
The project page and interactive simulator are hosted at:  
👉 **`https://aaron0745.github.io/ORBITA_Methodology/`**

---

## 📌 Project Overview
Organ transplantation requires continuous preservation within a narrow hypothermic window ($2^\circ\text{C} - 8^\circ\text{C}$, ideally $4^\circ\text{C}$). In many healthcare systems, including India, passive iceboxes lack real-time observability, dynamic temperature regulation, and predictive degradation alerting, while commercial machine perfusion systems are prohibitively expensive ($40,000–$80,000+).

**ORBITA** bridges this gap as a retrofit system costing under **₹8,000 (~$95 USD)**.

---

## 🛠️ Hardware Bill of Materials (BOM)

| Component | Specification | Technical Purpose | Approx Cost (INR) |
|---|---|---|---|
| **Microcontroller** | ESP32 DevKit V1 (30-pin) | Dual-core processing, FreeRTOS, sensor fusion | ₹450 |
| **Internal Temp Sensors** | 2x DS18B20 (Waterproof) | Dual redundant core temperature measurement | ₹300 |
| **Ambient Temp & Humidity** | SHT31 / DHT22 (AM2302) | Chamber humidity and ambient baseline | ₹350 |
| **Shock & Kinematics** | MPU-6050 (6-DOF IMU) | Detecting transit shocks (>2.0g) and RMS vibration | ₹180 |
| **Location & Velocity** | NEO-6M / NEO-8M GPS | Real-time transit coordinates & speed | ₹600 |
| **Lid / Tamper Sensor** | Magnetic Reed Switch | Continuous lid-closure and seal monitoring | ₹80 |
| **Power Telemetry** | INA219 I2C Sensor | Battery voltage, current, and SoC monitoring | ₹200 |
| **Active Cooling** | TEC1-12706 Peltier + Heatsink | Chamber temperature stabilization | ₹1,100 |
| **Actuator Driver** | IRF520 MOSFET / 10A Relay | PWM duty-cycle control for cooling | ₹120 |
| **Cellular Uplink** | A7672S / SIM7600 4G LTE | Highway telemetry streaming without Wi-Fi | ₹1,900 |
| **Battery Power** | 12V 3S Li-ion (with BMS) + Buck | 6–10 hour portable operation | ₹1,800 |
| **Display & Chassis** | 0.96" OLED + Insulated Box | Local status readouts and chassis | ₹700 |
| **Total Prototype Cost** | | | **~₹7,850 (~$95)** |

---

## 📐 Transport Risk Index (TRI) Model

The **Transport Risk Index (TRI)** is calculated continuously as a composite score:

$$TRI(t) = \min\Big(100, \; 0.40 \cdot S_{temp}(t) + 0.30 \cdot S_{time}(t) + 0.15 \cdot S_{shock}(t) + 0.15 \cdot S_{lid}(t)\Big)$$

- **$S_{temp}(t)$**: Thermal penalty combining instantaneous piecewise deviation from $[2^\circ\text{C}, 6^\circ\text{C}]$ and cumulative degree-hour thermal debt.
- **$S_{time}(t) = 100 \times (t / CIT_{max})^2$**: Quadratic exhaustion of cellular viability against organ Cold Ischemia Time limits (Heart: 6h, Liver: 12h, Kidney: 30h).
- **$S_{shock}(t)$**: Accumulated impact forces exceeding $2.0g$.
- **$S_{lid}(t)$**: Cumulative penalty for unauthorized lid openings and ambient air breaches.

---

## 🚀 How to Enable GitHub Pages
1. Push this repository to GitHub on branch `main`.
2. Go to **Settings** > **Pages** in the repository.
3. Under **Build and deployment > Source**, select **Deploy from a branch**.
4. Choose Branch: **`main`** and Folder: **`/ (root)`**, then click **Save**.
5. Your webpage will be live in 1–2 minutes!
