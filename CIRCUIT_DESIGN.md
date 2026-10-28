# 🔌 Circuit Design and Simulation

## Overview

The Smart Home Automation System circuit was designed using [Cirkit Designer](https://app.cirkitdesigner.com/project/16c253a6-4140-4000-9674-1d9d3eeca3b8), an online electronics design environment.

The circuit integrates an ESP32 microcontroller with motion, gas, and vibration sensors to demonstrate a smart home safety and automation system.

## Circuit Design Link

**Open the interactive circuit design:** [Smart Home Automation Circuit – Cirkit Designer](https://app.cirkitdesigner.com/project/16c253a6-4140-4000-9674-1d9d3eeca3b8)

Use this link to access the circuit project in Cirkit Designer.

## Components Included

- **ESP32 Development Board:** Processes sensor signals and manages system operations.
- **PIR Motion Sensor:** Detects movement for motion-based lighting.
- **MQ-2 Gas Sensor:** Monitors gas and smoke-related changes.
- **SW-420 Vibration Sensor:** Detects vibrations and physical disturbances.
- **LED:** Provides visual indication when motion is detected.
- **Buzzer:** Produces audible alerts for configured hazard conditions.
- **Resistors and Jumper Wires:** Support current limiting and circuit connections.

## Working Principle

1. The sensors monitor motion, gas levels, and vibration.
2. The ESP32 reads the sensor signals and evaluates predefined conditions.
3. The LED and buzzer respond according to the programmed control logic.
4. The ESP32 can transmit sensor readings to ThingSpeak over Wi-Fi for remote monitoring.

## Purpose of the Circuit

The circuit provides a hardware-level representation of the Smart Home Automation System and helps illustrate the connections between the microcontroller, sensors, and output devices.

For the complete project overview, implementation details, and results, refer to the main [`README.md`](README.md).
