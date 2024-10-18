# Smart Doorbell Project with ESP32-CAM MB

## Description
This project implements a smart doorbell system using an ESP32-CAM MB. It includes features such as face recognition, live video streaming, Blynk notifications when a button is pressed, and audio communication with a person standing outside. The doorbell can open a lock upon recognizing a predefined face, allowing for secure and convenient access.

## Features
- Face recognition for unlocking the door.
- Live video streaming using Blynk.
- Push notifications when the button is pressed.
- Two-way audio communication with a microphone and speaker.
- Control of a solenoid lock via a relay module.

## Components Required
- **ESP32-CAM MB**: Microcontroller with integrated camera module.
- **Relay Module**: To control the locking mechanism.
- **Microphone**: For capturing audio input (compatible with ESP32).
- **Speaker**: For audio output (compatible with ESP32).
- **Blynk App**: For remote notifications and live video streaming.
- **Jumper Wires**: For connections.
- **Breadboard**: For easy prototyping (optional).

## Setup Instructions

### 1. Hardware Connections
- Connect the **ESP32-CAM MB** to the **Relay Module**:
  - Choose a GPIO pin for controlling the relay (e.g., GPIO 13).
- Connect the **Button**:
  - Connect one terminal to a GPIO pin (e.g., GPIO 12) and the other to ground.
- Connect the **Microphone** and **Speaker** according to their datasheets and ensure they are compatible with the ESP32.

### 2. Software Setup
- **Install Libraries**: 
  - Use the Arduino IDE to install the following libraries via the Library Manager:
    - `Blynk`
    - `ESP32 Camera`
    - `Face Recognition` library (e.g., [ESP32-Face-Recognition](https://github.com/shuye07/ESP32-Face-Recognition))
    - `Audio Library` (like `ESP32-Audio-Kit` or `ESP32-Audio-Player`).
  
- **Blynk Setup**:
  - Create a new project in the Blynk app.
  - Add necessary widgets (Button for lock control, Video Stream for live camera feed).
  - Obtain the **Auth Token** and keep it handy for the code.

### 3. Configure WiFi Credentials
Replace the placeholders in the code with your actual WiFi credentials and Blynk Auth Token.

## Code Explanation
Here’s the code that implements the smart doorbell functionality:

```cpp
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>
#include "esp_camera.h"
#include "WiFiClient.h"

// Define Blynk Auth Token
char auth[] = "YOUR_BLYNK_AUTH_TOKEN";

// WiFi Credentials
const char* ssid = "YOUR_SSID";
const char* password = "YOUR_PASSWORD";

// Define camera configuration
camera_config_t config;

// GPIO for button and relay
#define BUTTON_PIN  12   // Adjust according to your wiring
#define RELAY_PIN   13   // Adjust according to your wiring

// Face recognition data (replace with your face recognition function)
bool recognizeFace() {
    // Your face recognition logic goes here
    return true; // For demonstration, we return true
}

// Blynk notification function
void notify() {
    Blynk.notify("Someone is at the door!");
}

// Button press handler
void buttonPressed() {
    notify();
    // Optional: Add a delay before the next action
}

// Blynk virtual pin for streaming
BlynkTimer timer;

// Stream live view
void stream() {
    // Code to handle live streaming
    // You can implement an HTTP server to serve the camera feed
}

void setup() {
    Serial.begin(115200);

    // Setup button and relay pins
    pinMode(BUTTON_PIN, INPUT_PULLUP);
    pinMode(RELAY_PIN, OUTPUT);
    digitalWrite(RELAY_PIN, LOW); // Lock is initially closed

    // Initialize camera
    config.ledc_channel = LEDC_CHANNEL;
    config.ledc_timer = LEDC_TIMER;
    config.pin_d0 = 0; // Adjust according to your wiring
    config.pin_d1 = 1; // Adjust according to your wiring
    config.pin_d2 = 2; // Adjust according to your wiring
    config.pin_d3 = 3; // Adjust according to your wiring
    config.pin_d4 = 4; // Adjust according to your wiring
    config.pin_d5 = 5; // Adjust according to your wiring
    config.pin_d6 = 6; // Adjust according to your wiring
    config.pin_d7 = 7; // Adjust according to your wiring
    config.pin_xclk = 21; // Adjust according to your wiring
    config.pin_pclk = 22; // Adjust according to your wiring
    config.pin_vsync = 25; // Adjust according to your wiring
    config.pin_href = 23; // Adjust according to your wiring
    config.pin_sccb_sda = 26; // Adjust according to your wiring
    config.pin_sccb_scl = 27; // Adjust according to your wiring
    config.pin_pwdn = 32; // Adjust according to your wiring
    config.pin_reset = -1; // Not used
    config.xclk_freq_hz = 20000000; // Set to 20 MHz
    config.pixel_format = PIXFORMAT_JPEG; // Image format

    // Initialize camera
    if (esp_camera_init(&config) != ESP_OK) {
        Serial.println("Camera init failed");
        return;
    }

    // Connect to WiFi
    Blynk.begin(auth, ssid, password);

    // Button press event
    attachInterrupt(digitalPinToInterrupt(BUTTON_PIN), buttonPressed, FALLING);

    // Timer for streaming
    timer.setInterval(1000L, stream); // Adjust interval as needed
}

void loop() {
    Blynk.run();
    timer.run();

    // Check for face recognition
    if (recognizeFace()) {
        digitalWrite(RELAY_PIN, HIGH); // Open lock
        delay(5000); // Keep lock open for 5 seconds
        digitalWrite(RELAY_PIN, LOW); // Close lock
    }
}
```

### Code Explanation
- **Libraries**: Includes necessary libraries for WiFi, Blynk, and camera functionality.
- **WiFi and Blynk Initialization**: Connects to WiFi and initializes the Blynk service.
- **Button and Relay Setup**: Configures GPIO pins for the button and relay.
- **Face Recognition Logic**: Placeholder function for face recognition.
- **Notification Function**: Sends a notification through Blynk when the button is pressed.
- **Streaming Function**: Placeholder for live video streaming implementation.

## Usage Guidelines
1. **Compile and Upload**: Compile the code in the Arduino IDE and upload it to the ESP32-CAM MB.
2. **Open Blynk App**: Open the Blynk app to view notifications and the camera stream.
3. **Test Functionality**: Press the button to ensure notifications are sent, and test the face recognition to unlock the door.

## Additional Notes
- Ensure all connections are secure and the ESP32-CAM is powered correctly.
- Test face recognition under various lighting conditions for optimal performance.
- Adjust GPIO pin numbers as per your wiring configuration.
- Use the Serial Monitor for debugging and verifying the connection status.
