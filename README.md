# PCB-STEVE
STM32F4 based Flight Computer Development PCB

STEVE, the name of this flight computer, is an acronym:
Starter Testbed for Evolving the Vehicle Electronics

As the name implies, the intention of STEVE is to be a testbed circuitboard for proving out avionics functionality.
STEVE is very much a development board as this is the first STM32 PCB that I have designed.

Future versions of STEVE will have a focus on exapnding a flight vehicle's envelope 
(Starter Testbed for Expanding the Vehicle Envelope)

STEVE is intended to be used on a flight vehicle such as a model rocket but can also be used in static environments such as a ground test stand.

## STEVE Version 1 Hardware Features
- 1 STM32F407 Microcontroller
    - (STM32F407VGT6 is the specific SKU being used)
    - 1024 KB (1MB) of internal flash memory
    - 192 (112+16+64) KB of system RAM
- Reset and Boot buttons
- USB-C input for programming the microcontroller
    - the GCT USB4105-GF-A connector is allegedly rated for 5A
    - also usable for power when not connected to the PSM board
- Terminal block for 5V regulated input
- Micro SD card
- Winbond W25Q 128 Mbit (16 MB) external flash storage
- 1 BMI270 Inertial Measurement Unit (IMU) connected over SPI
- 1 BMP390 Barometric Pressure Sensor connected over SPI
- A 2x5 1.27mm pitch debug header
- A 32.768 kHz Low Speed External Crystal Oscillator
- A 12 MHz High Speed External Crystal Oscillator
    - this might be updated to 8 or 16 MHz in the future
- A TI TLV1117 1A 3.3V Output Linear Regulator
- A dedicated telemetry modem connection
    - uses screwless terminal blocks or a JST-GH connector
        - (each JST-GH connection is rated for 1A and the RFD900 has a max draw of ~1A at 5V)
    - GND, 5V, and UART signals (RX and TX) are present
    - placed close to both the USB-C and Regulated 5V power inputs
- 2 JST-SH 4 pin connectors for I2C
    - allows for easy hardware development for I2C devices (load cells, GNSS, etc)
- 1 passive buzzer (passive buzzers allow for different beep noises)
- 4 standard LEDs
- 2 WS2812 (NeoPixel) Addressable LEDs
- Additional GPIO and bus pins broken out
    - SPI2 (also used for BMP390) pins
    - UART1 pins
    - 2 ADC (12-bit) capable pins
    - Uses screwless terminal blocks
- Connectors for PSM board signals (3 x 6 pin connectors)
    - Uses JST-GH connectors
    - Servo PWM signals (4)
    - Mosfet gate signals (5)
    - Mosfet continuity signals (5)
    - Battery #1 Voltage sense line


## Future Updates

### Future STEVE Updates
- 6 layer board variant, potentially with all components on one side for ease of manufacturing
- use a PMOS mosfet for reverse polarity protection
- add additional IMUs to the board
- add an RJ45 connector to utilize the ethernet capabilities of the STM32F407 (this might be part of a completely different board design)

## Using/opening this project on a different machine

- open the project file in KiCad

On the top bar, the following thing needs to be updated based on the machine you are using:
- Preferences > Configure Paths
Add an enironment variable with a name of:
CURRENT_PROJ_DIR
The value of the enirnment variable should be:
your-repo-dir-path/PCB-STEVE/hardware

On the top bar, the following things should not need to be updated but both use the CURRENT_PROJ_DIR variable 
- Preferences > Manage Symbol Libraries > Project Specific Libraries (tab)
- Preferences > Manage Footprint Libraries > Project Specific Libraries (tab)


## PCB Ordering Notes

#### STEVE V1.0.0 
STEVE V1.0.0 is a 4 layer PCB that uses vias as small as 
0.2mm (hole size) / 0.4mm (overall via diameter)
A future 6 layer version will require different ordering options

For JLC PCB Assembly, the following nonstandard options should be selected for JLC's "Standard PCB/PCBA service:

- $16.10 Surface Finish = ENIG
- $16.10 Via Covering = Epoxy Filled and Capped
- $16.29 Min via hole size/diameter = 0.2mm/(0.3/0.35mm)
    - $16.02 this option requires a 4-Wire Kelvin Test
- Mark on PCB = 2D barcode (Serial Number)
    - 2D barcode Only | QR Code | STEVE_V1-0-0_SN | 0001 | 8*8mm (5x5 also ok)

Advanced Options
- $0.71 Blank Box

PCB Assembly Options
STEVE 1.0.0 is a 50x50mm board; using PCBA auotmatically sets the board size to 
70x70mm for adding edge rails/fiducials. This slightly increases the cost of the 
above options.
- PCBA Type = Standard
- Assembly Side = Both Sides
- PCBA Qty = 2 (can choose 2+ based on component availibility)
- Edge Rails/Fiducials = Added by JLCPCB (default)
- Confirm Parts Placement = Yes

Advanced Options
- Photo Confirmation = Yes
- Conformal Coating (+cleaning) = No (can choose yes for future boards)
- Packaging = ESD+Cardboard
- Solder Paste = Sn96.5/Ag3.0/Cu0.5 (Do NOT use Bismuth/Bi solder)

## Other Notes
- Don't use special characters such as "µ" for part designators, footprints, or values as this can cause issues with processing the bom and positions (CPL) files.

