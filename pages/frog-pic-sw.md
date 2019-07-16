---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# PIC Robot FrogBrain Software


## Development Environment

The MPLAB environment from Microchip is quite good and is used for all the development described below.  The software on GitHub is divided into project (denoted by the prefix ``frog-``) and the ``libfrog`` library directory.  Since the MPLAB environment is a bit hard to figure out when it comes to configuring debug and makefile dependencies for libraries, any required library source code files are added directly to the ``Source Files`` folder in the active project.  This is a bit clunky but fine for a relatively small number of files.


## PIC Configuration

Generating the pin and hardware module configuration code is done using the handy MPLAB Code Configurator (MCC) tool.  For the PIC16F1778, the following configuration options need to be enabled:
- In Device Resources, enable the EUSART (the one with PIC10/PIC12/.. etc.).  Within the EUSART module:
  - Select SPI master.
  - CKP is idle high, active low.
  - CKE is idle to active.
  - SMP is set to middle (note that a single bit doesn't really have 4 states, there are two separate states for when the PIC is in SPI master or slave mode).
- In Device Resources, enable the EUSART (the one with PIC10/PIC12/.. etc.).  Within the EUSART module:
  - Enable Transmit.
  - Enable Receive.
  - Set baud to 9600.
  - Transmission and reception bits should both be 8 bits.
  - Data polarity is Non-Inverted.
  - Don't bother with redirecting STDIO to USART.
- In Device Resources, enable the TMR1 module.  Within TMR1:
  - Select FOSC for clock source.
  - Prescaler should be 1:1.
  - Enable synchronization.
  - Timer period is "22.676 us" which corresponds to the 44.1~kHz audio sampling frequency.
  - Enable Timer Interrupts.
  - Set the Callback Function Rate to be 1 times ther period.  Setting this creates a timer callback function that saves a bit of work navigating the details of interrupts.  More details [here](http://microchip.com/projects:callback).
- In Device Resources, enable the DAC1 (10 bit) module.  Within DAC1:
  - Right justify the DAC reference format.
  - Positive source is VDD and negative is VSS.
  - Set Vdd in the software settings to 3.3
- In the Pin Manager (Grid View):
  - Lock RC1 as EUSART TX.
  - Lock RC0 as EUSART RX.
  - Lock RC2 to SCK.
  - Lock RC3 to SDO.
  - Lock RC4 to SDI.
  - Lock RC7 to GPIO output (for FLASHSEL).
- In the System Module:
  - Set the oscillator to INTOSC and the internal clock to 1MHz_HF.


## SPI

Since the FLASH chip is currently our only SPI device, this discussion focuses on it.

The FLASH chip operates in modes 0 or 3 (it shouldn't care what state SCK is at when in idle mode).  It wants to latch input data on SCK rising edge and will output on the falling edge of SCK.  The following config bits set the clock behavior.

- CKE=1: Tx occurs from active to idle clock state.
- CKE=0: Tx occurs from idle to active clock state.
- CKP=1: Idle state for clock is high.
- CKP=0: Idle state for clock is low.

Arbitrarily choosing high as our idle clock state, Fig. 32-6 of the datasheet indicates we get the behavior we want when CKP=1 (idle state for clock is high) and CKE=0 (tx occurs from active to idle so that data is output on the falling SCK edge to be latched at the rising SCK edge by the FLASH chip).  The input sample behavior is set by the SMP bit:

- SMP=1: Input data sampled at end of data output time.
- SMP=0: Input data sampled in middle of data output time.

We want SMP=0 since we will sample data on the rising edge while the FLASH chip outputs it on the falling edge.

## FLASH Data Storage

The FLASH chip has a 32 Mbit capacity which is divided up into $2^{22}/256 = 16,384$ 256 byte pages (address range 0x000000 to 0x3fffff).  The chip moves from low to high addresses when programming and reading.  It will also wrap around within a page if it reaches the end of a page boundary.

### Frog File System

A rudimentary file system is used where the first page (starting at address 0x000000) contains an index table for multiple files stored within the FLASH chip.  Each file is represented by a 20 byte entry:
- Byte 0: Valid entry ID bit equal to 0x33 (invalid entries will have the "erased" value of 0xff).
- Bytes 1-13: Stores the file name in ASCII chars, terminated by a null char.
- Bytes 14-16: Address of first byte in the file.  Files always start at the beginning of a page.
- Bytes 17-19: Address of last byte in the file.

Once files are created, they are referenced for reading and writing using the file descriptor index number (the first descriptor is index 0, the second is index 1, etc.).


Files are constrained to start on multiples of 4 kB to allow for block erase operations.  Currently, the file system allows only for the addition of files.  The only way to delete is to reset the file system by performing a full chip erase 



### Reading and Writing

While extra pins can be used in parallel to enhance read speed, only the single pin read command (opcode 0x03) is supported.  It is assumed the read speed will always be below the 50 MHz maximum for the 0x03 read.  Once the 3 address bytes are clocked in, data is continuously read until $\widebar{CS}$ is diasserted.  When the end of address space is reached (0x3fffff), the read wraps around to 0x000000.  The read routine accepts the file index number, a number of bytes to read and an array for storing the bytes.

Before a block can be erased or programmed, the write enable latch (WEL) bit must be set to 1 using opcode 0x06.  The bit is set back to 0 after each successful program and erase so opcode 0x06 must be used before every erase and/or programming operation.

Erasing can be performed in chunks of bytes (4K, 32K or 64K) or the whole chip can be erased.  Note that when erasing in 32K chunks, for example, the device divides its entire address space in to 32K chunks so the location of the erased chunk is determined by address bits A22-A15 (A14-A0 are ignored).  So, you can give an address that falls anywhere within the chunk and the whole thing gets wiped.  It's probably easiest conceptually just to use the start, though, (ie. A14-A0 are all zeros).

Before an address space can be programmed, it must be erased.  Currently, files can only be written to the file system and the only way to delete is to wipe the entire FLASH chip clean with a chip erase.

Both filename and file size are passed to the file creation routine.  After that, the file is indenfied using its index number.  Data is passed into a write routine that accepts the file index number, a pointer to the data array and an integer indicating array size.  The array can be up to 256 bytes long.



## Serial Code

### Linux PC Serial Debugging
First, you will require the `usbmon` kernel module to be loaded.  Google it.

When using a USB to UART conversion device, the command `lsusb` will list all the USB connections.  Take note of the bus and device number.

When examining kermit exchanges, USB traffic is captured using a command like

`cat /sys/kernel/debug/usb/usbmon/3u > usbdump.txt`

where this command captures all traffic on USB bus number 3.  When looking just for the device and assuming your device number is 11, grep for `":011:"` in `usbdump.txt`.

### User Interface
The user interface is currently a simple 1 character input scheme with `'?'` listing a menu of options.  It is implemented using macros in `uart-menu.h`.

### Kermit
This is a *very* lightweight implementation of the kermit protocol meant for downloading/uploading data to/from the SPI FLASH chip.  Currently, it only allows the PIC to accept uploads from a computer kermit program.  It is implemented in `pic-kermit.c` and `pic-kermit.h`.

When debugging, it's useful to use the `log packets` option in kermit.  However, note that only received packets that are correctly formatted (and likely pass the checksum tho haven't verified) get written to the logfile.  So, it's not super useful to see what the kermit program is doing with bytes it receives but doesn't like.

To upload a binary file, we type the following commands into kermit

```
set baud 115200
send file.extension
```

On the mac, it's also necessary to use the option `set carrier-watch off`.


