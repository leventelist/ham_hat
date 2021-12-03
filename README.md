# Raspberry PI hat for radio amateurs

![](https://github.com/leventelist/ham_hat/blob/master/images/HAM_Hat.png)

## History

I've been doing lots of SOTA activations with Raspberry PI like SBCs, and there
where always issues, like RF interference, and power supply shorts, so I started to
add things like galvanically decoupled audio interface, a step down power supply. It
was working, but it looked like a mess.

This piece hardware integrates all needed equipment in one nice hat. It is designed
to put the RPI in a metallic box to further isolate from RF signals.

It was designed using KiCad.

## Application

* HF portable digital modes (PSK, FT8, etc)
* VHF AX.25 based modes (Packet, APRS, etc)

## Features

 * 3A power supply with wide input voltage range: 8 to 35V
 * Ublox MAX-8 GPS receiver for position and time synchronization
 * Inductive audio couplers to minimize GND loops. Up to 4kHz.
 * PWM controlled cooling fan
 * PTT from the PI

GPS antenna is not integrated in the device, so an external antenna connector is
mounted on the PCB.

The sound card is not included, and you have to use an external, cheap USB soundcard.
I use [this](https://www.axagon.eu/en/produkty/ada-17) particular device with good
results. I usually break the plastic housing, and solder a shielded cable directly
to the audio interface (J105...J108).

## Schematic

Grab the [schematic](https://github.com/leventelist/ham_hat/blob/master/doc/HAM_Hat.pdf)
for a quick look.

BoM can be found [here](https://github.com/leventelist/ham_hat/blob/master/doc/HAM_Hat_bom.csv).

## Connection to the radio

The hat comes with a DB9 connector to connect up your rig. I wanted to have a screw lock
connector, and this was the best choice. The pin out looks like this.

| Signal name | Pin of the DB9 | Comment                  |
|-------------|----------------|--------------------------|
| GND         | 1,2,3,4,5      | Audio ground             |
| RX audio    | 6              | Sound output of your rig |
| TX audio    | 7              | Sound input of your rig  |
| PTT         | 8              | PTT input of your rig    |
| NC          | 9              | Not connected            |

## Connection to the soundcard

| Signal name | Direct solder connector on the PCB | Comment                          |
|-------------|------------------------------------|----------------------------------|
| RX audio    | J105                               | Mic input of your soundcard      |
| TX audio    | J107                               | Speaker output of your soundcard |
| GND         | J106, J108                         | Audio ground                     |

## Setting up

There are two potentiometers (RV101 and RV102) to adjust sound level in RX and TX direction respectively. Adjust TX and RX
audio levels to a certain point where you are not over driving either input. If you
are using it for HF, monitor your ALC, and make sure it is not active.

## Power connection

J101 provides power connection. The maximum input voltage is 35Volts.


## GPS

Connect your passive or active GPS antenna to J104. Use 3.3V active antenna.

## Contact me if you have further questions

leventelist@gmail.com
