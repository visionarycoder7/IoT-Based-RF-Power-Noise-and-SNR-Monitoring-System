# IoT-Based-RF-Power-Noise-and-SNR-Monitoring-System

# 📡 IoT-Based RF Power, Noise and SNR Monitoring System

### Real-Time RF Monitoring Using ESP32, AD8317, LNA and a Web Dashboard

An IoT-based Radio Frequency (RF) monitoring system designed to measure RF signal power, estimate noise levels, calculate Signal-to-Noise Ratio (SNR), and visualize measurements through a web-based dashboard.

The system integrates an **ESP32 microcontroller, AD8317 logarithmic RF detector, optional Low-Noise Amplifier (LNA), OLED display, Python Flask REST API, SQLite database, and a browser-based dashboard** to provide a low-cost RF monitoring platform.

---

## 📌 Project Overview

Traditional RF measurement instruments, such as spectrum analyzers and professional RF power meters, can be expensive for undergraduate laboratories and experimental projects.

This project provides an educational alternative by combining RF sensing hardware with embedded processing, wireless communication, data logging, and web-based visualization.

The ESP32 acquires the analog output of the AD8317 RF detector, processes the measurements, displays information on an OLED, and transmits measurement records over Wi-Fi to a Flask server running on a laptop.

The backend stores the measurements in SQLite, while the dashboard provides live readings, historical graphs, basic statistics, and CSV export.

> **Note:** The AD8317-based system measures broadband RF power levels. Frequency-spectrum analysis and identification of individual RF signals require additional frequency-selective hardware, such as a Software-Defined Radio (SDR).

## ✨ Key Features

- 📶 **RF Power Monitoring:** Acquire RF signal-level measurements using the AD8317 detector.
- 🔊 **Noise Estimation:** Implement a defined procedure for estimating the noise level.
- 📊 **SNR Calculation:** Calculate Signal-to-Noise Ratio in decibels.
- 📡 **Optional LNA Front-End:** Amplify weak RF signals before detection.
- 🔌 **ESP32 Integration:** Perform ADC sampling, digital processing, and Wi-Fi communication.
- 🖥️ **OLED Display:** Display measurement information locally using a 0.96-inch I2C OLED.
- 🌐 **REST API:** Transfer measurement records through a custom Python Flask backend.
- 🗄️ **Data Logging:** Store measurements in an SQLite database.
- 📈 **Web Dashboard:** Visualize live readings and historical trends.
- 📁 **CSV Export:** Export recorded measurements for further analysis.
- 🔧 **Extensible Architecture:** Support future enhancements such as multiple monitoring nodes, anomaly detection, and SDR integration.

## 🏗️ System Architecture

```text
        RF Source / Antenna
                 |
                 v
       Low-Noise Amplifier
             (Optional)
                 |
                 v
        AD8317 RF Detector
                 |
           Analog VOUT
                 |
                 v
              ESP32
        ADC + Processing
           /         \
          v           v
    OLED Display    Wi-Fi
                        |
                    HTTP/JSON
                        |
                        v
                 Python Flask
                   REST API
                        |
                        v
                   SQLite DB
                        |
                        v
                Web Dashboard
                HTML / CSS / JS
                        |
                        v
             Graphs, Statistics
                 and CSV Export
```

### How It Works

1. The antenna receives incoming RF energy.
2. The optional LNA amplifies weak RF signals within its supported frequency band.
3. The AD8317 converts the RF input level into an analog voltage.
4. The ESP32 samples the detector output through its ADC.
5. Firmware averages multiple samples and applies calibration parameters.
6. Signal and noise estimates are processed to calculate SNR.
7. Measurement information is displayed on the OLED.
8. The ESP32 sends measurement records to the Flask API over Wi-Fi.
9. The backend validates incoming JSON data and stores measurements in SQLite.
10. The web dashboard retrieves stored data and presents graphs, statistics, and export options.

## 🧰 Hardware Requirements

| Component | Purpose |
|---|---|
| ESP32 Development Board | ADC sampling, processing, and Wi-Fi communication |
| AD8317 RF Detector Module | Converts RF input level into an analog voltage |
| Broadband LNA Module (Optional) | Amplifies weak RF signals |
| 0.96-inch I2C OLED Display | Local measurement display |
| RF Antenna | Receives RF energy |
| SMA Connectors and Coaxial Cables | RF signal connections |
| Breadboard and Jumper Wires | Prototyping and circuit connections |
| USB Cable | ESP32 power and firmware upload |
| Resistors and Capacitors | Signal conditioning and power decoupling |

