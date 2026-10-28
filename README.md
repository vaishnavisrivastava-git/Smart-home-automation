# 🏠 Smart Home Automation System

An IoT-based Smart Home Safety and Automation System using **ESP32, PIR Motion Sensor, MQ-2 Gas Sensor, SW-420 Vibration Sensor, and ThingSpeak Cloud**. The system combines motion-activated lighting, gas leakage monitoring, and vibration detection to improve household safety, automation, and remote environmental monitoring.

## 📌 Project Overview

Traditional home monitoring systems often require manual operation and may lack real-time monitoring capabilities. This project addresses these limitations by integrating multiple sensors with an ESP32 microcontroller to detect movement, monitor potentially hazardous gases, and identify physical disturbances.

The ESP32 processes sensor readings and controls output devices based on predefined conditions. Using its built-in Wi-Fi connectivity, the system transmits sensor data to the ThingSpeak IoT cloud platform through HTTP GET requests, enabling remote monitoring and visualization of sensor activity.

### 🎯 Objectives

- **Motion-Activated Lighting:** Automatically turn an LED on when motion is detected and off when motion is no longer detected.
- **Gas Leakage Detection:** Monitor gas sensor readings and activate a buzzer when the measured value exceeds a predefined threshold.
- **Vibration Monitoring:** Detect vibrations or shocks that may indicate physical disturbances or possible tampering.
- **Cloud-Based Monitoring:** Upload sensor readings and event statuses to ThingSpeak for remote visualization and logging.
- **Affordable Automation:** Develop a low-cost, sensor-driven system using readily available electronic components.

## ✨ Features

- Motion detection using a Passive Infrared (PIR) sensor.
- Automatic LED control based on detected motion.
- Gas and smoke-related monitoring using the MQ-2 sensor.
- Buzzer alerts when the gas reading crosses a configured threshold.
- Vibration detection using the SW-420 sensor.
- Wireless communication through the ESP32's built-in Wi-Fi.
- Real-time sensor data logging and visualization on ThingSpeak.
- Serial Monitor output for debugging and observing sensor states.
- Modular design that can be extended with additional sensors and automation features.

## 🛠️ Hardware Components

| Component | Purpose |
|---|---|
| ESP32 Development Board | Main controller for processing sensor inputs and managing Wi-Fi communication |
| PIR Motion Sensor (HC-SR501) | Detects changes in infrared radiation associated with movement |
| MQ-2 Gas Sensor | Detects combustible gases and smoke-related changes in the surrounding air |
| SW-420 Vibration Sensor | Detects mechanical vibration and physical shocks |
| Active Buzzer | Produces an audible warning when triggered |
| Red LED | Provides visual indication of detected motion |
| BC547 / switching transistor | Supports switching functions in the circuit where required |
| Resistors | Provide current limiting and signal conditioning |
| Breadboard | Enables circuit prototyping without soldering |
| Jumper Wires | Connect the sensors, controller, and output devices |

## 💻 Software and Technologies

- **Programming Language:** C/C++
- **Microcontroller Platform:** ESP32
- **Development Environment:** Arduino IDE
- **Connectivity:** Wi-Fi
- **Communication Protocol:** HTTP
- **Cloud Platform:** ThingSpeak
- **Libraries:** `WiFi.h`, `HTTPClient.h`

## 🔌 Circuit Connections

The following pin mapping is documented in the project's ESP32 implementation.

| ESP32 GPIO | Connected Component | Interface |
|---|---|---|
| GPIO 34 | MQ-2 Gas Sensor | Analog input |
| GPIO 27 | Active Buzzer | Digital output |
| GPIO 18 | SW-420 Vibration Sensor | Digital input |
| GPIO 4 | PIR Motion Sensor | Digital input |
| GPIO 19 | Red LED | Digital output |

**Note:** Verify these pin assignments against your final circuit and source code before wiring the hardware. Ensure that every signal connected to an ESP32 GPIO remains within its supported voltage range. In particular, do not apply a 5 V signal directly to an ESP32 input.

## ⚙️ System Architecture

The system follows a sensor-to-controller-to-output and cloud-monitoring architecture.

1. **Sensor Layer:** The PIR, MQ-2, and SW-420 sensors monitor motion, gas-related changes, and vibration.
2. **Processing Layer:** The ESP32 reads analog and digital signals and evaluates them against the programmed conditions.
3. **Automation Layer:** The ESP32 controls the LED and buzzer according to the sensor readings.
4. **Communication Layer:** The ESP32 connects to a Wi-Fi network and sends sensor data using HTTP GET requests.
5. **Cloud Layer:** ThingSpeak records and visualizes the uploaded data through channel fields and time-series graphs.

## 🔄 Working Principle

### 1. Motion-Activated Lighting

The PIR sensor detects motion by sensing changes in infrared radiation. Its digital output is read by the ESP32.

- When motion is detected, the ESP32 turns the LED ON.
- When motion is no longer detected, the ESP32 turns the LED OFF according to the sensor output.
- The motion status is uploaded to ThingSpeak for monitoring.

This functionality helps improve visibility and reduce unnecessary lighting.

### 2. Gas Leakage Detection

The MQ-2 sensor monitors the surrounding air for combustible gases and smoke-related changes.

