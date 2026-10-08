# NN-nRF52840-CW308-target-board

An **open-source hardware design** for a [ChipWhisperer CW308 UFO](https://chipwhisperer.readthedocs.io/en/latest/Targets/CW308%20UFO.html) target board
featuring the [Nordic nRF52840](https://www.nordicsemi.com/Products/nRF52840), a modern ARM Cortex-M4 microcontroller with integrated BLE 5.4
connectivity commonly found in IoT and smart home devices. Designed for **hardware security research**, this board enables researchers and security
professionals to conduct side-channel analysis and fault-injection experiments on real-world IoT targets. The platform facilitates the study of
physical attack vectors against secure microcontrollers, supporting applications such as characterizing clock-glitch windows, analyzing power
consumption patterns, and validating the resilience of cryptographic implementations. Released under the open-source CERN-OHL-S v2 license, this
design empowers the security research community to reproduce, modify, and build upon cutting-edge defense mechanisms for embedded systems.

## Features

- Nordic **nRF52840** SoC (AQFN-73, 7 x 7 mm) — ARM Cortex-M4F @ 64 MHz, BLE 5.4 / 802.15.4 radio
- Standard **CW308 UFO 20-pin** interface (3 x 20-pin headers, J2/J3/J4)
- 32 MHz crystal with solder jumper (**JP1**) to AC-couple the CW308 **CLKIN** signal into the HF clock circuit — useful for clock-glitching experiments
- **CLKOUT** output (12 Ω series) so the target can clock the capture board
- 2.4 GHz radio: **U.FL** antenna connector (J1) with discrete pi-match (3.9 nH + 2 x 1 pF)
- NFC antenna connectors: 2-pin header (J5) and optional 5-pin, 0.5 mm-pitch **FPC** connector (J6)
- CW308 current-shunt sense lines (**SHUNTH**/SHUNTL) routed on-board (R1 = 12 Ω bridge, local decoupling)
- Powered from the CW308 3.3 V rail (VDD and VDDH tied to VCC)
- Standard CW308 form factor: 53.3 x 66.0 mm, 3 x M3 mounting holes

## Signal mapping

| UFO signal | nRF52840 pin | Notes |
|---|---|---|
| SCK | P0.26 | SPI |
| MISO | P0.04 | SPI |
| MOSI | P0.06 | SPI |
| GPIO1_TX | P1.13 | UART TX to CW308 |
| GPIO2_RX | P1.15 | UART RX from CW308 |
| GPIO3 | P0.02 | spare IO |
| GPIO4 | P0.29 | spare IO |
| LED1 | P0.24 | CW308 user LED |
| LED2 | P0.22 | CW308 user LED |
| LED3 | P0.20 | CW308 user LED |
| CLKIN | XC2 (via R2/C20 and JP1) | external clock injection |
| CLKOUT | P1.10 (via R3 = 12 Ω) | target clock to CW308 |
| HDR1 | P0.07 | spare IO |
| HDR2 | P1.09 | spare IO |
| HDR3 | P0.12 | spare IO |
| HDR4 | P0.13 | spare IO |
| HDR5 | P0.15 | spare IO |
| SWDIO | SWDIO | debug |
| SWDCLK | SWDCLK | debug |
| SWO | P1.00 | trace / debug |
| NRST | P0.18 | reset |
| NFC1 | P0.09 / NFC1 | NFC antenna |
| NFC2 | P0.10 / NFC2 | NFC antenna |

Programming and debugging are done through the CW308's onboard programmer (SWD), or by any external SWD adapter connected to the UFO.

## Repository layout

```
├── kicad_project/     KiCad schematic and PCB (nrf52840-ufo)
└── fabrication/       Gerbers, BOM and CPL ready for JLCPCB assembly
```

## Fabrication and assembly

- The files in `fabrication/` are prepared for **JLCPCB** assembly; the BOM includes the corresponding LCSC part numbers (e.g. `C190794` for the nRF52840-QIAA-R).
- The U.FL connector, the 20-pin UFO headers and the NFC pin header are **excluded from assembly** and must be sourced and soldered separately if needed.
- `C13`, `C16` and `C4` are DNP (no-connect placeholders kept for matching/tuning options).

## License

Hardware released under the **CERN Open Hardware Licence Version 2 - Strongly Reciprocal** (CERN-OHL-S-2.0). See [LICENSE](LICENSE).
