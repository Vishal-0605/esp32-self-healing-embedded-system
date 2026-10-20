# ESP32 Self-Healing Embedded System for Motor Monitoring

An embedded systems project exploring fault detection and parameter estimation to improve the reliability of motor monitoring and control applications.

## Project Overview

This project implements a self-healing monitoring concept using an ESP32 microcontroller. It monitors three important parameters of a motor-driven system: rotational speed, temperature, and supply voltage.

The system checks sensor readings for abnormal values, missing signals, and other fault conditions. When a single sensor fails, the system attempts to estimate the unavailable parameter using relationships between the remaining measurements.

The project also explores PWM-based motor speed control using an L298N motor driver.

## Key Features

- **Real-time monitoring:** Reads motor speed, temperature, and supply voltage.
- **Fault detection:** Identifies missing, invalid, or abnormal sensor readings.
- **Parameter estimation:** Estimates a missing measurement when sufficient related sensor data is available.
- **PWM motor control:** Controls a DC motor using the ESP32 and L298N driver.
- **Sensor signal processing:** Uses pulse counting, ADC conversion, averaging, and debouncing.
- **Fault handling:** Identifies conditions where estimation is not possible because multiple sensors have failed.

## Hardware Components

| Component | Purpose |
|---|---|
| ESP32 development board | Main controller and data processing |
| DC motor | Motor-drive test system |
| L298N motor driver | Motor interfacing and speed control |
| LM393 IR speed sensor | Generates pulses for RPM measurement |
| LM35 temperature sensor | Measures temperature |
| 0–25 V voltage sensor module | Monitors supply voltage |
| Power supply | Powers the circuit |
| Breadboard and connecting wires | Hardware interconnections |

## System Architecture

The system follows this processing flow:

1. Acquire speed, temperature, and voltage measurements.
2. Validate the sensor readings.
3. Detect abnormal or missing measurements.
4. Estimate an unavailable parameter using the remaining valid measurements, where possible.
5. Report measured and estimated values through the Serial Monitor.
6. Handle multiple-sensor failures when reliable estimation is unavailable.

## Self-Healing Logic

The project uses the concept of **analytical redundancy**: relationships between physical parameters help estimate measurements that are temporarily unavailable.

Examples described in the project report:

- **Temperature sensor failure:** Estimate temperature using motor speed and voltage.
- **Voltage sensor failure:** Estimate voltage using the relationship between motor speed and supply voltage.
- **Multiple sensor failures:** Recognize when the remaining information is insufficient for estimation.

These estimates depend on the model and operating conditions; they are not guaranteed to match actual measurements under every load or operating condition.

## Fault Scenarios Tested

The project report documents tests involving:

- Normal operation with all sensors working.
- Temperature sensor failure.
- Voltage sensor failure.
- Simultaneous speed and voltage sensor failure.
- Simultaneous speed and temperature sensor failure.
- Simultaneous temperature and voltage sensor failure.
- Failure of all sensors.

The tests illustrate both the potential of sensor-fault compensation and its limitations when multiple measurements become unavailable.

## Technologies and Concepts

- Embedded C
- ESP32 microcontroller
- Arduino IDE
- Analog-to-digital conversion (ADC)
- Pulse counting and RPM calculation
- Pulse-width modulation (PWM)
- Sensor interfacing and signal filtering
- Fault detection and parameter estimation
- Embedded system debugging

## Repository Structure

The repository will be organized as the project files are recovered and verified:

- `README.md` — Project overview and documentation
- `docs/` — Block diagram and technical documentation
- `images/` — Hardware setup and test results

## Applications

Potential application areas include industrial motor monitoring, automation, robotics, predictive maintenance, and smart equipment monitoring.

## Limitations and Future Improvements

- Calibrate estimation models against measured operating data.
- Improve fault detection to reduce false alarms.
- Test performance under different motor loads and operating conditions.
- Add data logging and diagnostic reporting.
- Establish safe behavior when sensor data is insufficient for reliable estimation.

## Project Context

Academic team project completed for the Embedded C Programming course at VIT Chennai during the 2025–2026 academic year.

## Disclaimer

This project is an educational prototype. Estimated values should not be treated as certified measurements or used as the sole basis for safety-critical motor control.
