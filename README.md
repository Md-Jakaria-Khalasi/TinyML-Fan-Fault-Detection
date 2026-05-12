# TinyML-Powered Framework for Predictive Maintenance of Rotating Machinery

<div align="center">
  <h3>Real-Time Fault Detection on Edge Devices using ESP32 & MPU6050</h3>
</div>

---

## 📌 Overview
This repository contains the complete source code, dataset samples, and deployment configuration for an intelligent, low-cost **Predictive Maintenance** system powered by **Tiny Machine Learning (TinyML)**. 

While the initial implementation utilizes a **Ceiling Fan** as a practical case study to validate the approach, the underlying framework is highly versatile. It is designed to be adapted for any rotating machinery—such as industrial AC motors, water pumps, or cooling fans—simply by collecting domain-specific vibration signatures and retraining the edge model.

## 🚀 Key Features
* **Edge Computing:** All sensor data processing and AI inference run locally on the **ESP32** microcontroller, eliminating the need for continuous cloud connectivity and ensuring zero latency.
* **Micro-Vibration Sensitivity:** Leverages the **MPU6050** MEMS accelerometer to capture intricate tri-axial vibration patterns.
* **Ultra-Low Resource Footprint:** Highly optimized for resource-constrained edge microcontrollers:
  * **Peak RAM Usage:** ~1.2 KB
  * **Flash Usage:** ~8.6 KB
* **High Reliability:** Achieved **100% classification accuracy** in differentiating between *Normal* operating states and *Faulty* (imbalanced/loose mounting) anomalies during test bench validation.

---

## 🛠️ Hardware Architecture & Pinout

### Required Components:
1. **Microcontroller:** ESP32 Development Board (or Arduino Uno)
2. **Sensor:** MPU6050 (6-axis MotionTracking device: 3-axis Accelerometer + 3-axis Gyroscope)
3. **Actuator/Alert:** Buzzer or LED for localized real-time fault alerts
4. **Subject:** Ceiling Fan / Portable Turbo Fan (for testing setup)

### ESP32 to MPU6050 Wiring Diagram:
| MPU6050 Pin | ESP32 GPIO | Function |
| :--- | :--- | :--- |
| **VCC** | `3.3V` | Power Supply |
| **GND** | `GND` | Common Ground |
| **SCL** | `GPIO 22` | I2C Clock Line |
| **SDA** | `GPIO 21` | I2C Data Line |

---

## 📂 Repository Structure

```text
├── Data_Collection_Code/
│   └── mpu6050_data_logger.ino   # Streams raw X, Y, Z accelerometer data to Serial
├── Deployment_Code/
│   └── tinyml_fault_detector.ino # Main inference code integrating the Edge Impulse model
├── Library/
│   └── ei-model-library.zip      # Pre-trained Edge Impulse C++ library ready for Arduino IDE
├── Dataset_Sample/
│   ├── normal_vibration.csv      # Sample dataset for stable operation
│   └── faulty_vibration.csv      # Sample dataset for induced mechanical imbalance
└── README.md                     # Comprehensive project documentation

```
# 📊 Dataset & Model Training

This TinyML-based fault detection system utilizes raw tri-axial accelerometer vibration data collected from multiple operational conditions of ceiling fans and rotating motors. The dataset is publicly available on Kaggle to support reproducibility, benchmarking, and future academic research.

👉 **Access the Full Kaggle Dataset:** *Fan Vibration Data for MPU6050*

## 🧠 TinyML Pipeline Configuration

- **Sampling Frequency:** 200 Hz  
- **Window Size:** 1000 ms (2 seconds per inference cycle)  
- **Window Increase:** 500 ms  
- **Digital Signal Processing (DSP):** Spectral Analysis using Fast Fourier Transform (FFT) for extracting frequency-domain features and spectral power distributions  
- **Model Architecture:** Fully Connected Dense Neural Network built using TensorFlow/Keras and deployed with TensorFlow Lite for Microcontrollers (TFLite Micro)

---

# ⚙️ Quick Start Guide

## Step 1: Data Collection (Optional for Custom Retraining)

1. Flash the code from the `/Data_Collection_Code/` directory to your ESP32 board.
2. Securely mount the MPU6050 sensor onto the target motor or ceiling fan chassis.
3. Use the **Edge Impulse Data Forwarder** or **Arduino Serial Monitor** to collect and export vibration data as `.csv` files.

---

## Step 2: Library Installation

1. Download the pre-trained model `.zip` library from the `/Library/` directory.
2. Open **Arduino IDE** → `Sketch` → `Include Library` → `Add .ZIP Library...`
3. Select the downloaded library file.

---

## Step 3: Deployment

1. Open the `/Deployment_Code/tinyml_fault_detector.ino` sketch in Arduino IDE.
2. Ensure the ESP32 board package is properly installed.
3. Compile and upload the code to the ESP32.
4. Open the **Serial Monitor** and set the baud rate to **115200**.
5. Real-time inference results and anomaly detection scores will now be displayed.

---

# 🔄 Transferability & Future Scope

The proposed TinyML pipeline is designed as a scalable and transferable framework for intelligent motor condition monitoring applications.

## 🏭 Industrial Scalability

By adjusting accelerometer sensitivity ranges (e.g., ±2g to ±16g), the same architecture can be adapted for:

- HVAC systems
- Industrial conveyor motors
- Water pumps
- Manufacturing equipment
- Rotary machinery fault diagnostics

## 🌐 IoT Expansion

Future development aims to integrate:

- **ESP-NOW-based mesh communication**
- Wireless multi-node monitoring
- Centralized real-time monitoring dashboard
- Edge-to-cloud predictive maintenance infrastructure

---

# 👨‍💻 Authors & Contributors

- **Md. Jakaria Khalasi** — Department of Computer Science & Engineering, BUBT 

---

# 📜 License

This project is licensed under the **MIT License**.

You are free to use, modify, distribute, and integrate this framework into academic, research, or commercial applications with proper attribution.