**Important:** Verify the supply voltage, pin labels, connector arrangement, and maximum input rating of the exact AD8317 and LNA modules being used.

## 💻 Software Requirements

| Technology | Application |
|---|---|
| Arduino IDE | ESP32 firmware development |
| C/C++ | Embedded programming |
| Python | Backend development and analysis |
| Flask | REST API development |
| SQLite | Measurement storage |
| HTML | Dashboard structure |
| CSS | Dashboard styling |
| JavaScript | Dashboard interactions and graphs |
| Git and GitHub | Version control and project documentation |

## 🔌 Circuit Connections

### ESP32 to OLED

| OLED Pin | ESP32 Pin |
|---|---|
| VCC | 3.3V, if supported by the OLED module |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

### AD8317 to ESP32

| AD8317 Signal | ESP32 Connection |
|---|---|
| VCC | Suitable supply according to the module datasheet |
| GND | Common GND |
| VOUT | GPIO 34 (ADC input) |
| RF IN | Antenna directly or LNA RF OUT |
| Enable | As required by the module |

### LNA Connections

| LNA Connection | Destination |
|---|---|
| RF IN | Antenna |
| RF OUT | AD8317 RF input |
| VCC | Supply specified by the module datasheet |
| GND | Common system ground |

**Wiring precautions:**

- Ensure that all modules share a common ground.
- GPIO 34 is an input-only ESP32 pin suitable for ADC input.
- Verify the AD8317 output voltage before connecting it to the ESP32.
- Keep the ADC input within the ESP32's permitted voltage range.
- Use the LNA only within its specified input-power and frequency limits.
- The reference design omits an RF attenuator; do not connect strong RF sources without verifying safe input levels.

## 🗂️ Recommended Repository Structure

```text
rf-monitor/
│
├── backend/
│   ├── app.py
│   ├── database.py
│   ├── models.py
│   └── routes/
│       └── measurements.py
│
├── firmware/
│   └── esp32_rf_monitor.ino
│
├── frontend/
│   ├── index.html
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── dashboard.js
│
├── analysis/
│   └── signal_analysis.py
│
├── simulator/
│   └── generate_data.py
│
├── requirements.txt
├── .gitignore
└── README.md
```

*This is the recommended project structure. Adjust the paths to match the files actually present in your repository.*

## ⚙️ Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/rf-monitor.git
cd rf-monitor
```

Replace `YOUR_USERNAME` with your GitHub username and `rf-monitor` with your repository name.

### 2. Set Up the Python Environment

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Activate it on Linux or macOS:

```bash
source venv/bin/activate
```

### 3. Install Dependencies

Create a `requirements.txt` file containing the packages used by your backend:

```text
Flask
numpy
pandas
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

SQLite is supported through Python's standard `sqlite3` module. Install any additional packages required by your actual implementation.

### 4. Configure the Backend

Implement the Flask application in `backend/app.py` and configure the database connection, API routes, and validation logic.

Start the server from the project root:

```bash
python backend/app.py
```

The example development server uses port `5000`.

### 5. Configure the ESP32

1. Open the firmware in Arduino IDE.
2. Install the ESP32 board package.
3. Install any libraries required by the firmware.
4. Configure the Wi-Fi SSID and password.
5. Set the laptop's local IP address and Flask API endpoint.
6. Select the correct ESP32 board and COM port.
7. Upload the firmware and open Serial Monitor to inspect diagnostic messages.

Example API endpoint:

```text
http://192.168.1.10:5000/api/measurements
```

Replace the example IP address with your laptop's actual local network address.

Ensure that the ESP32 and laptop are connected to the same Wi-Fi network and that the laptop firewall permits the required connection.

### 6. Launch the Dashboard

Open the dashboard HTML file or serve the frontend through your Flask application, depending on the implemented architecture.

The dashboard can be designed to display:

- Latest signal-level estimate
- Noise estimate
- Calculated SNR
- Measurement history
- Time-series graphs
- Basic statistical summaries
- CSV export

The dashboard requires a functioning backend and measurement data before live readings can be displayed.

## 🔗 REST API

