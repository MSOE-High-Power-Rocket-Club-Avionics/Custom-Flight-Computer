# IMU and Barometer

**Issue:** TBD

## Function

Measure acceleration, angular rate and atmospheric pressure, and send the measurements to the MCU.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| 3V3 / GND | Power block | Verify selected sensor supply/logic requirements |
| SENSOR_SCL | MCU | I2C clock |
| SENSOR_SDA | MCU | I2C configuration/commands; bidirectional |
| Ambient pressure | Enclosure vent | Pressure access for the barometer |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| SENSOR_SDA | MCU | I2C sensor data; bidirectional |
| IMU_INT / BARO_INT | MCU | Optional interrupts; polarity: TBD |
