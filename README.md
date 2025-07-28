# GemmaBot-AI 

## Overview
GemmaBot is an offline, AI-powered assistive robot for visually impaired users, using Google's Gemma 3n.

## AI Logic
- Gemma 3n model runs on laptop (`gemma3n:e2b`)
- Receives camera input
- Sends commands to ESP32: `STOP`, `GO_LEFT`, `GO_RIGHT`, `GO_FORWARD`

##  Hardware
- ESP32 (control)
- L298N (motor driver)
- MPU6050 (GY-521) motion sensor
- Webcam or ESP32-CAM (vision)
- Mecanum wheels
- 	Power source (battery or 5V external) 

##  Software Structure
- `esp32/`: Microcontroller code
- `pc/`: Python script to run Gemma and send commands

## Team
- Moamen Yehia
- Jomana Farag

##  Challenge
Google – The Gemma 3n Impact Challenge (Deadline: Aug 8)
