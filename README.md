# Preamble

A universal wireless communication library for embedded devices. Fork of [RadioLib](https://github.com/jgromes/RadioLib) by Jan Gromeš.

## Why this fork exists

RadioLib is excellent engineering. The chip support is broad, the abstraction layer is clean, and it runs on everything. We used it heavily in [MeshTNC](https://github.com/SourceParts/MeshTNC) and had real fixes to contribute — hardware quirks, initialization edge cases, things we found running the chips in production.

The upstream maintainer describes RadioLib as a hobby project and has made clear that outside contributions are unwelcome. Hardware-verified bug fixes were reviewed and dismissed as AI-generated slop. The project has a [code of conduct][upstream-coc]. It is not applied to the maintainer.

[upstream-coc]: https://github.com/jgromes/RadioLib/blob/7ea94eb01ad7c3069db2d9f4b369aa69a8ee416e/CODE_OF_CONDUCT.md#L3

We are not interested in maintaining a private patch set on top of someone else's repo forever. So we forked it properly, gave it a name, and are developing it as a first-class open project under SourceParts.

The name is apt: a LoRa preamble is the sync signal that starts every packet. This library is what gets your radio talking.

**Preamble ships the fixes RadioLib wouldn't take:**
- `SX127x/SX1272/SX1278`: crystal startup delay when `NRESET=NC` — without this, SPI transactions fail on cold boot
- `SX128x`: `setBandwidth()` snaps to the nearest valid LoRa BW value instead of returning an error on approximate inputs

## Fork attribution

Preamble diverges from RadioLib at commit [`802b969f0`](https://github.com/jgromes/RadioLib/commit/802b969f0). The original MIT license is retained. See `license.txt`.

## Supported modules

* __CC1101__ FSK radio module
* __LLCC68__ LoRa module
* __LR11x0__ series LoRa/GFSK modules (LR1110, LR1120, LR1121)
* __LR2021__ series LoRa/GFSK/LR-FHSS/FLRC/OOK modules
* __nRF24L01__ 2.4 GHz module
* __RF69__ FSK/OOK radio module
* __RFM2x__ series FSK modules (RFM22, RFM23)
* __RFM9x__ series LoRa modules (RFM95, RFM96, RFM97, RFM98)
* __Si443x__ series FSK modules (Si4430, Si4431, Si4432)
* __STM32WL__ integrated microcontroller/LoRa module
* __SX126x__ series LoRa modules (SX1261, SX1262, SX1268)
* __SX127x__ series LoRa modules (SX1272, SX1273, SX1276, SX1277, SX1278, SX1279)
* __SX128x__ series LoRa/GFSK/BLE/FLRC modules (SX1280, SX1281, SX1282)
* __SX123x__ FSK/OOK radio modules (SX1231, SX1233)

## Supported protocols and digital modes

* [__ADS-B__](https://mode-s.org/1090mhz/content/ads-b/1-basics.html) using OOK for LR2021
* [__AX.25__](https://www.sigidwiki.com/wiki/PACKET) using 2-FSK or AFSK for modules:  
SX127x, RFM9x, SX126x, RF69, SX1231, CC1101, RFM2x, Si443x, LR11x0, LR2021 and SX128x
* [__RTTY__](https://www.sigidwiki.com/wiki/RTTY) using 2-FSK or AFSK for modules:  
SX127x, RFM9x, SX126x, RF69, SX1231, CC1101, nRF24L01, RFM2x, Si443x, LR11x0, LR2021 and SX128x
* [__Morse Code__](https://www.sigidwiki.com/wiki/Morse_Code_(CW)) using 2-FSK or AFSK for modules:  
SX127x, RFM9x, SX126x, RF69, SX1231, CC1101, nRF24L01, RFM2x, Si443x, LR11x0, LR2021 and SX128x
* [__SSTV__](https://www.sigidwiki.com/wiki/SSTV) using 2-FSK or AFSK for modules:  
SX127x, RFM9x, SX126x, RF69, SX1231, CC1101, RFM2x and Si443x
* [__Hellschreiber__](https://www.sigidwiki.com/wiki/Hellschreiber) using 2-FSK or AFSK for modules:  
SX127x, RFM9x, SX126x, RF69, SX1231, CC1101, nRF24L01, RFM2x, Si443x, LR11x0, LR2021 and SX128x
* [__APRS__](https://www.sigidwiki.com/wiki/APRS) using AFSK for modules:  
SX127x, RFM9x, SX126x, RF69, SX1231, CC1101, nRF24L01, RFM2x, Si443x and SX128x
* [__POCSAG__](https://www.sigidwiki.com/wiki/POCSAG) using 2-FSK for modules:  
SX127x, RFM9x, RF69, SX1231, CC1101, nRF24L01, RFM2x and Si443x
* [__LoRaWAN__](https://lora-alliance.org/) using LoRa and FSK for modules:  
SX127x, RFM9x, SX126x, LR11x0, LR2021 and SX128x
  * Supports Class A and C (and Multicast over C).
  * Pre-certified for Class A.

## Supported Arduino platforms

* __Arduino__  
  * [__AVR__](https://github.com/arduino/ArduinoCore-avr) - Arduino Uno, Mega, Leonardo, Pro Mini, Nano etc.
    * NOTE: Arduino boards based on ATmega328 (Uno, Pro Mini, Nano etc.) and smaller are NOT recommended. This is because the ATmega328 MCU is very constrained in terms of program and memory size, so the library will end up taking most of the space available. 
  * [__mbed__](https://github.com/arduino/ArduinoCore-mbed) - Arduino Nano 33 BLE and Arduino Portenta H7
  * [__megaAVR__](https://github.com/arduino/ArduinoCore-megaavr) - Arduino Uno WiFi Rev.2 and Nano Every
  * [__SAM__](https://github.com/arduino/ArduinoCore-sam) - Arduino Due
  * [__SAMD__](https://github.com/arduino/ArduinoCore-samd) - Arduino Zero, MKR boards, M0 Pro etc.
  * [__Renesas__](https://github.com/arduino/ArduinoCore-renesas) - Arduino Uno R4

* __Adafruit__
  * [__SAMD__](https://github.com/adafruit/ArduinoCore-samd) - Adafruit Feather M0 and M4 boards (Feather, Metro, Gemma, Trinket etc.)
  * [__nRF52__](https://github.com/adafruit/Adafruit_nRF52_Arduino) - Adafruit Feather nRF528x, Bluefruit and CLUE

* __Espressif__
  * [__ESP32__](https://github.com/espressif/arduino-esp32) - ESP32-based boards
  * [__ESP8266__](https://github.com/esp8266/Arduino) - ESP8266-based boards

* __Intel__
  * [__Curie__](https://github.com/arduino/ArduinoCore-arc32) - Arduino 101

* __SparkFun__
  * [__Apollo3__](https://github.com/sparkfun/Arduino_Apollo3) - Sparkfun Artemis Redboard

* __ST Microelectronics__
  * [__STM32__ (official core)](https://github.com/stm32duino/Arduino_Core_STM32) - STM32 Nucleo, Discovery, Maple, BluePill, BlackPill etc.
  * [__STM32__ (unofficial core)](https://github.com/rogerclarkmelbourne/Arduino_STM32) - STM32F1 and STM32F4-based boards

* __MCUdude__
  * [__MegaCoreX__](https://github.com/MCUdude/MegaCoreX) - megaAVR-0 series (ATmega4809, ATmega3209 etc.)
  * [__MegaCore__](https://github.com/MCUdude/MegaCore) - AVR (ATmega1281, ATmega640 etc.)

* __Raspberry Pi__
  * [__RP2040__ (official core)](https://github.com/arduino/ArduinoCore-mbed) - Raspberry Pi Pico and Arduino Nano RP2040 Connect
  * [__RP2040__ (unofficial core)](https://github.com/earlephilhower/arduino-pico) - Raspberry Pi Pico/RP2040-based boards
  * [__Raspberry Pi__](https://github.com/me-no-dev/RasPiArduino) - Arduino framework for RaspberryPI

* __Heltec__
  * [__CubeCell__](https://github.com/HelTecAutomation/CubeCell-Arduino) - ASR650X series (CubeCell-Board, CubeCell-Capsule, CubeCell-Module etc.)

* __PJRC__
  * [__Teensy__](https://github.com/PaulStoffregen/cores) - Teensy 2.x, 3.x and 4.x boards

* __Silicon Labs__
  * [__EFR32__](https://github.com/SiliconLabs/arduino) - Silicon Labs xG24, xG27 and other boards

Preamble includes an internal hardware abstraction layer that makes it portable to non-Arduino environments as well.

## Upstream tracking

This fork tracks `jgromes/RadioLib` for relevant upstream changes and
security updates. Security fixes from upstream will be prioritized. Bug
fixes, chip support, and protocol improvements from upstream will be
merged on a best-effort basis. Fork-specific changes — hardware fixes,
initialization edge cases, and contributions rejected upstream — are
maintained here.

We do not guarantee parity with upstream, and divergence is expected
where upstream behavior is incorrect or incompatible with production
hardware use.

## Code of Conduct

Contributors and maintainers are expected to follow the project's
[code of conduct](./CODE_OF_CONDUCT.md).
