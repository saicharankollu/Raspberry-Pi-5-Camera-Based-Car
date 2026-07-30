# Raspberry Pi 5 Camera-Based Car

A hybrid robotic car built using a **Raspberry Pi 5**, **Arduino Uno**, and **Raspberry Pi Camera Module 3**. The Raspberry Pi handles camera processing and keyboard input, while the Arduino controls the motors through an L298N motor driver using serial communication.

---

## Project Overview

This project demonstrates a hybrid embedded system where:

- Raspberry Pi 5 acts as the main controller.
- Arduino Uno controls the DC motors.
- Raspberry Pi Camera Module 3 provides a live camera preview.
- The car is controlled remotely from a laptop using keyboard inputs.

This architecture is useful when motor control is delegated to an Arduino while the Raspberry Pi handles high-level tasks such as camera processing, computer vision, and AI applications.

---

# Hardware Used

- Raspberry Pi 5
- Raspberry Pi Camera Module 3 (Wide)
- Arduino Uno
- L298N Motor Driver
- 2 × DC Geared Motors
- 2S Li-ion Battery Pack
- USB Cable
- Jumper Wires
- Robot Chassis

---

# Software Used

## Raspberry Pi

- Ubuntu / Raspberry Pi OS
- Python 3
- pySerial
- pynput
- xrdp (Remote Desktop)
- OpenSSH Server

## Camera Software

This project uses the official **rpicam-apps** package provided by Raspberry Pi.

Applications used:

- `rpicam-hello` – Live camera preview
- `rpicam-still` – Capture images (optional)
- `rpicam-vid` – Record videos (optional)

The camera is accessed using **libcamera**, which is the official camera framework for Raspberry Pi OS.

# System Architecture

```
Laptop
   │
Keyboard Input
   │
   ▼
Raspberry Pi 5
   │
USB Serial
   │
Arduino Uno
   │
L298N Motor Driver
   │
DC Motors

Raspberry Pi Camera Module 3
             │
             ▼
      Live Camera Preview
```

---

# Circuit Connections

## Arduino → L298N

| Arduino | L298N |
|----------|--------|
| D5 | ENA |
| D6 | ENB |
| D8 | IN1 |
| D9 | IN2 |
| D10 | IN3 |
| D11 | IN4 |
| GND | GND |

---

## L298N → Motors

| L298N | Motor |
|--------|-------|
| OUT1 & OUT2 | Left Motor |
| OUT3 & OUT4 | Right Motor |

---

## Power Connections

- Battery → L298N Motor Driver
- Arduino powered through USB from Raspberry Pi
- All grounds connected together

---

# Raspberry Pi Setup

## 1. Enable SSH

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

Connect from your laptop:

```bash
ssh <username>@<raspberry-pi-ip>
```

---

## 2. Enable Remote Desktop

Install XRDP if necessary.

```bash
sudo apt update
sudo apt install xrdp
```

Enable XRDP.

```bash
sudo systemctl enable xrdp
sudo systemctl restart xrdp
```

On Windows:

- Press **Win + R**
- Type:

```
mstsc
```

- Enter the Raspberry Pi IP address.
- Log in with your Raspberry Pi username and password.

You can now access the Raspberry Pi desktop remotely.

---

# Camera Setup

Open a terminal.

```bash
unset LD_LIBRARY_PATH
```

Start the live preview.

```bash
rpicam-hello -t 0
```

If the camera is connected correctly, a live preview window will appear.

---

# Installation

Clone the repository.

```bash
git clone https://github.com/saicharankollu/Raspberry-Pi-5-Camera-Based-Car.git
```

Move into the project directory.

```bash
cd Raspberry-Pi-5-Camera-Based-Car
```

Create a virtual environment.

```bash
python3 -m venv venv
```

Activate it.

```bash
source venv/bin/activate
```

Install dependencies.

```bash
pip install -r requirements.txt
```

---

# Running the Project

## Step 1

Connect the Arduino Uno to the Raspberry Pi using USB.

---

## Step 2

Activate the Python virtual environment.

```bash
source venv/bin/activate
```

---

## Step 3

Run the keyboard controller.

```bash
python3 raspberry_pi/keyboard_control.py
```

---

## Step 4

Open another terminal and launch the camera preview.

```bash
unset LD_LIBRARY_PATH
rpicam-hello -t 0
```

---

# Keyboard Controls

| Key | Action |
|------|--------|
| W | Move Forward |
| S | Move Backward |
| A | Turn Left |
| D | Turn Right |
| Release Key | Stop |
| Esc | Exit |

---

# Serial Commands

The Raspberry Pi sends the following commands to the Arduino.

| Command | Action |
|----------|--------|
| F | Forward |
| B | Backward |
| L | Left |
| R | Right |
| S | Stop |

---

# Author

**Sai Charan Kollu**

GitHub: https://github.com/saicharankollu

---

