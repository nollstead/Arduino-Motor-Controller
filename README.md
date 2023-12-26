# Project Description

The inspiration for this project stems from my interest in learning robotics.  I initially started with an Arduino and experimenting with various plug-and-play components.  Over time, as you can expect, this led to a mess of wires and interconnects as the number of components grew.  As I also had an interest in circuit design I set to learn how to create my own circuit boards, still based on Arduino but with wires and components on the board.  This project represents culmination of my learning to date and I'm making this public in case others may find it useful.  Note that this is a hobby project and is NOT a commercial product and has not undergone EMI testing/certification.

It's a shield for an Arduino Mega or Giga that can be used to control a robot car (for example).  It incorporates the following features:

# Specifications

### Board Dimentions and Layout

Since this is designed as a shield for an Arduino Mega or Giga, the dimentions of the board are somewhat constrained.  

### Power

Shield uses 3.3v logic to support both the Arduino Mega (5v) and the Arduino Giga (3.3v).  Power is supplied via a JST connector though that could be replaced with a 2.54mm terminal block if desired.  The assumption is this will use a 7.4v LIPO battery though it should support up to 12V.  Power input also includes a reverse polarity protection MOSFET and power LED.  This prevents damaging internal circuitry if you accidentally plug power wires in backwards.  If the LED is on then power is wired correctly

Power is sent to the Arduino, so no additional power is required.  A jumper (J1) is included to bypass this should that be needed.  Connect the jumper to supply battery voltage to the Arduino via its VIN pin, remove it to isolate the board; in this case Arduino power must be supplied separately (USB, etc.).  In most cases the jumper will be in place though it's there as an option in case there is a need to isolate power

### Motor Controllers

- Two dual-motor controllers, allowing the control of up to four motors.

### Radio Interface

- 2x4 header block for the connection of an NRF24L01 transceiver (remote control).  The Arduino Giga supports Wifi and Bluetooth natively so that's another option, however, the Arduino Mega has no native support - hance the radio interface.  This block include a 10uF decoupling capacitor so that doesn't need to be soldered onto the NRF module.

### Servo's

- Four servo connectors with separate 5v power supplied via an onboard 5v voltage regulator (i.e., not supplied by Arduino).

- Battery monitor connected to Arduino port A0.  This is implemented via a simple voltage divider that assumes 8.4v (fully charged 7.4v LIPO)

### LED's

- Two blocks of JST connectors for front (white) and rear (red) headlights (assuming a robot car).

### I2C Connectors

- Ambent light sensor that can be
- Two JST 2.54 I2C connectors.  These can be used for vision sensors or anything else you want to experiment with.


# Schematic

# Board Images

# Next Steps

- Consider adding a solder jumper pad in case you don't always want the power LED on.

# Repository Guide

# References

Below are some of the resources that I found useful

- Phils's Lab
- 
