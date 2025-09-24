# IoT-Driven Student Movement Monitoring System

## Overview

An **IoT-powered real-time student movement monitoring system** using **ESP32 devices** for passive **MAC address detection**. Data flows via **MQTT protocol** to a **Flask–MySQL backend**, where it is validated, stored, and visualized in a **web-based analytics dashboard**.

This platform provides:

* Real-time **attendance tracking** (students inside campus at any moment)
* **Heatmaps & temporal trends** for entry/exit traffic
* **Demographic insights** (year, gender, hostel, stream, etc.)
* **Live monitoring** with headcount and recent activity

## Demo Video
Click this link for a complete working demo video of the app: 
[demo_video](https://drive.google.com/file/d/18zhf3fuYR6_WcU_hZ6Fcosrs3iNr7Lbm/view?usp=drive_link)

---

## 🏗️ System Architecture

```
          ┌────────────┐
          │   ESP32    │   (MAC address detection)
          └─────┬──────┘
                │
         Wi-Fi / Hotspot
                │
        ┌───────▼────────┐
        │   MQTT Broker   │  (Mosquitto on port 1883)
        └───────┬────────┘
                │
        ┌───────▼────────┐
        │ Flask Backend  │  (Validation + API Layer)
        └───────┬────────┘
                │
        ┌───────▼────────┐
        │   MySQL DB     │  (Persistent storage)
        └───────┬────────┘
                │
        ┌───────▼──────────────┐
        │   Web Dashboard UI   │  (Heatmaps, Trends, Attendance)
        └──────────────────────┘
```

---

##  Features

* **ESP32 + MQTT** → Passive MAC detection & message publishing.
* **Flask–MySQL Backend** → Data validation, duplicate filtering, offline logging.
* **Real-Time Dashboard** → Heatmaps, temporal trends, demographic breakdowns, and live attendance tracking.

---

##  Setup Guide

### 1️ Install Mosquitto Broker

1. Go to your Mosquitto installation folder (`C:\Program Files\mosquitto`).
2. Edit `mosquitto.conf`:

   ```ini
   listener 1883 0.0.0.0
   allow_anonymous true
   ```
3. Save file.
4. Start broker:

   ```bash
   mosquitto.exe -v -c mosquitto.conf
   ```

   OR from Windows **Services** → find **Mosquitto Broker** → click **Start**.

---

### 2️ Configure MQTT Explorer

1. Open **MQTT Explorer**.
2. Create new connection:

   * **Name**: Custom
   * **Protocol**: mqtt://
   * **Host**: IPv4 of local hotspot
   * **Port**: 1883

---

### 3️ Publish & Subscribe (Test)

####  Publish

Run in Mosquitto terminal:

```bash
mosquitto_pub -t topic_name/sub_topic -h broker_IPV4 -m "your_message"
```

####  Subscribe

```bash
mosquitto_sub -t topic_name/sub_topic -h broker_IPV4
```

Subscribe to all topics:

```bash
mosquitto_sub -t topic_name/# -h broker_IPV4
```

---

##  Dashboard Features

* **Live Attendance** → Current students inside campus.
* **Daily Trends** → Entry/exit by hour.
* **30-Day Patterns** → Line chart of entries/exits.
* **Demographic Distribution** → Year, gender, hostel, branch, stream.
* **Weekly Heatmaps** → Day vs hour activity visualization.
* **Recent Activity** → Last 5 entries with roll no. & timestamps.
* **Safety & Load Insights** → Peak load, weekend patterns, anomalies.

---

##  Tech Stack

* **Hardware**: ESP32
* **Communication**: MQTT (Mosquitto Broker)
* **Backend**: Flask, MySQL
* **Frontend**: HTML, CSS, JS (Dashboard UI)

---

##  Repository Structure

```
├── createData    
├── final frontend
├── macRollform
├── recieve_edit_upload
├── entry_code.py
├── exit_code.py
├── extra.md
├── tutorial.md
```

---

##  Future Enhancements

* Role-based access for administrators.
* Integration with biometric/RFID for hybrid attendance.
* Cloud deployment for scalability.
  \`\`