- The ESP32 reads the sensor's analog output using an ADC-capable GPIO.
- The reading is compared with a predefined threshold.
- If the reading exceeds the threshold, the ESP32 activates the buzzer.
- The gas reading and detection status are transmitted to ThingSpeak.

The project uses a threshold of `275` in its example implementation. This is a configured analog reading, not a calibrated gas concentration in ppm.

### 3. Vibration Detection

The SW-420 module detects vibration or mechanical shocks and produces a digital output.

- The ESP32 reads the sensor's digital signal.
- The program determines whether a vibration event has been detected.
- The resulting status is uploaded to ThingSpeak.
- The data can be inspected over time to observe disturbances or repeated sensor triggers.

This feature can support basic disturbance and tampering monitoring. It is not a certified earthquake detection or early-warning system.

### 4. Cloud Monitoring with ThingSpeak

The ESP32 uses its built-in Wi-Fi functionality to communicate with ThingSpeak.

- Connect to the configured Wi-Fi network.
- Read the current sensor values.
- Construct an HTTP GET request containing the sensor readings and status fields.
- Send the request to the ThingSpeak update endpoint.
- Check the HTTP response code and print the result to the Serial Monitor.
- Repeat the process at the configured interval.

The implementation uses a **15-second delay** between updates to respect the standard ThingSpeak free-channel update interval used by the project.

## ☁️ ThingSpeak Data Fields

The system sends four fields to the ThingSpeak channel.

| Field | Data | Description |
|---|---|---|
| Field 1 | Gas Reading | Analog reading from the MQ-2 sensor |
| Field 2 | Gas Status | Indicates whether the configured gas threshold has been exceeded |
| Field 3 | Vibration Status | Indicates whether vibration has been detected |
| Field 4 | Motion Status | Indicates whether motion has been detected |

The cloud dashboard can display these fields as time-series graphs, allowing sensor activity to be monitored remotely.

## 🚀 Getting Started

### Prerequisites

Before running the project, ensure you have:

- An ESP32 development board.
- The required sensors and circuit components.
- Arduino IDE installed on your computer.
- ESP32 board support configured in Arduino IDE.
- A Wi-Fi connection with internet access.
- A ThingSpeak account and configured channel.
- The required Arduino libraries installed.

### Installation

1. Clone or download this repository.

   ```bash
   git clone <YOUR_REPOSITORY_URL>
   ```

2. Open the Arduino source file in Arduino IDE.

3. Install or verify the required libraries:
   - WiFi library for ESP32.
   - HTTPClient library for ESP32.

4. Connect the components according to the verified circuit pin mapping.

5. Configure your Wi-Fi and ThingSpeak credentials.

6. Select the appropriate ESP32 board and serial port.

7. Upload the program to the ESP32.

8. Open the Serial Monitor and set the baud rate to `115200`.

9. Verify Wi-Fi connectivity and check the sensor readings.

10. Open your ThingSpeak channel to view uploaded data.

## 🔐 Configuration and Security

Before uploading the program, configure the Wi-Fi credentials and ThingSpeak Write API Key.

Use placeholders in the source code rather than publishing real credentials:

```cpp
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";

const char* apiKey = "YOUR_THINGSPEAK_WRITE_API_KEY";
const char* server = "http://api.thingspeak.com/update";
```

**Security recommendations:**

- Never commit real Wi-Fi passwords or API keys to a public repository.
- Store credentials in a separate, untracked configuration file or use a suitable secrets-management approach.
- If credentials have already been exposed publicly, change them.
- Do not share screenshots containing active credentials.

## 🧪 Testing and Results

The project report documents successful operation of the three sensor modules and cloud data logging.

### Motion Detection Test

Move within the PIR sensor's detection range.

**Expected behavior:**
- The motion status changes when movement is detected.
- The LED turns ON during detected motion.
- The motion status is recorded on ThingSpeak.

### Gas Sensor Test

Observe the MQ-2 sensor reading under normal conditions and during a controlled test.

**Expected behavior:**
- The analog reading is displayed in the Serial Monitor.
- When the reading crosses the configured threshold, the buzzer activates.
- The sensor reading and gas status are uploaded to ThingSpeak.

### Vibration Sensor Test

Apply a small, controlled vibration to the sensor assembly.

**Expected behavior:**
- The digital vibration state changes according to the sensor's response.
- The vibration status is logged to ThingSpeak.
- Repeated triggers can be examined through the cloud graph.

### Cloud Communication Test

Monitor the Serial Monitor and ThingSpeak dashboard.

**Expected behavior:**
- The ESP32 reports Wi-Fi connection status.
- Sensor readings are periodically sent to ThingSpeak.
- HTTP response codes are printed to the Serial Monitor.
- The cloud graphs display the received data.

Actual detection accuracy depends on sensor calibration, placement, sensitivity, and environmental conditions.

## 📊 Observed Results

The project report describes the following observations:

- PIR sensor readings changed between motion-detected and no-motion states.
- The MQ-2 sensor produced higher analog readings during a gas-related test.
- The vibration channel recorded vibration status values.
- ThingSpeak displayed the sensor data over time.
- The Serial Monitor provided status information and HTTP response codes.

These observations demonstrate the integration of sensor monitoring, basic automated responses, and cloud-based data logging.

## ⚠️ Limitations

- **Limited sensing range:** PIR and vibration sensors have physical detection limitations.
- **False triggers
