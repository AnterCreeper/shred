# SHRED: (S)ystem for (H)igh-performance (R)eal-time (E)lectric guitar (D)igital effects

If you have any questions, feel free to open Issues & PRs.

**WARNING! This project has not been fully tested in long-term production environments and is provided without warranty of any kind. Use at your own risk!**

## License

This project is licensed under the LGPL-2.1-or-later license.

**DO NOT** download or clone this project until you have read and agreed to the LICENSE.

## TODO

1. plug subboard designs
2. FPGA RTL integration
3. controller firmware

## Overview

This project implements an audio system for electric guitars and consists of essential components, including the hardware (core and plug) with Gerber files and schematics, digital logic designs, mechanical designs for the pickguard, and firmware for a low-power microcontroller that provides HMI and system controls.

The TFT screen is not included, which is from Waveshare ([Click here](https://www.waveshare.net/wiki/1.9inch_LCD_Module)) and would be easy to obtain.

![PCB Preview Picture](https://github.com/antercreeper/shred/blob/main/core_preview.jpg?raw=true)

## Functions

- Audio Record & Playback (SD Card)
- Audio Mixer
- USB Audio Input and Output
- Wireless BLE Real-time Audio Monitor
- Audio Effects (chorus, distortion, EQ...)

## Directory

### Core

This directory contains PCB designs (KiCad) for the main board, which implements most functions. It includes battery management (TI `BQ25601` charger with `TPD2S300` for Type-C PD high-voltage fast charging, and TI `BQ27720` energy gauge), system microcontroller (WCH `CH32X035`), FPGA unit (Gowin `Tang Primer 25K`), and the audio subsystem (ADI/Maxim `MAX9850` I2S DAC + onsemi `FAN3852` AFE+ADC to PDM, and Skyworks/Silicon Labs `Si5351` for clock generation). In addition, this system includes a BLE module (Nordic `nRF5340`) to provide ultra-low latency LE Audio streaming capability.

The power rails are carefully designed to provide long battery life. The system employs several load switches (MPS `MP5095` and Diodes `AP2151`) and ultra-low quiescent current regulators (TI `TPS62743` and `TPS7A20`), allowing specific components (keys and screen, audio system, flash storage, Bluetooth) to be shut down or set to low-power states.

The dual magnetic pickups are connected via IPEX-4 (some soldering work is required to modify the connection wires), which provides low-noise, pure raw signals.

### Plug

This directory contains PCB designs (KiCad) for the plug subboard, which includes an `audio jack`, `microSD slot`, `USB-C receptacle`, `charge indicator`, and `ambient light sensor`.

### RTL

This directory contains the audio processing logic:
- Core processor
- Audio synthesizer
- FLAC encoder & decoder
- Audio I/O interface
- USB device interface
- I2C device interface
- SD host controller interface

### Controller

This directory contains the system controller firmware, which sets up every device, monitors system states, renders the HMI, and reacts to user input events.

### LE-Audio

This directory contains the BLE module firmware subproject from a separate repository. It scans, connects, and pairs with earbuds, and then performs real-time audio streaming (LC3). This module acts as a peripheral to the system controller, communicating via a standard AT interface over UART.

### Others

Miscellaneous files under the root:
- `pickguard.dxf`: Pickguard CAD designs.

## Usage

**This section is W.I.P. and will be completed in the future.**

[![Star History Chart](https://api.star-history.com/svg?repos=antercreeper/shred&type=date&legend=top-left)](https://www.star-history.com/#antercreeper/shred&type=date&legend=top-left)