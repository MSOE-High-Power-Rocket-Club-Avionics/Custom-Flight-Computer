# Telemetry Radio

**Issue:** TBD

## Function

Transmit flight data to the ground receiver and pass received data/status to the MCU.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| 3V3 / GND | Power block | Supply and transmit-current requirements: TBD |
| RADIO_SCK / MOSI / CS_N | MCU | SPI clock, commands/data and chip select |
| RADIO_RESET_N | MCU | If supported; verify reset polarity |
| RADIO_RF | Antenna | Received RF; shared transmit/receive connection |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| RADIO_MISO | MCU | SPI data/status |
| RADIO_IRQ / BUSY | MCU | If supported by selected radio |
| RADIO_RF | Antenna | Transmitted RF; shared transmit/receive connection |
