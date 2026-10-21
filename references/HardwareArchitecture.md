# Document for Hardware Architecture (WORK IN PROGRESS)

*Here we will have a hardware overview of the project,
This will help us to break down the schematic and eventually
PCB design into more digestable pieces.*
*...* indicates that more needs to be added



## System Architecture

*This is for the system as a whole broken down into the potential components that we will need for the main computer module*

## Blocks
*List of Blocks*

### CORE
- MCU
- Power System
- IMU(Gyroscope + Accelerometer)
- GPS
- Storage System(data) - SD Card?
- Parachute System
- Barametric Sensor
- Radio
- *Payload Electronics

### REDUNDANT
- MCU
- Pyro Channels

## Boards

- Off the shelf :(  - Back-up
    - battery
    - other dumb stuff :(


- Core Stack
    - Power Board
        - Power System
        - Battery(1 of 2)
        - Pyro Channels (Drogue, Drogue redundant, Parachute, Parachute redundant, *Payload, Payload redundant*) *Off the shelf fires redundant pryo channels*
    - Control Board
        - MCU
        - IMU
        - Barrometer
        - Micro SD Card
    - Communication Board
        - GPS
        - Radio
        - Telemetry

- Extra Boards
    - Payload... Conversations will be had
    - Redundancy board(s)
        - Control
        - Power
        - ...




## Blocks I/O
Overview of each blocks input and outputs

- MCU
    - Inputs
        - Power (3.3V + GND) *MAYBE 5V*
        - I2C (SCL SDA) - Common Bus
            - IMU
            - GPS Module
            - Off the shelf Flight computer
            - Radio
            - *Payload Electronics*
            - Storage System
            - ...
        - SPI (MOSI MISO SCK CS)
            - If needed
            - ...
            *Some modules that we buy may use SPI instead of I2C so it is important to be able to support both*
        - ...
    - Outputs
        - Power (3.3 + GND)
        - I2C (SCL SDA) - Common Bus
            - IMU (Mostly for initialization and requesting data if thats needed)
            - Radio
            - Parachute System
            - Storage System
            - ...
        - SPI
            - ...
        - ...
    - Inside
        - ...
    *Design Notes:*
    We should pick the peripherals that we want to use with the MCU before selecting which MCU to use. This way we can pick one with enough SPI, I2C, GPIO channels. This makes it much easier to implement.

- Power System
    - Inputs
        - Battery PWR and GND
        - ...
    - Outputs
        - 3.3V and GND
        - *MAYBE* 5V if needed
    - Insides
        - Reverse polarity protection
            - Likely just some diodes reverse polarity mosfets most likely uneccesary here
        - Overvoltage protection
            - Zener(clamping) diode
            *VERY IMPORTANT* when we are designing our electronics every component MUST have a voltage rating above our `Zener Diode's Breakdown Voltage`. We will go over why this is but for now use it as a rule of thumb especially because we are dealing with battery power. 
# Diagram
    


