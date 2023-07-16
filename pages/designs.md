---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Designs

## dAuratus

The dAuratus board is named after [dendrobates auratus](https://en.wikipedia.org/wiki/Green_and_black_poison_dart_frog) (aka the green and black poison dart frog) which is currently acknowledged to be the smartest of all frogs.  This is my [AVR](avr) MCU board that serves as the platform for most of my home hobby projects.

- A VDD of 3.3V is provided by an [ADP7104](https://www.analog.com/en/products/adp7104.html) regulator able to accept a VIN of up to 20V.  Includes a switch for turning VDD on/off which doubles as the hardware reset mechanism for the MCU.

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
  + SPI requires MOSI, MISO, SCK and one I/O pin per device for slave select (SS).
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




## Lithobot

Named after the Northern Leopard frog, [lithobates pipiens](https://www.ab-conservation.com/avamp/identification-keys/juvenile-and-adult-amphibians-of-alberta/northern-leopard-frog/); a frog that can help keep gardens healthy by eating pests and is currently [threatened in Alberta](https://naturealberta.ca/what-happened-to-the-northern-leopard-frog/).

Implemented using a dAuratus board with the following functionality:
- Soil moisture sensor(s).
- Photocell sunlight sensor.
- Temperature sensor.
- eRibbit wireless link.

### Moisture Sensor

Similar to many moisture sensor designs, this design measures moisture levels using the change in capacitance between two plates on a PCB.  This is a coplanar capacitor.  The exact capacitance for a coplanar capacitor [can be derived](https://doi-org.ezproxy.lib.ucalgary.ca/10.1016/j.elstat.2019.103371) for two rectangular strips of width $d$ and center point separation $w$.  My actual plate layout is based on existing moisture sensors with a double wide center plate surrounded by a "U" shaped outer plate.  I assume (with no strong theoretical basis) that this is equivalent to two rectangular plates of identical width and twice the length.  The relative dielectric constant, $\epsilon_r$, of water is approximately 80 and air is approximately 1 so we can expect soil to fall between these two extremes.  Dry earth is between 3 and 5.

The sensor is based on putting the moisture sensitive capacitor into a simple RC circuit and driving it with a square wave.  The period should be such that the positive pulse equals the length of time required for the RC circuit to easily reach its maximum for its smallest possible time constant (air).  As moisture is added to the soil, capacitance increases, rise time increases and the waveform maximum amplitude will reduce.  This RC waveform is passed through a diode and lowpass filter to convert to a constant analog voltage.  This voltage will drop as soil moisture level increases.

The following spice simulation demonstrates (as is typical with these kinds of things) that the analog voltage isn't linear with the differences in relative permittivity.  The relative permittivity corresponds to a moisture capacitor equivalent to two plates 4mm wide and 120mm long separated by 2.3mm.  The pulse width corresponds to what's easy to generate with a low clock rate MCU.  Open the voltage window in a new tab if you can't see the font.

![SoilMoistureSim](../src/SoilMoistureSpice.png)
![SoilMoistureVoltages](../src/SoilMoistureVoltage.png)








## bbBufo

The central bbb interface to the home network.  Named after Bufo marinus, the [largest known](https://www.guinnessworldrecords.com/world-records/71033-largest-toad) toad.


## eRibbit

A wireless protocol built on top of LoRa.


## Ignis Filesystem

A simple filesystem for the external FLASH chips used on the dAuratus board.  A play on will-o-the-wisps or [ignis fatuus](https://en.wikipedia.org/wiki/Will-o%27-the-wisp) which were flashes in swamps scientifically attributed to the spontaneous combustion of marsh gas.   

