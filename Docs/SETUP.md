# Setup

## First Time

1. Install Git and sign in to GitHub using your team's preferred Git client/authentication method.
2. On Windows, use **Git Bash** for the commands below. On macOS/Linux, use Terminal.
3. Set your identity using the email associated with your GitHub account:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git clone https://github.com/MSOE-High-Power-Rocket-Club-Avionics/Custom-Flight-Computer.git
cd Custom-Flight-Computer
```

## Hardware

Install KiCad compatible with the checked-in files, currently generated with **10.0**. Confirm the team's common version before saving changes. Open `Hardware/Modular Flight Computer.kicad_pro` to inspect the starter project. Agree on your board project and sheet before editing.

See [hardware instructions](../Hardware/README.md).

## Mechanical

The existing native part is `Mechanical/Base Disk.SLDPRT`. Use compatible SolidWorks software; ask the mechanical owner for a preview or neutral export if needed.

## Software

For this project I am going to highly recommend to use STM32CUBEIDE and VSCODE

## Begin Work

Find your [assignment](Blocks/README.md), then follow the [issue and PR workflow](../CONTRIBUTING.md).

Authentication/setup help: [GitHub's Git setup guide](https://docs.github.com/en/get-started/git-basics/set-up-git).
