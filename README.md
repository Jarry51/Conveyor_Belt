# Conveyor Belt Controller

An Arduino-based conveyor belt system that moves items along a belt using a DC gear motor, with adjustable speed and automatic item counting.

## Overview

This project controls a small conveyor belt using an Arduino and an L298N motor driver. The user starts and stops the belt with a push button, adjusts the belt speed with a potentiometer, and an IR sensor detects and counts every item that passes. The item count is printed in real time to the Serial Monitor.

## Features

- Push-button start/stop with debouncing
- Adjustable belt speed using PWM, controlled by a potentiometer
- IR sensor that detects and counts items passing along the belt
- Real-time item count and belt status over serial output
- Minimum speed limit so the motor does not stall at low settings

## Components

| Component | Purpose |
|---|---|
| Arduino Uno | Main controller |
| L298N motor driver | Drives the DC motor |
| DC gear motor | Moves the conveyor belt |
| IR obstacle sensor | Detects and counts items |
| Push button | Start/stop |
| Potentiometer | Speed control |
| External 6-12V power supply | Powers the motor |

## Wiring

| Part | Arduino Pin |
|---|---|
| L298N ENA | D9 (PWM) |
| L298N IN1 | D7 |
| L298N IN2 | D8 |
| IR sensor OUT | D2 |
| Push button (other leg to GND) | D3 |
| Potentiometer middle pin | A0 |

Connect the L298N GND to the Arduino GND, and power the motor from a separate supply.

## How It Works

1. The button toggles the belt between running and stopped.
2. While running, the Arduino reads the potentiometer and maps it to a PWM value (80 to 255) that sets the motor speed.
3. The IR sensor goes LOW when an item passes. Each detection adds 1 to the item counter, and a debounce delay prevents double counting.
4. Belt status and item count are printed to the Serial Monitor at 9600 baud.

## How to Run

1. Install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Wire the components using the table above.
3. Open `conveyor_belt.ino` in the Arduino IDE.
4. Select your board and port under **Tools**.
5. Click **Upload**.
6. Open the Serial Monitor (9600 baud).
7. Press the button to start the belt, turn the potentiometer to change speed, and pass an object in front of the IR sensor to see the count increase.

## Troubleshooting

- **Belt runs backwards:** swap the IN1 and IN2 values in the code.
- **Counts twice per item:** increase `IR_DEBOUNCE_MS`.
- **Counts nothing:** your IR module may be active HIGH, so change `ir == LOW` to `ir == HIGH`.

## Future Improvements

- Add an LCD to show the item count
- Add a stepper motor or encoder for precise movement
- Send count data to a dashboard using an ESP32

## Author

Jarmaine Abdul ([@Jarry51](https://github.com/Jarry51)) 
