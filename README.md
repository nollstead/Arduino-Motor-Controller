# Project Description

This is a shield for an Arduino Mega or Giga that can be used to control a robot car (for example) and has additional inputs for additional sensors.  

The inspiration for this project stems from my interest in learning robotics.  I initially started with an Arduino and experimenting with various plug-and-play components.  Over time, as you can expect, this led to a mess of wires and interconnects as the number of components grew.  As I also had an interest in circuit design I set to learn how to create my own circuit boards, still based on Arduino but with wires and components on the board.  This project represents culmination of my learning to date and I'm making this public in case others may find it useful.  Note that this is a hobby project and is NOT a commercial product and has not undergone EMI testing/certification.

# Specifications

### Board Dimentions and Layout

Since this is designed as a shield for an Arduino Mega or Giga the dimentions of the PCB are somewhat constrained.  They board dimensions and pinouts match those boards, so I really just had the middle area to work with.  As much as possible I tried to use the back pins on the Arduino - to have PWM and Analog pins available in the future.  Space constraints limited that a bit as there just wasn't enough room to route everything so six of the PWM pins are used for non-PWM digital signals (servos and light transistors).  

### Power

The shield uses 3.3v logic to support both the Arduino Mega (5v) and the Arduino Giga (3.3v).  Power is supplied via a JST connector though that could be replaced with a 2.54mm terminal block if desired.  The assumption is this will use a 7.4v LIPO battery though it should support up to 12V.  Power input also includes a reverse polarity protection MOSFET and power LED.  This prevents damaging internal circuitry if you accidentally plug power wires in backwards.  If the LED is on then power is wired correctly

Power is sent to the Arduino, so no additional power is required.  A jumper (J1) is included to bypass this should that be desired - perhaps during programming or debugging using the USB - though I haven't found that to be necessary.  Connect the jumper to supply battery voltage to the Arduino via its VIN pin, remove it to isolate the board; in this case Arduino power must be supplied separately (USB, etc.).  In most cases the jumper will be in place though it's there as an option in case there is a need to isolate power

The NRF24L01 transceiver is recommended to use a separate voltage supply and the motor controllers require one as they can pull much more current than the Arduino pins can support.  Hence the need for voltaage conversion.  I started with two linear voltage regulators and eventually decided to implement a buck converter -  for the increased efficience as well as the learning experience.  These could just as easily both be voltage regulators, which would simplify the design, as I doubt the small current draws will make an enormous difference.  

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

- [EasyEDA](https://easyeda.com/):  Circuit design software.  Most YouTube videos mention Altium and include a link for a free trial.  Altium interests me but it's expensive and they don't appear to have a hobby license - so the free trial is a bit pointless for me.  EasyEDA is made by JLCPCB.com and is very much geared towards fabricating with them and therefore at least gives you a good place to start.  I'm sure it's missing things that a professional would want but for a hobbiest it's likely all you need.
- [jlcpcb.com](https://jlcpcb.com):  PCB manufacturing.  There are lots to choose from.  I tend to use JLCPCB mainly because 1) that's the first one I used, 2) their quality, speed of manufacturing and support meet my needs and 3) their EasyEDA software makes it easy to get started.  
- [Phils's Lab](https://www.youtube.com/@PhilsLab):  Phil does a great job in explaining circuit design.  When I started watching his videos I probalby understood 10% of what he said.  Over time as I continuied my research I'm probably up to 60%:  
- [Voltage Divider Calculator](https://ohmslawcalculator.com/voltage-divider-calculator).  I used this to determine the resistors needed for the voltage monitor.  
