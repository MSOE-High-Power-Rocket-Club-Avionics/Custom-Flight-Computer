# STM32 Support

**Issue:** [Design mcu schematic](https://github.com/MSOE-High-Power-Rocket-Club-Avionics/Custom-Flight-Computer/issues/7)

## Function

Provide the selected STM32 with power, reset, clock and debug circuitry, and connect it to the other hardware blocks.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| 3V3 / GND | Power block | Supply all required MCU power pins |
| SD_MISO / SD_DETECT | Storage block | SPI data; optional card-detect input |
| GPS_RX | GPS TX | UART data from GPS |
| RADIO_MISO / IRQ / BUSY | Radio block | SPI data and supported status signals |
| VBAT_SENSE | Power block | ADC input; voltage limits: TBD |
| IMU_INT / BARO_INT | Sensors block | Optional interrupt inputs |
| DROGUE_CONT / MAIN_CONT / ARM_STATUS | Deployment block | Digital or analog feedback: TBD |
| SENSOR_SDA / SCL | Sensor bus | Open-drain bus; SDA bidirectional, SCL may be stretched |
| SWDIO / SWCLK / NRST | Debug/reset interface | SWDIO bidirectional; clock/reset inputs |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| SENSOR_SDA / SCL | Sensors block | I2C commands/data and clock; pins: TBD |
| SD_SCK / SD_MOSI / SD_CS_N | Storage block | SPI clock, write data and chip select |
| GPS_TX | GPS RX | UART commands to GPS |
| RADIO_SCK / MOSI / CS_N / RESET_N | Radio block | SPI/control; confirm reset polarity |
| DROGUE_CMD / MAIN_CMD | Deployment drivers | Control commands; inactive startup state required |
| STATUS_LED / BUZZER_CTRL | Indicators block | GPIO/PWM control |
| SWDIO | Debug probe | Bidirectional debug data |
| VTREF / GND | Debug probe | Target voltage reference and return |
