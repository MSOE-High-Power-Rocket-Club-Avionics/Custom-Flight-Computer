# Pyro Channels

**Issue:** [Design pyro schematic](https://github.com/MSOE-High-Power-Rocket-Club-Avionics/Custom-Flight-Computer/issues/12)

## Function

Control the assigned pyro channels using flight-computer commands and an arming input, and provide continuity and arming-status feedback.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| PYRO_SUPPLY / return | Agreed deployment supply | Voltage/current and return path: TBD |
| DROGUE_CMD / MAIN_CMD | Responsible flight computer | Driver control; active level and inactive/reset state: TBD |
| ARM_INPUT | Arming hardware | Arming connection and limits: TBD |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| Drogue / main output pairs | Assigned deployment connections | Driver outputs; connector/ratings: TBD |
| DROGUE_CONT / MAIN_CONT | Responsible flight computer | Continuity feedback; ADC or digital limits: TBD |
| ARM_STATUS | Responsible flight computer | Arming feedback; signal limits: TBD |
