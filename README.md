# Isolated RP2040 Debug Probe

An electrically isolated CMSIS-DAP debug probe based on the Raspberry Pi Debug Probe design, with full USB galvanic isolation for improved safety and robustness when debugging embedded hardware.

This project recreates the Raspberry Pi Debug Probe hardware from the published schematic and adds:

- USB full-speed isolation
- ESD protection on both USB and target ports
- Isolated DC/DC power for the target side
- Improved protection against ground loops and high-energy faults

---

## ⚠️ Important Disclaimer

This is an independent, community-made hardware design.

This project is not affiliated with, endorsed by, or supported by Raspberry Pi Ltd.
“Raspberry Pi” is a trademark of Raspberry Pi Ltd.

The original debug probe design and firmware are created by Raspberry Pi.
This repository only provides a compatible hardware implementation based on their publicly released schematic.

Original documentation:
https://www.raspberrypi.com/documentation/microcontrollers/debug-probe.html

---

## Why an Isolated Debug Probe?

Standard USB debug probes share ground between:

- your PC
- the probe
- the target device

This is usually fine — until it isn't.

Real-world embedded targets often include:
- switching power supplies
- motor drivers
- high-current loads
- long cable harnesses
- industrial equipment

Connecting a non-isolated probe can cause:

- ground loops
- USB disconnects
- corrupted SWD communication
- damage to the target
- damage to your laptop USB port

This design introduces galvanic isolation between the USB host and the target interface (SWD/UART), protecting both sides.

---

## Features

- RP2040-based CMSIS-DAP probe
- SWD debugging (OpenOCD, ... compatible)
- USB CDC UART bridge
- Full USB isolation
- Isolated target power domain
- Protection against negative voltages and ground offsets
- Drop-in compatible with existing Raspberry Pi Debug Probe software

---

## Hardware Overview

The probe consists of two electrically separated domains:

### Host Side
- USB connector
- USB interface isolator

### Target Side (Isolated)
- RP2040 microcontroller
- SWD interface (SWCLK, SWDIO)
- UART (TX/RX)
- Assumes fixed 3.3V target voltage
- Can power the target (up to 50mA) if desired
- Powered through isolated DC/DC converter

Isolation is implemented using:
- USB isolator IC
- isolated DC/DC converter

No electrical ground connection exists between the PC and the target device.

---

## Firmware

The probe runs the official Raspberry Pi Debug Probe firmware for the RP2040.

Flashing instructions:
1. Connect the probe while holding the BOOTSEL button
2. The device appears as a USB mass storage drive
3. Copy the debugprobe.uf2 firmware to the drive

Firmware download:
https://github.com/raspberrypi/debugprobe/releases

---

## Building the Hardware

### Requirements
- 4-layer PCB recommended
- Hot-air or reflow assembly
- 0603 passives
- Fine-pitch soldering capability

Or simply order via JLCPCB

Files provided in this repository:
- Schematic
- PCB layout
- Gerbers
- BOM
- Pick & Place

---

## Known Limitations

- No more tha 50mA of target power may be supplied by the probe
- USB full-speed only (12 Mbps), same as the original debug probe

---

## License

### This repository
Hardware design files in this repository are released under the CERN-OHL-S v2 (or choose your preferred open hardware license).

### Raspberry Pi materials
Portions of the information (such as pinout descriptions) are derived from Raspberry Pi documentation, which is licensed under Creative Commons.

© Raspberry Pi Ltd.
Used with attribution.

---

## Acknowledgements

This project would not exist without the excellent work by the Raspberry Pi engineers who designed the original Debug Probe and released its schematic and firmware publicly.

If you simply need a normal probe, please consider buying the official product — it directly supports Raspberry Pi and their open hardware efforts.