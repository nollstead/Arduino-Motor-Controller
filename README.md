# Project Description

This is a shield for an Arduino Mega or Giga that can be used to control a robot car (for example) and has inputs for additional sensors.  

The inspiration for this project stems from my interest in learning robotics.  I initially started with an Arduino and experimenting with various plug-and-play components.  Over time, as you can expect, this led to a mess of wires and interconnects as the number of components grew.  As I also had an interest in circuit design I set to learn how to create my own circuit boards, still based on Arduino but with wires and components on the board.  This project represents culmination of my learning to date and I'm making this public in case others may find it useful.  Note that this is a hobby project and is NOT a commercial product and has not undergone EMI testing/certification.

# Specifications

### Board Dimentions and Layout

Since this is designed as a shield for an Arduino Mega or Giga the dimentions of the PCB are somewhat constrained.  They board dimensions and pinouts match those boards, so I really just had the middle area to work with.  As much as possible I tried to use the back pins on the Arduino - to have PWM and Analog pins available in the future.  Space constraints limited that a bit as there just wasn't enough room to route everything so six of the PWM pins are used for non-PWM digital signals (servos and light transistors).  

### Power

The shield uses 3.3v logic to support both the Arduino Mega (5v) and the Arduino Giga (3.3v).  Power is supplied via a JST connector though that could be replaced with a 2.54mm terminal block if desired.  The assumption is this will use a 7.4v LIPO battery though it should support up to 12V.  Power input also includes a reverse polarity protection MOSFET and power LED.  This prevents damaging internal circuitry if you accidentally plug power wires in backwards.  If the LED is on then power is wired correctly

Power is sent to the Arduino, so no additional power is required.  A jumper (J1) is included to bypass this should that be desired - perhaps during programming or debugging using the USB - though I haven't found that to be necessary.  Connect the jumper to supply battery voltage to the Arduino via its VIN pin, remove it to isolate the board; in this case Arduino power must be supplied separately (USB, etc.).  In most cases the jumper will be in place though it's there as an option in case there is a need to isolate power

Battery monitoring is possible due to a voltage regulator connected to Arduino port A0 that steps VCC (calculated at 8.4v) down to 3.3v - the max for the giga.  If higher battery voltages are used some additional math would likely be needed to get the correct battery level.

The NRF24L01 transceiver is recommended to use a separate 3.3v voltage supply so that was used across the board as supply since the circuitry is already in place.  I started with a linear voltage regulator and eventually decided to implement as a buck converter - for the increased efficience as well as the learning experience.  This could likely as easily both be a voltage regulator (as was done for 5v), which would simplify the design and I doubt the small current draws will make an enormous difference.  

### Motor Controllers

Motors are controlled via two TB6612FNG dual-motor controllers.  Each one can control two motors with 1.2A continuous current and 3A max (for 20 MS).  To support this current the VCC and motor traces are widened to 30 mil.  Note that 30 mil is based on 2oz copper on top and bottom - which is also needed for the buck converter.  If 1oz is used (and the buck converter is replaced with a LVR) then those traces will likely need to be widened.  

### Radio Interface

- 2x4 header block for the connection of an NRF24L01 transceiver (remote control).  The Arduino Giga supports Wifi and Bluetooth natively so that's another option, however, the Arduino Mega has no native support - hance the radio interface.  This block includes a 10uF decoupling capacitor, which is optional but highly recommended to achieve higher range, so that doesn't need to be soldered onto the NRF module as is commonly done.  

### Servo's

Connectors are supplied for up to four servos, wired in parallel (I think) supplied with 5v (they'd be underpowered at 3.3v).  Note that this is the only place where 5v is used and the purpose for the voltage regulator.  The Arduino could most likely handle 1 servo but not sure about four of them, especially if there is a load, so stepping this down from the battery to avoid overloading the Arduino 5v pin.

### LEDs

There are two blocks of JST connectors for front (white) and rear (red) headlights (assuming a robot car).  Each set has a transistor connected to an arduino pin that allows them to turn on and off.  There is also an ambient light sensor connected to pin A1.  Reading this value allow for an "auto" on/off headlight based on light - mimicing auto headlights on a real car.  The assumption is a remote would have a 3-way switch for On / Off / and Auto for headlights.  So if the value is below a defined threshold and the pin is set to auto then turn on the headlights, etc.  

Note that these can be used for other purposes, however, the resistor values were calculated assuming white for the front two and red for the rear.  

### I2C Connectors

- Two JST 2.54mm I2C connectors.  These can be used for any purpose (e.g. vision sensor, etc.).  No other components use I2C so there are no inherent address conflicts.  Note that the SDA and SCL pins DO NOT have pullup resistors as, in my experience, most external I2C components include those in their circuitry.

# Schematic

# Board Images

# Next Steps

- Consider adding a solder jumper pad in case you don't always want the power LED on.

# Repository Guide

# Example Code

Coming soon...

# References

Below are some of the resources that I found useful

- [EasyEDA](https://easyeda.com/):  Circuit design software.  Most YouTube videos mention Altium and include a link for a free trial.  Altium interests me but it's expensive and they don't appear to have a hobby license - so the free trial is a bit pointless for me.  EasyEDA is made by JLCPCB.com and is very much geared towards fabricating with them and therefore at least gives you a good place to start.  I'm sure it's missing things that a professional would want but for a hobbiest it's likely all you need.
- [jlcpcb.com](https://jlcpcb.com):  PCB manufacturing.  There are lots to choose from.  I tend to use JLCPCB mainly because 1) that's the first one I used, 2) their quality, speed of manufacturing and support meet my needs and 3) their EasyEDA software makes it easy to get started.  
- [Phils's Lab](https://www.youtube.com/@PhilsLab):  Phil does a great job in explaining circuit design.  When I started watching his videos I probalby understood 10% of what he said.  Over time as I continuied my research I'm probably up to 60%:  
- [Voltage Divider Calculator](https://ohmslawcalculator.com/voltage-divider-calculator).  I used this to determine the resistors needed for the voltage monitor.
- [PCB Trace Width Calculator](https://www.digikey.com/en/resources/conversion-calculators/conversion-calculator-pcb-trace-width)
- 
