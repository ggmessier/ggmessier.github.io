---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Displays

## Little Screen

My "little screen" is the NHD-0208BZ-RN-YBW 3.3V 8x2 character LCD display.  The display uses the ST7066U display driver chip which has a much more informative data sheet than the display itself.



It works in 4 bit parallel mode that requires 4 data bits (DB7-DB4) and the E,R/W and RS control bits.
- R/W: 0 = write, 1 = read
- RS: register select, 0 = command, 1 = data
- E: operation enable (falling edge trigger)
- DB0-DB3: not used for 4 bit mode, can be NC
- V0: contrast variable voltage that is connected to a pot



## Big Screen

My "big screen" is the SSD1306 Adafruit OLED display which has some [excellent documentation and support](https://learn.adafruit.com/monochrome-oled-breakouts/downloads).  Since I'm rolling my own code in C, I don't directly use the existing Arduino Adafruit libraries but I'm adapting a lot of their library code and learning a bunch from it.








