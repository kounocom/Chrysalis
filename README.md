# Chrysalis

**A shield PCB for the nRF52840 Supermini/Pro Micro with an IMU, magnetometer, two buttons and n RGB LED, designed for nRF-based SlimeVR trackers**

## Overview

Chrysalis is a compact, back-mounted shield that solders directly to the underside of the nRF52840 Supermini or Pro Micro. It adds:

- 3-axis accelerometer/gyroscope (TDK InvenSense ICM-45686)  
- 3-axis magnetometer (QMC6309)  
- Two push-buttons for SW0 and RESET 
- An RGB LED
- Pads for battery wires 

All exposed pads are marked with a star (`*`) and **must** be soldered.

## Requirements

- Assembled Chrysalis board
- nRF52840 Supermini or Pro Micro  
- Soldering iron (chisel or knife-type tip recommended), solder wire, flux (optional but recommended)

## Ordering Information

Chrysalis requires:
- Castellated holes on two sides  
- ENIG surface finish (for the QMC6309 BGA pads)  
- Thin PCB stack-up (0.8 mm or 1.0 mm recommended)

Manufacturing is most cost-effective at volume. For small quantities, consider ordering from [here](https://nekumori.pink/products/chysalis-v1_3).

## Hardware Assembly

1. **Prepare the Supermini**  
   - Update your bootloader **before** soldering and verify functionality. SWD pads will be covered after soldering, so unbricking/recovery will require removing the shield.  

2. **Align Chrysalis**  
   - Flip the Supermini upside-down (chips side down).  
   - Match the silkscreen markers on the backside of Chrysalis:  
     - **USB above** → near the USB connector 
     - **Antenna below** → near the antenna

3. **Solder Every Exposed Pad**  
   - All castellated pads are marked with `*`.  
   - Tack one corner pad to secure alignment, then solder the rest.  
   - Use direct solder connections—no wires or pin-headers.  
   - Inspect joints under magnification; check for cold or dry joints and bridges.

## Pinout & Connections

| Supermini Pin | Signal    |
|---------------|-----------|
| P0.17         | IMU INT1  |
| P0.24         | MISO      |
| P0.06         | MOSI      |
| P0.08         | SCK       |
| P0.22         | CS        |
| P1.00         | SW0       |
| RST / P0.18   | RESET     |
| P0.20         | CLK_CTL   |
| GND           | GND       |
| P0.31         | VCC       |
| P0.02         | R         |
| P1.15         | G         |
| P0.29         | B         |

> **Note:**  
> - The module intentionally sources power from one of the nRF52840's GPIOs (P0.31), as the voltage of it is adjustable.
> - The QMC6309 requires a minimum supply voltage of 2.5 V.

_For the complete schematic and up-to-date pin mapping, see `Chrysalis.kicad_sch`._

## Usage

1. Plug the assembled Supermini+Chrysalis combo into your host via USB.  
2. Flash the SlimeVR firmware:   
   - Download the pre-compiled firmware:  
     https://docs.slimevr.dev/smol-slimes/firmware/smol-pre-compiled-firmware.html 
   - In the configurator select:  
     - **Schematic Type:** PCB
     - **Microcontroller:** Pro Micro (Subject to change — sub-variant with RGB LED support not added yet)
     - **Interface:** SPI  
     - **Enable Clock:** ✅  
     - **WOM:** ✅ / ❌ (user preference)
     - **SW0:** ✅ 
    - Follow the guide:  
     https://docs.slimevr.dev/smol-slimes/firmware/smol-flashing-firmware.html 
3. Open a serial console to verify IMU, magnetometer and button functionality.

> **Note:**  
> - At the time of writing this, the magnetometer will not be detected, because the IMU's sensorhub functionality has not been fully implemented.

## License

This project is licensed under the CERN Open Hardware Licence 2.0 – Strongly Reciprocal (CERN-OHL-S).  
See `LICENSE.md` for full terms