# GPS

**Issue:** TBD

## Function

Receive satellite signals and provide position, time and receiver status to the MCU.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| 3V3 / GND | Power block | Verify module supply and logic levels |
| GPS_TX | MCU TX → GPS RX | UART configuration/commands |
| GPS_RF | GPS antenna | Antenna connection per selected module |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| GPS_RX | GPS TX → MCU RX | UART position/time/status data |
