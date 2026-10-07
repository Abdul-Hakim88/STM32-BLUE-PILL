# STM32F103C8T6 Development Board

A compact 2-layer development board built around the STM32F103C8T6 (Cortex-M3, LQFP48), designed in Altium Designer and intended for fabrication at JLCPCB. It follows the familiar "Blue Pill" style: all usable GPIO broken out to two 20-pin headers, native USB, SWD programming, and an onboard 3.3 V regulator.

## Features

- MCU: STM32F103C8T6 (72 MHz Cortex-M3, 64 KB flash, 20 KB RAM)
- 8 MHz HSE crystal and 32.768 kHz LSE crystal
- Micro-USB connector wired to the MCU's native USB (PA11 / PA12), also used as the 5 V input
- 3.3 V LDO regulator (RT9193-33GB)
- SWD header (J4) for programming and debugging
- Boot mode selection through a 2x3 header (J5) for BOOT0 / BOOT1
- Reset button with pull-up and debounce capacitor
- Two red status LEDs (power and user)
- Two 20-pin headers (J1, J2) exposing the GPIO, NRST, 3.3 V and GND

## Block overview

| Block | Parts | Notes |
|---|---|---|
| MCU | U1 STM32F103C8T6 | VBAT and VDDA tied to 3.3 V |
| Power | REG1 RT9193-33GB, C1-C4 | 5 V in, 3.3 V out, EN tied to VIN |
| Decoupling | C5-C8 (0.1 uF) | Place close to the VDD pins |
| HSE | Y1 (ATS08A-E), C10/C11 22 pF, R3 10 MOhm | On PD0 / PD1 |
| LSE | Y2 32.768 kHz | On PC14 / PC15 |
| Reset | S1, R2 10 K, C9 0.1 uF | NRST pull-up with debounce cap |
| Boot | J5 (2x3), R1 10 K (BOOT0), R4 10 K (BOOT1) | Pull-downs, jumpers select mode |
| USB | J3 Micro-USB, R7 | D+ on PA12, D- on PA11 |
| SWD | J4 | GND, SWCLK, SWDIO, 3V3 |
| LEDs | LED1 + R5 1K, LED2 + R6 1K | LED2 driven from PB12 |
| Headers | J1, J2 | See pinout below |

## Pinout

J1 (20 pins): 3V3, GND, PB12, PB13, PB14, PB15, PA8, PA9, PA10, PA11, PA12, PA15, PB3, PB4, PB5, PB6, PB7, 3V3, GND

J2 (20 pins): GND, 3V3, PB11, PB10, PB1, PB0, PA7, PA6, PA5, PA4, PA3, PA2, PA1, PA0, NRST, PC13, PB9, PB8, GND

Check the exact pin order against the schematic before wiring anything. PB12 is shared between the header and LED2.

Reserved functions:

| Pin | Function |
|---|---|
| PA11 / PA12 | USB D- / D+ |
| PA13 / PA14 | SWDIO / SWCLK |
| PC14 / PC15 | 32.768 kHz crystal |
| PD0 / PD1 | 8 MHz crystal |
| PB2 | BOOT1 |
| PB12 | LED2 |

## Programming and boot modes

Flash over SWD with an ST-Link or compatible probe, connected to J4.

Boot mode is selected with the jumpers on J5:

| BOOT1 | BOOT0 | Boot from |
|---|---|---|
| X | 0 | Main flash (normal run) |
| 0 | 1 | System memory (UART bootloader) |
| 1 | 1 | Embedded SRAM |

Default (no jumpers on BOOT0) boots from flash.

## PCB specification

| Parameter | Value |
|---|---|
| Layers | 2 |
| Board thickness | 1.6 mm |
| Outer copper | 1 oz |
| Material | FR-4 |
| Surface finish | HASL or ENIG (your choice at order time) |
| Tool | Altium Designer |
| Fabricator | JLCPCB |

Altium stackup: dielectric 1.51 mm, copper 0.03556 mm per side, solder mask 0.01016 mm. These are only for documentation; JLCPCB builds from the Gerbers and the options chosen at checkout.

## Repository layout

```
.
├── README.md
├── Schematic.SchDoc
├── Schematic2.SchDoc
├── Controller_Page.SchDoc
├── Connector_Page.SchDoc
├── PCB Design.PcbDoc
├── Gerbers/
├── BOM/
└── Images/
```

Adjust this to match the actual repo contents.

## Ordering from JLCPCB

1. Generate Gerbers and drill files from Altium and zip them.
2. Upload the zip to JLCPCB.
3. Select 2 layers, 1.6 mm thickness, 1 oz outer copper.
4. For assembly, export the BOM and pick-and-place files and match parts to the JLC parts library.

## License

Add a license here (for example MIT for the design files).
