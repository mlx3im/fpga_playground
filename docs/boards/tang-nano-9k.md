# Sipeed Tang Nano 9K

## Role in This Project

The Tang Nano 9K is the project’s primary and initially only supported FPGA
board. This document records board facts and integration assumptions; it does
not define a complete design or build flow.

## Device and Resources

The board documentation identifies the FPGA as Gowin
`GW1NR-LV9QN88PC6/I5` (also described as the GW1NR-9 family). The board
provides the following relevant resources:

- 8,640 LUT4 logic units
- 6,480 registers/flip-flops
- 468 Kbit block SRAM
- 20 embedded multipliers
- 2 PLLs
- 27 MHz onboard oscillator
- 6 programmable LEDs
- 2 programmable buttons
- HDMI, RGB, and SPI display interfaces
- 32 Mbit SPI flash
- 64 Mbit external PSRAM
- onboard BL702 USB-JTAG and USB-UART bridge

Sources:

- [Sipeed Tang Nano 9K documentation](https://en.wiki.sipeed.com/hardware/en/tang/Tang-Nano-9K/Nano-9K.html)
- [Gowin Tang Nano 9K board listing](https://www.gowinsemi.com/en/support/devkits_detail/43/)

Exact pin assignments, electrical standards, and timing constraints must be
taken from the board schematic and device documentation when implementation
begins. This document intentionally does not duplicate a pin constraint file.

## Planned Integration Boundary

The board wrapper will eventually own:

- the top-level module used for implementation
- the 27 MHz input clock connection
- reset and button input conditioning
- LED and peripheral output mapping
- vendor-specific PLL or primitive instances
- board-specific constraints

Reusable core modules should communicate through logical interfaces rather than
depending on these physical details.

## Initial Hardware Workflow

The first documented hardware workflow should use the official Gowin toolchain
as its reference implementation. Programming may be performed through the
Gowin tools or a separately evaluated utility, but the selected process must be
recorded with tool versions and board settings.

An open-source synthesis and programming flow is a possible future improvement,
not a current project requirement.

## Deferred Decisions

- simulator and version
- synthesis and place-and-route flow
- programming utility
- first board demonstration
- pin constraint file location and naming
- use of PLL, flash, PSRAM, HDMI, or other board-specific resources
