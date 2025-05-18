# 🔐 IoT Student Fingerprint Access Control System

A smart, low-cost biometric access system built with **ESP32**, **AS608 fingerprint sensor**, and **0.96" OLED display**. The system grants or denies access based on fingerprint recognition and logs access attempts to a **local server**, viewable via a **web dashboard**.

---

## 📸 Overview

This project is ideal for school environments, labs, or restricted facilities where only registered users (students) should be allowed entry. Each student registers their fingerprint, and future access is authenticated locally and logged remotely.

---

## 📦 Components

| Component                | Quantity | Description                                 |
|--------------------------|----------|---------------------------------------------|
| ESP32 Dev Board          | 1        | Wi-Fi-enabled microcontroller               |
| AS608 Fingerprint Sensor | 1        | Captures and stores student fingerprints    |
| OLED Display (0.96")     | 1        | Displays access messages                    |
| Local Server             | 1        | Receives access logs (Node.js, PHP, etc.)   |
| Web Dashboard            | 1        | Displays user access logs and stats         |
| Breadboard & Jumpers     | As needed| For prototyping connections                 |

---

## ✨ Features

- 🔐 **Fingerprint-based access control**
- 📟 **Real-time OLED display feedback**
- 🌐 **Wi-Fi-enabled local server communication**
- 🖥️ **Web dashboard** to monitor access logs
- 🗃️ **Fingerprint storage** on AS608 module
- 📅 **Timestamps for each access attempt**

---

## 🔌 Circuit Connections

| Module                  | ESP32 Pin |
|-------------------------|-----------|
| AS608 TX                | GPIO16 (RX2) |
| AS608 RX                | GPIO17 (TX2) |
| AS608 VCC               | 3.3V or 5V |
| AS608 GND               | GND       |
| OLED SDA                | GPIO21    |
| OLED SCL                | GPIO22    |

---

## 🧰 Required Libraries

Install these via Arduino Library Manager:

- `Adafruit_Fingerprint`
- `Adafruit_GFX`
- `Adafruit_SSD1306`
- `WiFi`
- `HTTPClient`

---

## 📲 How It Works

1. **Enrollment Mode**: Admin registers each student's fingerprint to the AS608 sensor's internal memory.
2. **Authentication Mode**: Students place their finger on the scanner.
3. **Access Check**:
   - If the fingerprint is recognized:
     - "Access Granted" is shown on the OLED.
     - Data is sent to the local server.
   - If unrecognized:
     - "Access Denied" is shown.
     - Attempt is still logged.
4. **Logging**:
   - The ESP32 sends a POST request with `user_id`, `status`, and `timestamp` to the server.

---

## 🌐 API Request Format

The ESP32 sends the following JSON payload to your backend:

```json
{
  "user_id": 3,
  "name": "Jane Doe",
  "status": "Access Granted",
  "timestamp": "2025-05-18T14:22:33"
}
