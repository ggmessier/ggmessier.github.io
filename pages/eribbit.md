---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# eRibbit

## Overview
A wireless protocol built on top of LoRa.
- Star network topology with a single main node and several secondary nodes.
- Assume the Semtech SX12xx chips which provide physical layer and packet CRC functionality.

eRibbit functionality:
- DL layer packet level ARQ retransmission using CRC information and timers.
- MAC layer main polling of sec nodes.  Addressing is a simple integer system where the main node is address 0 and sec nodes increase from there.
- Application layer implementation of commands.  Main sends commands to an addressed sec node.  The sec node application layer only replies to main queries.

The application layer protocol will be initially tested using direct UART connections between the main node and one secondary node.


## Wireless

Wireless connectivity for my home hobby devices is provided using the [LoRa protocol](https://en.wikipedia.org/wiki/LoRa) implemented using dev boards that make use of Semtech devices.  Check [here](https://www.semtech.com/lora/what-is-lora) for Semtech info and their LoRa overview.  This page focuses on how to use the Semtech [SX1280](https://www.semtech.com/products/wireless-rf/lora-24ghz/sx1280) device.

My network uses a star topology with a single access point implemented by connecting a [Beaglebone](bbb) to an SX1280 dev board.  The network nodes are [AVR MCUs](avr) connected to SX1280 dev boards.  The SPI serial bus is used for both the Beaglebone and AVR interfaces.


**Power Budget**
Rx worst case cost:
- (Sleep to STDBY_RC) = 1200 us @ 700 uA = 2.3e-7 mAh
- (STDBY_RC to RX) = 85 us @ 700 uA = 1.652e-8 mAh
- (Rx Time @ 325 kBit/sec) = 3.1 us/bit  @ 7 mA = 6e-9 mAh/bit

Tx worst case cost:
- (Sleep to STDBY_RC) = 1200 us @ 700 uA = 2.3e-7 mAh
- (STDBY_RC to RX) = 85 us @ 700 uA = 1.652e-8 mAh
- (Tx Time @ 325 kBit/sec) = 3.1 us/bit  @ 18 mA = 1.54e-8 mAh/bit

**Pinout**
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


