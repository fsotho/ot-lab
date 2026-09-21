# 🛡️ OT-Lab (Operational Technology Lab)

A modern, 100% open-source, and containerized Operational Technology (OT) simulation laboratory structured around the **Purdue Enterprise Reference Architecture (PERA)**. 
This project builds an industrial network environment from physical simulation to AI-driven anomaly detection and alert notifications.

---

## 🏗️ Purdue Architecture Layers

[ C0: Field/Process ] ──>    [ C1: Basic Control ] ──>   [ C2: Supervision ] ──>   [ C3: Operations ] ──>     [ C4: Analytics ] ──>    [ C5: Alerts ]
(diagslave/modpoll)          (OpenPLC Runtime)            (Node-RED HMI)           (Mosquitto + InfluxDB)     (OpenClaw Agent)         (Telegram API)
                                                                                                                > Working                > Working

- **Layer 0 (Field & Process):** Simulates field devices and raw Modbus registers using `diagslave` and `modpoll` (TCP ports 5020/5021).
- **Layer 1 (Basic Control):** Runs an **OpenPLC** runtime acting as a local Modbus TCP master, reading raw field data and mapping registers (`%IW100`, `%IX100.1`) exposed on port `502`[cite: 1, 2].
- **Layer 2 (Supervision & HMI):** Uses **Node-RED** as a local supervisory gateway, converting Modbus TCP streams into MQTT payloads and powering local dashboards[cite: 1, 2].
- **Layer 3 (Plant Operations & Historian):** 
  - **Eclipse Mosquitto:** Real-time publish/subscribe message broker (Port `1883`)[cite: 2].
  - **InfluxDB:** Industrial time-series database (`otlab_001` historian, Port `8086`) paired with **Grafana** for visualization (`last()` aggregations)[cite: 2].
- **Layer 4 (Enterprise Analytics & AI):** **OpenClaw** (self-hosted autonomous agent) performing differential analysis (C0 vs. C1 raw-to-processed validation) to detect anomalies or tampering attempts[cite: 1, 2].
- **Layer 5 (Remote Extranet / Notifications):** Automated critical alerts and operational updates dispatched directly via **Telegram Bot API**[cite: 2].


## 🚀 Quick Start / Tech Stack

Required for use the lab:
- OpenPLC (https://github.com/thiagoralves/OpenPLC_v3)
- Mosquitto (https://mosquitto.org/)
- `diagslave`, `modpoll` (https://www.modbusdriver.com/diagslave.html)
- Node-RED: (https://nodered.org/)
- InfluxDB: (https://www.influxdata.com/)
- Grafana: (https://github.com/grafana/grafana)

- <img width="1614" height="1507" alt="image" src="https://github.com/user-attachments/assets/e467af41-bf6c-490f-ae9a-07c1d6302741" />
