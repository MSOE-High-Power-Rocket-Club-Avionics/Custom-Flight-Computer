# Power and Battery Monitoring

**Issue:** [Design power schematic](https://github.com/MSOE-High-Power-Rocket-Club-Avionics/Custom-Flight-Computer/issues/6)

## Function

Convert battery power into regulated supplies for the boards and provide battery-voltage feedback to the MCU.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| BAT+ / BAT− | Core battery | Battery operating voltage/current: TBD |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| 3V3 / GND | Control and Communication boards | Regulated 3.3 V; current and tolerance: TBD |
| VBAT_SENSE | MCU ADC | Scaled battery voltage within ADC limits |
| Optional 5 V / GND | Any confirmed 5 V loads | Include only if needed |
