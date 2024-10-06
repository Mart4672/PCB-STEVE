# PCB-STEVE
STM32F4 based Flight Computer Development PCB

## STEVE
STEVE, the name of this flight computer, is an acronym:
Starter Testbed for Evolving the Vehicle Electronics

As the name implies, the intention of STEVE is to be a testbed circuitboard for proving out avionics functionality.
STEVE is very much a development board as this is the first STM32 PCB that I have designed.

Future versions of STEVE will have a focus on exapnding a flight vehicle's envelope 
(Starter Testbed for Expanding the Vehicle Envelope)

STEVE is intended to be used on a flight vehicle such as a model rocket but can also be used in static environments such as a ground test stand.

### Planned Hardware Features for STEVE Version 1
- Host 1 STM32F407 Microcontroller
    - 128 Mbit / 16 MB external flash
    - Micro SD card
    - Reset and Boot buttons
- Have 1 BMI270 Inertial Measurement Unit (IMU) connected over SPI
- Have 1 BMP388 Barometric Pressure Sensor connected over SPI
- Have a battery input voltage range that covers 6 to 16.8V
    - This voltage range ensures that 2s to 4s LiPo batteries can be used to power STEVE
    - Use terminal blocks for battery connection
    - Have a second set of terminal blocks and 2 diodes for a supplementary battery input
- Have a voltage regulator circuit that converts the battery input voltage to 5V
    - This voltage regulator should be rated to handle at least 5A continuous
- Have a voltage regulator that converts the 5V to 3.3V
- Have a dedicated telemetry modem connection
    - Use screwless terminal blocks or a JST-GH connector
    - only GND, 5V, RX, and TX need to be connected
    - Microcontroller UART pins should be connected here
- Have 2 JST-SH 4 pin connectors for I2C
- Have 1 buzzer
- Have 3 standard LEDS
- Have 1 WS2812 (NeoPixel) Addressable LED
- Have 5 Mosfet channels
    - 2 5V channels
    - 3 VBatt channels
    - continuity checking on all channels
- Have 4 Servo connections
    - Use "Screwless - Spring Cage, Tension Clamp" terminal blocks
    - Each set of 3 terminals should have a GND pin and a 5V pin
- Have additional GPIO and bus pins broken out
    - Use screwless terminal blocks

### Planned Hardware Features for STEVE Version 2
- Use a PMOS mosfet for reverse polarity protection
- Have a second PMIC (6-8A) to support 2 additional servos
