# Smart Fire Alarm System 🔥

An IoT-based fire detection and alert system with real-time monitoring, automated emergency response, and web interface.

---

## 📹 Demo Video  
🎥 Watch our demo here: [https://youtu.be/bkFqhul_pnc?si=WVrjKbAA0X_dvNA2](https://youtu.be/bkFqhul_pnc?si=WVrjKbAA0X_dvNA2)

---

# 🚢 Containerizing Smart Fire Alert System

This repo contains two Docker build targets:

- **`hardware`** (`src/main.py`): for hardware system functions; initialises all hardware components.  
- **`website`** (`website/app.py`): hosts a website that provides a web-interface for users.  

### Build & Run with Docker  

#### Hardware
```bash
docker pull yzhzh09/smart-fire-alert-hardware:latest2
docker run --privileged yzhzh09/smart-fire-alert-hardware:latest2
```

#### Website
```bash
docker pull yzhzh09/smart-fire-alert-website:latest
docker run --privileged -p 5000:5000 yzhzh09/smart-fire-alert-website:latest
```

#### Using Docker Compose
To build and run both services together:
```bash
docker-compose up --build
```
- The `website` service will be available on the Raspberry Pi IP Address.

---

# 👥 Team Contributions

### **Colin Wee**
- Smoke Detection (IR + LDR integration & testing)  
- Fire Detection (temperature integration & multi-sensor logic)  
- RFID System integration with pytest tests  
- System Integration across all modules  
- Programmed `main.py` for threading, emergency response, and notifications  
- Documentation (requirements refinement, architecture diagrams)  

---

### 🔹 **Meenakshi Ramasubramanian**
- **SRS Documentation** (system architecture, use cases, requirements)  
- **Sprint Planning** (coordinated tasks, timelines, stand-ups)  
- **Website Development** (frontend & backend with Flask + Firebase)  
- **Camera Integration** (Picamera2 live CCTV + stream to website)  
- **Hardware-Software Integration** (API for sensor data + alerts)  

---

### **Phoo Pyae Sone Aye**
- **SRS (V1 & V2)** (architecture, UML diagrams, flowcharts)  
- **Frontend Dashboard & Profile Pages** (real-time data + resident info)  
- **Backend Flask Integration** (`app.py` for auto-refreshing live data)  
- **Sensor Data Handling** (temperature, humidity, ultrasonic presence detection)  

---

### **Yao Zhenghan**
- **SRS Edits** (functional & non-functional requirements)  
- **Sprint Planning V2** (task distribution & tracking)  
- **LCD Integration** (context-aware messaging)  
- **Keypad Module** (manual override)  
- **Potentiometer, Servo, DC Motor, Buzzer, Moisture Sensor Logic**  
- **Dockerization** (hardware & website containers, Docker Hub images)  

---

# 📋 Table of Contents  

- [Features](#features)  
- [Hardware Components](#hardware-components)  
- [System Architecture](#system-architecture)  
- [Installation](#installation)  
- [Configuration](#configuration)  
- [Usage](#usage)  
- [Web Interface](#web-interface)  
- [Testing](#testing)  
- [Troubleshooting](#troubleshooting)  
- [API Endpoints](#api-endpoints)  
- [Contributing](#contributing)  
- [License](#license)  

---

## ✨ Features  

- **Multi-sensor Fire Detection** (Temperature, Smoke (IR + LDR), Humidity)  
- **Automated Emergency Response** (Sprinklers, Water pump)  
- **Real-time Notifications** (Email + Telegram)  
- **Web Dashboard** (Live monitoring, user management)  
- **Manual Override** (Keypad with passcode)  
- **Video Recording** (Automatic incident documentation)  
- **RFID Access Control** (Secure activation)  

![System Overview](./images/system-overview.png)

---

## 🔧 Hardware Components  

| Component | Quantity | Purpose |  
|-----------|----------|---------|  
| Raspberry Pi 4 | 1 | Main controller |  
| DHT22 Sensor | 1 | Temperature/Humidity |  
| IR Sensor | 1 | Smoke detection |  
| LDR | 1 | Light level monitoring |  
| Moisture Sensor | 1 | Water confirmation |  
| Servo Motor | 1 | Sprinkler positioning |  
| DC Motor | 1 | Water pump |  
| RFID Reader | 1 | Access control |  
| LCD Display (16x2) | 1 | Status display |  
| 4x4 Keypad | 1 | Manual input |  
| Buzzer | 1 | Audio alerts |  
| LED | 1 | Visual indicators |  
| Camera Module | 1 | Recording |  

![Hardware Components](./images/hardware-components.png)

---

## 🏗️ System Architecture  

```
Sensors → Raspberry Pi → Emergency Response
   ↓           ↓              ↓
 Data      Processing     Actuators
Collection   & Logic      & Alerts
```

- **Fire Detection Engine** – Multi-parameter detection  
- **Emergency Response** – Sprinklers & alerts  
- **Web Interface** – Dashboard & user management  
- **Manual Override** – Shutdown via keypad  

![System Architecture](./images/architecture-diagram.png)

---

## 🚀 Installation

### Prerequisites
- Raspberry Pi 4 with Raspbian OS
- Python 3.8+
- Internet connection

### Quick Setup

```bash
# Clone repository
git clone https://github.com/yourusername/smart-fire-alarm-system.git
cd smart-fire-alarm-system

# Initialize submodules
git submodule init
git submodule update

# Install dependencies
pip3 install flask picamera2 RPi.GPIO requests

# Configure system
cp config.json.template config.json
nano config.json

# Run system
python3 src/main.py
```

### Hardware Setup
1. Connect sensors according to pin configuration  
2. Ensure proper power supply for motors  
3. Test individual components before integration  

---

## ⚙️ Configuration

Edit `src/config.json`:

```json
{
  "location": "Your Location",
  "recipient_email": "alert@example.com",
  "telegram_bot_token": "YOUR_BOT_TOKEN",
  "telegram_chat_id": "YOUR_CHAT_ID"
}
```

---

## 📱 Usage

### Starting the System
```bash
# Main fire detection system
python3 src/main.py

# Web dashboard (separate terminal)
python3 src/app.py
```

---

## 🌐 Web Interface

Access the dashboard at `http://raspberry-pi-ip:5000`

---

## 🧪 Testing

```bash
# Fire detection tests
python3 -m pytest src/test_Fire_detection.py -v
```

---

## 🔧 Troubleshooting

- Check sensor wiring  
- Ensure Flask server is running  
- Verify notification credentials  

---

## 📊 API Endpoints

- `GET /` - Main dashboard  
- `GET /data` - JSON sensor data  
- `GET /profile` - User profile page  
