---
layout: project
repository_url: https://github.com/ggmessier/robot
---
# To Do
* PCB for mainboard
* Open source robot voice generator
* BOM:
  * Screens
  * AA battery holder
  * Coin battery holder
  * IR LED
  * IR sensor
  * Small speaker
  * Push buttons (individual or array)


# Processor

## Mainboard

* 20 pin SOIC PIC
* SPI external FLASH
* Low profile headers for all IO
* Programming connector
* Power connector

## Daughtercards

* Prototyping board with just through-hole vias on all I/O pins.


# Power

Include power budgets here and expected lifetime

* AA for servo control
* Lithium coin for electronic only


# Interface

Data Communication:
* USB to Andriod tablet and/or phone.  Could be extended later to a USB link to a PIC that has a wireless interface to other PICs.

Sensors:
* Infra-red proximity.
* Infra-red remote control.
* SPI accelerometer/gyro
* Mechanical whiskers

Actuators:
* Servos

Human inputs
* Bank of buttons
* Microphone (clapping and maybe voice later...?)

Human outputs
* Small LED screen
* Speaker



# Mechanical Design

Aesthetic will be rounded creatures with legs or wheels.  Screen will be the face.

* PCB 55mm x 45 mm


## Head/Neck
* Houses: screen, speaker, mainboard, IR sensor, programming/USB ports, buttons

## Bodies
* Power only with legs
* Wheels with power and servos
* Wheels+ with also room for arms, camera, whatever.


