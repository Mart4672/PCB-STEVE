# PCB-STEVE
STM32F4 based Flight Computer Development PCB

STEVE, the name of this flight computer, is an acronym:
*Starter Testbed for Evolving the Vehicle Electronics*

As the name implies, the intention of STEVE is to be a testbed circuitboard for proving out avionics functionality.
STEVE is very much a development board as this is the first STM32 PCB that I have designed.

Future versions of STEVE will have a focus on exapnding a flight vehicle's envelope 
(Starter Testbed for Expanding the Vehicle Envelope)

STEVE is intended to be used on a flight vehicle such as a model rocket but can also be used in static environments such as a ground test stand.

## STEVE Version 1.1.0 Hardware Features
- 70 x 70 mm, 6 layer board with all components on one side for ease of manufacturing
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
- A 8 MHz High Speed External Crystal Oscillator
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
- use a 3.3V plane on layer 5 (some signals ok) if doing a 6 layer board with components on 1 side
- move the 5V components to the same area
- make the board smaller (60 x 60 mm)
- consider moving the complicated components (BMI, BMP, WS2812) to a separate board
    - probably a bad idea since creating a simple daughter board with Standard PCBA would cost at least (10 PCB + 30 PCBA + 25 shipping) = $65
    - using Economic PCBA only saves ~$25
- give serious consideration to creating a STEVE revision with the PSM circuitry on the same board
    - keep in mind that any board orders also have tarrifs, taxes, and shipping applied, which can easily double the initial PCB/PCBA cost
- use a PMOS mosfet for reverse polarity protection
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

#### STEVE V1.1.0 
STEVE V1.1.0 is a 6 layer PCB that uses vias as small as 
0.3mm (hole size) / 0.45mm (overall via diameter)

On JLC's website, 6 layer boards use the "Advanced PCB/PCBA service".
This has different default options from the standard service

Nonstandard options chosen for the advanced PCB service:

- (optional) Specify Stackup > No requirement
- Mark on PCB = 2D barcode (Serial Number)
    - 2D barcode Only | QR Code | STEVE_V1-1-0_SN | Remove Unique Number | 0001 
        - 8*8mm (5x5 also ok) | Specify Position (No Requirement is ok too)

Advanced Options
- $0.71 Blank Box

PCB Assembly Options
A board with 6 or fewer layers and single sided assembly qualifies for 
JLC's Economic PCBA
https://jlcpcb.com/capabilities/pcb-assembly-capabilities
See the above link for Economic PCBA constraints such as
- only supporting green silkscreens
- only supporting the ENIG finish

STEVE 1.1.0 is a 70 x 70mm board; using Standard PCBA auotmatically sets the 
board size to at least 70x70mm for adding edge rails/fiducials.
"The board size would be modified to be 80*70mm for Standard PCBA due to adding two 5mm edge rails on the shorter sides"

Nonstandard PCBA options chosen:
- PCBA Qty = 2 (can choose 2+ based on component availibility)
- Edge Rails/Fiducials = Added by JLCPCB (default)
- Confirm Parts Placement = Yes

Advanced Options
- Photo Confirmation = Yes (Not available for Economic)
- Conformal Coating (+cleaning) = No (can choose yes for future boards)
    - Not available for Economic PCBA
- Packaging = ESD+Cardboard (Cardboard is ok too)
- Solder Paste = Sn96.5/Ag3.0/Cu0.5 (Do NOT use Bismuth/Bi solder)
- The "Bake Components" option is not available for Economic PCBA
    - Will need to use the Standard PCBA service or omit the WS2812 LEDs (C2761795) from being assembled since they are moisture sensitive
- The BMI270 and BMP390 also require Standard PCBA

"Note: The setup fee is $25 per assembly side for Standard PCBA."

Stencil Order Options
- No stencil being ordered
    - If boards with many small pitch components (ex: STM32) are going to be assembled, a reflow oven is strongly recommended
    - if a stencil is ordered, make sure to get it cut to size to save on shipping costs

## Other Notes
- Don't use special characters such as "µ" for part designators, footprints, or values as this can cause issues with processing the bom and positions (CPL) files.

