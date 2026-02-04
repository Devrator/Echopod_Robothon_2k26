# ECHOPOD – ESP32 Ultrasonic Assistive Device

ECHOPOD is an indoor navigation assistive device designed for visually impaired users. It uses three ultrasonic sensors mounted at the front, left, and right to detect nearby obstacles and provides direction-wise vibration feedback using vibration motors.

## 🔧 Features
- Three ultrasonic sensors (Front, Left, Right)
- Directional vibration feedback
- Distance-based vibration frequency
- Faster vibration as obstacle comes closer
- Continuous vibration for very close objects
- Serial monitoring for debugging
- No buzzer (silent, vibration-only feedback)

## 🧠 Working Principle
Each ultrasonic sensor measures the distance to nearby obstacles.  
- If no obstacle is detected within range, the motor remains OFF.
- As an obstacle enters the warning range, the corresponding motor starts vibrating.
- The vibration frequency increases as the obstacle distance decreases.
- When the obstacle is very close, the motor vibrates continuously.

This step-less frequency change helps users intuitively judge how close an obstacle is.

## 🧩 Hardware Components
- ESP32 Development Board
- 3 × HC-SR04 Ultrasonic Sensors
- 3 × Vibration Motors
- 3 × NPN Transistors (BC547 / 2N2222)
- Flyback Diodes (1N4007)
- Resistors (1kΩ)
- External Power Source / Boost Converter

## 🔌 Pin Configuration

### Ultrasonic Sensors
| Direction | TRIG | ECHO |
|---------|------|------|
| Front | GPIO 5 | GPIO 18 |
| Left  | GPIO 17 | GPIO 19 |
| Right | GPIO 16 | GPIO 21 |

### Vibration Motors
| Direction | GPIO |
|---------|------|
| Front | GPIO 25 |
| Left  | GPIO 26 |
| Right | GPIO 27 |

> ⚠️ Motors must be driven via transistors. Do not connect directly to ESP32 pins.

## ⚙️ Software
- Language: Embedded C++
- Platform: Arduino IDE
- Core Functions Used:
  - `pulseIn()`
  - `digitalWrite()`
  - `delayMicroseconds()`
  - `map()`

## 🖥️ Serial Output
The system prints warning messages when obstacles are detected within the defined range:

## THE PROJECT IS DEVLOPED BY
- Daksh Saini
- Mr.Deepak Sharma
- Chitvansh Agrawal
- Harshita Chauhan