The planned backend exposes the following endpoints:

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/measurements` | Receive and store measurements |
| GET | `/api/latest` | Retrieve the latest measurement |
| GET | `/api/history` | Retrieve historical records |
| GET | `/api/statistics` | Retrieve summary statistics |

### Example JSON Payload

```json
{
  "device_id": "RF001",
  "signal_dbm": -47.2,
  "noise_dbm": -91.5,
  "snr_db": 44.3,
  "timestamp": "2026-09-26T10:00:00"
}
```

The values above are illustrative examples, not verified experimental results.

The backend should validate the incoming fields, reject malformed requests, and store valid records in SQLite.

## 📐 Measurement and SNR Calculation

### RF Power Calibration

The AD8317 output voltage is related to the RF input level. Calibration using known reference RF input levels is required to estimate power in dBm.

A simple calibration model is:

\[
P_{\mathrm{dBm}} = aV+b
\]

Where:

- \(P_{\mathrm{dBm}}\) is the estimated RF input power.
- \(V\) is the detector output voltage.
- \(a\) and \(b\) are experimentally determined calibration constants.

The model is valid only over an appropriately calibrated operating region.

### Signal-to-Noise Ratio

When signal and noise are measured as powers in dBm under the same reference conditions:

\[
\mathrm{SNR}_{\mathrm{dB}}
=
P_{\mathrm{signal,dBm}}
-
P_{\mathrm{noise,dBm}}
\]

A repeatable measurement procedure must define the noise measurement mode, measurement bandwidth, and calibration method.

**Measurement limitation:** The AD8317 provides a broadband power-level measurement. It does not independently separate signal and noise or distinguish simultaneous Wi-Fi, Bluetooth, and cellular signals. Reliable noise and SNR estimates therefore depend on the implemented measurement procedure and suitable experimental validation.

## 📊 Dashboard and Data Logging

The intended web dashboard supports:

- Live signal, noise, and SNR readings
- Device status indication
- Historical time-series graphs
- Historical measurement filtering
- Mean, minimum, maximum, and standard deviation
- CSV export
- Optional threshold-based warning indicators

SQLite provides local storage for measurement records, including device ID, timestamp, calibrated signal estimate, noise estimate, and SNR.

## 🧪 Testing and Validation

The system should be validated through both software and hardware tests.

### Software Testing

- Test valid and invalid JSON requests.
- Verify database insertion and retrieval.
- Check API response codes.
- Test dashboard rendering.
- Verify CSV export.
- Validate SNR calculations using controlled numerical inputs.
- Test missing fields and malformed requests.

### Hardware Testing

- Verify power and ground connections.
- Check LNA supply voltage and current.
- Verify detector output voltage and ADC readings.
- Compare readings with and without the LNA under a fixed reference RF input.
- Evaluate measurement repeatability.
- Calibrate against known or reference RF power levels.
- Test Wi-Fi communication between the ESP32 and laptop.

### Experimental Results

Record actual measurements after assembling and testing the prototype. Do not present simulated values or illustrative examples as experimental results.

## 🌍 Potential Applications

- RF equipment monitoring
- Wireless site surveys
- Antenna position and orientation comparisons
- RF-level variation logging
- Preliminary RF interference investigations
- IoT deployment planning
- Educational RF and embedded-systems laboratories

The system can track changes in broadband RF levels, but it cannot identify the exact frequency or source of interference without additional hardware.

## 🚀 Future Scope

Possible extensions include:

- **Multi-Node Monitoring:** Connect multiple ESP32-based sensing nodes to one central server.
- **AI-Based Anomaly Detection:** Identify unusual patterns in historical RF measurements.
- **Predictive Maintenance:** Flag persistent RF-level changes for further investigation.
- **GPS-Based RF Mapping:** Associate measurements with geographic coordinates.
- **SDR Integration:** Add frequency-selective analysis and spectrum visualization.
- **Cloud Deployment:** Move the backend and database to a remote server.
- **Mobile Application:** Provide remote access to measurements and alerts.

These are future enhancements and should not be considered implemented features unless supported by the actual prototype.

## ⚠️ Limitations

- Measurement accuracy depends on calibration, detector characteristics, antenna response, cable losses, ADC behavior, and source stability.
- The optional LNA improves weak-signal sensitivity only within its operating limits and can also introduce noise or overload under unsuitable conditions.
- The current architecture does not provide frequency-resolved spectrum analysis.
- Noise estimation and SNR calculation require a clearly defined measurement method.
- The local Flask and SQLite setup is intended for development and educational use, not automatically a production-ready deployment.
- Performance claims must be supported by experimental validation against suitable reference equipment.

This project is an educational RF monitoring platform and is not a replacement for a calibrated professional spectrum analyzer.

## 📄 License

No license has been specified yet. Add a `LICENSE` file if you intend to publish the repository under an open-source license.

## ⭐ Acknowledgements

Thanks to the project guide, department faculty, and laboratory staff for their guidance and support during the development and testing of this project.

---

If you find this project useful for learning RF measurement, ESP32 programming, IoT communication, and web-based monitoring, consider starring the repository.
