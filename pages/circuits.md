---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Hardware Hacking

This page describes the various embedded microcontroller and circuit design projects I'm enjoying.  Much of this is frog themed due to a long time love of [Kermit](https://en.wikipedia.org/wiki/Kermit_the_Frog) and their [role in our ecosystems](https://www.naturewatch.ca/wp-content/biguploads/senior_guide_712.pdf).

## Eagle

I use [eagle](https://www.autodesk.ca/en/products/eagle/free-download) for my PCB design.  While a little dated, I still like Jeremy Blum's eagle tutorial in parts [1](https://www.youtube.com/watch?v=1AXwjZoyNno&t=618s), [2](https://www.youtube.com/watch?v=CCTs0mNXY24) and [3](https://www.youtube.com/watch?v=oId-h6AeXXE&t=1191s).  It's also handy to be able to know how to create a [custom library part](https://www.youtube.com/watch?v=yvRGmltr_P8).

## Frog Brain

The microcontroller board I use for most of my projects is implmented using a PIC from [Microchip](http://microchip.com).  The processors I've selected are from the [PIC16F1777/8/9](http://www.microchip.com/wwwproducts/en/PIC16F1779) family since they seem to be the 8 bit PICs that have the most options for interfacing to analog circuitry.  

* [Hardware](pic-hw)
* [Software](pic-sw)
* [Audio Playback](audio)


## Wireless

Wireless connectivity is implemented using the [LoRa](https://en.wikipedia.org/wiki/LoRa) standard.  I chose this since I don't need a lot of speed for simple PIC applications and the excellent link budget is really nice for home projects.  I'm using a now unavailable transceiver board that is essentially a direct interface to the Semtech [SX1280](https://www.semtech.com/products/wireless-rf/24-ghz-transceivers/sx1280) chip with the RF front end and on-board antenna.


## Tadpole Boards

Aka daughter boards (haha).  These boards plug into the PIC brain board using headers.

- [Breadboard:](https://github.com/ggmessier/frogs/tree/master/boards/Tadpole%20-%20Breadboard) This is a very simple breakout board for the PIC brainboard headers that has room to accomodate a small prototyping breadboard.  Use for low speed prototyping and troubleshooting applications only.







