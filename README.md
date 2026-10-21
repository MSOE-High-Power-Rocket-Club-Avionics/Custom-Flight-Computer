# Custom Flight Computer

A modular flight computer project by the **Milwaukee School of Engineering High Power Rocket Club Avionics team**, being developed for future club flights and **IREC 2028**.

Our goal is to build a customizable flight computer that gives the team more control over its electronics and flight data. The design centers on a core board stack, with additional modules planned to extend its capabilities.

## Current Status

**Early development — requirements, research, and system architecture.**

The repository currently contains project planning documents, a proposed hardware architecture, a KiCad project, and an initial mechanical part. The KiCad schematic and PCB files are currently empty starting points. Software architecture and pseudocode are placeholders; buildable firmware has not yet been added.

`...` marks sections where more information needs to be added. Hardware choices and interfaces are still being evaluated.

## Project Goals

- Collect and store flight data for analysis and future club projects.
- Support GPS tracking and radio telemetry.
- Develop custom parachute deployment electronics alongside an off-the-shelf backup flight computer.
- Use a modular board stack that can support additional payload and sensor modules.
- Develop an easy-to-read digital dashboard for flight data.

These are intended capabilities; implementation and testing are still ahead.

## Proposed Hardware Architecture

| Board or System | Planned Responsibilities |
| --- | --- |
| Power board | Battery connections, voltage regulation, protection, and pyro channels |
| Control board | MCU, IMU, barometric pressure sensor, and microSD storage |
| Communication board | GPS, RF radio, and telemetry |
| Additional modules | Payload electronics and possible redundancy boards... |
| Off-the-shelf backup | Backup flight computer with a dedicated battery; integration details remain under discussion |

Component selection, board connections, and the division of responsibilities between the custom and backup systems are still in progress. See the [hardware architecture](Docs/Architecture/HardwareArchitecture.md) for the current proposal.

## Repository Guide

| Location | Contents |
| --- | --- |
| [Hardware/](Hardware/) | KiCad project, schematic, and PCB files |
| [Software/](Software/) | Software planning and pseudocode |
| [3DModels/](3DModels/) | Mechanical CAD, currently a SolidWorks base disk part |
| [Docs/Architecture/](Docs/Architecture/) | Hardware architecture and software architecture placeholder |
| [Docs/Requirements/](Docs/Requirements/) | Core requirements and IREC avionics requirements notes |
| [Docs/CFC General/](Docs/CFC%20General/) | Project overview and proposal |
| [Docs/Research/](Docs/Research/) | Research materials and course notes |
| [Docs/PCB Design Resources/](Docs/PCB%20Design%20Resources/) | PCB design learning resources |
| [Docs/Flight Computer Resources/](Docs/Flight%20Computer%20Resources/) | Flight computer reference designs |
| [Docs/SETUP.md](Docs/SETUP.md) | Team Git, GitHub, and collaboration guide |

## Getting Started

1. Read the [team setup guide](Docs/SETUP.md) for Git setup and the branch and pull request workflow.
2. Clone the repository:

   ```bash
   git clone https://github.com/MSOE-High-Power-Rocket-Club-Avionics/Custom-Flight-Computer.git
   cd Custom-Flight-Computer
   ```

3. Review the [project overview](Docs/CFC%20General/Custom%20Flight%20Computer.docx), [core requirements](Docs/Requirements/Requirements.docx), and [hardware architecture](Docs/Architecture/HardwareArchitecture.md).
4. Choose the area you are working on:
   - **Hardware:** Open `Hardware/Modular Flight Computer.kicad_pro` in KiCad. The current design files were generated with KiCad 10.0.
   - **Software:** Start with [SoftwareArchitecture.md](Docs/Architecture/SoftwareArchitecture.md) and [SudoCode.md](Software/SudoCode.md). Firmware setup and build instructions will be added when a firmware project is available...
   - **Mechanical:** Review `3DModels/Base Disk.SLDPRT` using SolidWorks or a compatible viewer.

## Contributing

Use a separate branch for each task and submit changes through a pull request. Follow the [team workflow](Docs/SETUP.md#3-team-workflow), request a teammate's review, and avoid committing directly to `main`.

When updating the design, keep the relevant requirements and architecture documents in sync. Coordinate changes to shared CAD files with the team.

## Next Steps

- Refine requirements and select the MCU, sensors, and communication components.
- Define board interfaces, power requirements, and the expansion interface.
- Develop the schematics, PCB layouts, and mechanical integration.
- Define the software architecture and begin firmware development.
- Document subsystem tests and integration results.
- Add dashboard and payload module details...

## License

This repository is licensed under the [MIT License](LICENSE).
