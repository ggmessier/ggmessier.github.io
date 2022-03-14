---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Wireless

Wireless connectivity for my home hobby devices is provided using the [LoRa protocol](https://en.wikipedia.org/wiki/LoRa) implemented using dev boards that make use of Semtech devices.  Check [here](https://www.semtech.com/lora/what-is-lora) for Semtech info and their LoRa overview.  This page focuses on how to use the Semtech [SX1280](https://www.semtech.com/products/wireless-rf/lora-24ghz/sx1280) device.

My network uses a star topology with a single access point implemented by connecting a [Beaglebone](bbb) to an SX1280 dev board.  The network nodes are [AVR MCUs](avr) connected to SX1280 dev boards.  The SPI serial bus is used for both the Beaglebone and AVR interfaces.


## Pinout

Relevant pins for my designs:
```
GND
VDD: 1.8V to 3.7V.
NSS_CTS (input): SPI slave select (active low).
MOSI_RX (input): SPI slave input.
MISO_TX (ouput): SPI slave output.
CLK_RTSN (input): SPI clock.
NRST (input): Active low reset signal.
BUSY (ouput): Transceiver busy indicator.
```