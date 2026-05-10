# 🏥 IoT-Based Health Risk Prediction System Using Machine Learning with Web-Enabled Alerts

A real-time patient health monitoring system that integrates **IoT sensors**, **Machine Learning**, and a **Flask web application** to predict health risk levels and automatically alert the nearest hospital during critical conditions.

> 🎓 Final Year Project — B.Tech in Electronics and Communication Engineering  
> Gayatri Vidya Parishad College of Engineering for Women, Visakhapatnam (2022–2026)  
> **Guide:** Mrs. Ch. Sirisha, Assistant Professor

---

## 📌 Abstract

A predictive healthcare framework developed by integrating **IoT-enabled sensors** with **Machine Learning** for real-time risk assessment. Patient vital parameters — Temperature, SpO₂, Heart Rate, and Blood Pressure — are collected using an **Arduino-based system** and transmitted to a **Flask REST API**, where **Logistic Regression models** predict the patient's risk level. When a critical condition is detected, the system automatically locates the nearest hospital using the **Browser Geolocation API** and **Overpass API (OpenStreetMap)** and sends an emergency alert with ambulance dispatch request.

---

## ✨ Features

- 📡 Real-time monitoring of patient vitals via IoT sensors
- 🤖 ML-based risk classification — **No Alert / Medium Alert / High Alert**
- 🌐 Patient and Hospital web dashboards
- 📍 Automatic nearest hospital identification using OpenStreetMap
- 🚑 Emergency alert and ambulance dispatch for high-risk cases
- 💾 Patient data stored in CSV for records and future analysis

---

## 🧠 System Architecture

```
IoT Sensors (Arduino Uno)
    │
    ▼ Serial Communication (PySerial)
Flask Backend (app.py)
    │
    ├── Logistic Regression Models (.pkl)
    │       ├── Heart Rate Model
    │       ├── SpO₂ Model
    │       ├── Blood Pressure Model
    │       └── Temperature Model
    │
    ├── Risk Level Classification
    │       ├── 0 Abnormal  →  NO ALERT
    │       ├── 1–2 Abnormal → MEDIUM ALERT
    │       └── ≥3 Abnormal  → HIGH ALERT
    │
    ├── Patient Web Dashboard
    └── Hospital Web Dashboard
            └── Ambulance Dispatch
```

---

## 🔧 Hardware Components

| Component | Purpose |
|-----------|---------|
| Arduino Uno (ATmega328P) | Central microcontroller |
| DHT11 Temperature Sensor | Body temperature monitoring |
| MAX30100 Pulse Oximeter | SpO₂ (oxygen saturation) measurement |
| Digital Blood Pressure Sensor | Systolic BP, Diastolic BP and Heart Rate |
| Arduino IDE | Sensor code development and upload |

---

## 💻 Software and Technologies

| Category | Tools |
|----------|-------|
| Programming Language | Python 3.x |
| ML Development | Google Colab, Scikit-learn |
| Data Handling | NumPy, Pandas |
| Backend Framework | Flask |
| Serial Communication | PySerial |
| Web Frontend | HTML, CSS, JavaScript |
| Location Services | Browser Geolocation API, Overpass API (OpenStreetMap) |
| Model Saving | Joblib (.pkl files) |

---

## 🤖 Machine Learning Models

Four independent **Logistic Regression** models trained on **50,000 patient records** from Kaggle — one per vital parameter.

### Performance Summary

| Model | Train Accuracy | Test Accuracy | Precision | Recall | F1-Score | ROC AUC |
|-------|:--------------:|:-------------:|:---------:|:------:|:--------:|:-------:|
| Heart Rate Alert | 100% | 100% | 100% | 100% | 100% | 100% |
| SpO₂ Level Alert | 100% | 100% | 100% | 100% | 100% | 100% |
| Blood Pressure Alert | 86.97% | 87.17% | 89.35% | 89.19% | 89.27% | 95.35% |
| Temperature Alert | 90.28% | 90.63% | 89.77% | 89.06% | 89.41% | 89.06% |

### Risk Level Logic

```
Abnormal count = 0      →  🟢 NO ALERT      (Patient stable)
Abnormal count = 1 or 2 →  🟡 MEDIUM ALERT  (Show nearby hospitals)
Abnormal count ≥ 3      →  🔴 HIGH ALERT    (Auto-alert hospital + Ambulance dispatch)
```

---

## 🗂️ Project Structure

```
project/
│
├── app.py                    # Main Flask application
│
├── models/                   # Trained ML models
│   ├── hr_model.pkl
│   ├── spo2_model.pkl
│   ├── bp_model.pkl
│   └── temp_model.pkl
│
├── templates/                # HTML pages
│   ├── login.html
│   ├── register.html
│   ├── patient_dashboard.html
│   ├── hospital_login.html
│   └── hospital_dashboard.html
│
├── static/                   # CSS and JavaScript
│
└── data/
    └── patient_data.csv      # Stored patient readings
```

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install flask scikit-learn numpy pandas pyserial joblib
```

### Run the Application
```bash
# Activate virtual environment
myenv\Scripts\activate      # Windows
source myenv/bin/activate   # Linux/Mac

# Start Flask server
python app.py
```

The server runs at `http://127.0.0.1:5000`

---

## 🖥️ System Output

### 🟢 No Alert — All Vitals Normal
```
Risk Level: NO ALERT
HR: 99 bpm | SpO₂: 93% | BP: 111/77 | Temp: 31.3°C
No critical alerts detected.
```

### 🟡 Medium Alert — 1 or 2 Abnormal Parameters
```
Risk Level: MEDIUM ALERT
Alerts: Abnormal Blood Pressure
HR: 96 bpm | SpO₂: 94% | BP: 139/87 | Temp: 35.6°C

Nearby Hospitals:
  Harini Hospital     — 0.3 km
  Gowtami Hospital    — 0.6 km
  Visakha Child Care  — 0.8 km
```

### 🔴 High Alert — 3 or More Abnormal Parameters
```
Risk Level: HIGH ALERT
Alerts: Abnormal Heart Rate, Low SpO₂, Abnormal BP, Abnormal Temp
HR: 103 bpm | SpO₂: 87% | BP: 129/86 | Temp: 38°C

Nearest Hospital: Harini Hospital (0.3 km)
🚑 EMERGENCY REQUEST ACTIVE — Ambulance Dispatched!
```

---

## 📊 Data Preprocessing Steps

1. **Data Cleaning** — Removed null values, duplicates, and outliers
2. **Feature Selection** — Heart Rate, SpO₂, Blood Pressure, Body Temperature
3. **Label Encoding** — Normal → 0, Abnormal → 1
4. **Train-Test Split** — 80% training / 20% testing
5. **Normalization** — Scaled input features to uniform range

---

## 🔮 Future Scope

- Deep Learning models for improved accuracy on borderline BP and Temperature values
- Cloud integration (AWS / Azure) for remote data storage and access
- Dedicated mobile app for patients and families
- Wearable device integration for continuous monitoring
- Multi-patient simultaneous monitoring support
