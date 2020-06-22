---
layout: project
repository_url: https://github.com/ggmessier/frogs/tree/master/boards/FrogBrain
use_math: true
---
# PIC Hardware

Let's start with the PIC16F1778 since it comes in a 28 pin SOIC package which is a compromise between being easy to solder and having the most pins.  

## Interconnect

90 degree female header pins are used for power, in-circuit programming and UART communication with the PIC.  Male headers will be used to allow daughtercards to plug into the PIC board.


## Power

An ADP7104 voltage regulator is used to provide 3.3~V to the circuit.  This means the input voltage connected to "Vin" on the header can range from ~4~V up to 44~V.  This means the board will run on 3 AA/AAA batteries (minimum) or any of the thousands of 12~V wall warts I seem to have lying around.

The ADP7104 supplies 500~mA of current at 3.3~V.  The current draw of the board components is:

| Part    | Draw (mA) |
|:-------:|:---------:|
| PIC (32~MHz int osc) | 4.2 |
| AT25SF321 FLASH (Programming/Erasing) | 16 |
| LEDS (30~mA each) | 30 |
| **TOTAL** | 50.2 |


## External FLASH

The brain will have an Adesto [AT25SF321](https://www.adestotech.com/wp-content/uploads/DS-AT25SF321_047.pdf) 32Mb external FLASH chip for storing measurements, audio clips, etc.

- The max SPI clock frequency is $f_{osc}/4$ = 8~MHz, assuming the 32~MHz internal oscillator.
- The Read Array command allows data bytes to be read one after the other for a maximum read rate of 8~MHz/8~bits/byte = 1Mbyte/sec.
- The slowest read rate would occur assuming a separate Read Array command was issued for each byte.  This introduces 4 bytes of command/address overhead which results in a read rate of 8~MHz/40~bits/read = 200~kbyte/sec.  This is still easily fast enough for audio applications.


## Daughtercard Interface

A group of 4 1x8 headers are used to allow the brain board to plug into a daughter card.  The headers are divided into 2 groups of 2.  In each group, the headers are separated by 2.54~mm (the header pin spacing) and the centers of the two groups are separated by 32~mm.




