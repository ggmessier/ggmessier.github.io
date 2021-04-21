---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Hardware Hacking

This page describes the various embedded microcontroller and circuit design projects I'm enjoying.  Much of this is frog themed due to a long time love of [Kermit](https://en.wikipedia.org/wiki/Kermit_the_Frog) and their [role in our ecosystems](https://www.naturewatch.ca/wp-content/biguploads/senior_guide_712.pdf).

## Software

I use a linux machine to run all of the software for my projects.

### Eagle

I use [eagle](https://www.autodesk.ca/en/products/eagle/free-download) for my PCB design.  While a little dated, I still like Jeremy Blum's eagle tutorial in parts [1](https://www.youtube.com/watch?v=1AXwjZoyNno&t=618s), [2](https://www.youtube.com/watch?v=CCTs0mNXY24) and [3](https://www.youtube.com/watch?v=oId-h6AeXXE&t=1191s).  It's also handy to be able to know how to create a [custom library part](https://www.youtube.com/watch?v=yvRGmltr_P8).


### MPLAB



## The PIC

The microcontroller I use is a PIC from [Microchip](http://microchip.com).  The processor I've selected is from the [PIC16F1777/8/9](http://www.microchip.com/wwwproducts/en/PIC16F1779) family since they seem to be the 8 bit PICs that have the most options for interfacing to analog circuitry.  

On my repository, I have several tutorial style projects that serve as a starting point for more elaborate work.


## Audio

### Capturing Audio Clips

Audio clips are currently captured from YouTube, recorded using Screenflow and then exported in AIFF format.  At that point, they're loaded into Audacity, converted to mono and exported as header-less unsigned 8-bit PCM files at a sample rate of 44.1~kHz.  The pulse coded modulation (PCM) seems just to be the raw 8 bit sample values.

### Electronics

Sound is expressed in decibels which, of course, is just a ratio of relative powers.  The reference level chosen for audio is the 0.02~mPa (the pressure of air) so audio levels are given by $20\log_{10} A/0.02$, where $A$ is the pressure of the sound on your ears.  Generally, 10~dB is approximately as loud as someone breathing and 60~dB is as loud as a conversation.

Consider the 8~ohm, 800~mW SP-1605 speaker (Digikey Part: 433-1104-ND).  The speaker is rated to deliver 88~dB at 1~W (an extrapolated value since the speaker can't take 1~W) and let's assume we want a volume range from 50~dB to 68~dB.  That corresponds to a maximum and minimum power of

$$
\begin{array}{cc}
P_{\rm max} = 30 - 20 = 10~{\rm dBm} &
P_{\rm min} = 30 - 38 = -8~{\rm dBm}
\end{array}
$$

Assume a sinusoidal tone and that these powers are RMS so that the peak current through the speaker to get these power levels is $i = \sqrt{2P/R}$, where $R$ = 8~ohms.  This means the min and max currents are 50~mA and 6.3~mA to get the volume range we want.  This corresponds to a max voltage of 

With a 3.3~VDC rail, the maximum RMS voltage of our sinusoid is 3.3/$\sqrt{2}$ = 2.33~V which gives a max RMS current through the 8~ohm speaker of 292~mA.  This is lower than the 350~mA maximum of the TLV4112 op-amp used for the design.  

Using an inverting op-amp amplifier, the positive op-amp input is connected to ground.  The DAC input is connected to the negative terminal through a resistor $R_{in}$.  The negative terminal is also connected to the op-amp output via a second resistor $R_f$.  The voltage gain of the amplifier is $V_o/V_i = -R_f/R_{in}$.  We want a maximum gain of 1 so that $R_{in}$ is fixed and $R_f$ is a pot with maximum resistance equal to $R_{in}$.  We also do not want to exceed the 50~mA max current supplied by the PIC output so $R_{in}$ is chosen to be 1~kohm.  



the positive op-amp terminal will be connected to the PIC DAC output.  The negative input is connected to a grounded resistor $R_1$ and also the the output terminal through a second resistor $R_f$.  The output voltage is given by $V_o = (1+R_f/R_1)V_i$.  Note that the minimum gain of the amplifier is unity when $R_f$ = 0.



the max current through the 8~ohm speaker is 3.3/8 = 0.4125~mA.  The TLV4112 is limited 



The max output current sourced by the PIC 16x op-amp is 100~mA so this is within our range.  The peak voltage across with 8~ohm speaker will vary between 400~mV and 50.4~mV.  

Utilizing a non-inverting op-amp amplifier design, the positive op-amp input terminal will be connected internally in the PIC to the DAC output and the negative input  will be connected to a grounded resistor $R_1$ and a second variable resistor $R_f$ connected to the output terminal.  The output voltage is given by $V_o = (1+R_f/R_1)V_i$.  Note that the minimum gain of the amplifier is unity when $R_f$ = 0.

Assuming the 10-bit DAC is used, the maximum voltage value is $V_{DD}$.  Since our audio files only us the bottom 8 bits, the maximum input voltage to the op-amp will vary between 0~V and $V_DD \cdot 256/1024$ = 825~mV.  Since we're using a DC blocking cap, can assume we're working with a zero DC offset sinusoid with a peak voltage of $825/2$ = 412.5~mV.

Since this voltage is greater than our target maximum voltage even with no amplification, we need to put a resistor in series with the speaker.  Assuming a minimum amplifier gain of unity, the series resistance is equal to

$$
R_s = 412.5/50.4 \cdot (8 - 8 \cdot 50.4/412.5) = 57.5\ \Omega
$$


We require a linear voltage gain that varies between unity and 8.  Assuming $R_1$ = 410~Ohm, $R_f$ needs to vary between 0~Ohm and $820 \cdot (8-1)$ = 2.87~kOhm.

Finally, a blocking capacitor must be used to remove the DC offset of the signal generated by the op-amp.  This capacitor in series with the load resistance forms a high-pass filter with a 3~dB cutoff given by $f_c = 1/(2\pi R C)$.  For a 100~Hz cutoff frequency and load resistance of 35~Ohms, the required series capacitor is 607.5~uF.  





## Frog Brain

This section discusses the specific "Frog Brain" PIC microcontroller board I designed in Eagle.


* [Hardware](pic-hw)
* [Software](pic-sw)
* [Audio Playback](audio)


## Wireless

Wireless connectivity is implemented using the [LoRa](https://en.wikipedia.org/wiki/LoRa) standard.  I chose this since I don't need a lot of speed for simple PIC applications and the excellent link budget is really nice for home projects.  I'm using a now unavailable transceiver board that is essentially a direct interface to the Semtech [SX1280](https://www.semtech.com/products/wireless-rf/24-ghz-transceivers/sx1280) chip with the RF front end and on-board antenna.


## Tadpole Boards

Aka daughter boards (haha).  These boards plug into the PIC brain board using headers.

- [Breadboard:](https://github.com/ggmessier/frogs/tree/master/boards/Tadpole%20-%20Breadboard) This is a very simple breakout board for the PIC brainboard headers that has room to accomodate a small prototyping breadboard.  Use for low speed prototyping and troubleshooting applications only.







