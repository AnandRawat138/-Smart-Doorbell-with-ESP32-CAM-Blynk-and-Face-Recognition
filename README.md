Introduction

The smart doorbell project combines the ESP32-CAM module with Blynk cloud connectivity, a push button, and a solenoid lock to enhance home security. This project allows the user to receive notifications on their phone when someone presses the doorbell, automatically unlock the door using face recognition, and remotely control the lock from the Blynk app. It provides an efficient and affordable solution for managing home access through modern IoT technology.

Components Used

- ESP32-CAM MB: A low-cost module with a built-in camera (OV2640) and Wi-Fi capability.
- OV2640 Camera: Camera module used for live video streaming and face recognition.
- Push Button: Trigger for the doorbell mechanism, connected to the ESP32-CAM.
- Solenoid Lock: Electric lock controlled by the ESP32-CAM via a relay.
- Relay Module: Used to switch the solenoid lock on or off.
- Power Supply: Provides the required voltage for the ESP32-CAM, relay, and solenoid lock.
- Blynk Cloud: Platform for IoT control and real-time notifications.
- Blynk App: Mobile interface for notifications and controlling the door lock remotely.

Features and Functionality

1 Doorbell Press Notifications:

- A push button is used to detect when someone presses the doorbell.
- When the button is pressed, the ESP32-CAM sends a notification to the user’s smartphone via the Blynk app.

2 Face Recognition for Automated Lock Control:

- The ESP32-CAM utilizes its built-in face recognition capability to detect known faces.
- If a recognized face is detected, the solenoid lock is activated, allowing the door to be unlocked.

3 Remote Control via Blynk App:

- The Blynk app allows the user to remotely control the solenoid lock. This is useful for unlocking the door manually from the app if a guest arrives.
- The app can also display a live video stream from the ESP32-CAM, adding an additional layer of security.

4 Real-Time Security:

- The ESP32-CAM can continuously monitor for face recognition and notify the user when someone is at the door.
- The user can unlock the door manually or let the system automatically unlock the door for recognized visitors.

Circuit Diagram

Below is the explanation for the connection setup of components:

1 ESP32-CAM MB:

- GPIO 12: Connected to the push button for doorbell press detection.
- GPIO 14: Connected to the relay module, which controls the solenoid lock.
- 5V and GND: Power connections for the ESP32-CAM MB and relay module.

2 Relay Module:

- The relay is used to switch the solenoid lock on or off.
- One side of the relay is connected to the solenoid lock, and the other side is connected to ESP32-CAM GPIO 14.

3 Power Supply:

A 5V or 12V power supply is needed to power the ESP32-CAM and solenoid lock.

System Workflow

1 Button Press:

- When the button connected to the ESP32-CAM MB is pressed, the system detects this event and sends a notification via the Blynk platform. The notification is received in real-time on the user’s smartphone. 

2 Face Recognition:

- The ESP32-CAM continuously captures images using the OV2640 camera. The face recognition algorithm processes these images to check if the detected 
   face matches any of the stored known faces.
- If the face is recognized, the ESP32-CAM sends a signal to the relay, activating the solenoid lock and unlocking the door.

3 Remote Lock Control:

- The Blynk app offers manual control over the solenoid lock. The user can press a button on the app interface to unlock the door remotely.
- Additionally, a live feed from the camera can be displayed on the app, allowing the user to monitor the door remotely.

Software Implementation

1 Blynk Setup:

- The user needs to create a new project in the Blynk app and add a button widget for controlling the lock, and configure the notification settings.
- Virtual pins are used to send notifications and handle the relay control.

2 Face Recognition:

- The ESP32-CAM comes with built-in face detection and recognition features through the esp-face library.
- The program continuously processes frames from the camera to detect faces. Once a match is found, the relay is activated to unlock the solenoid lock.

3 Code Overview:

Code is attached with project as file name Code.ino

4Blynk Notifications and Lock Control:

- The Blynk notification function (Blynk.notify()) is used to send alerts to the mobile app when the doorbell button is pressed.
- A virtual pin can be assigned in the Blynk app to manually trigger the relay, unlocking or locking the door remotely.

Challenges and Solutions

1 Wi-Fi Connectivity:

- Since the ESP32-CAM relies on Wi-Fi, unstable connections can lead to delays in notifications or control.
- Solution: Ensure the doorbell is placed within a strong Wi-Fi signal range, or consider using a Wi-Fi repeater.

2 Face Recognition Accuracy:

- The face recognition feature may not always be 100% accurate under varying lighting conditions.
- Solution: Optimize camera placement for consistent lighting, or integrate additional sensors (e.g., PIR motion sensors) to improve accuracy.

3 Power Supply Considerations:

- The ESP32-CAM and solenoid lock require a stable power supply, especially the solenoid lock, which might draw significant current.
- Solution: Use a reliable power supply that meets the voltage and current requirements of all components.

Conclusion

This smart doorbell system is an excellent demonstration of the power of IoT technology, combining face recognition, real-time notifications, and remote control via a smartphone. It enhances home security and convenience by allowing the homeowner to monitor their front door and unlock the door for known visitors automatically.

With further improvements, such as adding more secure face recognition algorithms or integrating additional sensors for detecting motion, this system could be extended into a more comprehensive home automation solution.
