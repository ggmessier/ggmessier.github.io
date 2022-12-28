---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# AVR Micro-Controllers (MCUs)

The AVR MCU family from [Microchip](https://www.microchip.com/) are my devices of choice for simple computing.  Microchip's 8-bit compilers and development environment are free to download and work on all major operating systems.  Microchip also builds the processors used by [Arduino](https://www.arduino.cc/).  I like the AVR family since they're a Swiss Army knife type processor with a ton of mixed signal peripherals built into them.  I also use the AVR devices as my example micro-architecture in the intro to computer architecture class I teach at the University of Calgary.  You can view all the lectures on my [YouTube channel](https://www.youtube.com/channel/UC9lbQ5Kkad4yI338WcdQ1SQ).


## Development Environment

The [MPLabX](https://www.microchip.com/en-us/tools-resources/develop/mplab-x-ide) development environment and the [8 bit XC compilers](https://www.microchip.com/en-us/tools-resources/develop/mplab-xc-compilers) need to be downloaded and installed separately.

## Programmer

- The SNAP programmer requires a 1.2 kOhm on the UPDI line.
- When upgrading MPLAB, it appears that there's an automatic firmware download to the programmers.  This will time out rather than giving a "success" message.  Restart MPLAB and power cycle the programmer after this occurs.





## UART Communications

I use `minicom` as my terminal program on my Mac installed using `port install minicom`.  The serial port devices on the Mac belong to the `wheel` group.  To add your username to `wheel` using the directory service command line utility:

```
sudo dscl . -append /groups/wheel GroupMembership <username>
```

and you can verify you added the user correcly using `id <username>`.

It's necessary to use a USB to tty UART translator chip (easily found on Amazon).  To determine which tty device corresponds to the translator after you plug it in, `ls /dev/tty.*` will give you a listing of all USB serial devices.  The translator should be easy to find.

Start minicom using `minicom -D <tty translator device>`.  To test the translator, connect the transmit and receive pins to see if your terminal characters are echoed back onto the screen.  Enable local echo.

If using the low power 32.768 kHz internal oscillator, 2400 baud seems like the fastest we can go.  Configure for 8N1 (8 bit data frames, no parity, 1 stop bit).  Transmit and receive are both implemented by polling the interrupt bits rather than through actual interrupt service routines.


## External SPI FLASH

Uses the 32 Mbit AT25SF321 and AT25SF321B devices.  ~WP and ~HOLD are both tied to VCC.














