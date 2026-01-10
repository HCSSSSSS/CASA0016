# CASA0016
Indoor Air Quality Monitoring System

## Project Overview

This repository contains the source code, design files, and documentation for a modular indoor air safety monitoring terminal. The project addresses the need for accurate, real-time monitoring of indoor environmental quality, specifically focusing on ventilation efficiency and hazardous gas detection.

The system employs a sensor fusion approach by integrating an industrial-grade NDIR CO2 sensor (Sensirion SCD30) with a Metal-Oxide Semiconductor gas sensor (Pimoroni MiCS-6814). Unlike standard monitors that rely on estimated values, this device physically measures carbon dioxide concentration to assess metabolic saturation and detects reducing gases (CO/VOCs) to identify potential chemical hazards.

Key technical features include:
*   **Sensor Fusion:** Simultaneous processing of physical (optical) and chemical sensing data.
*   **Thermal Decoupling:** A custom enclosure design that utilizes the chimney effect to isolate temperature-sensitive components from heat-generating electronics.
*   **Non-blocking Architecture:** Firmware designed with asynchronous timers to ensure real-time responsiveness for the user interface and alarm systems.
*   **Tool-free Assembly:** A screwless, friction-fit 3D printed enclosure designed for manufacturability.

## System Architecture

The hardware architecture is built around the ESP32-WROOM-32D microcontroller, utilizing a shared I2C bus topology for communication with all peripherals. Power management is split between a 5V rail for sensor heating elements and a 3.3V rail for logic and display operations.


### Hardware Bill of Materials

| Component | Specification | Function |
| :--- | :--- | :--- |
| **Microcontroller** | ESP32-WROOM-32D (NodeMCU) | Central processing unit. |
| **CO2 Sensor** | Sensirion SCD30 | NDIR CO2, Temperature, and Humidity measurement. |
| **Gas Sensor** | Pimoroni MiCS-6814 Breakout | Detection of Carbon Monoxide (CO) and Nitrogen Dioxide (NO2). |
| **Display** | 0.96" OLED (SSD1306) | Real-time data visualization. |
| **Alarm** | Active Buzzer | Audible warning for critical safety thresholds. |
| **Enclosure** | PLA (Polylactic Acid) | Custom FDM 3D printed housing. |

### Pin Configuration

*   **I2C Bus (SDA):** GPIO 21
*   **I2C Bus (SCL):** GPIO 22
*   **Buzzer Output:** GPIO 13
*   **Sensor Power:** 5V (VIN)
*   **Display Power:** 3.3V

## Software Implementation

The firmware is developed using C++ within the PlatformIO ecosystem (VS Code).

### Core Logic
1.  **State Machine:** The system categorizes air quality into three states: FRESH, STUFFY, and DANGER.
2.  **Relative Gas Indexing:** To mitigate the baseline drift inherent in MOX sensors, the software implements a dynamic baseline algorithm. It calculates a relative index based on the ratio of the initial baseline resistance to the current resistance.
3.  **Alert System:** An audible alarm is triggered only upon a state transition to DANGER to avoid continuous noise disturbance.

### Dependencies
The project requires the following libraries, configured in `platformio.ini`:
*   `SparkFun SCD30 Arduino Library`
*   `Adafruit SSD1306`
*   `Adafruit GFX Library`
*   `IOExpander` (ZodiusInfuser) - Required for the Pimoroni Breakout module.

## Enclosure Design

The physical housing was designed in Autodesk Fusion 360 with a focus on functional engineering and ease of assembly.

*   **Mounting Strategy:** The internal structure uses rib-retention slots to secure the PCBs without adhesive or screws.
*   **Assembly:** The case utilizes a friction-fit pin-and-boss mechanism for a secure snap-fit closure.
*   **Airflow:** Ventilation intakes at the base and exhaust grills at the top facilitate passive convection, ensuring sensors are exposed to fresh air.


## Repository Structure

*   `/src`: Contains the main C++ source code (`main.cpp`).
*   `/stl`: Contains the `.stl` files for 3D printing (Base and Lid).
*   `/images`: Documentation images and schematics.
*   `platformio.ini`: Configuration file for the build environment and library dependencies.

## Installation and Replication

1.  **Clone the Repository:** Download this repository to your local machine.
2.  **Hardware Assembly:** Wire the components according to the pin configuration provided above.
3.  **Software Setup:**
    *   Open the project folder in Visual Studio Code.
    *   Ensure the PlatformIO extension is installed.
    *   PlatformIO will automatically download the required libraries defined in `platformio.ini`.
4.  **Upload:** Connect the ESP32 via USB and upload the firmware.
5.  **Warm-up Procedure:** Upon first power-up, allow the device to run for approximately 20 minutes to allow the MOX sensor heater to stabilize.

## Video Presentation
### [Click here  watch the demo for Testing CO2] https://github.com/HCSSSSSS/CASA0016/releases/tag/Demo1

### [Click here  watch the demo for Testing CO] https://github.com/HCSSSSSS/CASA0016/releases/tag/CO
