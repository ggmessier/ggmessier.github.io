---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Beaglebone Black

## Resources

Derek Molloy's [site](http://derekmolloy.ie) and [book](https://read.amazon.ca/kp/embed?asin=B07MMVV65W&preview=newtab&linkCode=kpe&ref_=cm_sw_r_kb_dp_YNn8Eb45V762V) with [companion site](http://exploringbeaglebone.com) are great resources.  The book especially is well laid out and ranges from very basic introductory material to very specific and advanced concepts.  That said, my version of the book is from 2015 and some of the items are now a bit dated, often topics related to the BBB linux OS.  I've noted some of the differences in the sections below.



## Board Configuration

### Hardware Version

It can be a bit tricky to determine which version of the BBB you have.  The BBB [eLinux page](https://elinux.org/Beagleboard:BeagleBoneBlack) and the [schematic](https://cdn.sparkfun.com/datasheets/Dev/Beagle/BBB_SCH_C.pdf) are helpful.

### Operating System

Images for the BBB can be downloaded from [here](https://beagleboard.org/latest-images) and a description of how to burn the image onto an SD card and then flash the onboard BBB memory with the OS is [here](http://derekmolloy.ie/write-a-new-image-to-the-beaglebone-black/).  **Note**: If you want to burn the eMMC onboard memory with the OS, don't forget to download a "flasher" image rather than the regular ones meant to run natively off of the SD card.



## Development Environment

### Setup Discussion

Since the BBB runs a full linux distro, it's certainly possible to download compilers and develop code directly on the BBB.  However, it's also nice to be able to perform cross-compiled development on a PC since you can use fully featured development environments and version control.

My install is broadly based on Derek Molloy's [tutorial video](https://youtu.be/T9yFyWsyyGk) which is somewhat dated.  At time of writing, I installed on Ubuntu Bionic Beaver on my PC and didn't need to do any of the sources.list updates.  The whole install was done with the following commands:

```
sudo dpkg --add-architecture armhf
sudo apt-get update
sudo apt-get install crossbuild-essential-armhf
```

The hint Derek gives about being able to install cross-compiled libraries using the `:armhf` suffix is very useful.  For example

```
sudo apt-get install libicu-dev:armhf
```

Rather than downloading eclipse directly as suggested in the tutorial video, I installed the version on offer from the Ubuntu software install tool.  This ensures the eclipse version is compatible with whatever version of Java your machine is running.  The only extra step was to install C++ GCC Cross Compile functionality within eclipse which wasn't loaded by default.  After that, creating the Hello World cross-compiler project works exactly as described in the tutorial video.

To enable the RSA, I had to install both Remote Systems User Actions and Remote Systems End-System Runtime within eclipse.  Also, the terminal connection is now part of the TM Terminal package that needs to be installed and run separately from RSA.  I might skip that next time since it's easier to just run an ssh window outside of eclipse.  The manual copying within RSA is also not that much more convenient than regular sftp but the post-compile scp copy of the binary directly to the BBB described in the tutorial is very handy.

To get the on-target debugging working, I needed to install C/C++ Remote Launch.  I didn't have the BeagleBone connection displayed by default like in the tutorial video and instead needed to create a new SSH connection with the BBB IP address and username.  The key copying for automatic authentication described in the tutorial works well here and no password is required.

### New Project Creation Summary

Once things are all set up, here's a summary of the steps to create a new project:
1. If this is a new BBB, you'll need to grant your PC password free access to it using `ssh-keygen`:
  - On your PC, type `ssh-keygen` and leave all the fields blank.
  - Run `ssh-copy-id <BbbUsername>@<BbbIpAddress>`, where you should sub in your BBB username and IP address.
  - Confirm you can ssh to the BBB without being queried for a password.
  
1. Create a new project by selecting C/C++ Project, C++ Managed Build, Cross GCC.  Choose a single name project since that makes the executables easier to copy over.   The cross compiler prefix is `arm-linux-gnueabihf-` and the path is `/usr/bin`.

1. Right click on the project and run Build Project.  It should work straight away.

1. In project properties, select Build Steps in C/C++ Build, Settings and enter the following command to copy the executable over to the BBB once it's compiled: `scp <ExecutableName> <BbbUsername>@<BbbIpAddress>:<BbbHomeDir>/<BbbExecutableName>`.

1. Confirm that `gdbserver` and `gdb-multiarch` are installed on the BBB and your PC, respectively.

1. In your project directory, create a file called `.gdbinit` that contains the line `set architecture arm`.

1. Under Debug Configurations, create a new C/C++ Remote application:
  - Main tab: Create a new ssh connection to the BBB using public key authentication.
  - Main tab: Set the Remote Absolute File Path to the location of the executable on the BBB.
  - Under Debugger, browse for the specific .gdbinit file you created in the previous step and change the GDB debugger to `/usr/bin/gdb-multiarch`.



## Digital I/O and Buses



### Pin Configuration

- These [pinout diagrams](https://elinux.org/Beagleboard:Cape_Expansion_Headers#Full_Headers_with_8_Modes) are essential when working with the P8 and P9 expansion headers.
- The preferred method to configure pins is using  `config-pin` command as part of the [Universal IO](https://github.com/cdsteinkuehler/beaglebone-universal-io) project.  Pin configuration can be automated by placing these `config-pin` commands in a script that is executed at boot up time.
- Chapter 6 of Molloy's book is a bit dated (my version, anyway) and tends to emphasize device tree overlay files which aren't necessary to understand in most cases if you're using `config-pin`.  However, `config-pin` appears to still use device tree overlays under the hood so it can be nice to understand them to dig into the details.  Some resources:
  - [Device tree user guide](https://elinux.org/Device_Tree_Usage) 
  - [Device tree reference](https://elinux.org/Device_Tree_Reference)
  - [Raspberry PI overlay page](https://www.raspberrypi.org/documentation/configuration/device-tree.md)
- When working with GPIO, you still need to configure the direction of the pins and other parameters via the linux OS files in `/sys/class/gpio` as described in Molloy's Chapter 6.  Even setting pin values is performed by writing 1's and 0's to these files from within your C/C++ application.

### GPIO

- The pins available for GPIO by default are listed as "ocp" pins in `/sys/devices/platform/ocp`.  
- GPIO pins are divided into four groups of 32 pins, each corresponding to a GPIO "chip".  The kernel ID number is (<chip number>*32+offset).  For example, P9.30 is listed as `gpio3[16]` which means it's associated with the fourth chip.  The kernel ID number for this pin is (3*32+16)=112.
- `config-pin` can configure the pin as `gpio` (no internal resistor), `gpio_pu` (pull-up resistor) and `gpio_pd` (pull-down resistor).
- Pull-up resistors are connected between VDD and a switch that can short the bottom of the resistor to ground (ie. the voltage is "pulled-up" when the switch is open).  Pull-down resistors are connected to ground and allow a switch connected to VDD to be connected to the other end of the resistor (ie. the voltage is "pulled-down" to zero when the switch is open).
- The internal pull-up/pull-down resistors are only needed if ones aren't provided externally.
- A program interacts with GPIO pins by reading from/writing to the files located in `/sys/class/gpio` where the pin directory number corresponds to the kernel GPIO ID.
- The main files here are:
  - `direction`: The pin is configured as an output/input by writing the string 'out'/'in' to it.
  - `value`: When the pin is an output, writing a 0/1 makes the pin go low/high.  When the pin is an input, we can read from this file to determine the logic value present on the pin.
  - `edge`: An input can be configured to block a read until an event occurs.  Valid strings that can be written to this file are 'none' (default behavior), 'rising', 'falling' and 'both'.  It's possible to read from this file to query the current edge behavior.
  - `active_low`: Inverts the logic level on the pin.  A voltage level of Vcc/Gnd corresponds to 1/0 if this file contains 0.  A value of 1 inverts the logic levels.
- Toggling the GPIO pins between 0 and 1 can reach a maximum switching speed of approx. 3.5 microseconds (on my Beaglebone Black RevB) with lots of random delays (likely from OS related stuff).

### SPI

The BBB has built-in [serial peripheral interface (SPI)](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface) communications capability which is nice for low level interfacing to a variety of IC's.

+ This section assumes the BBB always serves as the master device.
+ Two SPI ports are available (`spi0` and `spi1`) on the P9 header.
+ The SPI pins are as follows:
```
SCLK: Serial clock output.
D1: Master Out, Slave In (MOSI)
D0: Master In, Slave Out (MISO)
CS0: Chip select, assumes slave chip select is active low.
```
+ The SPI pins are configured as:
```
config-pin p9.17 spi_cs
config-pin p9.21 spi
config-pin p9.18 spi
config-pin p9.22 spi_sclk
```



### LoRa Development Board Interface

[LoRa](wireless) connectivity is implemented by using the BBB as both a SPI master and power source for the SX1280 development board.

+ The pin connections are as follows:
```
BBB                     SX1280          Notes
---                     ------          -----
P9-2, GND               GND
P9-4, VDD_3V3 (out)     VDD (in)
P9-17, SPI0_CS0 (out)   NSS_CTS (in)    Slave chip select.
P9-18, SPI0_D1 (out)    MOSI_RX (in)    Master out, slave in.
P9-21, SPI0_D0 (in)     MISO_TX (out)   Master in, slave out.
P9-22, SPI0_SCLK (out)  CLK_RTSN (in)   SPI clock.
P9-23, GPIO_49 (out)    NRST (in)       Active low SX1280 reset.
P9-24, GPIO_15 (in)     BUSY (out)      SX1280 transceiver busy.
```
+ The SX1280 uses CPOL=0 and CPHA=0 (Mode 0).








