# LEDs and Buzzer

**Issue:** TBD

## Function

Turn MCU control signals into visible and audible system status.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| 3V3 / GND | Power block | Verify selected LED/sounder supply and current |
| STATUS_LED | MCU | LED control signal; active level: TBD |
| BUZZER_CTRL | MCU | GPIO or PWM depending on sounder |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| Light | User | LED status indication |
| Sound | User | Audible status indication |
