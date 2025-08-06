# GemmaBot-AI 
### An Offline Visual Assistance Robot Powered by Google’s Gemma 3n

---

 ## Overview

**GemmaBot-AI** is an assistive robot designed to help visually impaired users navigate their surroundings safely — using **offline**, AI-powered scene understanding.

Built using **Google’s Gemma 3n** model running locally on a PC, and a **Wi-Fi-enabled robot (ESP32)**, GemmaBot processes real-world images, interprets the environment, and sends directional voice and motion commands to the robot — **without requiring internet access**.

This project is part of the [Google Gemma 3n Impact Challenge](https://ai.google.dev/gemma/impact-challenge).

---

## How It Works

###  PC Side (Brain):
- Captures real-time images using a **mobile phone camera over IP**.
- Processes the image locally using **Gemma 3n:2B via Ollama**.
- Interprets the scene using **prompt engineering**, and extracts commands.
- Sends movement instructions (like `GO_LEFT`, `STOP`) to the robot using **HTTP over Wi-Fi**.

### Robot Side (Body):
- An **ESP32** board acts as the receiver.
- Interprets commands and drives **4 standard DC motors via L298N** motor driver.
- Uses an **ultrasonic sensor** to detect and avoid nearby obstacles.
- Plays voice feedback using a **Bluetooth speaker** (planned feature).

---

## Hardware Used

| Component            | Role                                                       |
|----------------------|------------------------------------------------------------|
| ESP32                | Wi-Fi-enabled microcontroller for robot control            |
| L298N Motor Driver   | Controls DC motor direction and speed                      |
| DC Motors (x4)       | Drive the robot’s movement                                 |
| Standard Wheels (x4) | Forward/backward + turning movement                        |
| Ultrasonic Sensor    | Detects obstacles and prevents collision                   |
| Mobile Camera        | Captures real-time input (via IP webcam app)               |
| Bluetooth Speaker    | Voice guidance feedback (to be integrated)                 |
| Battery Pack         | Powers the ESP32 and motor driver                          |
| Chassis & Frame      | Holds all components together                              |

---

## System Architecture
User (Visually Impaired)
│
Camera (Mobile)
│
Laptop (Gemma 3n via Ollama)
│
[Python HTTP Sender]
│
Wi-Fi (HTTP GET)
│
ESP32 Microcontroller
│
Motor Driver (L298N) ─ Ultrasonic Sensor
│
Robot Movement + Voice Feedback

## Software Flow

1. **Image Capture** – Get a live image using mobile camera (via IP webcam app).
2. **Gemma Inference** – Process it using the Gemma 3n model + prompt engineering.
3. **Parse Response** – Extract command like `GO_LEFT`, `STOP`, etc.
4. **Send Command** – Send command to ESP32 over HTTP.
5. **Robot Execution** – ESP32 executes motion + checks obstacles.
   ---
   
 ##  Repository Structure
 GemmaBot-AI/
│
├── hardware/                     # ESP32 code + robot setup
│   ├── esp32_http_server.ino     # ESP32 sketch
│   ├── wiring_diagram.png        # Circuit diagram
│   └── components_list.md        # All hardware components
│
├── software/                     # Python scripts running on PC
│   ├── pc_command_sender.py      # Sends command to ESP32
│   ├── gemma_integration.py      # Runs Gemma + interprets image
│   ├── image_capture_mobile.md   # How to set up the mobile IP cam
│   └── requirements.txt          # pip packages
│
├── images/                       # Diagrams & design visuals
│   ├── repo_structure_diagram.png
│   ├── robot_design.png
│   └── project_logo.png
│
├── docs/                         # Documentation
│   ├── system_overview.md
│   ├── hardware_setup.md
│   ├── software_setup.md
│   └── usage_guide.md
│
├── data/                         # Test images
│   ├── test_image_1.jpg
│   └── test_image_2.jpg
│
├── tests/                        # QA & testing
│   ├── test_connection.py
│   └── test_gemma_model.py
│
└── README.md 


---

###  Requirements

Install Ollama & Python dependencies:
```bash
# Install Gemma 3n via Ollama
ollama pull gemma:2b

# Create virtual env & install dependencies
python -m venv venv
source venv/bin/activate
pip install -r software/requirements.txt

Run on PC
Connect your mobile camera via IP Webcam app (e.g., Android app).
Launch gemma_integration.py to generate scene description + movement command.
Launch pc_command_sender.py to send that command to ESP32 over HTTP.

 Setup Robot (ESP32)
Flash esp32_http_server.ino to your ESP32.
Connect motors, sensor, power, and speaker.
Make sure both ESP32 and PC are on same Wi-Fi.

Tests
test_connection.py → verifies connection to ESP32.
test_gemma_model.py → ensures Gemma 3n returns valid command outputs.

Team
Moamen Yehia 
Jomana Farag

Acknowledgment
Thanks to Google for releasing Gemma 3n as an open, performant language model — enabling real-world, privacy-respecting AI systems to come to life.

