# microSD Storage

**Issue:** TBD

## Function

Store flight data on a microSD card and allow the MCU to read it back.

## Inputs

| Connection | From | Details |
| --- | --- | --- |
| 3V3 / GND | Power block | Verify card supply and write-current needs |
| SD_SCK | MCU | SPI clock → card CLK |
| SD_MOSI | MCU | SPI commands/data → card CMD/DI |
| SD_CS_N | MCU | Active-low select → card DAT3/CS |

## Outputs

| Connection | To | Details |
| --- | --- | --- |
| SD_MISO | MCU | SPI data/status from card DAT0/DO |
| SD_DETECT | MCU | Optional socket card-detect signal |
