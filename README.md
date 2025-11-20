# Bluetooth-Controlled Arduino Car

## Overview

I made this for my little cousin bc his parents wouldn't buy him a remote controlled car (so I made him one-- aren't i the best cousin ever?!?!?!!?!?)
This project is a Bluetooth-controlled robotic car built with an Arduino, an HC-05 Bluetooth module, and a dual-motor driver. The system is split into two parts:

* **Sender**: A handheld controller with a joystick and multiple buttons. It sends commands to the car over Bluetooth.
* **Receiver**: The car itself, which interprets Bluetooth commands and drives the motors accordingly.

This project demonstrates wireless communication, motor control, and basic robotics.

---

## Features

* **Bluetooth control** using HC-05 modules paired between sender and receiver
* **Joystick-based movement**: forward, backward, left, right
* **Stop command** when joystick returns to center
* **Simple DC motor driving** using H-bridge logic pins
* **Serial monitoring** for debugging

---

## Components Used

### Receiver (Car)

* Arduino Uno
* HC-05 Bluetooth module
* Dual DC motors with motor driver circuitry
* Motor driver pins:

  * Left motor: forward → pin 6, backward → pin 5
  * Right motor: forward → pin 8, backward → pin 9
* 2WD or 4WD robot chassis
* Battery pack

### Sender (Controller)

* Arduino Uno/Nano
* HC-05 Bluetooth module
* Analog joystick (x-axis → A0, y-axis → A1)
* Buttons (pins 2–7, 8 for joystick click)
* 9V battery or USB power

---

## How It Works

### 1. **Communication Flow**

Two HC-05 modules pair together. The sender reads joystick/button input and transmits characters to the receiver:

* `'W'` → move forward
* `'A'` → turn left
* `'S'` → move backward
* `'D'` → turn right
* `'o'` → stop

The receiver continuously checks for incoming characters and executes motor actions.

### 2. **Motor Driving Logic**

Each motor has two pins (forward/backward). Setting one pin HIGH and the other LOW determines direction.

### 3. **Joystick Mapping**

Certain analog values from the joystick correspond to movement directions:

* Up: (x ≈ 509, y = 1023) → `'W'`
* Right: (x = 1023, y ≈ 504) → `'D'`
* Left: (x = 0, y ≈ 504) → `'A'`
* Down: (x ≈ 509, y = 0) → `'S'`
* Center: send `'o'`

---

## Wiring Summary

### Receiver

* HC-05 TX → Arduino pin 11
* HC-05 RX → Arduino pin 10
* Left motor → pins 6 (forward), 5 (backward)
* Right motor → pins 8 (forward), 9 (backward)

### Sender

* HC-05 TX → pin 11
* HC-05 RX → pin 10
* Joystick X → A0
* Joystick Y → A1
* Buttons → pins 2–7
* Joystick click → pin 8

---

## Setup Instructions

1. Upload **sender code** to the controller Arduino.
2. Upload **receiver code** to the robot Arduino.
3. Configure HC-05 modules:
   * Example AT command found in code comments: `AT+ADDR: 98D3,41,F67628`
4. Power both devices and allow the HC-05 modules to pair.
5. Move the joystick to control the car.
