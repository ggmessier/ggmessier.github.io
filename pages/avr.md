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


## SPI Communications

Operate the MCU in Normal mode where the MCU is always the master device.  Sending involves writing a byte to the SPI DATA register and polling the SPI interrupt till it goes high.  Receiving requires that dummy data is written to DATA (to clear the interrupt) and then polling the interrupt until it goes high.  SPI allows for simultaneous tx/rx so sending the dummy data doesn't cost any extra time (it's ignored).  The received data is buffered and then copied into the DATA register once the 8 bit tx/rx transfer is complete.  The interrupt goes high once the received data is copied in.


### External SPI FLASH

Uses the 32 Mbit AT25SF321 and AT25SF321B devices.  ~WP and ~HOLD are both tied to VCC.  The FLASH chip operates in modes 0 or 3 so the MCU is configured to Mode 0.

The FLASH chip has a 32 Mbit capacity which is divided up into $2^{22}/256 = 16,384$ 256 byte pages (address range 0x000000 to 0x3fffff).  The chip moves from low to high addresses when programming and reading.  It will also wrap around within a page if it reaches the end of a page boundary.

#### Ignis Filesystem

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
















