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
- In Device Resources, enable the EUSART (the one with PIC10/PIC12/.. etc.).
- In the EUSART module:
  - Enable Transmit.
  - Enable Receive.
  - Set baud to 9600.
  - Transmission and reception bits should both be 8 bits.
  - Data polarity is Non-Inverted.
  - Don't bother with redirecting STDIO to USART.
- In the Pin Manager (Grid View):
  - Lock RC1 as EUSART TX.
  - Lock RC0 as EUSART RX.
- In the System Module:
  - Set the oscillator to INTOSC and the internal clock to 1MHz_HF.


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



