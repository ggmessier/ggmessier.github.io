---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# dAuratus

The dAuratus board is named after [dendrobates auratus](https://en.wikipedia.org/wiki/Green_and_black_poison_dart_frog) (aka the green and black poison dart frog) which is currently acknowledged to be the smartest of all frogs.  This is my [AVR](avr) MCU board that serves as the platform for most of my home hobby projects.

- A VDD of 3.3V is provided by an [ADP7104](https://www.analog.com/en/products/adp7104.html) regulator able to accept a VIN of up to 20V.  Includes a switch for turning VDD on/off which doubles as the hardware reset mechanism for the MCU.  The max output current of the regulator is 500mA.

- Pins for interfacing to external devices:

| Pins | Count | Notes |
| :---: | :---: | :--- |
| PA0-PA7 | 8 | The USART and SPI default pins.  |
| PC0-PC3 | 4 | Timer, CCL default pins.  USART/SPI secondary pins. |
| PD0-PD7 | 8 | Comparator, ADC, DAC default pins. |
| VDD     | 2 | |
| GND     | 2 | |

- Co-locate communication pins for easy connector design:
  + Serial terminal communications requires USART TxD, RxD and GND.
  + SPI requires MOSI, MISO, SCK and one I/O pin per device for secondary select (SS).
  + VDD, GND and UPDI for programming (keep same order as SNAP).  Place on 3 pin dedicated vertical male header.

- External device header layout

Pin  | J1        | J3         | J2   |
:--: | :--:      | :--:       | :--: |
  1  | PA7 (SS)  | PC0 (MOSI) | GND  |
  2  | PA6 (SS)  | PC1 (MISO) | PD1  |
  3  | PA5       | PC2 (SCK)  | PD2  |
  4  | PA4       | PC3 (SS)   | PD3  |
  5  | PA3       | GND        | PD4  |
  6  | PA2       | VDD        | PD5  |
  7  | PA1 (RxD) | VDD        | PD6  |
  8  | PA0 (TxD) | GND        | PD7  |

- Power traces are speced for 500~mA (the max regulator current) and signal traces are speced for 50~mA (the max sink/source current of the AVR).  For a 1oz copper trace, this corresponds to pretty small traces (0.115mm for power) but I set my signal and power traces to 0.3mm and 0.5mm, the same as the Phil's Lab KiCad tutorial.

## Ignis Filesystem

A simple filesystem for the external FLASH chips used on the dAuratus board.  A play on will-o-the-wisps or [ignis fatuus](https://en.wikipedia.org/wiki/Will-o%27-the-wisp) which were flashes in swamps scientifically attributed to the spontaneous combustion of marsh gas.   

### External SPI FLASH

Uses the 32 Mbit AT25SF321 and AT25SF321B devices.  ~WP and ~HOLD are both tied to VCC.  The FLASH chip operates in modes 0 or 3 so the MCU is configured to Mode 0.

The FLASH chip has a 32 Mbit capacity which is divided up into $2^{22}/256 = 16,384$ 256 byte pages (address range 0x000000 to 0x3fffff).  The chip moves from low to high addresses when programming and reading.  It will also wrap around within a page if it reaches the end of a page boundary.

### Filesystem Design

Based on a basic file attribute table stored at the start of the FLASH memory address space.  Each file is described using a struct and a file is referred to using its attribute table index number.  The struct that describes each file contains the following information:
- A file valid flag.
- The file name.
- Start address of the file.
- Current read and write addresses.  Note that the current write address is always the first unused byte in the file so that file size = (write address - start address).
- The maximum size of the file.

Currently, this file system is designed for a SPI FLASH chip that is soldered on to the same PCB as the MCU.  So, the code assumes that the number of files stored on the chip will always match the number hard coded in our software constants.

The device has a total capacity of 32 Mbit (4 Mbyte) organized into 256 byte pages and 4 kbyte blocks.  A block is the smallest unit of memory that can be erased so the maximum amount of free space allocated to each file will be constrained to be multiples of a block.

To avoid dealing with file fragmentation, the maximum number of files is hard coded and the available address space is divided evenly between that maximum number of potential files.  Note that this means that applications that just want a single file will only have access to a fraction of the FLASH unless the hard coded maximum file limit is changed.

While this is overkill, the first entire 4 Kbyte block is allocated to store the file system index table.  Therefore, maximum file size is equal to

```
int( (SPI_MAX_BYTES/SPI_BLOCK_BYTES - 1)/NUMBER_OF_FILES )
```






### Reading and Writing

While extra pins can be used in parallel to enhance read speed, only the single pin read command (opcode 0x03) is supported.  It is assumed the read speed will always be below the 50 MHz maximum for the 0x03 read.  Once the 3 address bytes are clocked in, data is continuously read until $\widebar{CS}$ is diasserted.  When the end of address space is reached (0x3fffff), the read wraps around to 0x000000.  The read routine accepts the file index number, a number of bytes to read and an array for storing the bytes.

Before a block can be erased or programmed, the write enable latch (WEL) bit must be set to 1 using opcode 0x06.  The bit is set back to 0 after each successful program and erase so opcode 0x06 must be used before every erase and/or programming operation.

Erasing can be performed in chunks of bytes (4K, 32K or 64K) or the whole chip can be erased.  Note that when erasing in 32K chunks, for example, the device divides its entire address space in to 32K chunks so the location of the erased chunk is determined by address bits A22-A15 (A14-A0 are ignored).  So, you can give an address that falls anywhere within the chunk and the whole thing gets wiped.  It's probably easiest conceptually just to use the start, though, (ie. A14-A0 are all zeros).

Before an address space can be programmed, it must be erased.  Currently, files can only be written to the file system and the only way to delete is to wipe the entire FLASH chip clean with a chip erase.

Both filename and file size are passed to the file creation routine.  After that, the file is indenfied using its index number.  Data is passed into a write routine that accepts the file index number, a pointer to the data array and an integer indicating array size.  The array can be up to 256 bytes long.


