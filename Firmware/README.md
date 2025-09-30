# ESPiderman Access Point Firmware

Firmware for the ESPiderman robot, designed for ESP32 boards. This firmware enables WiFi access point mode, web-based camera streaming, and advanced servo control for walking gaits and robot actions.

---

## Overview

ESPiderman firmware turns your ESP32 into a wireless robot controller and live camera server. Key features:
- **WiFi AP** for direct connection (no router needed)
- **Web server** with live camera stream and interactive controls
- **Servo control** via Adafruit PWM Servo Driver (PCA9685)
- **Multiple walking gaits**, calibration, and feedback
- **Embedded HTML/CSS** web interface for control and status

## Hardware Requirements
- ESP32 board (AI Thinker, M5Stack, WROVER KIT, etc.)
- Compatible camera module (see code for supported models)
- PCA9685 PWM Servo Driver
- Servos for robot legs
- Power supply for servos and ESP32

## Software Requirements
- Arduino IDE or PlatformIO
- ESP32 board support package
- Libraries:
  - `esp_camera`, `WiFi`, `esp_timer`, `img_converters`, `Arduino`, `fb_gfx`, `esp_http_server`, `Wire`, `Adafruit_PWMServoDriver`

## Installation & Setup
1. Install Arduino IDE or PlatformIO
2. Add ESP32 board support (via Boards Manager)
3. Install required libraries (see above)
4. Connect ESP32, camera, PCA9685, and servos
5. Open `ESPidermanAccesPoint.ino`
6. Select correct board and port
7. Upload firmware

## Usage
- On boot, ESP32 creates a WiFi AP (SSID and password configurable in code)
- Connect to WiFi from your device
- Open browser to ESP32 IP (default: `192.168.4.1`)
- Use web interface for live camera and robot controls

## Main Code Structure (ESPidermanAccesPoint.ino)

- **WiFi Setup:** ESP32 AP initialization, SSID/password config
- **Camera Configuration:** Pin setup, model selection, streaming
- **Servo Control:** Adafruit PWM driver for up to 12 servos, calibration, and range
- **Web Server:** Embedded HTML/CSS (`INDEX_HTML`), command handling, camera stream endpoint
- **Feedback Variables:** Status, sensor, and robot state reporting
- **Walking Gaits:** Movement patterns, calibration routines, and gait parameter variables

## Key Variables & Configuration
- `ssid`, `password`: WiFi credentials (change for security)
- `Adafruit_PWMServoDriver pwm`: Servo driver instance
- `stepLift`, `stepLength`: Step height/length for gaits
- `comp0` ... `compN`: Servo calibration offsets (per leg)
- `pos0`, `pos180`: PWM pulse values for servo range
- Camera model selection: `#define CAMERA_MODEL_AI_THINKER` (or other supported)

## Web Interface
- HTML/CSS embedded in firmware (`INDEX_HTML`)
- Buttons and status displays for robot control
- Live camera stream in browser (MJPEG)

## Troubleshooting
- `cannot open source file` errors: Check library installation and include paths
- Select correct camera model in code (`#define CAMERA_MODEL_...`)
- Verify wiring and power for servos/camera
- Use serial monitor for debug output

## Extending & Customizing
- Add new gaits/actions by editing movement logic
- Customize web interface (HTML/CSS in code)
- Integrate more sensors or feedback
- Adjust calibration and gait parameters for your robot

## License
Educational and research use only

---

## Technical Documentation

### WiFi & Web Server
- ESP32 AP setup via `WiFi.h`
- Web server with camera streaming and control endpoints
- HTML/CSS interface in `INDEX_HTML`

### Camera Setup
- Pin configuration by model (`#define CAMERA_MODEL_...`)
- Streaming via multipart HTTP responses (MJPEG)

### Servo Control
- Adafruit PWM Servo Driver for up to 12 servos
- Calibration offsets and pulse ranges configurable
- Walking gaits via step height/length variables

### Feedback & Communication
- Status/sensor data sent to client via web interface
- Variables: `feedBackToClient`, `light`, `armed`, `height`, etc.

### Customization
- Change WiFi credentials in code
- Adjust servo calibration/gait parameters
- Edit web interface for custom controls/displays

## Contact & Support
For questions, issues, or contributions, open an issue or pull request on GitHub.
