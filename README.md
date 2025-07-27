# Voice-Activated-Audio-Monitoring-System
Voice Pulse is an ESP32-based project that detects voice activity using a microphone. It records audio only when voice is detected and manages file size efficiently. Designed for low-power, event-driven audio capture in smart embedded systems.
# Voice-Activated Audio Monitoring System

This project is a smart, ESP32-based embedded system that monitors voice activity using a microphone and records audio only when voice is detected. The recorded audio is sent to an AWS S3 bucket, and transcription is performed using the Deepgram API.

## Features

- 🔊 **Voice Activity Detection (VAD):** Only records when human voice is detected, reducing storage and power consumption.
- 🎙️ **Microphone Input:** Captures audio via an analog microphone module.
- 💾 **Smart Storage Handling:** Automatically splits recordings into multiple files to keep each under 500KB.
- 📡 **Wi-Fi Enabled:** Connects to a Wi-Fi network for real-time data transmission.
- 🌐 **AWS S3 Integration:** Uploads recorded audio files to a designated S3 bucket.
- 🧠 **Automatic Transcription:** Once uploaded, audio files are transcribed using Deepgram’s Speech-to-Text API.
- 🔄 **RGB LED Feedback (Optional):** Indicates system status (e.g., Wi-Fi connected, recording active, idle).

## Hardware Requirements

- ESP32 Development Board  
- Analog Microphone (e.g., MAX9814 or MAX4466)  
- RGB LED (Common Anode/Cathode) *(optional for status indication)*  
- Power Supply or USB Cable  

## Software Requirements

- Arduino IDE with ESP32 board support  
- AWS S3 bucket setup  
- Deepgram API Key  
- Libraries:
  - `WiFi.h`
  - `HTTPClient.h`
  - `ArduinoJson.h`
  - `SPIFFS` or `SD` (depending on storage method)

## How It Works

1. On power-up, the ESP32 connects to Wi-Fi.
2. It continuously monitors the audio input for voice activity.
3. When voice is detected:
   - Audio is recorded and saved in chunks (max ~500KB each).
   - Once a recording is complete or silence is prolonged, the audio is uploaded to AWS S3.
4. A backend process or lambda function triggers transcription via Deepgram API using the uploaded file URL.
5. Transcription output can be viewed, stored, or analyzed further.

## Setup Instructions

1. **Configure Wi-Fi Credentials:**
   ```cpp
   const char* ssid = "your_SSID";
   const char* password = "your_PASSWORD";
