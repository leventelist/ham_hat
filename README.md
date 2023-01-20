# Raspberry PI hat for radio amateurs

![](https://github.com/leventelist/ham_hat/blob/master/images/HAM_Hat.png)


## History

I've been doing lots of SOTA activations with Raspberry PI like SBCs, and there
where always issues, like RF interference, and power supply shorts. I started to
add things like galvanically decoupled audio interface, a step down power supply. It
was working, but it looked like a mess.

This piece of hardware integrates all needed equipment in one nice hat. It is designed
to put the RPI in a metallic box to further isolate from RF signals.

It was designed using [KiCad](https://www.kicad.org/).


## Applications

* HF/VHF digital modes (PSK, FT8, etc)
* HF/VHF AX.25 based modes (Packet, APRS, etc)


## Features

 * 3A power supply with wide input voltage range: 8 to 35V
 * Ublox MAX-8 GPS receiver for position and time synchronization
 * Inductive audio couplers to minimize GND loops. Up to 4kHz.
 * PWM controlled cooling fan
 * PTT from the PI
 * RTC

GPS antenna is not integrated in the device, so an external antenna connector is
mounted on the PCB.

The sound card is not included. I use
[this](https://www.axagon.eu/en/produkty/ada-17) particular device with good
results. I usually break the plastic housing, and solder a shielded cable
directly to the audio interface (J109).

The GPS is needed for APRS and time synchronization. There is an onbard RTC to have some redundancy.


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

J109 provides connection to the soundcard.

| Signal name | Pin of J109            | Comment                          |
|-------------|------------------------|----------------------------------|
| RX audio    | 1                      | Mic input of your soundcard      |
| TX audio    | 4                      | Speaker output of your soundcard |
| GND         | 2, 3                   | Audio ground                     |


## Setting up audio levels

There are two potentiometers (RV101 and RV102) to adjust sound level in RX and TX direction respectively. Adjust TX and RX
audio levels to a certain point where you are not over driving either input. If you
are using it for HF, monitor your ALC, and make sure it is not active.


## Power connection

J101 provides power connection. The maximum input voltage is 35Volts.


## GPS

Connect your passive or active GPS antenna to J104. Use 3.3V active antenna. PPS signal is provided on GPIO18.

[Here](https://austinsnerdythings.com/2021/04/19/microsecond-accurate-ntp-with-a-raspberry-pi-and-pps-gps/) is an excellent article how to set up GPIO-PPS for ntpd.


## RTC

DS3231 based precision RTC is provided for backup if the GPS can't provide accurate timing. It has internal temperature compensated crystal oscillator.

A nice tutorial how to set up the [RTC](https://thepihut.com/blogs/raspberry-pi-tutorials/17209332-adding-a-real-time-clock-to-your-raspberry-pi) on an RPI.

Connect a 3V battery to BT101 for offline RTC operation.


## FAN control

PWM shall be enabled on GPIO13.

If you don't want PWM control, short JP101, and the fan will spin at full power all times.

There's a non-PWM control of the fan that works out of the box using the Raspberry PI OS.

Open raspi-config, under Performance Options, you shall select the desired temperature,
and the GPIO pin which is 13.

## Accessories

These items needed for the hat for full functionality.

All sourced from [Farnell](https://www.farnell.com/), unless othervise noted. (Sorry, I'm Hungary based.)

| Item | Source designator        | Comment |
|--------------------|------------|---------|
| RTC Battery        | 1892670    | The idea is to use heatshrink tube and some wires. |
| RTC Battery holder | 3583203    | External battery holder for CR2032 |
| Heatsink           | 1211701 or https://www.alza.hu/raspberry-pi-rb-hutoborda-d4147799.htm?o=21 ||
| Standoff           | 1466844 | It must be 12mm in length |
| Mounting screws M2.5x6 | | |
| GPS antenna        | [This](https://www.soselectronic.hu/products/2j/2j431gmp-250rg174-c20n-173902) or [this](https://www.soselectronic.hu/products/2j/2j0801b-c814g-217598) | Use 3V active antenna |
| RPI4 | 3369503 (8GB) or 3051887 (4GB) | |
| USB audio interface| [Alza](https://www.alza.hu/axagon-ada-10-mini-d1470921.htm) | Any other do the job. Check Linux driver availability. |
| Monitor| [Ebay](https://www.ebay.com/itm/353758771148?_trkparms=ispr%3D1&hash=item525daa77cc:g:jNQAAOSwnmlhhkpn&amdata=enc%3AAQAGAAACoPYe5NmHp%252B2JMhMi7yxGiTJkPrKr5t53CooMSQt2orsSd0ReTLyM7cxPnI6zs468EDJJHdbu7%252F6aAGgDwzooo3WFCnsE6WY2NN3WIFz%252BU3j%252B6nlMSYOqthKl8%252BB0CNXkHJGfWJwzf20ZY2tdDWUhthRak%252B0O%252FHuC9ltiij5XgROuZ1Yt7ahYbZ19ddFFTaniueENCnYQ1aBhlktfzWv7xNvLbyiVUMCgdXy2uwy0Qm1PC1w8PtdFCrKUjBzWedhAdATUyusA%252BLFfS8lKdAnUeEkUiXBHqDyRACtOih8HyopSoYK%252BuetmxNqJMW1yetVzEuVG55kdREQp8NK3DiaAyJ3VxZ2eCQS7MBWAslEs%252BcjPr5pLBJmvXicOdQsxG78lY3RixTMapBEXkMyMhr8CZ%252B%252BUgXa6K6nssZMYzkzb8xh6HKPf1HGRgakrkSU8iv0Jb0qSPHQQbUU%252BDDCgloGfOgyy3KP%252FVC8YO8aAXQEpuWYDxkgLVD9bG29n%252FxRT5bK91LAbViZxXBj7t3CMtKnw2FXJZp9tf8PF83bIWHzxw3%252FWPs3Q16F6D8dQrHa7%252FQKrBkX9ECfOG3J8w%252BXIaV0JdErB2c39fbNJsezMG0qO7EeJPmYWaZ4isKdigC4pZBSkcRq6YpXnZEsE%252FZbSkspYbLs5C%252F9QS17yAUWT6I9ebc9k7iy9tjIt2p2E%252F8tQXl7IEDUfLabC98laQ883Xs2%252BFUGj8w%252B%252FzyhRREPPlbA7segxjevzekGn9GUOD6kM6yCYgyqf3eMCqXgKofQIa6dmLZviddtP9L0a4A2mYfWhoSsyY%252FoBn6oAKnoTd9ymHzWRMWE5W5Act9JD6YpZT0wU8zPgG6x9%252BwGaIeGsotEsk1Bm2ccUKsKW1YO18BFmLPTsdw%253D%253D%7Cclp%3A2334524%7Ctkp%3ABFBM_P_ZwrNf)
| Keyboard | https://www.pcland.hu/genius-luxemate-100-usb-fekete-hun-billentyuzet-31300725113 | Any USB Keyboard. I use the one without keypad, for its compact size. |
| Mice | | Any USB, or BLE mice |
| SD card with Raspbian image. | | |
| uHDMI to HDMI cable | [Alza](https://www.alza.hu/vention-micro-hdmi-to-hdmi-cable-2m-black-d5891200.htm?o=1) | |
