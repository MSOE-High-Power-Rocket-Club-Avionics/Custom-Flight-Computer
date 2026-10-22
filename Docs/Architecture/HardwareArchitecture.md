# Hardware Architecture

**Status: Work in Progress**

## 1. Purpose

This document provides a hardware overview of the project. It breaks the system into manageable components to guide schematic development and PCB design.

`...` indicates that more information needs to be added. Items marked **Tentative** require further discussion or confirmation.

## 2. Hardware Requirements

### 2.1 Core Hardware

- STM32 microcontroller (MCU)
- Battery power system
- Inertial measurement unit (IMU): gyroscope and accelerometer
- GPS module
- Data storage: SD card
- Parachute deployment system: parachutes and pyro channels
- Barometric pressure sensor
- RF radio
- Battery-voltage sensing
- Visual and audible status indicators
- **Tentative:** Payload electronics

### 2.2 Redundant Hardware

- MCU
- Pyro channels

## 3. System Architecture

The proposed architecture divides the main flight computer into a core board stack, additional boards, and an off-the-shelf backup flight computer.

### 3.1 Core Board Stack

- Three-board stack
- Target board diameter: Pending but around 2.4 inches diameter
- Mounting pattern, stack spacing, connector positions, and enclosure clearances...

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

- STM32 MCU
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

Directions below are relative to the block being described. Power and ground connections are listed separately from signal interfaces. STM32 is the selected MCU family; device-specific pins and electrical limits must match the final components.

The working interface allocation is I2C for the IMU and barometer, UART for GPS, and SPI for telemetry and storage. Update these assignments if the selected devices require a different interface. Digital sensor data does not require MCU ADC conversion; the ADC is used for analog signals such as battery-voltage sensing.

### 4.1 MCU Block — STM32

#### Inputs

- Regulated 3.3 V and GND
- SPI MISO: data from telemetry and storage devices
- UART RX: position and status data from the GPS module's TX pin
- ADC: scaled battery-voltage signal from the power system
- GPIO/interrupt inputs:
  - IMU and barometer interrupts, if supported
  - Telemetry IRQ and BUSY, if supported
  - Deployment-channel continuity and arming status, using suitable digital or analog feedback
- ...

#### Outputs

- SPI MOSI, SCK, and device-specific CS signals
- UART TX: configuration or commands to the GPS module's RX pin
- GPIO: deployment-driver commands and telemetry reset
- GPIO/PWM: LED and buzzer control, as required by the selected indicators
- ...

#### Bidirectional Interfaces

- I2C SDA and SCL: common bus for the IMU and barometer
  - SDA carries commands and sensor data.
  - With STM32 as controller, SCL provides the bus clock; it is an open-drain line and may also be affected by target clock stretching.
- SWD programming/debug: SWDIO, SWCLK, reference voltage, GND, and reset access
- **Tentative:** Payload communication...

#### Supporting Circuitry and Configuration

- Decoupling, reset, clock, and boot circuitry required by the selected STM32
- I2C pull-ups to the appropriate logic supply
- SPI chip-select allocation and inactive-state behavior
- UART, ADC, GPIO, and interrupt assignments
- Programming connector and test access
- ...

#### Design Notes

Confirm the selected STM32 has enough interfaces and pins for the assigned peripherals. Record exact pin mappings and alternate functions as the schematic develops.

Peripheral power comes from the power system, not MCU GPIO. A possible 5 V system rail must not be treated as an STM32 supply or assumed compatible with every signal pin.

### 4.2 Power System Block

#### Inputs

- BAT+ and BAT− from the battery
- ...

#### Outputs

- Regulated 3.3 V and GND for system electronics
- Pyro supply and its defined return connection
- VBat sense: scaled battery-voltage signal to an MCU ADC input
- **Tentative:** Regulated 5 V, if required by a selected peripheral
- ...

#### Protection and Supporting Circuitry

- Voltage regulation, likely using a buck converter where appropriate for battery and rail voltages
- Regulator inductors, resistors, and capacitors selected from the regulator's design requirements
- Reverse-polarity protection
  - Initial proposal: diode-based protection
  - MOSFET-based protection: evaluate whether it is necessary
- Overvoltage protection
  - Initial proposal: Zener clamping diode
- Battery-voltage sensing divider and any required filtering/protection
- Battery connector, rail test points, and power distribution
- Battery chemistry, capacity, cell configuration, and connector details...

#### Power Design Notes

