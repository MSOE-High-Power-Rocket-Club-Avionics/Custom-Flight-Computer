# Current Requirements

**Draft for team agreement.** This page separates the working project scope from older brainstorming notes. TBD values require agreement before the affected circuit is approved.

| Area | Working requirement | Still to confirm |
| --- | --- | --- |
| Structure | Power, Control and Communication boards | Connectors, spacing and mounting |
| Size | Target 2.30-inch board diameter; 3-inch minimum body tube in existing notes | Mechanical fit approval |
| MCU | STM32 family, per team direction | Record exact chosen part/package |
| Sensors | IMU and barometer | Selected parts, ranges and sample rates |
| Logging | microSD storage | Data rate and storage needs |
| Communications | GPS and RF telemetry | Modules, antennas and ground receiver |
| Power | Battery-powered; 3.3 V working core rail | Battery range, current budget and protection |
| Recovery | Core pyro channels and commercial backup | Channel ownership, arming and independence |
| Indicators | Visible and audible status | Parts and control signals |
| Expansion | Optional payload electronics | ... |

Proposed interfaces are I2C for sensors, UART for GPS and SPI for storage/radio. Confirm against selected devices. The exact component datasheets determine voltage limits and pin assignments.

Use [block pages](Blocks/README.md) for function/input/output definitions and [Components](Components.md) for selected parts. Resolve requirement changes with affected owners and update documentation in the same PR.
