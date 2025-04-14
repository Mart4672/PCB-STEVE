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

### STEVE Version 1 Hardware Features
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

TODO
- 1 passive buzzer (passive buzzers allow for different beep noises)
- 3 standard LEDS
- 1 WS2812 (NeoPixel) Addressable LED
- 1 battery voltage sense line
- Connectors for PSM board signals (3 x 6 pin connectors)
    - Uses JST-GH connectors
    - Servo PWM signals (4)
    - Mosfet gate signals (5)
    - Mosfet continuity signals (5)
    - Battery Voltage sensing lines (1)
- Additional GPIO and bus pins broken out
    - 1 additional SPI bus (could be used for a GNSS device)
    - Uses screwless terminal blocks

### Modular/Configurable PSM Board "Version A" Features
- Power Supply Module board that supports power, servos, and mosfets
    - all high current devices should be managed by this board
- Supports a battery input voltage range that covers 6 to 16.8V
    - This voltage range ensures that 2s to 4s LiPo batteries can be used
- Has a PMIC that outputs a regulated 5V and supports at least 5A continuous
- Has a high current diode rectifier to support a second power input
    - intended for a secondary battery or a power supply for keeping the main PSM battery from discharging
- Has terminal blocks for battery connections

TODO
- 5 Mosfet channels
    - 2 5V channels
    - 3 VBatt channels
    - continuity checking on all channels
        - optionally uses alternative continuity circuit (NFET instead of voltage divider) [1/15/2025]
    - current limiting resistors or fuses on all channels
        - uses a high wattage-rated resistor to limit the current to a level that the traces can handle
- 4 Servo connections
    - uses a screwless terminal block connection
        - ex: TE 1-2834015-4 Buchanan WireMate
    - uses inline PTC fuses for each servo
- Connectors for STEVE board signals
    - Uses screwless terminal block connectors or JST-GH connectors
    - Servo PWM signals (4)
    - Mosfet gate signals (5)
    - Mosfet continuity signals (5)
    - Battery Voltage sensing lines (1)

- import/assign missing 3D part models

## Future Updates

### Future STEVE Updates
- use a PMOS mosfet for reverse polarity protection
- add additional IMUs to the board
- add an RJ45 connector to utilize the ethernet capabilities of the STM32F407 (this might be part of a completely different board design)

### Future PSM Board Updates
- create additional PSM boards with more/less features depending on desired capability
    - ex: a larger PSM board with a second PMIC to support more servos and mosfets
    - ex: a smaller PSM board with fewer supported servos/mosfets and/or a lower current rating
- use a PMOS mosfet for reverse polarity protection
- current draw sensing that can be reported to the main STEVE board