Component voltage ratings and the protection circuit must be reviewed together. The Zener diode's nominal breakdown voltage alone does not establish the maximum voltage that connected components may experience; actual clamping voltage and operating conditions also need to be considered.

Scale VBat sense to remain within the selected ADC's limits throughout the battery operating range. Battery voltage supports monitoring but is not a direct measurement of remaining capacity.

...

### 4.3 IMU Block

#### Inputs

- 3.3 V and GND, subject to the selected device's supply requirements
- I2C SCL: clock from the MCU
- Configuration commands through I2C SDA

#### Outputs

- Accelerometer and gyroscope data through I2C SDA
- Optional data-ready or interrupt signal to the MCU

#### Bidirectional Interfaces

- I2C SDA: commands and returned sensor data

#### Supporting Circuitry and Notes

- Decoupling and address configuration as required by the selected device
- Defined mounting orientation and axis mapping
- Gyroscope measures angular rate; accelerometer measures specific force. Orientation estimation is a software function using sensor data.
- Selected sensor, measurement ranges, sample rates, and interrupt use...

### 4.4 Barometric Sensor Block

#### Inputs

- 3.3 V and GND, subject to the selected device's supply requirements
- I2C SCL: clock from the MCU
- Configuration commands through I2C SDA
- Ambient pressure through the enclosure's venting arrangement

#### Outputs

- Pressure and, if supported, temperature data through I2C SDA
- Optional data-ready or interrupt signal to the MCU

#### Bidirectional Interfaces

- I2C SDA: commands and returned sensor data

#### Supporting Circuitry and Notes

- Decoupling and address configuration as required by the selected device
- Pressure data used by software to estimate altitude
- Selected device, sample rate, and venting details...

### 4.5 GPS / GNSS Block

#### Inputs

- 3.3 V and GND, subject to the selected module's supply requirements
- UART RX on the GPS module, connected to MCU TX
- RF signal from the GNSS antenna

#### Outputs

- UART TX on the GPS module, connected to MCU RX: position, time, and receiver status as supported
- ...

#### Supporting Circuitry and Notes

- Antenna connection and any supply/filtering required by the selected module and antenna
- Confirm supply voltage and UART logic levels independently
- Selected module, antenna placement, and update rate...

### 4.6 Telemetry / RF Radio Block

#### Inputs

- 3.3 V and GND, subject to the selected radio's supply requirements
- SPI MOSI, SCK, and CS from the MCU
- RESET command from the MCU
- Received RF signal through the telemetry antenna

#### Outputs

- SPI MISO to the MCU
- IRQ and BUSY to the MCU, if supported by the selected radio
- Transmitted RF signal through the telemetry antenna

#### Supporting Circuitry and Notes

- Radio module or transceiver, antenna connection, and associated power/RF circuitry
- GNSS reception and telemetry have separate RF interface requirements; finalize the antenna arrangement with the selected devices
- Selected radio, operating band, antenna placement, and ground receiver...

### 4.7 Data Storage Block

#### Inputs

- 3.3 V and GND
- SPI MOSI, SCK, and CS from the MCU

#### Outputs

- SPI MISO to the MCU: returned data and status
- **Tentative:** Card-detect signal, if provided by the socket

#### Supporting Circuitry and Notes

- microSD socket with decoupling and signal biasing as required
- Working interface: SPI
- **Tentative:** Additional flash storage, if needed
- Storage capacity, write-rate requirements, and socket details...

### 4.8 Pyro Channel Block

#### Inputs

- Pyro supply and return
- GPIO control commands from the responsible flight computer
- Arming input
- ...

#### Outputs

- Switched deployment connections for the assigned channels
- Continuity feedback to the responsible flight computer
- Arm-status feedback to the responsible flight computer
- ...

#### Supporting Circuitry and Notes

- Driver, protection, and sensing circuitry between MCU logic and deployment connections
- MCU GPIO provides a control signal; it does not directly power an initiator
- Channel ownership, feedback signal levels, and arming connections must be documented
- The off-the-shelf backup retains the redundant-channel responsibility described in Section 3; these are not implicitly additional outputs of the core STM32
- Detailed circuit design and test interfaces...

### 4.9 Indicators Block

#### Inputs

- 3.3 V and GND, subject to the selected indicators' requirements
- GPIO/PWM commands from the MCU

#### Outputs

- Visible light from status LEDs
- Audible sound from a buzzer or other selected sounder

#### Supporting Circuitry and Notes

- LED current-limiting resistors and drivers where required
- Buzzer driver if required by load current or sounder type
- Indicator placement, status meanings, and exact components...

## 5. System Diagram

...
