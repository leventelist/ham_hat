# Raspberry PI hat for radio amateurs

![](https://github.com/leventelist/ham_hat/blob/master/images/HAM_Hat.png)

## History

I've been doing lots of SOTA activations with Raspberry PI like SBCs, and there
was always issues, like RF interference, and power supply issues, so I started to
add things like galvanically decoupled audio interface step down power supply. It
was working, but it looked mess.

This piece hardware integrates all needed equipment in one nice hat. It is designed
to put the RPI in a metallic box to further isolate from RF signals.

It was designed using KiCad.

## Features

 * 3A power supply with wide input voltage range: 8 to 35V
 * Ublox max8 GPS receiver for position and time synchronization
 * Inductive audio couplers to minimize GND loops
 * PWM controlled cooling fan
 * PTT from the PI

GPS antenna is not integrated in the device, so an external antenna connector is
mounted on the PCB.
