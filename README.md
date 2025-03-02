# ESP32-Ultrasonic-LED

# ESP32 Web Server with LED Control & Ultrasonic Sensor
This project sets up an ESP32 as a WiFi access point with a web server. The webpage allows users to:

- Toggle an LED on and off.
- View real-time distance measurements from an ultrasonic sensor (HC-SR04).

# Features:
- Control an LED remotely via a web interface.
- Display real-time ultrasonic sensor data.
- Auto-refresh the sensor data every second.

# Components Required:
- ESP32
- HC-SR04 Ultrasonic Sensor
- 220Ω resistor (for LED)
- LED
- Breadboard & Jumper wires

# Connections
<b>HC-SR04 - ESP32</b>
- VCC (Power)	- 5V
- GND (Ground) - GND
- Trig (Trigger) - GPIO 5
- Echo (Echo) - GPIO 18

<b> LED -	ESP32 </b>
- Anode (Long leg) - GPIO 35 (Through a 220Ω resistor)
- Cathode (Short leg)	- GND
