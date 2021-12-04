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

## Applications

* HF/VHF digital modes (PSK, FT8, etc)
* HF/VHF AX.25 based modes (Packet, APRS, etc)

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

## Mechanics

It is designed to fit on the Raspberry PI 4. Be aware, that if the heatsink on the CPU is too high, it might
conflict with the screws of the fan. If that happens, mount the heatsink 45 degrees.

![](https://github.com/leventelist/ham_hat/blob/master/images/hat_assembly.png)

## Connection to the radio

The hat comes with a DB9 connector to connect up your rig. I wanted to have a screw lock
connector, and this was the best choice. The pin out looks like this.

| Signal name | Pin of the DB9 | Comment                  |
|-------------|----------------|--------------------------|
| TX audio    | 1              | Audio input of your rig  |
| NC          | 2              | Not connected            |
| PTT         | 3              | PTT input of your rig    |
| NC          | 4              | Not connected            |
| RX audio    | 5              | Audio output of your rig |
| GND         | 6              | Audio ground             |
| NC          | 7              | Not connected            |
| NC          | 8              | Not connected            |
| NC          | 9              | Not connected            |

PTT is connected to GPIO17. It is buffered, and logic one means transmit.

## Connection to the soundcard

| Signal name | Direct solder connector on the PCB | Comment                          |
|-------------|------------------------------------|----------------------------------|
| RX audio    | J105                               | Mic input of your soundcard      |
| TX audio    | J107                               | Speaker output of your soundcard |
| GND         | J106, J108                         | Audio ground                     |

## Setting up audio levels

There are two potentiometers (RV101 and RV102) to adjust sound level in RX and TX direction respectively. Adjust TX and RX
audio levels to a certain point where you are not over driving either input. If you
are using it for HF, monitor your ALC, and make sure it is not active.

## Power connection

J101 provides power connection. The maximum input voltage is 35Volts.

## GPS

Connect your passive or active GPS antenna to J104. Use 3.3V active antenna. PPS signal is provided on GPIO18.

[Here](https://austinsnerdythings.com/2021/04/19/microsecond-accurate-ntp-with-a-raspberry-pi-and-pps-gps/) is an excellent article how to set up GPIO-PPS for ntpd.

## FAN control

PWM shall be enabled on GPIO13. TBD.

If you don't want PWM control, short JP101, and the fan will spin at full power all times.

## Contact me if you have further questions

leventelist@gmail.com
