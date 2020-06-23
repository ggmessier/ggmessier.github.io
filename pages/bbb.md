---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Beaglebone Black

## Resources

Derek Molloy's [site](http://derekmolloy.ie) and [book](https://read.amazon.ca/kp/embed?asin=B07MMVV65W&preview=newtab&linkCode=kpe&ref_=cm_sw_r_kb_dp_YNn8Eb45V762V) with [companion site](http://exploringbeaglebone.com) are great resources.  The book especially is well laid out and ranges from very basic introductory material to very specific and advanced concepts.

## Development Environment

Since the BBB runs a full linux distro, it's certainly possible to download compilers and develop code directly on the BBB.  However, it's also nice to be able to perform cross-compiled development on a PC since you can use fully featured development environments and version control.




## Version

It can be a bit tricky to determine which version of the BBB you have.  The BBB [eLinux page](https://elinux.org/Beagleboard:BeagleBoneBlack) and the [schematic](https://cdn.sparkfun.com/datasheets/Dev/Beagle/BBB_SCH_C.pdf) are helpful.



## Operating System

Images for the BBB can be downloaded from [here](https://beagleboard.org/latest-images) and a description of how to burn the image onto an SD card and then flash the onboard BBB memory with the OS is [here](http://derekmolloy.ie/write-a-new-image-to-the-beaglebone-black/).  **Note**: If you want to burn the eMMC onboard memory with the OS, don't forget to download a "flasher" image rather than the regular ones meant to run natively off of the SD card.


