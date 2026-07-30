# Raspberry-Pi-5-Camera-Based-Car
A Raspberry Pi 5 and Arduino Uno based robotic car that streams live video from the Raspberry Pi Camera while allowing real-time keyboard control from a laptop. The Raspberry Pi handles the high-level control, while the Arduino controls the motors through an L298N motor driver.

---

## Hardware Used

- Raspberry Pi 5
- Raspberry Pi Camera Module 3
- Arduino Uno
- L298N Motor Driver
- 2 × DC Geared Motors
- 2S Li-ion Battery Pack
- Arduino uno Cable (Pi ↔ Arduino)
- Jumper Wires
- Chassis and Wheels
- Power Bank 

---

# System Architecture

```
Laptop
   │
Keyboard Controls
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

Raspberry Pi Camera
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
| OUT1, OUT2 | Left Motor |
| OUT3, OUT4 | Right Motor |

---

## Power

- Battery → L298N
- Arduino powered via USB from Raspberry Pi
- Common ground between Arduino and L298N
- Power the Pi using Power Bank 

---

# Raspberry Pi Setup

## 1. Enable SSH

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

Connect from your laptop using:

```bash
ssh <username>@<raspberry-pi-ip>
```

---

## 2. Enable Remote Desktop

Install xrdp if it is not already installed.

```bash
sudo apt update
sudo apt install xrdp
```

Enable and start the service:

```bash
sudo systemctl enable xrdp
sudo systemctl restart xrdp
```

On Windows:

1. Press **Win + R**
2. Type

```
mstsc
```

3. Enter your Raspberry Pi IP address.
4. Log in using your Raspberry Pi username and password.

You should now see the Raspberry Pi desktop remotely.

---

# Camera Setup

Open a terminal on the Raspberry Pi.

Run:

```bash
unset LD_LIBRARY_PATH
```

Then start the camera preview:

```bash
rpicam-hello -t 0
```

A live preview window should appear.

---

# Install Python Dependencies

Clone the repository.

Create a virtual environment.

```bash
python3 -m venv venv
```

Activate it.

```bash
source venv/bin/activate
```

Install the required packages.

```bash
pip install -r requirements.txt
```

---

# Running the Project

## Step 1

Connect the Arduino to the Raspberry Pi using a USB cable.

---

## Step 2

Open a terminal and activate the virtual environment.

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

Open another terminal.

Launch the camera preview.

```bash
unset LD_LIBRARY_PATH
rpicam-hello -t 0
```

---

# Keyboard Controls

| Key | Action |
|------|--------|
| W | Forward |
| S | Backward |
| A | Left |
| D | Right |
| Release Key | Stop |
| Esc | Exit Program |

---

# Serial Communication

The Raspberry Pi sends the following commands to the Arduino.

| Command | Action |
|----------|--------|
| F | Forward |
| B | Backward |
| L | Left |
| R | Right |
| S | Stop |

---

## Author

**Sai Charan Kollu**
