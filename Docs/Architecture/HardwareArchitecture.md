# Hardware Architecture

**Status: Work in Progress**

## 1. Purpose

This document provides a hardware overview of the project. It breaks the system into manageable components to guide schematic development and PCB design.

`...` indicates that more information needs to be added. Items marked **Tentative** require further discussion or confirmation.

## 2. Hardware Requirements

### 2.1 Core Hardware

- Microcontroller (MCU)
- Battery power system
- Inertial measurement unit (IMU): gyroscope and accelerometer
- GPS module
- Data storage: SD card
- Parachute deployment system: parachutes and pyro channels
- Barometric pressure sensor
- RF radio
- **Tentative:** Payload electronics

### 2.2 Redundant Hardware

- MCU
- Pyro channels

## 3. System Architecture

The proposed architecture divides the main flight computer into a core board stack, additional boards, and an off-the-shelf backup flight computer.

### 3.1 Core Board Stack

#### Power Board

- Power regulation and protection
- Battery connection: one of two batteries
- Pyro channels:
  - Drogue
  - Redundant drogue
  - Main parachute
  - Redundant main parachute
  - **Tentative:** Payload
  - **Tentative:** Redundant payload

**Design note:** The current proposal assigns redundant pyro-channel firing to the off-the-shelf backup flight computer. Board connections and responsibilities remain to be confirmed.

#### Control Board

- MCU
- IMU
- Barometric pressure sensor
- microSD card

#### Communication Board

- GPS module
- RF radio
- Telemetry interfaces

### 3.2 Additional Boards

- Payload board: requirements and implementation to be discussed...
- Redundancy board(s):
  - Control
  - Power
  - ...

### 3.3 Off-the-Shelf Backup Flight Computer

- Dedicated battery
- Additional required components and connections...

## 4. Hardware Block Interfaces

This section describes each block's power connections, signal interfaces, and supporting circuitry. Interface assignments are preliminary until specific components are selected.

### 4.1 MCU Block

#### Power Input

- 3.3 V and GND
- **Tentative:** 5 V supply, depending on the selected MCU or module
- ...

#### Communication Interfaces

These interfaces support both transmitting and receiving data, so they are listed together rather than duplicated under inputs and outputs.

**I2C — SCL and SDA**

Potential devices on the common bus, subject to interface compatibility:

- IMU: configuration, initialization, and data acquisition
- GPS module
- Off-the-shelf backup flight computer
- RF radio
- **Tentative:** Payload electronics
- Storage system, if supported by the selected device
- ...

**SPI — MOSI, MISO, SCK, and CS**

- Devices that require SPI instead of I2C
- SD Card
- ...

**Design note:** Support both I2C and SPI when selecting the MCU, since the interfaces required will depend on the selected modules.

#### Control Outputs

- Parachute deployment system: control interface to be determined
- ...

#### Power Distribution Connections

- 3.3 V and GND connections for peripherals, supplied by the power system
- ...

#### Supporting Circuitry and Configuration

- Resistors and capacitors required by the selected MCU's specifications
- I2C channel configuration
- ...

#### MCU Selection Notes

Select the required peripherals and identify their interfaces before choosing the MCU. Use those requirements to determine the necessary number of SPI, I2C, and GPIO connections.

### 4.2 Power System Block

#### Inputs

- Battery power and GND
- ...

#### Outputs

- Regulated 3.3 V and GND
- **Tentative:** Regulated 5 V, if required

#### Protection and Supporting Circuitry

- Reverse-polarity protection
  - Initial proposal: diode-based protection
  - MOSFET-based protection: evaluate whether it is necessary
- Overvoltage protection
  - Initial proposal: Zener clamping diode

#### Power Design Notes

Component voltage ratings and the protection circuit must be reviewed together. The Zener diode's nominal breakdown voltage alone does not establish the maximum voltage that connected components may experience; the actual clamping voltage and operating conditions also need to be considered.

...

## 5. System Diagram

...
