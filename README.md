# Electric-guitar Audio eFfectX

If any questions, welcome for Issues & PRs

**WARNING! This Project is not been fully long-term productive tested and without warranty of any kind, use at your own risk!**

## License

This project is licensed under the LGPL-2.1-or-later license. **DO NOT** download or clone this project until you have read and agree the LICENSE.

## TODO

1. plug subboard designs
2. FPGA RTL integration
3. controller firmwares

## Overview

This project is used to perform audio system for electric guitars, and consists of essential components, including the hardware(core and plug) with GERBER and schematics, digital logic designs, mechanicals of pickguard and firmware of low power microcontroller which provide HMI and system controls. The TFT screen is not included, which is from Waveshare [Click here](https://www.waveshare.net/wiki/1.9inch_LCD_Module) and would be very easy to fetch.

![PCB Preview Picture](https://github.com/antercreeper/gafx/blob/main/core_preview.jpg?raw=true)

## Functions

- Audio Record & PlayBack (SDCard)
- Audio Mixer
- USB Audio Input and Output
- Wireless BLE Real-time Audio Monitor
- Audio Effects (chorus, distortion, EQ...)

## Directory

#### Core

This directory consists of PCB designs(KiCad) of main board, which take the most functions. It includes battery management(TI `BQ25601` charger with `TPD2S300` for Type-C PD high-voltage fast charge, and TI `BQ27720` energy guage), system microcontroller(WCH `CH32X035`), FPGA unit(Gowin `Tang Primer 25k`), and the audios(ADI/Maxim `MAX9850` I2S DAC + Onsemi `FAN3852` AFE+ADC to PDM, and Skyworks/Silabs `Si5351` for clock). Besides, this system takes a BLE module(Nordic `nRF5340`) to provide ultra-low latency LE Audio streaming ability.

The power rails are carefully designed to provide long experience endurance. The system occupied several load switches(MPS `MP5095` and Diode `AP2151`) and ultra-low quiescent regulators(TI `TPS62743` and `TPS7A20`), and we can shutdown or set specific components(keys and screen, the audio system, flash storage, bluetooth) to low power states.

The dual magnetic pickups are attached via IPEX-4(need some solder works to modify the connect wires), which would provide low noise pure raw signals.

#### Plug

This directory consists of PCB designs(KiCad) of plug subboard, which consists of `audio jack`, `microSD slot`, `usb-c receptacle`, `charge indicator` and `ambient light sensor`.
Output
#### RTL

This directory consists of the audio process logics:
- core processor
- audio synthesizer
- flac encoder & decoder
- audio i/o interface
- usb device interface
- i2c device interface
- sd host controller interface

#### Controller

This directory consists of the system controller firmwares, which setup every device, sense the system states, render the HMI and react to user input events.

#### LE-Audio

This directory consists of the BLE module firmware subproject from another individual repository. It would scan, connect and pair with earbuds, and then perform real-time audio streaming(LC3). This module acts as a device(system controller host) with standard AT interface over UART.

#### Others

Misc files under the root:
- pickguard.dxf: Pickguard CAD designs.

## Usage

**This Section is W.I.P and would be completed in the future.**

[![Star History Chart](https://api.star-history.com/svg?repos=antercreeper/gafx&type=date&legend=top-left)](https://www.star-history.com/#antercreeper/gafx&type=date&legend=top-left)